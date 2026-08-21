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
<a href="interview-scripts/001-what-problem-does-gitlab-ci-cd-solve.yml"><img src="https://img.shields.io/badge/Question%201%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 1 script"></a>
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
<a href="interview-scripts/002-what-is-a-gitlab-project.yml"><img src="https://img.shields.io/badge/Question%202%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 2 script"></a>
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
<a href="interview-scripts/003-what-is-a-repository.yml"><img src="https://img.shields.io/badge/Question%203%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 3 script"></a>
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
<a href="interview-scripts/004-what-is-a-commit.yml"><img src="https://img.shields.io/badge/Question%204%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 4 script"></a>
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
<a href="interview-scripts/005-what-is-a-branch.yml"><img src="https://img.shields.io/badge/Question%205%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 5 script"></a>
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
<a href="interview-scripts/006-what-is-a-merge-request.yml"><img src="https://img.shields.io/badge/Question%206%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 6 script"></a>
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
<a href="interview-scripts/007-what-is-a-protected-branch.yml"><img src="https://img.shields.io/badge/Question%207%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 7 script"></a>
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
<a href="interview-scripts/008-what-is-a-gitlab-ci-yml-file.yml"><img src="https://img.shields.io/badge/Question%208%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 8 script"></a>
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
<a href="interview-scripts/009-what-is-a-pipeline.yml"><img src="https://img.shields.io/badge/Question%209%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 9 script"></a>
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
<a href="interview-scripts/010-what-is-a-stage.yml"><img src="https://img.shields.io/badge/Question%2010%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 10 script"></a>
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
<a href="interview-scripts/011-what-is-a-job.yml"><img src="https://img.shields.io/badge/Question%2011%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 11 script"></a>
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
<a href="interview-scripts/012-what-is-a-runner.yml"><img src="https://img.shields.io/badge/Question%2012%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 12 script"></a>
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
<a href="interview-scripts/013-what-is-an-executor.yml"><img src="https://img.shields.io/badge/Question%2013%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 13 script"></a>
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
<a href="interview-scripts/014-what-is-the-purpose-of-an-image-in-a-job.yml"><img src="https://img.shields.io/badge/Question%2014%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 14 script"></a>
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
<a href="interview-scripts/015-what-does-the-script-keyword-define.yml"><img src="https://img.shields.io/badge/Question%2015%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 15 script"></a>
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
<a href="interview-scripts/016-what-is-the-difference-between-before-script-and-after.yml"><img src="https://img.shields.io/badge/Question%2016%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 16 script"></a>
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
<a href="interview-scripts/017-what-is-an-artifact.yml"><img src="https://img.shields.io/badge/Question%2017%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 17 script"></a>
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
<a href="interview-scripts/018-what-is-a-cache.yml"><img src="https://img.shields.io/badge/Question%2018%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 18 script"></a>
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
<a href="interview-scripts/019-how-do-artifacts-differ-from-cache.yml"><img src="https://img.shields.io/badge/Question%2019%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 19 script"></a>
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
<a href="interview-scripts/020-what-are-predefined-ci-cd-variables.yml"><img src="https://img.shields.io/badge/Question%2020%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 20 script"></a>
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
<a href="interview-scripts/021-what-is-ci-commit-sha.yml"><img src="https://img.shields.io/badge/Question%2021%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 21 script"></a>
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
<a href="interview-scripts/022-what-is-ci-commit-ref-name.yml"><img src="https://img.shields.io/badge/Question%2022%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 22 script"></a>
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
<a href="interview-scripts/023-how-do-you-define-a-custom-variable.yml"><img src="https://img.shields.io/badge/Question%2023%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 23 script"></a>
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
<a href="interview-scripts/024-what-is-a-manual-job.yml"><img src="https://img.shields.io/badge/Question%2024%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 24 script"></a>
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
<a href="interview-scripts/025-what-does-when-manual-do.yml"><img src="https://img.shields.io/badge/Question%2025%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 25 script"></a>
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
<a href="interview-scripts/026-what-is-a-pipeline-environment.yml"><img src="https://img.shields.io/badge/Question%2026%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 26 script"></a>
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
<a href="interview-scripts/027-how-do-you-name-a-staging-environment.yml"><img src="https://img.shields.io/badge/Question%2027%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 27 script"></a>
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
<a href="interview-scripts/028-what-is-a-pipeline-rule.yml"><img src="https://img.shields.io/badge/Question%2028%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 28 script"></a>
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
<a href="interview-scripts/029-what-does-workflow-rules-control.yml"><img src="https://img.shields.io/badge/Question%2029%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 29 script"></a>
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
<a href="interview-scripts/030-how-do-you-run-a-job-only-on-the-default-branch.yml"><img src="https://img.shields.io/badge/Question%2030%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 30 script"></a>
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
<a href="interview-scripts/031-what-is-a-docker-in-docker-service.yml"><img src="https://img.shields.io/badge/Question%2031%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 31 script"></a>
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
<a href="interview-scripts/032-how-do-you-build-a-docker-image-in-gitlab-ci.yml"><img src="https://img.shields.io/badge/Question%2032%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 32 script"></a>
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
<a href="interview-scripts/033-what-is-the-gitlab-container-registry.yml"><img src="https://img.shields.io/badge/Question%2033%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 33 script"></a>
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
<a href="interview-scripts/034-how-do-you-authenticate-to-the-registry.yml"><img src="https://img.shields.io/badge/Question%2034%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 34 script"></a>
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
<a href="interview-scripts/035-where-should-passwords-be-stored.yml"><img src="https://img.shields.io/badge/Question%2035%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 35 script"></a>
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
<a href="interview-scripts/036-what-is-a-masked-variable.yml"><img src="https://img.shields.io/badge/Question%2036%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 36 script"></a>
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
<a href="interview-scripts/037-what-is-a-protected-variable.yml"><img src="https://img.shields.io/badge/Question%2037%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 37 script"></a>
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
<a href="interview-scripts/038-how-do-you-inspect-a-failed-job-log.yml"><img src="https://img.shields.io/badge/Question%2038%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 38 script"></a>
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
<a href="interview-scripts/039-what-is-a-retry-and-when-is-it-appropriate.yml"><img src="https://img.shields.io/badge/Question%2039%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 39 script"></a>
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
<a href="interview-scripts/040-how-do-you-cancel-a-running-pipeline.yml"><img src="https://img.shields.io/badge/Question%2040%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 40 script"></a>
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
<a href="interview-scripts/041-how-do-jobs-move-through-stages.yml"><img src="https://img.shields.io/badge/Question%2041%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 41 script"></a>
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
<a href="interview-scripts/042-what-does-needs-change-about-pipeline-execution.yml"><img src="https://img.shields.io/badge/Question%2042%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 42 script"></a>
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
<a href="interview-scripts/043-how-do-you-construct-a-directed-acyclic-pipeline-graph.yml"><img src="https://img.shields.io/badge/Question%2043%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 43 script"></a>
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
<a href="interview-scripts/044-what-is-parallel-matrix.yml"><img src="https://img.shields.io/badge/Question%2044%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 44 script"></a>
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
<a href="interview-scripts/045-how-do-you-test-multiple-language-versions.yml"><img src="https://img.shields.io/badge/Question%2045%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 45 script"></a>
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
<a href="interview-scripts/046-how-do-you-pass-artifacts-between-jobs.yml"><img src="https://img.shields.io/badge/Question%2046%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 46 script"></a>
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
<a href="interview-scripts/047-how-do-you-set-artifact-expiration.yml"><img src="https://img.shields.io/badge/Question%2047%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 47 script"></a>
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
<a href="interview-scripts/048-how-do-you-cache-language-dependencies.yml"><img src="https://img.shields.io/badge/Question%2048%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 48 script"></a>
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
<a href="interview-scripts/049-how-do-cache-keys-affect-correctness.yml"><img src="https://img.shields.io/badge/Question%2049%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 49 script"></a>
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
<a href="interview-scripts/050-how-do-rules-differ-from-legacy-only-and-except.yml"><img src="https://img.shields.io/badge/Question%2050%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 50 script"></a>
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
<a href="interview-scripts/051-how-do-you-prevent-duplicate-branch-and-merge-request-p.yml"><img src="https://img.shields.io/badge/Question%2051%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 51 script"></a>
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
<a href="interview-scripts/052-how-do-you-create-a-review-app.yml"><img src="https://img.shields.io/badge/Question%2052%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 52 script"></a>
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
<a href="interview-scripts/053-how-do-you-stop-a-review-app.yml"><img src="https://img.shields.io/badge/Question%2053%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 53 script"></a>
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
<a href="interview-scripts/054-what-is-a-protected-environment.yml"><img src="https://img.shields.io/badge/Question%2054%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 54 script"></a>
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
<a href="interview-scripts/055-how-do-deployment-approvals-work.yml"><img src="https://img.shields.io/badge/Question%2055%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 55 script"></a>
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
<a href="interview-scripts/056-what-is-a-resource-group.yml"><img src="https://img.shields.io/badge/Question%2056%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 56 script"></a>
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
<a href="interview-scripts/057-how-do-you-prevent-concurrent-production-deployments.yml"><img src="https://img.shields.io/badge/Question%2057%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 57 script"></a>
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
<a href="interview-scripts/058-how-do-you-publish-junit-test-reports.yml"><img src="https://img.shields.io/badge/Question%2058%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 58 script"></a>
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
<a href="interview-scripts/059-what-is-a-dotenv-report.yml"><img src="https://img.shields.io/badge/Question%2059%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 59 script"></a>
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
<a href="interview-scripts/060-how-do-you-publish-code-quality-results.yml"><img src="https://img.shields.io/badge/Question%2060%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 60 script"></a>
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
<a href="interview-scripts/061-how-do-sast-templates-work.yml"><img src="https://img.shields.io/badge/Question%2061%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 61 script"></a>
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
<a href="interview-scripts/062-how-does-dependency-scanning-work.yml"><img src="https://img.shields.io/badge/Question%2062%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 62 script"></a>
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
<a href="interview-scripts/063-how-does-secret-detection-work.yml"><img src="https://img.shields.io/badge/Question%2063%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 63 script"></a>
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
<a href="interview-scripts/064-how-do-you-scan-container-images.yml"><img src="https://img.shields.io/badge/Question%2064%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 64 script"></a>
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
<a href="interview-scripts/065-how-do-you-lint-helm-charts-in-ci.yml"><img src="https://img.shields.io/badge/Question%2065%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 65 script"></a>
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
<a href="interview-scripts/066-how-do-you-run-terraform-validate-and-plan.yml"><img src="https://img.shields.io/badge/Question%2066%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 66 script"></a>
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
<a href="interview-scripts/067-how-do-you-prevent-terraform-plan-secrets-leaking-in-ar.yml"><img src="https://img.shields.io/badge/Question%2067%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 67 script"></a>
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
<a href="interview-scripts/068-what-is-an-environment-url.yml"><img src="https://img.shields.io/badge/Question%2068%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 68 script"></a>
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
<a href="interview-scripts/069-how-do-you-define-a-deployment-rollback-job.yml"><img src="https://img.shields.io/badge/Question%2069%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 69 script"></a>
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
<a href="interview-scripts/070-how-do-you-use-allow-failure-responsibly.yml"><img src="https://img.shields.io/badge/Question%2070%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 70 script"></a>
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
<a href="interview-scripts/071-what-is-a-scheduled-pipeline.yml"><img src="https://img.shields.io/badge/Question%2071%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 71 script"></a>
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
<a href="interview-scripts/072-how-do-you-identify-the-pipeline-source.yml"><img src="https://img.shields.io/badge/Question%2072%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 72 script"></a>
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
<a href="interview-scripts/073-what-are-gitlab-ci-includes.yml"><img src="https://img.shields.io/badge/Question%2073%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 73 script"></a>
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
<a href="interview-scripts/074-how-do-you-reuse-yaml-with-anchors-and-extends.yml"><img src="https://img.shields.io/badge/Question%2074%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 74 script"></a>
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
<a href="interview-scripts/075-what-is-a-ci-cd-component.yml"><img src="https://img.shields.io/badge/Question%2075%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 75 script"></a>
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
<a href="interview-scripts/076-how-do-you-share-templates-across-projects.yml"><img src="https://img.shields.io/badge/Question%2076%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 76 script"></a>
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
<a href="interview-scripts/077-how-do-you-use-runner-tags.yml"><img src="https://img.shields.io/badge/Question%2077%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 77 script"></a>
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
<a href="interview-scripts/078-what-are-protected-runners.yml"><img src="https://img.shields.io/badge/Question%2078%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 78 script"></a>
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
<a href="interview-scripts/079-how-do-you-troubleshoot-a-job-stuck-pending.yml"><img src="https://img.shields.io/badge/Question%2079%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 79 script"></a>
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
<a href="interview-scripts/080-how-do-you-design-a-pipeline-for-a-monorepo.yml"><img src="https://img.shields.io/badge/Question%2080%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 80 script"></a>
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
<a href="interview-scripts/081-design-a-secure-enterprise-gitlab-runner-architecture.yml"><img src="https://img.shields.io/badge/Question%2081%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 81 script"></a>
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
<a href="interview-scripts/082-how-do-shared-and-group-runners-differ.yml"><img src="https://img.shields.io/badge/Question%2082%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 82 script"></a>
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
<a href="interview-scripts/083-how-do-you-isolate-untrusted-merge-request-code.yml"><img src="https://img.shields.io/badge/Question%2083%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 83 script"></a>
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
<a href="interview-scripts/084-how-do-you-secure-privileged-docker-runners.yml"><img src="https://img.shields.io/badge/Question%2084%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 84 script"></a>
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
<a href="interview-scripts/085-what-are-the-risks-of-docker-in-docker.yml"><img src="https://img.shields.io/badge/Question%2085%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 85 script"></a>
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
<a href="interview-scripts/086-how-do-rootless-or-kaniko-style-builds-change-the-threa.yml"><img src="https://img.shields.io/badge/Question%2086%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 86 script"></a>
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
<a href="interview-scripts/087-how-do-you-implement-azure-oidc-federation-from-gitlab.yml"><img src="https://img.shields.io/badge/Question%2087%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 87 script"></a>
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
<a href="interview-scripts/088-how-do-you-implement-aws-oidc-federation-from-gitlab.yml"><img src="https://img.shields.io/badge/Question%2088%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 88 script"></a>
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
<a href="interview-scripts/089-why-are-short-lived-cloud-credentials-preferable.yml"><img src="https://img.shields.io/badge/Question%2089%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 89 script"></a>
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
<a href="interview-scripts/090-how-do-you-restrict-a-federated-role-to-one-project-and.yml"><img src="https://img.shields.io/badge/Question%2090%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 90 script"></a>
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
<a href="interview-scripts/091-how-do-you-manage-protected-secrets-across-environments.yml"><img src="https://img.shields.io/badge/Question%2091%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 91 script"></a>
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
<a href="interview-scripts/092-how-do-you-rotate-a-credential-without-pipeline-downtim.yml"><img src="https://img.shields.io/badge/Question%2092%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 92 script"></a>
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
<a href="interview-scripts/093-how-do-you-design-a-multi-account-aws-deployment-pipeli.yml"><img src="https://img.shields.io/badge/Question%2093%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 93 script"></a>
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
<a href="interview-scripts/094-how-do-you-design-a-multi-subscription-azure-deployment.yml"><img src="https://img.shields.io/badge/Question%2094%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 94 script"></a>
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
<a href="interview-scripts/095-how-do-you-promote-immutable-artifacts-between-environm.yml"><img src="https://img.shields.io/badge/Question%2095%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 95 script"></a>
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
<a href="interview-scripts/096-how-do-you-prevent-rebuilding-an-artifact-during-promot.yml"><img src="https://img.shields.io/badge/Question%2096%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 96 script"></a>
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
<a href="interview-scripts/097-how-do-you-implement-canary-deployment-in-gitlab.yml"><img src="https://img.shields.io/badge/Question%2097%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 97 script"></a>
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
<a href="interview-scripts/098-how-do-you-gate-production-on-health-metrics.yml"><img src="https://img.shields.io/badge/Question%2098%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 98 script"></a>
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
<a href="interview-scripts/099-how-do-you-automate-rollback-after-a-failed-smoke-test.yml"><img src="https://img.shields.io/badge/Question%2099%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 99 script"></a>
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
<a href="interview-scripts/100-how-do-child-pipelines-improve-pipeline-scalability.yml"><img src="https://img.shields.io/badge/Question%20100%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 100 script"></a>
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
<a href="interview-scripts/101-how-do-dynamic-child-pipelines-work.yml"><img src="https://img.shields.io/badge/Question%20101%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 101 script"></a>
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
<a href="interview-scripts/102-how-do-multi-project-pipelines-coordinate-dependencies.yml"><img src="https://img.shields.io/badge/Question%20102%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 102 script"></a>
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
<a href="interview-scripts/103-how-do-you-version-shared-pipeline-templates.yml"><img src="https://img.shields.io/badge/Question%20103%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 103 script"></a>
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
<a href="interview-scripts/104-how-do-you-prevent-breaking-changes-in-a-shared-templat.yml"><img src="https://img.shields.io/badge/Question%20104%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 104 script"></a>
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
<a href="interview-scripts/105-how-do-you-implement-deployment-concurrency-control.yml"><img src="https://img.shields.io/badge/Question%20105%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 105 script"></a>
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
<a href="interview-scripts/106-how-do-you-model-change-freezes.yml"><img src="https://img.shields.io/badge/Question%20106%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 106 script"></a>
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
<a href="interview-scripts/107-how-do-you-create-a-release-from-a-tag.yml"><img src="https://img.shields.io/badge/Question%20107%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 107 script"></a>
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
<a href="interview-scripts/108-how-do-you-sign-release-artifacts.yml"><img src="https://img.shields.io/badge/Question%20108%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 108 script"></a>
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
<a href="interview-scripts/109-how-do-you-verify-image-provenance-in-ci.yml"><img src="https://img.shields.io/badge/Question%20109%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 109 script"></a>
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
<a href="interview-scripts/110-how-do-you-integrate-sbom-generation-and-vulnerability.yml"><img src="https://img.shields.io/badge/Question%20110%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 110 script"></a>
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
<a href="interview-scripts/111-how-do-you-design-disaster-recovery-for-gitlab-itself.yml"><img src="https://img.shields.io/badge/Question%20111%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 111 script"></a>
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
<a href="interview-scripts/112-how-do-you-back-up-repositories-registry-data-and-ci-co.yml"><img src="https://img.shields.io/badge/Question%20112%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 112 script"></a>
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
<a href="interview-scripts/113-how-do-you-test-gitlab-backup-restoration.yml"><img src="https://img.shields.io/badge/Question%20113%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 113 script"></a>
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
<a href="interview-scripts/114-how-do-you-observe-pipeline-health-at-organization-scal.yml"><img src="https://img.shields.io/badge/Question%20114%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 114 script"></a>
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
<a href="interview-scripts/115-which-dora-metrics-can-gitlab-provide.yml"><img src="https://img.shields.io/badge/Question%20115%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 115 script"></a>
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
<a href="interview-scripts/116-how-do-you-reduce-pipeline-lead-time-without-reducing-s.yml"><img src="https://img.shields.io/badge/Question%20116%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 116 script"></a>
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
<a href="interview-scripts/117-how-do-you-handle-flaky-tests-without-hiding-defects.yml"><img src="https://img.shields.io/badge/Question%20117%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 117 script"></a>
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
<a href="interview-scripts/118-how-do-you-design-a-regulated-production-approval-workf.yml"><img src="https://img.shields.io/badge/Question%20118%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 118 script"></a>
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
<a href="interview-scripts/119-how-do-you-connect-gitlab-deployment-events-to-incident.yml"><img src="https://img.shields.io/badge/Question%20119%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 119 script"></a>
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
<a href="interview-scripts/120-design-a-secure-reusable-observable-gitlab-platform-for.yml"><img src="https://img.shields.io/badge/Question%20120%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 120 script"></a>
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
<a href="interview-scripts/121-write-a-pipeline-with-lint-test-build-and-deploy-stages.yml"><img src="https://img.shields.io/badge/Question%20121%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 121 script"></a>
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
<a href="interview-scripts/122-store-a-generated-report-as-an-artifact.yml"><img src="https://img.shields.io/badge/Question%20122%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 122 script"></a>
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
<a href="interview-scripts/123-cache-python-dependencies-with-a-branch-safe-key.yml"><img src="https://img.shields.io/badge/Question%20123%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 123 script"></a>
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
<a href="interview-scripts/124-run-deployment-only-on-the-default-branch.yml"><img src="https://img.shields.io/badge/Question%20124%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 124 script"></a>
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
<a href="interview-scripts/125-add-a-manual-production-job-with-a-protected-environmen.yml"><img src="https://img.shields.io/badge/Question%20125%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 125 script"></a>
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
<a href="interview-scripts/126-build-and-push-an-immutable-commit-sha-docker-tag.yml"><img src="https://img.shields.io/badge/Question%20126%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 126 script"></a>
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
<a href="interview-scripts/127-test-two-python-versions-and-two-database-engines-with.yml"><img src="https://img.shields.io/badge/Question%20127%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 127 script"></a>
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
<a href="interview-scripts/128-build-a-dag-so-independent-tests-run-in-parallel.yml"><img src="https://img.shields.io/badge/Question%20128%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 128 script"></a>
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
<a href="interview-scripts/129-create-a-review-app-and-manual-stop-job.yml"><img src="https://img.shields.io/badge/Question%20129%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 129 script"></a>
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
<a href="interview-scripts/130-always-upload-junit-test-results.yml"><img src="https://img.shields.io/badge/Question%20130%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 130 script"></a>
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
<a href="interview-scripts/131-include-sast-and-dependency-scanning-templates.yml"><img src="https://img.shields.io/badge/Question%20131%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 131 script"></a>
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
<a href="interview-scripts/132-include-secret-detection-and-fail-on-a-finding.yml"><img src="https://img.shields.io/badge/Question%20132%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 132 script"></a>
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
<a href="interview-scripts/133-add-a-helm-lint-job.yml"><img src="https://img.shields.io/badge/Question%20133%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 133 script"></a>
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
<a href="interview-scripts/134-add-a-terraform-validate-and-plan-job.yml"><img src="https://img.shields.io/badge/Question%20134%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 134 script"></a>
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
<a href="interview-scripts/135-obtain-azure-credentials-through-oidc.yml"><img src="https://img.shields.io/badge/Question%20135%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 135 script"></a>
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
<a href="interview-scripts/136-obtain-aws-identity-through-oidc.yml"><img src="https://img.shields.io/badge/Question%20136%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 136 script"></a>
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
<a href="interview-scripts/137-generate-a-child-pipeline-from-an-artifact.yml"><img src="https://img.shields.io/badge/Question%20137%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 137 script"></a>
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
<a href="interview-scripts/138-wait-for-an-infrastructure-project-with-a-multi-project.yml"><img src="https://img.shields.io/badge/Question%20138%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 138 script"></a>
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
<a href="interview-scripts/139-serialize-production-deployments-with-resource-group.yml"><img src="https://img.shields.io/badge/Question%20139%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 139 script"></a>
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
<a href="interview-scripts/140-create-a-canary-smoke-test-and-manual-promotion-flow.yml"><img src="https://img.shields.io/badge/Question%20140%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 140 script"></a>
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
<a href="interview-scripts/141-create-a-tag-based-release-job.yml"><img src="https://img.shields.io/badge/Question%20141%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 141 script"></a>
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
<a href="interview-scripts/142-run-a-job-only-from-a-scheduled-pipeline.yml"><img src="https://img.shields.io/badge/Question%20142%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 142 script"></a>
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
<a href="interview-scripts/143-block-production-changes-during-a-deployment-freeze.yml"><img src="https://img.shields.io/badge/Question%20143%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 143 script"></a>
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
<a href="interview-scripts/144-add-a-manual-rollback-job-for-a-previous-artifact.yml"><img src="https://img.shields.io/badge/Question%20144%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 144 script"></a>
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
<a href="interview-scripts/145-send-a-failure-notification-from-after-script.yml"><img src="https://img.shields.io/badge/Question%20145%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 145 script"></a>
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
<a href="interview-scripts/146-publish-pipeline-duration-metrics.yml"><img src="https://img.shields.io/badge/Question%20146%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 146 script"></a>
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
<a href="interview-scripts/147-retain-a-backup-artifact-for-30-days.yml"><img src="https://img.shields.io/badge/Question%20147%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 147 script"></a>
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
<a href="interview-scripts/148-protect-cloud-credentials-without-plaintext-secrets.yml"><img src="https://img.shields.io/badge/Question%20148%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 148 script"></a>
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
<a href="interview-scripts/149-build-a-reusable-yaml-component-for-security-gates.yml"><img src="https://img.shields.io/badge/Question%20149%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 149 script"></a>
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
<a href="interview-scripts/150-build-a-secure-pipeline-with-oidc-immutable-artifacts-c.yml"><img src="https://img.shields.io/badge/Question%20150%20script-Open-2088FF?style=for-the-badge&logo=github&logoColor=white" alt="Open question 150 script"></a>
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
