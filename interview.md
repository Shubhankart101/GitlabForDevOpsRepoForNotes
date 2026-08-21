# GitLab DevOps Interview Question Bank

This bank contains 150 questions organized by difficulty. Use the pipeline examples in `scripts/` and `examples/` to build practical answers.

## Worked Answers

### Beginner: stages and artifacts

**Question:** How do you pass a build result to a later job?

```yaml
stages: [test, build]

build:
	stage: build
	script:
		- echo "artifact" > build.txt
	artifacts:
		paths: [build.txt]
```

Artifacts are stored by GitLab and made available to later jobs or for download.

### Intermediate: review app

**Question:** How do you create and stop a review environment?

```yaml
review:
	script: ["./deploy.sh review"]
	environment:
		name: review/$CI_COMMIT_REF_SLUG
		on_stop: stop_review

stop_review:
	script: ["./destroy.sh review"]
	environment:
		name: review/$CI_COMMIT_REF_SLUG
		action: stop
	when: manual
```

The environment name is isolated per branch and can be manually cleaned up.

### Advanced: canary promotion

**Question:** How do you require a smoke test before production?

```yaml
verify_canary:
	stage: verify
	needs: [deploy_canary]
	script: ["./smoke-test.sh canary"]

production:
	needs: [verify_canary]
	script: ["./deploy.sh production"]
	when: manual
	resource_group: production
```

The production job cannot start until the canary verification succeeds, and the resource group prevents concurrent releases.

## Beginner: 1-40

1. What problem does GitLab CI/CD solve?
**Answer:** It addresses a recurring DevOps need by making delivery, operations, or infrastructure repeatable, reviewable, and safer to automate.
Script: [Question 1 script](interview-scripts/001-what-problem-does-gitlab-ci-cd-solve.yml)
```yaml
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
```

2. What is a GitLab project?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 2 script](interview-scripts/002-what-is-a-gitlab-project.yml)
```yaml
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
```

3. What is a repository?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 3 script](interview-scripts/003-what-is-a-repository.yml)
```yaml
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
```

4. What is a commit?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 4 script](interview-scripts/004-what-is-a-commit.yml)
```yaml
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
```

5. What is a branch?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 5 script](interview-scripts/005-what-is-a-branch.yml)
```yaml
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
```

6. What is a merge request?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 6 script](interview-scripts/006-what-is-a-merge-request.yml)
```yaml
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
```

7. What is a protected branch?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 7 script](interview-scripts/007-what-is-a-protected-branch.yml)
```yaml
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
```

8. What is a `.gitlab-ci.yml` file?
**Answer:** Use structured filesystem APIs, validate paths, quote inputs, handle missing resources deliberately, and avoid unsafe traversal or shell expansion.
Script: [Question 8 script](interview-scripts/008-what-is-a-gitlab-ci-yml-file.yml)
```yaml
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
```

9. What is a pipeline?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
Script: [Question 9 script](interview-scripts/009-what-is-a-pipeline.yml)
```yaml
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
```

10. What is a stage?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
Script: [Question 10 script](interview-scripts/010-what-is-a-stage.yml)
```yaml
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
```

11. What is a job?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
Script: [Question 11 script](interview-scripts/011-what-is-a-job.yml)
```yaml
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
```

12. What is a runner?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
Script: [Question 12 script](interview-scripts/012-what-is-a-runner.yml)
```yaml
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
```

13. What is an executor?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 13 script](interview-scripts/013-what-is-an-executor.yml)
```yaml
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
```

14. What is the purpose of an image in a job?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
Script: [Question 14 script](interview-scripts/014-what-is-the-purpose-of-an-image-in-a-job.yml)
```yaml
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
```

15. What does the `script` keyword define?
**Answer:** Keep the value in a protected secret store or workload identity, pass it at runtime, redact it from logs, and never commit it to source control.
Script: [Question 15 script](interview-scripts/015-what-does-the-script-keyword-define.yml)
```yaml
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
```

16. What is the difference between `before_script` and `after_script`?
**Answer:** Encapsulate the operation behind validated inputs, explicit exit behavior, safe argument handling, logging, and a testable return value.
Script: [Question 16 script](interview-scripts/016-what-is-the-difference-between-before-script-and-after.yml)
```yaml
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
```

17. What is an artifact?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 17 script](interview-scripts/017-what-is-an-artifact.yml)
```yaml
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
```

18. What is a cache?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 18 script](interview-scripts/018-what-is-a-cache.yml)
```yaml
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
```

19. How do artifacts differ from cache?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 19 script](interview-scripts/019-how-do-artifacts-differ-from-cache.yml)
```yaml
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
```

20. What are predefined CI/CD variables?
**Answer:** Keep environment-specific values outside reusable logic, validate them at the boundary, and provide safe defaults only where appropriate.
Script: [Question 20 script](interview-scripts/020-what-are-predefined-ci-cd-variables.yml)
```yaml
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
```

21. What is `CI_COMMIT_SHA`?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 21 script](interview-scripts/021-what-is-ci-commit-sha.yml)
```yaml
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
```

22. What is `CI_COMMIT_REF_NAME`?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 22 script](interview-scripts/022-what-is-ci-commit-ref-name.yml)
```yaml
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
```

23. How do you define a custom variable?
**Answer:** Keep environment-specific values outside reusable logic, validate them at the boundary, and provide safe defaults only where appropriate.
Script: [Question 23 script](interview-scripts/023-how-do-you-define-a-custom-variable.yml)
```yaml
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
```

24. What is a manual job?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
Script: [Question 24 script](interview-scripts/024-what-is-a-manual-job.yml)
```yaml
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
```

25. What does `when: manual` do?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 25 script](interview-scripts/025-what-does-when-manual-do.yml)
```yaml
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
```

26. What is a pipeline environment?
**Answer:** Keep environment-specific values outside reusable logic, validate them at the boundary, and provide safe defaults only where appropriate.
Script: [Question 26 script](interview-scripts/026-what-is-a-pipeline-environment.yml)
```yaml
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
```

27. How do you name a staging environment?
**Answer:** Keep environment-specific values outside reusable logic, validate them at the boundary, and provide safe defaults only where appropriate.
Script: [Question 27 script](interview-scripts/027-how-do-you-name-a-staging-environment.yml)
```yaml
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
```

28. What is a pipeline rule?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
Script: [Question 28 script](interview-scripts/028-what-is-a-pipeline-rule.yml)
```yaml
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
```

29. What does `workflow: rules` control?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 29 script](interview-scripts/029-what-does-workflow-rules-control.yml)
```yaml
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
```

30. How do you run a job only on the default branch?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
Script: [Question 30 script](interview-scripts/030-how-do-you-run-a-job-only-on-the-default-branch.yml)
```yaml
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
```

31. What is a Docker-in-Docker service?
**Answer:** Define the smallest required traffic path, restrict it with policy and identity, and verify connectivity from the same network boundary as the workload.
Script: [Question 31 script](interview-scripts/031-what-is-a-docker-in-docker-service.yml)
```yaml
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
```

32. How do you build a Docker image in GitLab CI?
**Answer:** Build a minimal immutable image, pin dependencies, scan and sign it, publish it to a controlled registry, and deploy by digest when possible.
Script: [Question 32 script](interview-scripts/032-how-do-you-build-a-docker-image-in-gitlab-ci.yml)
```yaml
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
```

33. What is the GitLab Container Registry?
**Answer:** Build a minimal immutable image, pin dependencies, scan and sign it, publish it to a controlled registry, and deploy by digest when possible.
Script: [Question 33 script](interview-scripts/033-what-is-the-gitlab-container-registry.yml)
```yaml
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
```

34. How do you authenticate to the registry?
**Answer:** Build a minimal immutable image, pin dependencies, scan and sign it, publish it to a controlled registry, and deploy by digest when possible.
Script: [Question 34 script](interview-scripts/034-how-do-you-authenticate-to-the-registry.yml)
```yaml
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
```

35. Where should passwords be stored?
**Answer:** Keep the value in a protected secret store or workload identity, pass it at runtime, redact it from logs, and never commit it to source control.
Script: [Question 35 script](interview-scripts/035-where-should-passwords-be-stored.yml)
```yaml
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
```

36. What is a masked variable?
**Answer:** Keep environment-specific values outside reusable logic, validate them at the boundary, and provide safe defaults only where appropriate.
Script: [Question 36 script](interview-scripts/036-what-is-a-masked-variable.yml)
```yaml
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
```

37. What is a protected variable?
**Answer:** Keep environment-specific values outside reusable logic, validate them at the boundary, and provide safe defaults only where appropriate.
Script: [Question 37 script](interview-scripts/037-what-is-a-protected-variable.yml)
```yaml
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
```

38. How do you inspect a failed job log?
**Answer:** Emit structured, correlation-aware telemetry with enough context to diagnose duration, failures, deployment version, and affected environment.
Script: [Question 38 script](interview-scripts/038-how-do-you-inspect-a-failed-job-log.yml)
```yaml
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
```

39. What is a retry and when is it appropriate?
**Answer:** Retry only transient failures, use bounded exponential backoff with jitter, and return the final error when the retry budget is exhausted.
Script: [Question 39 script](interview-scripts/039-what-is-a-retry-and-when-is-it-appropriate.yml)
```yaml
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
```

40. How do you cancel a running pipeline?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
Script: [Question 40 script](interview-scripts/040-how-do-you-cancel-a-running-pipeline.yml)
```yaml
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
```


## Intermediate: 41-80

41. How do jobs move through stages?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
Script: [Question 41 script](interview-scripts/041-how-do-jobs-move-through-stages.yml)
```yaml
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
```

42. What does `needs` change about pipeline execution?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
Script: [Question 42 script](interview-scripts/042-what-does-needs-change-about-pipeline-execution.yml)
```yaml
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
```

43. How do you construct a directed acyclic pipeline graph?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
Script: [Question 43 script](interview-scripts/043-how-do-you-construct-a-directed-acyclic-pipeline-graph.yml)
```yaml
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
```

44. What is `parallel:matrix`?
**Answer:** Bound concurrency, preserve a small failure domain, verify health between batches, and stop promotion when the error budget is exceeded.
Script: [Question 44 script](interview-scripts/044-what-is-parallel-matrix.yml)
```yaml
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
```

45. How do you test multiple language versions?
**Answer:** Automate syntax, static analysis, unit, and integration checks in CI; fail early and publish useful diagnostics as artifacts.
Script: [Question 45 script](interview-scripts/045-how-do-you-test-multiple-language-versions.yml)
```yaml
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
```

46. How do you pass artifacts between jobs?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
Script: [Question 46 script](interview-scripts/046-how-do-you-pass-artifacts-between-jobs.yml)
```yaml
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
```

47. How do you set artifact expiration?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 47 script](interview-scripts/047-how-do-you-set-artifact-expiration.yml)
```yaml
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
```

48. How do you cache language dependencies?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 48 script](interview-scripts/048-how-do-you-cache-language-dependencies.yml)
```yaml
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
```

49. How do cache keys affect correctness?
**Answer:** Keep the value in a protected secret store or workload identity, pass it at runtime, redact it from logs, and never commit it to source control.
Script: [Question 49 script](interview-scripts/049-how-do-cache-keys-affect-correctness.yml)
```yaml
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
```

50. How do `rules` differ from legacy `only` and `except`?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 50 script](interview-scripts/050-how-do-rules-differ-from-legacy-only-and-except.yml)
```yaml
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
```

51. How do you prevent duplicate branch and merge-request pipelines?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
Script: [Question 51 script](interview-scripts/051-how-do-you-prevent-duplicate-branch-and-merge-request-p.yml)
```yaml
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
```

52. How do you create a review app?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 52 script](interview-scripts/052-how-do-you-create-a-review-app.yml)
```yaml
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
```

53. How do you stop a review app?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 53 script](interview-scripts/053-how-do-you-stop-a-review-app.yml)
```yaml
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
```

54. What is a protected environment?
**Answer:** Keep environment-specific values outside reusable logic, validate them at the boundary, and provide safe defaults only where appropriate.
Script: [Question 54 script](interview-scripts/054-what-is-a-protected-environment.yml)
```yaml
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
```

55. How do deployment approvals work?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
Script: [Question 55 script](interview-scripts/055-how-do-deployment-approvals-work.yml)
```yaml
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
```

56. What is a resource group?
**Answer:** Declare requests and limits, measure real usage, set explicit capacity bounds, and test behavior under saturation and recovery.
Script: [Question 56 script](interview-scripts/056-what-is-a-resource-group.yml)
```yaml
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
```

57. How do you prevent concurrent production deployments?
**Answer:** Bound concurrency, preserve a small failure domain, verify health between batches, and stop promotion when the error budget is exceeded.
Script: [Question 57 script](interview-scripts/057-how-do-you-prevent-concurrent-production-deployments.yml)
```yaml
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
```

58. How do you publish JUnit test reports?
**Answer:** Automate syntax, static analysis, unit, and integration checks in CI; fail early and publish useful diagnostics as artifacts.
Script: [Question 58 script](interview-scripts/058-how-do-you-publish-junit-test-reports.yml)
```yaml
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
```

59. What is a dotenv report?
**Answer:** Define the smallest required traffic path, restrict it with policy and identity, and verify connectivity from the same network boundary as the workload.
Script: [Question 59 script](interview-scripts/059-what-is-a-dotenv-report.yml)
```yaml
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
```

60. How do you publish code-quality results?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 60 script](interview-scripts/060-how-do-you-publish-code-quality-results.yml)
```yaml
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
```

61. How do SAST templates work?
**Answer:** Extract the behavior behind a small documented interface, keep inputs and outputs explicit, and test the reusable unit independently.
Script: [Question 61 script](interview-scripts/061-how-do-sast-templates-work.yml)
```yaml
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
```

62. How does dependency scanning work?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 62 script](interview-scripts/062-how-does-dependency-scanning-work.yml)
```yaml
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
```

63. How does secret detection work?
**Answer:** Keep the value in a protected secret store or workload identity, pass it at runtime, redact it from logs, and never commit it to source control.
Script: [Question 63 script](interview-scripts/063-how-does-secret-detection-work.yml)
```yaml
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
```

64. How do you scan container images?
**Answer:** Build a minimal immutable image, pin dependencies, scan and sign it, publish it to a controlled registry, and deploy by digest when possible.
Script: [Question 64 script](interview-scripts/064-how-do-you-scan-container-images.yml)
```yaml
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
```

65. How do you lint Helm charts in CI?
**Answer:** Automate syntax, static analysis, unit, and integration checks in CI; fail early and publish useful diagnostics as artifacts.
Script: [Question 65 script](interview-scripts/065-how-do-you-lint-helm-charts-in-ci.yml)
```yaml
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
```

66. How do you run Terraform validate and plan?
**Answer:** Automate syntax, static analysis, unit, and integration checks in CI; fail early and publish useful diagnostics as artifacts.
Script: [Question 66 script](interview-scripts/066-how-do-you-run-terraform-validate-and-plan.yml)
```yaml
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
```

67. How do you prevent Terraform plan secrets leaking in artifacts?
**Answer:** Keep the value in a protected secret store or workload identity, pass it at runtime, redact it from logs, and never commit it to source control.
Script: [Question 67 script](interview-scripts/067-how-do-you-prevent-terraform-plan-secrets-leaking-in-ar.yml)
```yaml
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
```

68. What is an environment URL?
**Answer:** Keep environment-specific values outside reusable logic, validate them at the boundary, and provide safe defaults only where appropriate.
Script: [Question 68 script](interview-scripts/068-what-is-an-environment-url.yml)
```yaml
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
```

69. How do you define a deployment rollback job?
**Answer:** Keep the previous known-good version, validate the replacement, and automate a tested rollback or restore path with clear ownership and audit output.
Script: [Question 69 script](interview-scripts/069-how-do-you-define-a-deployment-rollback-job.yml)
```yaml
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
```

70. How do you use `allow_failure` responsibly?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 70 script](interview-scripts/070-how-do-you-use-allow-failure-responsibly.yml)
```yaml
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
```

71. What is a scheduled pipeline?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
Script: [Question 71 script](interview-scripts/071-what-is-a-scheduled-pipeline.yml)
```yaml
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
```

72. How do you identify the pipeline source?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
Script: [Question 72 script](interview-scripts/072-how-do-you-identify-the-pipeline-source.yml)
```yaml
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
```

73. What are GitLab CI includes?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 73 script](interview-scripts/073-what-are-gitlab-ci-includes.yml)
```yaml
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
```

74. How do you reuse YAML with anchors and extends?
**Answer:** Extract the behavior behind a small documented interface, keep inputs and outputs explicit, and test the reusable unit independently.
Script: [Question 74 script](interview-scripts/074-how-do-you-reuse-yaml-with-anchors-and-extends.yml)
```yaml
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
```

75. What is a CI/CD component?
**Answer:** Extract the behavior behind a small documented interface, keep inputs and outputs explicit, and test the reusable unit independently.
Script: [Question 75 script](interview-scripts/075-what-is-a-ci-cd-component.yml)
```yaml
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
```

76. How do you share templates across projects?
**Answer:** Extract the behavior behind a small documented interface, keep inputs and outputs explicit, and test the reusable unit independently.
Script: [Question 76 script](interview-scripts/076-how-do-you-share-templates-across-projects.yml)
```yaml
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
```

77. How do you use runner tags?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
Script: [Question 77 script](interview-scripts/077-how-do-you-use-runner-tags.yml)
```yaml
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
```

78. What are protected runners?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
Script: [Question 78 script](interview-scripts/078-what-are-protected-runners.yml)
```yaml
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
```

79. How do you troubleshoot a job stuck pending?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
Script: [Question 79 script](interview-scripts/079-how-do-you-troubleshoot-a-job-stuck-pending.yml)
```yaml
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
```

80. How do you design a pipeline for a monorepo?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
Script: [Question 80 script](interview-scripts/080-how-do-you-design-a-pipeline-for-a-monorepo.yml)
```yaml
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
```


## Advanced: 81-120

81. Design a secure enterprise GitLab runner architecture.
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
Script: [Question 81 script](interview-scripts/081-design-a-secure-enterprise-gitlab-runner-architecture.yml)
```yaml
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
```

82. How do shared and group runners differ?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
Script: [Question 82 script](interview-scripts/082-how-do-shared-and-group-runners-differ.yml)
```yaml
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
```

83. How do you isolate untrusted merge-request code?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 83 script](interview-scripts/083-how-do-you-isolate-untrusted-merge-request-code.yml)
```yaml
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
```

84. How do you secure privileged Docker runners?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
Script: [Question 84 script](interview-scripts/084-how-do-you-secure-privileged-docker-runners.yml)
```yaml
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
```

85. What are the risks of Docker-in-Docker?
**Answer:** Build a minimal immutable image, pin dependencies, scan and sign it, publish it to a controlled registry, and deploy by digest when possible.
Script: [Question 85 script](interview-scripts/085-what-are-the-risks-of-docker-in-docker.yml)
```yaml
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
```

86. How do rootless or Kaniko-style builds change the threat model?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 86 script](interview-scripts/086-how-do-rootless-or-kaniko-style-builds-change-the-threa.yml)
```yaml
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
```

87. How do you implement Azure OIDC federation from GitLab?
**Answer:** Use provider-native identity with least privilege, explicit environment boundaries, tagging, policy controls, and repeatable infrastructure definitions.
Script: [Question 87 script](interview-scripts/087-how-do-you-implement-azure-oidc-federation-from-gitlab.yml)
```yaml
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
```

88. How do you implement AWS OIDC federation from GitLab?
**Answer:** Use provider-native identity with least privilege, explicit environment boundaries, tagging, policy controls, and repeatable infrastructure definitions.
Script: [Question 88 script](interview-scripts/088-how-do-you-implement-aws-oidc-federation-from-gitlab.yml)
```yaml
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
```

89. Why are short-lived cloud credentials preferable?
**Answer:** Keep the value in a protected secret store or workload identity, pass it at runtime, redact it from logs, and never commit it to source control.
Script: [Question 89 script](interview-scripts/089-why-are-short-lived-cloud-credentials-preferable.yml)
```yaml
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
```

90. How do you restrict a federated role to one project and branch?
**Answer:** Use a structured client, explicit timeouts, status handling, pagination, schema validation, and safe authentication rather than string parsing.
Script: [Question 90 script](interview-scripts/090-how-do-you-restrict-a-federated-role-to-one-project-and.yml)
```yaml
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
```

91. How do you manage protected secrets across environments?
**Answer:** Keep the value in a protected secret store or workload identity, pass it at runtime, redact it from logs, and never commit it to source control.
Script: [Question 91 script](interview-scripts/091-how-do-you-manage-protected-secrets-across-environments.yml)
```yaml
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
```

92. How do you rotate a credential without pipeline downtime?
**Answer:** Keep the value in a protected secret store or workload identity, pass it at runtime, redact it from logs, and never commit it to source control.
Script: [Question 92 script](interview-scripts/092-how-do-you-rotate-a-credential-without-pipeline-downtim.yml)
```yaml
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
```

93. How do you design a multi-account AWS deployment pipeline?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
Script: [Question 93 script](interview-scripts/093-how-do-you-design-a-multi-account-aws-deployment-pipeli.yml)
```yaml
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
```

94. How do you design a multi-subscription Azure deployment pipeline?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
Script: [Question 94 script](interview-scripts/094-how-do-you-design-a-multi-subscription-azure-deployment.yml)
```yaml
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
```

95. How do you promote immutable artifacts between environments?
**Answer:** Keep environment-specific values outside reusable logic, validate them at the boundary, and provide safe defaults only where appropriate.
Script: [Question 95 script](interview-scripts/095-how-do-you-promote-immutable-artifacts-between-environm.yml)
```yaml
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
```

96. How do you prevent rebuilding an artifact during promotion?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 96 script](interview-scripts/096-how-do-you-prevent-rebuilding-an-artifact-during-promot.yml)
```yaml
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
```

97. How do you implement canary deployment in GitLab?
**Answer:** Bound concurrency, preserve a small failure domain, verify health between batches, and stop promotion when the error budget is exceeded.
Script: [Question 97 script](interview-scripts/097-how-do-you-implement-canary-deployment-in-gitlab.yml)
```yaml
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
```

98. How do you gate production on health metrics?
**Answer:** Check a meaningful dependency or application endpoint, fail the operation when the check fails, and use the result to stop or roll back promotion.
Script: [Question 98 script](interview-scripts/098-how-do-you-gate-production-on-health-metrics.yml)
```yaml
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
```

99. How do you automate rollback after a failed smoke test?
**Answer:** Check a meaningful dependency or application endpoint, fail the operation when the check fails, and use the result to stop or roll back promotion.
Script: [Question 99 script](interview-scripts/099-how-do-you-automate-rollback-after-a-failed-smoke-test.yml)
```yaml
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
```

100. How do child pipelines improve pipeline scalability?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
Script: [Question 100 script](interview-scripts/100-how-do-child-pipelines-improve-pipeline-scalability.yml)
```yaml
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
```

101. How do dynamic child pipelines work?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
Script: [Question 101 script](interview-scripts/101-how-do-dynamic-child-pipelines-work.yml)
```yaml
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
```

102. How do multi-project pipelines coordinate dependencies?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
Script: [Question 102 script](interview-scripts/102-how-do-multi-project-pipelines-coordinate-dependencies.yml)
```yaml
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
```

103. How do you version shared pipeline templates?
**Answer:** Extract the behavior behind a small documented interface, keep inputs and outputs explicit, and test the reusable unit independently.
Script: [Question 103 script](interview-scripts/103-how-do-you-version-shared-pipeline-templates.yml)
```yaml
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
```

104. How do you prevent breaking changes in a shared template?
**Answer:** Extract the behavior behind a small documented interface, keep inputs and outputs explicit, and test the reusable unit independently.
Script: [Question 104 script](interview-scripts/104-how-do-you-prevent-breaking-changes-in-a-shared-templat.yml)
```yaml
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
```

105. How do you implement deployment concurrency control?
**Answer:** Bound concurrency, preserve a small failure domain, verify health between batches, and stop promotion when the error budget is exceeded.
Script: [Question 105 script](interview-scripts/105-how-do-you-implement-deployment-concurrency-control.yml)
```yaml
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
```

106. How do you model change freezes?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 106 script](interview-scripts/106-how-do-you-model-change-freezes.yml)
```yaml
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
```

107. How do you create a release from a tag?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
Script: [Question 107 script](interview-scripts/107-how-do-you-create-a-release-from-a-tag.yml)
```yaml
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
```

108. How do you sign release artifacts?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
Script: [Question 108 script](interview-scripts/108-how-do-you-sign-release-artifacts.yml)
```yaml
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
```

109. How do you verify image provenance in CI?
**Answer:** Build a minimal immutable image, pin dependencies, scan and sign it, publish it to a controlled registry, and deploy by digest when possible.
Script: [Question 109 script](interview-scripts/109-how-do-you-verify-image-provenance-in-ci.yml)
```yaml
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
```

110. How do you integrate SBOM generation and vulnerability gates?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 110 script](interview-scripts/110-how-do-you-integrate-sbom-generation-and-vulnerability.yml)
```yaml
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
```

111. How do you design disaster recovery for GitLab itself?
**Answer:** Keep the previous known-good version, validate the replacement, and automate a tested rollback or restore path with clear ownership and audit output.
Script: [Question 111 script](interview-scripts/111-how-do-you-design-disaster-recovery-for-gitlab-itself.yml)
```yaml
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
```

112. How do you back up repositories, registry data, and CI configuration?
**Answer:** Keep environment-specific values outside reusable logic, validate them at the boundary, and provide safe defaults only where appropriate.
Script: [Question 112 script](interview-scripts/112-how-do-you-back-up-repositories-registry-data-and-ci-co.yml)
```yaml
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
```

113. How do you test GitLab backup restoration?
**Answer:** Automate syntax, static analysis, unit, and integration checks in CI; fail early and publish useful diagnostics as artifacts.
Script: [Question 113 script](interview-scripts/113-how-do-you-test-gitlab-backup-restoration.yml)
```yaml
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
```

114. How do you observe pipeline health at organization scale?
**Answer:** Check a meaningful dependency or application endpoint, fail the operation when the check fails, and use the result to stop or roll back promotion.
Script: [Question 114 script](interview-scripts/114-how-do-you-observe-pipeline-health-at-organization-scal.yml)
```yaml
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
```

115. Which DORA metrics can GitLab provide?
**Answer:** Emit structured, correlation-aware telemetry with enough context to diagnose duration, failures, deployment version, and affected environment.
Script: [Question 115 script](interview-scripts/115-which-dora-metrics-can-gitlab-provide.yml)
```yaml
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
```

116. How do you reduce pipeline lead time without reducing safety?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
Script: [Question 116 script](interview-scripts/116-how-do-you-reduce-pipeline-lead-time-without-reducing-s.yml)
```yaml
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
```

117. How do you handle flaky tests without hiding defects?
**Answer:** Automate syntax, static analysis, unit, and integration checks in CI; fail early and publish useful diagnostics as artifacts.
Script: [Question 117 script](interview-scripts/117-how-do-you-handle-flaky-tests-without-hiding-defects.yml)
```yaml
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
```

118. How do you design a regulated production approval workflow?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 118 script](interview-scripts/118-how-do-you-design-a-regulated-production-approval-workf.yml)
```yaml
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
```

119. How do you connect GitLab deployment events to incident management?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
Script: [Question 119 script](interview-scripts/119-how-do-you-connect-gitlab-deployment-events-to-incident.yml)
```yaml
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
```

120. Design a secure, reusable, observable GitLab platform for Azure, AWS, and on-premises delivery.
**Answer:** Emit structured, correlation-aware telemetry with enough context to diagnose duration, failures, deployment version, and affected environment.
Script: [Question 120 script](interview-scripts/120-design-a-secure-reusable-observable-gitlab-platform-for.yml)
```yaml
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
```


## HackerRank-Style CI/CD Challenges: 121-150

121. Write a pipeline with lint, test, build, and deploy stages.
**Answer:** Test the happy path, invalid input, timeout, retry exhaustion, and partial failure with mocks for external systems and an assertion on the final result.
Script: [Question 121 script](interview-scripts/121-write-a-pipeline-with-lint-test-build-and-deploy-stages.yml)
```yaml
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
```

122. Store a generated report as an artifact.
**Answer:** Separate validation, build, promotion, and verification jobs; use immutable artifacts, protected variables or OIDC, and manual approval for production.
Script: [Question 122 script](interview-scripts/122-store-a-generated-report-as-an-artifact.yml)
```yaml
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
```

123. Cache Python dependencies with a branch-safe key.
**Answer:** Implement the solution with validated inputs, deterministic behavior, clear failure handling, tests, and an example execution command for GitLab CI/CD.
Script: [Question 123 script](interview-scripts/123-cache-python-dependencies-with-a-branch-safe-key.yml)
```yaml
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
```

124. Run deployment only on the default branch.
**Answer:** Deploy an immutable version, run a health or smoke check, promote only on success, and invoke a tested rollback while preserving the failure in logs.
Script: [Question 124 script](interview-scripts/124-run-deployment-only-on-the-default-branch.yml)
```yaml
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
```

125. Add a manual production job with a protected environment.
**Answer:** Parse with the platform's structured data tool, validate required fields and types at the boundary, and return a clear nonzero failure for malformed input.
Script: [Question 125 script](interview-scripts/125-add-a-manual-production-job-with-a-protected-environmen.yml)
```yaml
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
```

126. Build and push an immutable commit-SHA Docker tag.
**Answer:** Use declarative manifests with pinned images, probes, resource controls, least-privilege identity, and a rollout strategy that can be observed and rolled back.
Script: [Question 126 script](interview-scripts/126-build-and-push-an-immutable-commit-sha-docker-tag.yml)
```yaml
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
```

127. Test two Python versions and two database engines with a matrix.
**Answer:** Test the happy path, invalid input, timeout, retry exhaustion, and partial failure with mocks for external systems and an assertion on the final result.
Script: [Question 127 script](interview-scripts/127-test-two-python-versions-and-two-database-engines-with.yml)
```yaml
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
```

128. Build a DAG so independent tests run in parallel.
**Answer:** Use a bounded worker pool, collect each success and exception separately, and fail the operation when the defined error threshold is exceeded.
Script: [Question 128 script](interview-scripts/128-build-a-dag-so-independent-tests-run-in-parallel.yml)
```yaml
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
```

129. Create a review app and manual stop job.
**Answer:** Separate validation, build, promotion, and verification jobs; use immutable artifacts, protected variables or OIDC, and manual approval for production.
Script: [Question 129 script](interview-scripts/129-create-a-review-app-and-manual-stop-job.yml)
```yaml
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
```

130. Always upload JUnit test results.
**Answer:** Test the happy path, invalid input, timeout, retry exhaustion, and partial failure with mocks for external systems and an assertion on the final result.
Script: [Question 130 script](interview-scripts/130-always-upload-junit-test-results.yml)
```yaml
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
```

131. Include SAST and dependency scanning templates.
**Answer:** Implement the solution with validated inputs, deterministic behavior, clear failure handling, tests, and an example execution command for GitLab CI/CD.
Script: [Question 131 script](interview-scripts/131-include-sast-and-dependency-scanning-templates.yml)
```yaml
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
```

132. Include secret detection and fail on a finding.
**Answer:** Implement the solution with validated inputs, deterministic behavior, clear failure handling, tests, and an example execution command for GitLab CI/CD.
Script: [Question 132 script](interview-scripts/132-include-secret-detection-and-fail-on-a-finding.yml)
```yaml
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
```

133. Add a Helm lint job.
**Answer:** Separate validation, build, promotion, and verification jobs; use immutable artifacts, protected variables or OIDC, and manual approval for production.
Script: [Question 133 script](interview-scripts/133-add-a-helm-lint-job.yml)
```yaml
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
```

134. Add a Terraform validate and plan job.
**Answer:** Express the desired state with typed inputs, stable addresses, policy validation, protected state, and a reviewed plan before apply.
Script: [Question 134 script](interview-scripts/134-add-a-terraform-validate-and-plan-job.yml)
```yaml
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
```

135. Obtain Azure credentials through OIDC.
**Answer:** Separate validation, build, promotion, and verification jobs; use immutable artifacts, protected variables or OIDC, and manual approval for production.
Script: [Question 135 script](interview-scripts/135-obtain-azure-credentials-through-oidc.yml)
```yaml
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
```

136. Obtain AWS identity through OIDC.
**Answer:** Separate validation, build, promotion, and verification jobs; use immutable artifacts, protected variables or OIDC, and manual approval for production.
Script: [Question 136 script](interview-scripts/136-obtain-aws-identity-through-oidc.yml)
```yaml
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
```

137. Generate a child pipeline from an artifact.
**Answer:** Separate validation, build, promotion, and verification jobs; use immutable artifacts, protected variables or OIDC, and manual approval for production.
Script: [Question 137 script](interview-scripts/137-generate-a-child-pipeline-from-an-artifact.yml)
```yaml
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
```

138. Wait for an infrastructure project with a multi-project pipeline.
**Answer:** Separate validation, build, promotion, and verification jobs; use immutable artifacts, protected variables or OIDC, and manual approval for production.
Script: [Question 138 script](interview-scripts/138-wait-for-an-infrastructure-project-with-a-multi-project.yml)
```yaml
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
```

139. Serialize production deployments with `resource_group`.
**Answer:** Parse the input into structured records, use a map or counter for aggregation, sort only when ranking is required, and test empty, duplicate, and boundary inputs.
Script: [Question 139 script](interview-scripts/139-serialize-production-deployments-with-resource-group.yml)
```yaml
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
```

140. Create a canary, smoke-test, and manual promotion flow.
**Answer:** Test the happy path, invalid input, timeout, retry exhaustion, and partial failure with mocks for external systems and an assertion on the final result.
Script: [Question 140 script](interview-scripts/140-create-a-canary-smoke-test-and-manual-promotion-flow.yml)
```yaml
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
```

141. Create a tag-based release job.
**Answer:** Deploy an immutable version, run a health or smoke check, promote only on success, and invoke a tested rollback while preserving the failure in logs.
Script: [Question 141 script](interview-scripts/141-create-a-tag-based-release-job.yml)
```yaml
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
```

142. Run a job only from a scheduled pipeline.
**Answer:** Separate validation, build, promotion, and verification jobs; use immutable artifacts, protected variables or OIDC, and manual approval for production.
Script: [Question 142 script](interview-scripts/142-run-a-job-only-from-a-scheduled-pipeline.yml)
```yaml
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
```

143. Block production changes during a deployment freeze.
**Answer:** Deploy an immutable version, run a health or smoke check, promote only on success, and invoke a tested rollback while preserving the failure in logs.
Script: [Question 143 script](interview-scripts/143-block-production-changes-during-a-deployment-freeze.yml)
```yaml
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
```

144. Add a manual rollback job for a previous artifact.
**Answer:** Deploy an immutable version, run a health or smoke check, promote only on success, and invoke a tested rollback while preserving the failure in logs.
Script: [Question 144 script](interview-scripts/144-add-a-manual-rollback-job-for-a-previous-artifact.yml)
```yaml
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
```

145. Send a failure notification from `after_script`.
**Answer:** Implement the solution with validated inputs, deterministic behavior, clear failure handling, tests, and an example execution command for GitLab CI/CD.
Script: [Question 145 script](interview-scripts/145-send-a-failure-notification-from-after-script.yml)
```yaml
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
```

146. Publish pipeline duration metrics.
**Answer:** Separate validation, build, promotion, and verification jobs; use immutable artifacts, protected variables or OIDC, and manual approval for production.
Script: [Question 146 script](interview-scripts/146-publish-pipeline-duration-metrics.yml)
```yaml
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
```

147. Retain a backup artifact for 30 days.
**Answer:** Separate validation, build, promotion, and verification jobs; use immutable artifacts, protected variables or OIDC, and manual approval for production.
Script: [Question 147 script](interview-scripts/147-retain-a-backup-artifact-for-30-days.yml)
```yaml
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
```

148. Protect cloud credentials without plaintext secrets.
**Answer:** Implement the solution with validated inputs, deterministic behavior, clear failure handling, tests, and an example execution command for GitLab CI/CD.
Script: [Question 148 script](interview-scripts/148-protect-cloud-credentials-without-plaintext-secrets.yml)
```yaml
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
```

149. Build a reusable YAML component for security gates.
**Answer:** Separate validation, build, promotion, and verification jobs; use immutable artifacts, protected variables or OIDC, and manual approval for production.
Script: [Question 149 script](interview-scripts/149-build-a-reusable-yaml-component-for-security-gates.yml)
```yaml
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
```

150. Build a secure pipeline with OIDC, immutable artifacts, canary, rollback, and metrics.
**Answer:** Deploy an immutable version, run a health or smoke check, promote only on success, and invoke a tested rollback while preserving the failure in logs.
Script: [Question 150 script](interview-scripts/150-build-a-secure-pipeline-with-oidc-immutable-artifacts-c.yml)
```yaml
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
```


## Executable Answers

- [Beginner answers](interview-answers/beginner.yml): stages, dependencies, and artifacts.
- [Intermediate answers](interview-answers/intermediate.yml): matrix testing and review apps.
- [Advanced answers](interview-answers/advanced.yml): canary promotion, smoke tests, and deployment locking.
