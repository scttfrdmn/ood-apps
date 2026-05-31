# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/),
and this project adheres to [Semantic Versioning](https://semver.org/spec/v2.0.0.html).

## [Unreleased]

### Added
- `apps/aws-stepfunctions-genomics`: pre-filled app bundle for the reference genomics
  Step Functions pipeline (preprocess → align → variant-call → annotate), exposing its
  per-stage inputs (reads/output S3, HealthOmics workflow id, Batch job definition) as form
  fields. Pairs with the `ood-genomics-pipeline` state machine in aws-openondemand
  `examples/state-machines/` (aws-openondemand#8).
- `apps/aws-bedrock`: app bundle for the AWS Bedrock batch-inference adapter (form fields:
  job name, foundation model dropdown, input S3 manifest, output S3 prefix, service role
  ARN). Completes the ood-apps side of aws-openondemand#11.

## [0.1.0] - 2026-05-30

### Added
- `apps/aws-braket`: app bundle for the Amazon Braket quantum adapter (form fields:
  task name, device ARN, OpenQASM 3.0 circuit, shots, results bucket). Completes the
  ood-apps side of aws-openondemand#28 (braket was a dangling backend with no bundle).
- Initial OOD application bundles for all 8 AWS compute adapters in the aws-openondemand ecosystem. Each app provides a web UI form researchers use to submit jobs to one of the AWS compute backends.
