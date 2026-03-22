# Deploying OOD Apps to the Portal Instance

## App Deployment Paths

Open OnDemand looks for system-level apps in two locations:

- `/var/www/ood/apps/sys/` — default OOD system apps directory (OOD 2.x)
- `/etc/ood/apps/sys/` — alternative system apps directory (OOD 3.x/4.x)

Each app directory from this repo maps directly to a subdirectory under one of those paths.

## Manual Deployment

On the OOD portal instance:

```bash
# Clone the repo
git clone https://github.com/scttfrdmn/ood-apps.git /opt/ood-apps

# Deploy all apps to the system apps directory
sudo cp -r /opt/ood-apps/apps/* /var/www/ood/apps/sys/

# Fix ownership
sudo chown -R root:root /var/www/ood/apps/sys/

# Restart the OOD web server to pick up new apps
sudo systemctl restart httpd  # or nginx, depending on your setup
```

## Automated Deployment via Bootstrap

The [aws-openondemand](https://github.com/scttfrdmn/aws-openondemand) Terraform module provisions the OOD portal via an EC2 userdata script (`userdata.sh`). If the `ood_apps_repo` Terraform variable is set to this repository's URL, userdata.sh will:

1. Clone this repo during instance bootstrap
2. Copy all app bundles into `/var/www/ood/apps/sys/`
3. Restart the OOD web server

The relevant Terraform variable in `aws-openondemand`:

```hcl
variable "ood_apps_repo" {
  description = "Git URL for the ood-apps repository to deploy on bootstrap"
  default     = "https://github.com/scttfrdmn/ood-apps.git"
}
```

## Updating Apps

After modifying form definitions or ERB templates, redeploy with:

```bash
cd /opt/ood-apps && git pull
sudo cp -r apps/* /var/www/ood/apps/sys/
```

No OOD restart is required for form/template changes — OOD re-renders templates on each request.

## Verifying Deployment

After deploying, each app should appear in the OOD dashboard under the "AWS Compute" category. You can also check the OOD app manifest endpoint:

```
https://<your-ood-portal>/apps/sys/<app-name>/
```

If an app does not appear, check `/var/log/httpd/error_log` (or the nginx equivalent) for YAML parse errors.
