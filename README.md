# ood-apps

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](LICENSE)
[![OOD app bundles](https://img.shields.io/badge/Open%20OnDemand-app%20bundles-1f6feb.svg)](https://openondemand.org/)

Open OnDemand (OOD) application bundles for the [aws-openondemand](https://github.com/scttfrdmn/aws-openondemand) ecosystem. Each app provides a web UI form that researchers use to submit jobs to one of the 8 AWS compute adapters.

## Apps

| App Directory | Cluster | Adapter | Description | Key Form Fields |
|---|---|---|---|---|
| `apps/aws-batch/` | `aws-batch` | `ood-aws-batch-adapter` | Submit a containerized job to AWS Batch | job_name, script_body, queue, walltime, num_cores, memory_gb |
| `apps/aws-sagemaker/` | `aws-sagemaker` | `ood-sagemaker-adapter` | Launch a SageMaker Studio app | job_name, app_type, instance_type |
| `apps/aws-ec2/` | `aws-ec2` | `ood-ec2-adapter` | Launch an EC2 instance as a compute node | job_name, script_body, instance_type, walltime |
| `apps/aws-omics/` | `aws-omics` | `ood-omics-adapter` | Run a WDL/Nextflow workflow via AWS HealthOmics | job_name, workflow_id, workflow_type, output_uri, role_arn, storage_capacity |
| `apps/aws-emr/` | `aws-emr` | `ood-emr-adapter` | Run a Spark job on Amazon EMR Serverless | job_name, entry_point, entry_point_args, spark_submit_parameters, execution_role_arn |
| `apps/aws-sagemaker-training/` | `aws-sagemaker-training` | `ood-sagemaker-training-adapter` | Run a distributed ML training job on SageMaker | job_name, algorithm_image, instance_type, instance_count, volume_size_gb, input_s3, output_s3, role_arn |
| `apps/aws-fargate/` | `aws-fargate` | `ood-fargate-adapter` | Run a Docker container workload on AWS Fargate (ECS) | job_name, script_body, cpu, memory |
| `apps/aws-stepfunctions/` | `aws-stepfunctions` | `ood-stepfunctions-adapter` | Execute an orchestrated workflow via AWS Step Functions | job_name, state_machine_arn, input_json |

## App Structure

Each app follows the standard OOD `adapter_script` bundle layout:

```
apps/<app-name>/
  manifest.yml          # App metadata shown in the OOD dashboard
  form.yml              # Web form field definitions and widgets
  submit.yml.erb        # ERB template mapping form fields to the adapter's job spec
  template/
    script.sh.erb       # ERB template for the job script content
```

The cluster YAML files in `/etc/ood/config/clusters.d/` wire up the adapter binary. The `submit.yml.erb` emits the script content that the adapter reads to build the AWS API call.

## Deployment

See [docs/deployment.md](docs/deployment.md) for instructions on deploying apps to an OOD portal instance.

## Related Repositories

- [aws-openondemand](https://github.com/scttfrdmn/aws-openondemand) — Terraform infrastructure for the OOD portal
- [ood-aws-batch-adapter](https://github.com/scttfrdmn/ood-aws-batch-adapter)
- [ood-sagemaker-adapter](https://github.com/scttfrdmn/ood-sagemaker-adapter)
- [ood-ec2-adapter](https://github.com/scttfrdmn/ood-ec2-adapter)
- [ood-omics-adapter](https://github.com/scttfrdmn/ood-omics-adapter)
- [ood-emr-adapter](https://github.com/scttfrdmn/ood-emr-adapter)
- [ood-sagemaker-training-adapter](https://github.com/scttfrdmn/ood-sagemaker-training-adapter)
- [ood-fargate-adapter](https://github.com/scttfrdmn/ood-fargate-adapter)
- [ood-stepfunctions-adapter](https://github.com/scttfrdmn/ood-stepfunctions-adapter)

## License

MIT — see [LICENSE](LICENSE).
