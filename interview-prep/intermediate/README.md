# Intermediate GitLab CI Interview Code

```yaml
stages: [test, deploy]

test:
  stage: test
  image: python:3.12-slim
  script:
    - pip install -r requirements.txt
    - pytest -q
  artifacts:
    when: always
    reports:
      junit: report.xml

deploy_staging:
  stage: deploy
  script:
    - ./scripts/deploy.sh staging "$CI_COMMIT_SHA"
  environment:
    name: staging
    on_stop: stop_staging
  rules:
    - if: '$CI_COMMIT_BRANCH == $CI_DEFAULT_BRANCH'
```

Practice: explain rules versus only/except, artifacts versus cache, environments, review apps, and protected deployment branches.
