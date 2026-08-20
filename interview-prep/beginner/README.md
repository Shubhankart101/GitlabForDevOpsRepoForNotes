# Beginner GitLab CI Interview Code

```yaml
stages: [test, build]

unit_test:
  stage: test
  image: python:3.12-slim
  script:
    - python -m compileall app

build_image:
  stage: build
  image: docker:27
  services: [docker:27-dind]
  script:
    - docker build -t "$CI_REGISTRY_IMAGE:$CI_COMMIT_SHORT_SHA" .
```

Practice: explain stages, jobs, runners, artifacts, predefined variables, and why secrets belong in protected CI/CD variables.
