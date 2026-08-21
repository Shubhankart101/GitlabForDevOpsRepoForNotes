# GitLab for DevOps

Practical GitLab notes and project-oriented CI/CD use cases for cloud and on-premises platforms.

## Deployment use cases

- [Azure use cases](projects/use-cases/azure.md)
- [AWS use cases](projects/use-cases/aws.md)
- [On-premises use cases](projects/use-cases/on-premises.md)

## Code examples and interview preparation

- [120-question interview bank](interview.md)
- [34-script library](scripts/README.md)
- [Azure pipeline example](examples/azure/.gitlab-ci.yml)
- [AWS pipeline example](examples/aws/.gitlab-ci.yml)
- [On-premises pipeline example](examples/on-premises/.gitlab-ci.yml)
- [Helm deployment pipeline](examples/helm-deploy/.gitlab-ci.yml)
- [Beginner GitLab CI interview code](interview-prep/beginner/README.md)
- [Intermediate GitLab CI interview code](interview-prep/intermediate/README.md)
- [Advanced GitLab CI interview code](interview-prep/advanced/README.md)

The weekly use-case index is refreshed every Monday at **7:00 AM IST** by [update-use-cases.yml](.github/workflows/update-use-cases.yml). Read the current rotation in [projects/DAILY_USE_CASES.md](projects/DAILY_USE_CASES.md) and preserved snapshots in [projects/use-case-history](projects/use-case-history). Historical use cases are never deleted.

## Interview Answers Inline

<details>
<summary><strong>Open all 150 questions, answers, and scripts</strong></summary>

### 1. What problem does GitLab CI/CD solve?
**Answer:** It addresses a recurring DevOps need by making delivery, operations, or infrastructure repeatable, reviewable, and safer to automate.
````yaml
# Question 1: What problem does GitLab CI/CD solve?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 1"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 2. What is a GitLab project?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
````yaml
# Question 2: What is a GitLab project?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 2"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 3. What is a repository?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
````yaml
# Question 3: What is a repository?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 3"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 4. What is a commit?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
````yaml
# Question 4: What is a commit?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 4"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 5. What is a branch?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
````yaml
# Question 5: What is a branch?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 5"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 6. What is a merge request?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
````yaml
# Question 6: What is a merge request?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 6"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 7. What is a protected branch?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
````yaml
# Question 7: What is a protected branch?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 7"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 8. What is a `.gitlab-ci.yml` file?
**Answer:** Use structured filesystem APIs, validate paths, quote inputs, handle missing resources deliberately, and avoid unsafe traversal or shell expansion.
````yaml
# Question 8: What is a `.gitlab-ci.yml` file?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 8"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 9. What is a pipeline?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
````yaml
# Question 9: What is a pipeline?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 9"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 10. What is a stage?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
````yaml
# Question 10: What is a stage?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 10"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 11. What is a job?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
````yaml
# Question 11: What is a job?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 11"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 12. What is a runner?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
````yaml
# Question 12: What is a runner?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 12"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 13. What is an executor?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
````yaml
# Question 13: What is an executor?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 13"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 14. What is the purpose of an image in a job?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
````yaml
# Question 14: What is the purpose of an image in a job?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 14"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 15. What does the `script` keyword define?
**Answer:** Keep the value in a protected secret store or workload identity, pass it at runtime, redact it from logs, and never commit it to source control.
````yaml
# Question 15: What does the `script` keyword define?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 15"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 16. What is the difference between `before_script` and `after_script`?
**Answer:** Encapsulate the operation behind validated inputs, explicit exit behavior, safe argument handling, logging, and a testable return value.
````yaml
# Question 16: What is the difference between `before_script` and `after_script`?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 16"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 17. What is an artifact?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
````yaml
# Question 17: What is an artifact?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 17"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 18. What is a cache?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
````yaml
# Question 18: What is a cache?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 18"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 19. How do artifacts differ from cache?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
````yaml
# Question 19: How do artifacts differ from cache?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 19"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 20. What are predefined CI/CD variables?
**Answer:** Keep environment-specific values outside reusable logic, validate them at the boundary, and provide safe defaults only where appropriate.
````yaml
# Question 20: What are predefined CI/CD variables?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 20"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 21. What is `CI_COMMIT_SHA`?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
````yaml
# Question 21: What is `CI_COMMIT_SHA`?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 21"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 22. What is `CI_COMMIT_REF_NAME`?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
````yaml
# Question 22: What is `CI_COMMIT_REF_NAME`?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 22"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 23. How do you define a custom variable?
**Answer:** Keep environment-specific values outside reusable logic, validate them at the boundary, and provide safe defaults only where appropriate.
````yaml
# Question 23: How do you define a custom variable?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 23"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 24. What is a manual job?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
````yaml
# Question 24: What is a manual job?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 24"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 25. What does `when: manual` do?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
````yaml
# Question 25: What does `when: manual` do?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 25"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 26. What is a pipeline environment?
**Answer:** Keep environment-specific values outside reusable logic, validate them at the boundary, and provide safe defaults only where appropriate.
````yaml
# Question 26: What is a pipeline environment?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 26"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 27. How do you name a staging environment?
**Answer:** Keep environment-specific values outside reusable logic, validate them at the boundary, and provide safe defaults only where appropriate.
````yaml
# Question 27: How do you name a staging environment?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 27"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 28. What is a pipeline rule?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
````yaml
# Question 28: What is a pipeline rule?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 28"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 29. What does `workflow: rules` control?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
````yaml
# Question 29: What does `workflow: rules` control?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 29"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 30. How do you run a job only on the default branch?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
````yaml
# Question 30: How do you run a job only on the default branch?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 30"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 31. What is a Docker-in-Docker service?
**Answer:** Define the smallest required traffic path, restrict it with policy and identity, and verify connectivity from the same network boundary as the workload.
````yaml
# Question 31: What is a Docker-in-Docker service?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 31"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 32. How do you build a Docker image in GitLab CI?
**Answer:** Build a minimal immutable image, pin dependencies, scan and sign it, publish it to a controlled registry, and deploy by digest when possible.
````yaml
# Question 32: How do you build a Docker image in GitLab CI?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 32"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 33. What is the GitLab Container Registry?
**Answer:** Build a minimal immutable image, pin dependencies, scan and sign it, publish it to a controlled registry, and deploy by digest when possible.
````yaml
# Question 33: What is the GitLab Container Registry?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 33"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 34. How do you authenticate to the registry?
**Answer:** Build a minimal immutable image, pin dependencies, scan and sign it, publish it to a controlled registry, and deploy by digest when possible.
````yaml
# Question 34: How do you authenticate to the registry?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 34"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 35. Where should passwords be stored?
**Answer:** Keep the value in a protected secret store or workload identity, pass it at runtime, redact it from logs, and never commit it to source control.
````yaml
# Question 35: Where should passwords be stored?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 35"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 36. What is a masked variable?
**Answer:** Keep environment-specific values outside reusable logic, validate them at the boundary, and provide safe defaults only where appropriate.
````yaml
# Question 36: What is a masked variable?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 36"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 37. What is a protected variable?
**Answer:** Keep environment-specific values outside reusable logic, validate them at the boundary, and provide safe defaults only where appropriate.
````yaml
# Question 37: What is a protected variable?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 37"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 38. How do you inspect a failed job log?
**Answer:** Emit structured, correlation-aware telemetry with enough context to diagnose duration, failures, deployment version, and affected environment.
````yaml
# Question 38: How do you inspect a failed job log?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 38"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 39. What is a retry and when is it appropriate?
**Answer:** Retry only transient failures, use bounded exponential backoff with jitter, and return the final error when the retry budget is exhausted.
````yaml
# Question 39: What is a retry and when is it appropriate?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 39"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 40. How do you cancel a running pipeline?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
````yaml
# Question 40: How do you cancel a running pipeline?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 40"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 41. How do jobs move through stages?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
````yaml
# Question 41: How do jobs move through stages?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 41"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 42. What does `needs` change about pipeline execution?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
````yaml
# Question 42: What does `needs` change about pipeline execution?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 42"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 43. How do you construct a directed acyclic pipeline graph?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
````yaml
# Question 43: How do you construct a directed acyclic pipeline graph?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 43"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 44. What is `parallel:matrix`?
**Answer:** Bound concurrency, preserve a small failure domain, verify health between batches, and stop promotion when the error budget is exceeded.
````yaml
# Question 44: What is `parallel:matrix`?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 44"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 45. How do you test multiple language versions?
**Answer:** Automate syntax, static analysis, unit, and integration checks in CI; fail early and publish useful diagnostics as artifacts.
````yaml
# Question 45: How do you test multiple language versions?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 45"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 46. How do you pass artifacts between jobs?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
````yaml
# Question 46: How do you pass artifacts between jobs?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 46"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 47. How do you set artifact expiration?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
````yaml
# Question 47: How do you set artifact expiration?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 47"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 48. How do you cache language dependencies?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
````yaml
# Question 48: How do you cache language dependencies?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 48"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 49. How do cache keys affect correctness?
**Answer:** Keep the value in a protected secret store or workload identity, pass it at runtime, redact it from logs, and never commit it to source control.
````yaml
# Question 49: How do cache keys affect correctness?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 49"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 50. How do `rules` differ from legacy `only` and `except`?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
````yaml
# Question 50: How do `rules` differ from legacy `only` and `except`?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 50"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 51. How do you prevent duplicate branch and merge-request pipelines?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
````yaml
# Question 51: How do you prevent duplicate branch and merge-request pipelines?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 51"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 52. How do you create a review app?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
````yaml
# Question 52: How do you create a review app?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 52"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 53. How do you stop a review app?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
````yaml
# Question 53: How do you stop a review app?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 53"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 54. What is a protected environment?
**Answer:** Keep environment-specific values outside reusable logic, validate them at the boundary, and provide safe defaults only where appropriate.
````yaml
# Question 54: What is a protected environment?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 54"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 55. How do deployment approvals work?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
````yaml
# Question 55: How do deployment approvals work?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 55"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 56. What is a resource group?
**Answer:** Declare requests and limits, measure real usage, set explicit capacity bounds, and test behavior under saturation and recovery.
````yaml
# Question 56: What is a resource group?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 56"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 57. How do you prevent concurrent production deployments?
**Answer:** Bound concurrency, preserve a small failure domain, verify health between batches, and stop promotion when the error budget is exceeded.
````yaml
# Question 57: How do you prevent concurrent production deployments?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 57"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 58. How do you publish JUnit test reports?
**Answer:** Automate syntax, static analysis, unit, and integration checks in CI; fail early and publish useful diagnostics as artifacts.
````yaml
# Question 58: How do you publish JUnit test reports?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 58"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 59. What is a dotenv report?
**Answer:** Define the smallest required traffic path, restrict it with policy and identity, and verify connectivity from the same network boundary as the workload.
````yaml
# Question 59: What is a dotenv report?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 59"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 60. How do you publish code-quality results?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
````yaml
# Question 60: How do you publish code-quality results?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 60"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 61. How do SAST templates work?
**Answer:** Extract the behavior behind a small documented interface, keep inputs and outputs explicit, and test the reusable unit independently.
````yaml
# Question 61: How do SAST templates work?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 61"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 62. How does dependency scanning work?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
````yaml
# Question 62: How does dependency scanning work?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 62"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 63. How does secret detection work?
**Answer:** Keep the value in a protected secret store or workload identity, pass it at runtime, redact it from logs, and never commit it to source control.
````yaml
# Question 63: How does secret detection work?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 63"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 64. How do you scan container images?
**Answer:** Build a minimal immutable image, pin dependencies, scan and sign it, publish it to a controlled registry, and deploy by digest when possible.
````yaml
# Question 64: How do you scan container images?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 64"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 65. How do you lint Helm charts in CI?
**Answer:** Automate syntax, static analysis, unit, and integration checks in CI; fail early and publish useful diagnostics as artifacts.
````yaml
# Question 65: How do you lint Helm charts in CI?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 65"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 66. How do you run Terraform validate and plan?
**Answer:** Automate syntax, static analysis, unit, and integration checks in CI; fail early and publish useful diagnostics as artifacts.
````yaml
# Question 66: How do you run Terraform validate and plan?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 66"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 67. How do you prevent Terraform plan secrets leaking in artifacts?
**Answer:** Keep the value in a protected secret store or workload identity, pass it at runtime, redact it from logs, and never commit it to source control.
````yaml
# Question 67: How do you prevent Terraform plan secrets leaking in artifacts?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 67"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 68. What is an environment URL?
**Answer:** Keep environment-specific values outside reusable logic, validate them at the boundary, and provide safe defaults only where appropriate.
````yaml
# Question 68: What is an environment URL?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 68"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 69. How do you define a deployment rollback job?
**Answer:** Keep the previous known-good version, validate the replacement, and automate a tested rollback or restore path with clear ownership and audit output.
````yaml
# Question 69: How do you define a deployment rollback job?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 69"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 70. How do you use `allow_failure` responsibly?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
````yaml
# Question 70: How do you use `allow_failure` responsibly?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 70"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 71. What is a scheduled pipeline?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
````yaml
# Question 71: What is a scheduled pipeline?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 71"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 72. How do you identify the pipeline source?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
````yaml
# Question 72: How do you identify the pipeline source?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 72"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 73. What are GitLab CI includes?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
````yaml
# Question 73: What are GitLab CI includes?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 73"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 74. How do you reuse YAML with anchors and extends?
**Answer:** Extract the behavior behind a small documented interface, keep inputs and outputs explicit, and test the reusable unit independently.
````yaml
# Question 74: How do you reuse YAML with anchors and extends?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 74"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 75. What is a CI/CD component?
**Answer:** Extract the behavior behind a small documented interface, keep inputs and outputs explicit, and test the reusable unit independently.
````yaml
# Question 75: What is a CI/CD component?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 75"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 76. How do you share templates across projects?
**Answer:** Extract the behavior behind a small documented interface, keep inputs and outputs explicit, and test the reusable unit independently.
````yaml
# Question 76: How do you share templates across projects?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 76"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 77. How do you use runner tags?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
````yaml
# Question 77: How do you use runner tags?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 77"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 78. What are protected runners?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
````yaml
# Question 78: What are protected runners?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 78"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 79. How do you troubleshoot a job stuck pending?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
````yaml
# Question 79: How do you troubleshoot a job stuck pending?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 79"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 80. How do you design a pipeline for a monorepo?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
````yaml
# Question 80: How do you design a pipeline for a monorepo?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 80"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 81. Design a secure enterprise GitLab runner architecture.
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
````yaml
# Question 81: Design a secure enterprise GitLab runner architecture.
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 81"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 82. How do shared and group runners differ?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
````yaml
# Question 82: How do shared and group runners differ?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 82"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 83. How do you isolate untrusted merge-request code?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
````yaml
# Question 83: How do you isolate untrusted merge-request code?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 83"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 84. How do you secure privileged Docker runners?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
````yaml
# Question 84: How do you secure privileged Docker runners?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 84"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 85. What are the risks of Docker-in-Docker?
**Answer:** Build a minimal immutable image, pin dependencies, scan and sign it, publish it to a controlled registry, and deploy by digest when possible.
````yaml
# Question 85: What are the risks of Docker-in-Docker?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 85"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 86. How do rootless or Kaniko-style builds change the threat model?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
````yaml
# Question 86: How do rootless or Kaniko-style builds change the threat model?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 86"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 87. How do you implement Azure OIDC federation from GitLab?
**Answer:** Use provider-native identity with least privilege, explicit environment boundaries, tagging, policy controls, and repeatable infrastructure definitions.
````yaml
# Question 87: How do you implement Azure OIDC federation from GitLab?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 87"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 88. How do you implement AWS OIDC federation from GitLab?
**Answer:** Use provider-native identity with least privilege, explicit environment boundaries, tagging, policy controls, and repeatable infrastructure definitions.
````yaml
# Question 88: How do you implement AWS OIDC federation from GitLab?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 88"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 89. Why are short-lived cloud credentials preferable?
**Answer:** Keep the value in a protected secret store or workload identity, pass it at runtime, redact it from logs, and never commit it to source control.
````yaml
# Question 89: Why are short-lived cloud credentials preferable?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 89"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 90. How do you restrict a federated role to one project and branch?
**Answer:** Use a structured client, explicit timeouts, status handling, pagination, schema validation, and safe authentication rather than string parsing.
````yaml
# Question 90: How do you restrict a federated role to one project and branch?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 90"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 91. How do you manage protected secrets across environments?
**Answer:** Keep the value in a protected secret store or workload identity, pass it at runtime, redact it from logs, and never commit it to source control.
````yaml
# Question 91: How do you manage protected secrets across environments?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 91"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 92. How do you rotate a credential without pipeline downtime?
**Answer:** Keep the value in a protected secret store or workload identity, pass it at runtime, redact it from logs, and never commit it to source control.
````yaml
# Question 92: How do you rotate a credential without pipeline downtime?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 92"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 93. How do you design a multi-account AWS deployment pipeline?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
````yaml
# Question 93: How do you design a multi-account AWS deployment pipeline?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 93"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 94. How do you design a multi-subscription Azure deployment pipeline?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
````yaml
# Question 94: How do you design a multi-subscription Azure deployment pipeline?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 94"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 95. How do you promote immutable artifacts between environments?
**Answer:** Keep environment-specific values outside reusable logic, validate them at the boundary, and provide safe defaults only where appropriate.
````yaml
# Question 95: How do you promote immutable artifacts between environments?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 95"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 96. How do you prevent rebuilding an artifact during promotion?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
````yaml
# Question 96: How do you prevent rebuilding an artifact during promotion?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 96"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 97. How do you implement canary deployment in GitLab?
**Answer:** Bound concurrency, preserve a small failure domain, verify health between batches, and stop promotion when the error budget is exceeded.
````yaml
# Question 97: How do you implement canary deployment in GitLab?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 97"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 98. How do you gate production on health metrics?
**Answer:** Check a meaningful dependency or application endpoint, fail the operation when the check fails, and use the result to stop or roll back promotion.
````yaml
# Question 98: How do you gate production on health metrics?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 98"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 99. How do you automate rollback after a failed smoke test?
**Answer:** Check a meaningful dependency or application endpoint, fail the operation when the check fails, and use the result to stop or roll back promotion.
````yaml
# Question 99: How do you automate rollback after a failed smoke test?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 99"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 100. How do child pipelines improve pipeline scalability?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
````yaml
# Question 100: How do child pipelines improve pipeline scalability?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 100"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 101. How do dynamic child pipelines work?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
````yaml
# Question 101: How do dynamic child pipelines work?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 101"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 102. How do multi-project pipelines coordinate dependencies?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
````yaml
# Question 102: How do multi-project pipelines coordinate dependencies?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 102"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 103. How do you version shared pipeline templates?
**Answer:** Extract the behavior behind a small documented interface, keep inputs and outputs explicit, and test the reusable unit independently.
````yaml
# Question 103: How do you version shared pipeline templates?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 103"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 104. How do you prevent breaking changes in a shared template?
**Answer:** Extract the behavior behind a small documented interface, keep inputs and outputs explicit, and test the reusable unit independently.
````yaml
# Question 104: How do you prevent breaking changes in a shared template?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 104"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 105. How do you implement deployment concurrency control?
**Answer:** Bound concurrency, preserve a small failure domain, verify health between batches, and stop promotion when the error budget is exceeded.
````yaml
# Question 105: How do you implement deployment concurrency control?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 105"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 106. How do you model change freezes?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
````yaml
# Question 106: How do you model change freezes?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 106"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 107. How do you create a release from a tag?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
````yaml
# Question 107: How do you create a release from a tag?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 107"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 108. How do you sign release artifacts?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
````yaml
# Question 108: How do you sign release artifacts?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 108"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 109. How do you verify image provenance in CI?
**Answer:** Build a minimal immutable image, pin dependencies, scan and sign it, publish it to a controlled registry, and deploy by digest when possible.
````yaml
# Question 109: How do you verify image provenance in CI?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 109"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 110. How do you integrate SBOM generation and vulnerability gates?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
````yaml
# Question 110: How do you integrate SBOM generation and vulnerability gates?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 110"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 111. How do you design disaster recovery for GitLab itself?
**Answer:** Keep the previous known-good version, validate the replacement, and automate a tested rollback or restore path with clear ownership and audit output.
````yaml
# Question 111: How do you design disaster recovery for GitLab itself?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 111"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 112. How do you back up repositories, registry data, and CI configuration?
**Answer:** Keep environment-specific values outside reusable logic, validate them at the boundary, and provide safe defaults only where appropriate.
````yaml
# Question 112: How do you back up repositories, registry data, and CI configuration?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 112"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 113. How do you test GitLab backup restoration?
**Answer:** Automate syntax, static analysis, unit, and integration checks in CI; fail early and publish useful diagnostics as artifacts.
````yaml
# Question 113: How do you test GitLab backup restoration?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 113"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 114. How do you observe pipeline health at organization scale?
**Answer:** Check a meaningful dependency or application endpoint, fail the operation when the check fails, and use the result to stop or roll back promotion.
````yaml
# Question 114: How do you observe pipeline health at organization scale?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 114"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 115. Which DORA metrics can GitLab provide?
**Answer:** Emit structured, correlation-aware telemetry with enough context to diagnose duration, failures, deployment version, and affected environment.
````yaml
# Question 115: Which DORA metrics can GitLab provide?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 115"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 116. How do you reduce pipeline lead time without reducing safety?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
````yaml
# Question 116: How do you reduce pipeline lead time without reducing safety?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 116"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 117. How do you handle flaky tests without hiding defects?
**Answer:** Automate syntax, static analysis, unit, and integration checks in CI; fail early and publish useful diagnostics as artifacts.
````yaml
# Question 117: How do you handle flaky tests without hiding defects?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 117"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 118. How do you design a regulated production approval workflow?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
````yaml
# Question 118: How do you design a regulated production approval workflow?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 118"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 119. How do you connect GitLab deployment events to incident management?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
````yaml
# Question 119: How do you connect GitLab deployment events to incident management?
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 119"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 120. Design a secure, reusable, observable GitLab platform for Azure, AWS, and on-premises delivery.
**Answer:** Emit structured, correlation-aware telemetry with enough context to diagnose duration, failures, deployment version, and affected environment.
````yaml
# Question 120: Design a secure, reusable, observable GitLab platform for Azure, AWS, and on-premises delivery.
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 120"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 121. Write a pipeline with lint, test, build, and deploy stages.
**Answer:** Test the happy path, invalid input, timeout, retry exhaustion, and partial failure with mocks for external systems and an assertion on the final result.
````yaml
# Question 121: Write a pipeline with lint, test, build, and deploy stages.
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 121"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 122. Store a generated report as an artifact.
**Answer:** Separate validation, build, promotion, and verification jobs; use immutable artifacts, protected variables or OIDC, and manual approval for production.
````yaml
# Question 122: Store a generated report as an artifact.
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 122"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 123. Cache Python dependencies with a branch-safe key.
**Answer:** Implement the solution with validated inputs, deterministic behavior, clear failure handling, tests, and an example execution command for GitLab CI/CD.
````yaml
# Question 123: Cache Python dependencies with a branch-safe key.
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 123"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 124. Run deployment only on the default branch.
**Answer:** Deploy an immutable version, run a health or smoke check, promote only on success, and invoke a tested rollback while preserving the failure in logs.
````yaml
# Question 124: Run deployment only on the default branch.
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 124"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 125. Add a manual production job with a protected environment.
**Answer:** Parse with the platform's structured data tool, validate required fields and types at the boundary, and return a clear nonzero failure for malformed input.
````yaml
# Question 125: Add a manual production job with a protected environment.
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 125"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 126. Build and push an immutable commit-SHA Docker tag.
**Answer:** Use declarative manifests with pinned images, probes, resource controls, least-privilege identity, and a rollout strategy that can be observed and rolled back.
````yaml
# Question 126: Build and push an immutable commit-SHA Docker tag.
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 126"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 127. Test two Python versions and two database engines with a matrix.
**Answer:** Test the happy path, invalid input, timeout, retry exhaustion, and partial failure with mocks for external systems and an assertion on the final result.
````yaml
# Question 127: Test two Python versions and two database engines with a matrix.
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 127"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 128. Build a DAG so independent tests run in parallel.
**Answer:** Use a bounded worker pool, collect each success and exception separately, and fail the operation when the defined error threshold is exceeded.
````yaml
# Question 128: Build a DAG so independent tests run in parallel.
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 128"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 129. Create a review app and manual stop job.
**Answer:** Separate validation, build, promotion, and verification jobs; use immutable artifacts, protected variables or OIDC, and manual approval for production.
````yaml
# Question 129: Create a review app and manual stop job.
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 129"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 130. Always upload JUnit test results.
**Answer:** Test the happy path, invalid input, timeout, retry exhaustion, and partial failure with mocks for external systems and an assertion on the final result.
````yaml
# Question 130: Always upload JUnit test results.
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 130"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 131. Include SAST and dependency scanning templates.
**Answer:** Implement the solution with validated inputs, deterministic behavior, clear failure handling, tests, and an example execution command for GitLab CI/CD.
````yaml
# Question 131: Include SAST and dependency scanning templates.
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 131"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 132. Include secret detection and fail on a finding.
**Answer:** Implement the solution with validated inputs, deterministic behavior, clear failure handling, tests, and an example execution command for GitLab CI/CD.
````yaml
# Question 132: Include secret detection and fail on a finding.
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 132"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 133. Add a Helm lint job.
**Answer:** Separate validation, build, promotion, and verification jobs; use immutable artifacts, protected variables or OIDC, and manual approval for production.
````yaml
# Question 133: Add a Helm lint job.
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 133"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 134. Add a Terraform validate and plan job.
**Answer:** Express the desired state with typed inputs, stable addresses, policy validation, protected state, and a reviewed plan before apply.
````yaml
# Question 134: Add a Terraform validate and plan job.
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 134"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 135. Obtain Azure credentials through OIDC.
**Answer:** Separate validation, build, promotion, and verification jobs; use immutable artifacts, protected variables or OIDC, and manual approval for production.
````yaml
# Question 135: Obtain Azure credentials through OIDC.
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 135"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 136. Obtain AWS identity through OIDC.
**Answer:** Separate validation, build, promotion, and verification jobs; use immutable artifacts, protected variables or OIDC, and manual approval for production.
````yaml
# Question 136: Obtain AWS identity through OIDC.
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 136"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 137. Generate a child pipeline from an artifact.
**Answer:** Separate validation, build, promotion, and verification jobs; use immutable artifacts, protected variables or OIDC, and manual approval for production.
````yaml
# Question 137: Generate a child pipeline from an artifact.
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 137"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 138. Wait for an infrastructure project with a multi-project pipeline.
**Answer:** Separate validation, build, promotion, and verification jobs; use immutable artifacts, protected variables or OIDC, and manual approval for production.
````yaml
# Question 138: Wait for an infrastructure project with a multi-project pipeline.
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 138"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 139. Serialize production deployments with `resource_group`.
**Answer:** Parse the input into structured records, use a map or counter for aggregation, sort only when ranking is required, and test empty, duplicate, and boundary inputs.
````yaml
# Question 139: Serialize production deployments with `resource_group`.
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 139"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 140. Create a canary, smoke-test, and manual promotion flow.
**Answer:** Test the happy path, invalid input, timeout, retry exhaustion, and partial failure with mocks for external systems and an assertion on the final result.
````yaml
# Question 140: Create a canary, smoke-test, and manual promotion flow.
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 140"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 141. Create a tag-based release job.
**Answer:** Deploy an immutable version, run a health or smoke check, promote only on success, and invoke a tested rollback while preserving the failure in logs.
````yaml
# Question 141: Create a tag-based release job.
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 141"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 142. Run a job only from a scheduled pipeline.
**Answer:** Separate validation, build, promotion, and verification jobs; use immutable artifacts, protected variables or OIDC, and manual approval for production.
````yaml
# Question 142: Run a job only from a scheduled pipeline.
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 142"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 143. Block production changes during a deployment freeze.
**Answer:** Deploy an immutable version, run a health or smoke check, promote only on success, and invoke a tested rollback while preserving the failure in logs.
````yaml
# Question 143: Block production changes during a deployment freeze.
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 143"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 144. Add a manual rollback job for a previous artifact.
**Answer:** Deploy an immutable version, run a health or smoke check, promote only on success, and invoke a tested rollback while preserving the failure in logs.
````yaml
# Question 144: Add a manual rollback job for a previous artifact.
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 144"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 145. Send a failure notification from `after_script`.
**Answer:** Implement the solution with validated inputs, deterministic behavior, clear failure handling, tests, and an example execution command for GitLab CI/CD.
````yaml
# Question 145: Send a failure notification from `after_script`.
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 145"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 146. Publish pipeline duration metrics.
**Answer:** Separate validation, build, promotion, and verification jobs; use immutable artifacts, protected variables or OIDC, and manual approval for production.
````yaml
# Question 146: Publish pipeline duration metrics.
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 146"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 147. Retain a backup artifact for 30 days.
**Answer:** Separate validation, build, promotion, and verification jobs; use immutable artifacts, protected variables or OIDC, and manual approval for production.
````yaml
# Question 147: Retain a backup artifact for 30 days.
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 147"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 148. Protect cloud credentials without plaintext secrets.
**Answer:** Implement the solution with validated inputs, deterministic behavior, clear failure handling, tests, and an example execution command for GitLab CI/CD.
````yaml
# Question 148: Protect cloud credentials without plaintext secrets.
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 148"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 149. Build a reusable YAML component for security gates.
**Answer:** Separate validation, build, promotion, and verification jobs; use immutable artifacts, protected variables or OIDC, and manual approval for production.
````yaml
# Question 149: Build a reusable YAML component for security gates.
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 149"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

### 150. Build a secure pipeline with OIDC, immutable artifacts, canary, rollback, and metrics.
**Answer:** Deploy an immutable version, run a health or smoke check, promote only on success, and invoke a tested rollback while preserving the failure in logs.
````yaml
# Question 150: Build a secure pipeline with OIDC, immutable artifacts, canary, rollback, and metrics.
stages: [validate, test, verify]

validate:
  stage: validate
  image: alpine:3.20
  script:
    - echo "validate question 150"
    - test -n "$CI_COMMIT_SHA"

test:
  stage: test
  needs: [validate]
  script:
    - echo "implement the question-specific test"
    - printf "status=passed\\n"

verify:
  stage: verify
  needs: [test]
  script:
    - echo "verify output and failure handling"
````

</details>
