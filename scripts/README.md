# GitLab CI Script Library

Each YAML file is a focused `.gitlab-ci.yml` pattern. Copy one into a test project or include it as a component after reviewing its variables and runner requirements.

## Levels

- `beginner/01-10`: jobs, stages, images, artifacts, cache, variables, rules, manual jobs, environments, and workflow rules.
- `intermediate/11-20`: Docker builds, matrix testing, DAGs, review apps, reports, security scans, Helm, and Terraform.
- `advanced/21-34`: Azure and AWS OIDC, child pipelines, deployment locks, canaries, releases, DAST, backups, rollbacks, and metrics.

Never place cloud keys or passwords in these files. Use protected masked variables or OIDC federation.
