# Advanced GitLab CI Interview Code

```yaml
.deploy_template:
  image: alpine:3.20
  resource_group: production
  script:
    - ./scripts/deploy.sh "$TARGET" "$CI_COMMIT_SHA"
    - ./scripts/smoke-test.sh "$TARGET"
  after_script:
    - ./scripts/publish-deployment-metrics.sh

canary:
  extends: .deploy_template
  variables:
    TARGET: canary
  rules:
    - if: '$CI_COMMIT_TAG'

production:
  extends: .deploy_template
  variables:
    TARGET: production
  needs: [canary]
  when: manual
  environment:
    name: production
    deployment_tier: production
```

Advanced exercise: add OIDC cloud authentication, signed artifacts, child pipelines, concurrency control, progressive rollout metrics, and an automated rollback job. Explain runner trust boundaries and pipeline supply-chain risks.
