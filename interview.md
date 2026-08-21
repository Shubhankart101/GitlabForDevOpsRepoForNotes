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
2. What is a GitLab project?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 2 script](interview-scripts/002-what-is-a-gitlab-project.yml)
3. What is a repository?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 3 script](interview-scripts/003-what-is-a-repository.yml)
4. What is a commit?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 4 script](interview-scripts/004-what-is-a-commit.yml)
5. What is a branch?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 5 script](interview-scripts/005-what-is-a-branch.yml)
6. What is a merge request?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 6 script](interview-scripts/006-what-is-a-merge-request.yml)
7. What is a protected branch?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 7 script](interview-scripts/007-what-is-a-protected-branch.yml)
8. What is a `.gitlab-ci.yml` file?
**Answer:** Use structured filesystem APIs, validate paths, quote inputs, handle missing resources deliberately, and avoid unsafe traversal or shell expansion.
Script: [Question 8 script](interview-scripts/008-what-is-a-gitlab-ci-yml-file.yml)
9. What is a pipeline?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
Script: [Question 9 script](interview-scripts/009-what-is-a-pipeline.yml)
10. What is a stage?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
Script: [Question 10 script](interview-scripts/010-what-is-a-stage.yml)
11. What is a job?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
Script: [Question 11 script](interview-scripts/011-what-is-a-job.yml)
12. What is a runner?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
Script: [Question 12 script](interview-scripts/012-what-is-a-runner.yml)
13. What is an executor?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 13 script](interview-scripts/013-what-is-an-executor.yml)
14. What is the purpose of an image in a job?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
Script: [Question 14 script](interview-scripts/014-what-is-the-purpose-of-an-image-in-a-job.yml)
15. What does the `script` keyword define?
**Answer:** Keep the value in a protected secret store or workload identity, pass it at runtime, redact it from logs, and never commit it to source control.
Script: [Question 15 script](interview-scripts/015-what-does-the-script-keyword-define.yml)
16. What is the difference between `before_script` and `after_script`?
**Answer:** Encapsulate the operation behind validated inputs, explicit exit behavior, safe argument handling, logging, and a testable return value.
Script: [Question 16 script](interview-scripts/016-what-is-the-difference-between-before-script-and-after.yml)
17. What is an artifact?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 17 script](interview-scripts/017-what-is-an-artifact.yml)
18. What is a cache?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 18 script](interview-scripts/018-what-is-a-cache.yml)
19. How do artifacts differ from cache?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 19 script](interview-scripts/019-how-do-artifacts-differ-from-cache.yml)
20. What are predefined CI/CD variables?
**Answer:** Keep environment-specific values outside reusable logic, validate them at the boundary, and provide safe defaults only where appropriate.
Script: [Question 20 script](interview-scripts/020-what-are-predefined-ci-cd-variables.yml)
21. What is `CI_COMMIT_SHA`?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 21 script](interview-scripts/021-what-is-ci-commit-sha.yml)
22. What is `CI_COMMIT_REF_NAME`?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 22 script](interview-scripts/022-what-is-ci-commit-ref-name.yml)
23. How do you define a custom variable?
**Answer:** Keep environment-specific values outside reusable logic, validate them at the boundary, and provide safe defaults only where appropriate.
Script: [Question 23 script](interview-scripts/023-how-do-you-define-a-custom-variable.yml)
24. What is a manual job?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
Script: [Question 24 script](interview-scripts/024-what-is-a-manual-job.yml)
25. What does `when: manual` do?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 25 script](interview-scripts/025-what-does-when-manual-do.yml)
26. What is a pipeline environment?
**Answer:** Keep environment-specific values outside reusable logic, validate them at the boundary, and provide safe defaults only where appropriate.
Script: [Question 26 script](interview-scripts/026-what-is-a-pipeline-environment.yml)
27. How do you name a staging environment?
**Answer:** Keep environment-specific values outside reusable logic, validate them at the boundary, and provide safe defaults only where appropriate.
Script: [Question 27 script](interview-scripts/027-how-do-you-name-a-staging-environment.yml)
28. What is a pipeline rule?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
Script: [Question 28 script](interview-scripts/028-what-is-a-pipeline-rule.yml)
29. What does `workflow: rules` control?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 29 script](interview-scripts/029-what-does-workflow-rules-control.yml)
30. How do you run a job only on the default branch?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
Script: [Question 30 script](interview-scripts/030-how-do-you-run-a-job-only-on-the-default-branch.yml)
31. What is a Docker-in-Docker service?
**Answer:** Define the smallest required traffic path, restrict it with policy and identity, and verify connectivity from the same network boundary as the workload.
Script: [Question 31 script](interview-scripts/031-what-is-a-docker-in-docker-service.yml)
32. How do you build a Docker image in GitLab CI?
**Answer:** Build a minimal immutable image, pin dependencies, scan and sign it, publish it to a controlled registry, and deploy by digest when possible.
Script: [Question 32 script](interview-scripts/032-how-do-you-build-a-docker-image-in-gitlab-ci.yml)
33. What is the GitLab Container Registry?
**Answer:** Build a minimal immutable image, pin dependencies, scan and sign it, publish it to a controlled registry, and deploy by digest when possible.
Script: [Question 33 script](interview-scripts/033-what-is-the-gitlab-container-registry.yml)
34. How do you authenticate to the registry?
**Answer:** Build a minimal immutable image, pin dependencies, scan and sign it, publish it to a controlled registry, and deploy by digest when possible.
Script: [Question 34 script](interview-scripts/034-how-do-you-authenticate-to-the-registry.yml)
35. Where should passwords be stored?
**Answer:** Keep the value in a protected secret store or workload identity, pass it at runtime, redact it from logs, and never commit it to source control.
Script: [Question 35 script](interview-scripts/035-where-should-passwords-be-stored.yml)
36. What is a masked variable?
**Answer:** Keep environment-specific values outside reusable logic, validate them at the boundary, and provide safe defaults only where appropriate.
Script: [Question 36 script](interview-scripts/036-what-is-a-masked-variable.yml)
37. What is a protected variable?
**Answer:** Keep environment-specific values outside reusable logic, validate them at the boundary, and provide safe defaults only where appropriate.
Script: [Question 37 script](interview-scripts/037-what-is-a-protected-variable.yml)
38. How do you inspect a failed job log?
**Answer:** Emit structured, correlation-aware telemetry with enough context to diagnose duration, failures, deployment version, and affected environment.
Script: [Question 38 script](interview-scripts/038-how-do-you-inspect-a-failed-job-log.yml)
39. What is a retry and when is it appropriate?
**Answer:** Retry only transient failures, use bounded exponential backoff with jitter, and return the final error when the retry budget is exhausted.
Script: [Question 39 script](interview-scripts/039-what-is-a-retry-and-when-is-it-appropriate.yml)
40. How do you cancel a running pipeline?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
Script: [Question 40 script](interview-scripts/040-how-do-you-cancel-a-running-pipeline.yml)

## Intermediate: 41-80

41. How do jobs move through stages?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
Script: [Question 41 script](interview-scripts/041-how-do-jobs-move-through-stages.yml)
42. What does `needs` change about pipeline execution?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
Script: [Question 42 script](interview-scripts/042-what-does-needs-change-about-pipeline-execution.yml)
43. How do you construct a directed acyclic pipeline graph?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
Script: [Question 43 script](interview-scripts/043-how-do-you-construct-a-directed-acyclic-pipeline-graph.yml)
44. What is `parallel:matrix`?
**Answer:** Bound concurrency, preserve a small failure domain, verify health between batches, and stop promotion when the error budget is exceeded.
Script: [Question 44 script](interview-scripts/044-what-is-parallel-matrix.yml)
45. How do you test multiple language versions?
**Answer:** Automate syntax, static analysis, unit, and integration checks in CI; fail early and publish useful diagnostics as artifacts.
Script: [Question 45 script](interview-scripts/045-how-do-you-test-multiple-language-versions.yml)
46. How do you pass artifacts between jobs?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
Script: [Question 46 script](interview-scripts/046-how-do-you-pass-artifacts-between-jobs.yml)
47. How do you set artifact expiration?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 47 script](interview-scripts/047-how-do-you-set-artifact-expiration.yml)
48. How do you cache language dependencies?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 48 script](interview-scripts/048-how-do-you-cache-language-dependencies.yml)
49. How do cache keys affect correctness?
**Answer:** Keep the value in a protected secret store or workload identity, pass it at runtime, redact it from logs, and never commit it to source control.
Script: [Question 49 script](interview-scripts/049-how-do-cache-keys-affect-correctness.yml)
50. How do `rules` differ from legacy `only` and `except`?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 50 script](interview-scripts/050-how-do-rules-differ-from-legacy-only-and-except.yml)
51. How do you prevent duplicate branch and merge-request pipelines?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
Script: [Question 51 script](interview-scripts/051-how-do-you-prevent-duplicate-branch-and-merge-request-p.yml)
52. How do you create a review app?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 52 script](interview-scripts/052-how-do-you-create-a-review-app.yml)
53. How do you stop a review app?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 53 script](interview-scripts/053-how-do-you-stop-a-review-app.yml)
54. What is a protected environment?
**Answer:** Keep environment-specific values outside reusable logic, validate them at the boundary, and provide safe defaults only where appropriate.
Script: [Question 54 script](interview-scripts/054-what-is-a-protected-environment.yml)
55. How do deployment approvals work?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
Script: [Question 55 script](interview-scripts/055-how-do-deployment-approvals-work.yml)
56. What is a resource group?
**Answer:** Declare requests and limits, measure real usage, set explicit capacity bounds, and test behavior under saturation and recovery.
Script: [Question 56 script](interview-scripts/056-what-is-a-resource-group.yml)
57. How do you prevent concurrent production deployments?
**Answer:** Bound concurrency, preserve a small failure domain, verify health between batches, and stop promotion when the error budget is exceeded.
Script: [Question 57 script](interview-scripts/057-how-do-you-prevent-concurrent-production-deployments.yml)
58. How do you publish JUnit test reports?
**Answer:** Automate syntax, static analysis, unit, and integration checks in CI; fail early and publish useful diagnostics as artifacts.
Script: [Question 58 script](interview-scripts/058-how-do-you-publish-junit-test-reports.yml)
59. What is a dotenv report?
**Answer:** Define the smallest required traffic path, restrict it with policy and identity, and verify connectivity from the same network boundary as the workload.
Script: [Question 59 script](interview-scripts/059-what-is-a-dotenv-report.yml)
60. How do you publish code-quality results?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 60 script](interview-scripts/060-how-do-you-publish-code-quality-results.yml)
61. How do SAST templates work?
**Answer:** Extract the behavior behind a small documented interface, keep inputs and outputs explicit, and test the reusable unit independently.
Script: [Question 61 script](interview-scripts/061-how-do-sast-templates-work.yml)
62. How does dependency scanning work?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 62 script](interview-scripts/062-how-does-dependency-scanning-work.yml)
63. How does secret detection work?
**Answer:** Keep the value in a protected secret store or workload identity, pass it at runtime, redact it from logs, and never commit it to source control.
Script: [Question 63 script](interview-scripts/063-how-does-secret-detection-work.yml)
64. How do you scan container images?
**Answer:** Build a minimal immutable image, pin dependencies, scan and sign it, publish it to a controlled registry, and deploy by digest when possible.
Script: [Question 64 script](interview-scripts/064-how-do-you-scan-container-images.yml)
65. How do you lint Helm charts in CI?
**Answer:** Automate syntax, static analysis, unit, and integration checks in CI; fail early and publish useful diagnostics as artifacts.
Script: [Question 65 script](interview-scripts/065-how-do-you-lint-helm-charts-in-ci.yml)
66. How do you run Terraform validate and plan?
**Answer:** Automate syntax, static analysis, unit, and integration checks in CI; fail early and publish useful diagnostics as artifacts.
Script: [Question 66 script](interview-scripts/066-how-do-you-run-terraform-validate-and-plan.yml)
67. How do you prevent Terraform plan secrets leaking in artifacts?
**Answer:** Keep the value in a protected secret store or workload identity, pass it at runtime, redact it from logs, and never commit it to source control.
Script: [Question 67 script](interview-scripts/067-how-do-you-prevent-terraform-plan-secrets-leaking-in-ar.yml)
68. What is an environment URL?
**Answer:** Keep environment-specific values outside reusable logic, validate them at the boundary, and provide safe defaults only where appropriate.
Script: [Question 68 script](interview-scripts/068-what-is-an-environment-url.yml)
69. How do you define a deployment rollback job?
**Answer:** Keep the previous known-good version, validate the replacement, and automate a tested rollback or restore path with clear ownership and audit output.
Script: [Question 69 script](interview-scripts/069-how-do-you-define-a-deployment-rollback-job.yml)
70. How do you use `allow_failure` responsibly?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 70 script](interview-scripts/070-how-do-you-use-allow-failure-responsibly.yml)
71. What is a scheduled pipeline?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
Script: [Question 71 script](interview-scripts/071-what-is-a-scheduled-pipeline.yml)
72. How do you identify the pipeline source?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
Script: [Question 72 script](interview-scripts/072-how-do-you-identify-the-pipeline-source.yml)
73. What are GitLab CI includes?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 73 script](interview-scripts/073-what-are-gitlab-ci-includes.yml)
74. How do you reuse YAML with anchors and extends?
**Answer:** Extract the behavior behind a small documented interface, keep inputs and outputs explicit, and test the reusable unit independently.
Script: [Question 74 script](interview-scripts/074-how-do-you-reuse-yaml-with-anchors-and-extends.yml)
75. What is a CI/CD component?
**Answer:** Extract the behavior behind a small documented interface, keep inputs and outputs explicit, and test the reusable unit independently.
Script: [Question 75 script](interview-scripts/075-what-is-a-ci-cd-component.yml)
76. How do you share templates across projects?
**Answer:** Extract the behavior behind a small documented interface, keep inputs and outputs explicit, and test the reusable unit independently.
Script: [Question 76 script](interview-scripts/076-how-do-you-share-templates-across-projects.yml)
77. How do you use runner tags?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
Script: [Question 77 script](interview-scripts/077-how-do-you-use-runner-tags.yml)
78. What are protected runners?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
Script: [Question 78 script](interview-scripts/078-what-are-protected-runners.yml)
79. How do you troubleshoot a job stuck pending?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
Script: [Question 79 script](interview-scripts/079-how-do-you-troubleshoot-a-job-stuck-pending.yml)
80. How do you design a pipeline for a monorepo?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
Script: [Question 80 script](interview-scripts/080-how-do-you-design-a-pipeline-for-a-monorepo.yml)

## Advanced: 81-120

81. Design a secure enterprise GitLab runner architecture.
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
Script: [Question 81 script](interview-scripts/081-design-a-secure-enterprise-gitlab-runner-architecture.yml)
82. How do shared and group runners differ?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
Script: [Question 82 script](interview-scripts/082-how-do-shared-and-group-runners-differ.yml)
83. How do you isolate untrusted merge-request code?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 83 script](interview-scripts/083-how-do-you-isolate-untrusted-merge-request-code.yml)
84. How do you secure privileged Docker runners?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
Script: [Question 84 script](interview-scripts/084-how-do-you-secure-privileged-docker-runners.yml)
85. What are the risks of Docker-in-Docker?
**Answer:** Build a minimal immutable image, pin dependencies, scan and sign it, publish it to a controlled registry, and deploy by digest when possible.
Script: [Question 85 script](interview-scripts/085-what-are-the-risks-of-docker-in-docker.yml)
86. How do rootless or Kaniko-style builds change the threat model?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 86 script](interview-scripts/086-how-do-rootless-or-kaniko-style-builds-change-the-threa.yml)
87. How do you implement Azure OIDC federation from GitLab?
**Answer:** Use provider-native identity with least privilege, explicit environment boundaries, tagging, policy controls, and repeatable infrastructure definitions.
Script: [Question 87 script](interview-scripts/087-how-do-you-implement-azure-oidc-federation-from-gitlab.yml)
88. How do you implement AWS OIDC federation from GitLab?
**Answer:** Use provider-native identity with least privilege, explicit environment boundaries, tagging, policy controls, and repeatable infrastructure definitions.
Script: [Question 88 script](interview-scripts/088-how-do-you-implement-aws-oidc-federation-from-gitlab.yml)
89. Why are short-lived cloud credentials preferable?
**Answer:** Keep the value in a protected secret store or workload identity, pass it at runtime, redact it from logs, and never commit it to source control.
Script: [Question 89 script](interview-scripts/089-why-are-short-lived-cloud-credentials-preferable.yml)
90. How do you restrict a federated role to one project and branch?
**Answer:** Use a structured client, explicit timeouts, status handling, pagination, schema validation, and safe authentication rather than string parsing.
Script: [Question 90 script](interview-scripts/090-how-do-you-restrict-a-federated-role-to-one-project-and.yml)
91. How do you manage protected secrets across environments?
**Answer:** Keep the value in a protected secret store or workload identity, pass it at runtime, redact it from logs, and never commit it to source control.
Script: [Question 91 script](interview-scripts/091-how-do-you-manage-protected-secrets-across-environments.yml)
92. How do you rotate a credential without pipeline downtime?
**Answer:** Keep the value in a protected secret store or workload identity, pass it at runtime, redact it from logs, and never commit it to source control.
Script: [Question 92 script](interview-scripts/092-how-do-you-rotate-a-credential-without-pipeline-downtim.yml)
93. How do you design a multi-account AWS deployment pipeline?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
Script: [Question 93 script](interview-scripts/093-how-do-you-design-a-multi-account-aws-deployment-pipeli.yml)
94. How do you design a multi-subscription Azure deployment pipeline?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
Script: [Question 94 script](interview-scripts/094-how-do-you-design-a-multi-subscription-azure-deployment.yml)
95. How do you promote immutable artifacts between environments?
**Answer:** Keep environment-specific values outside reusable logic, validate them at the boundary, and provide safe defaults only where appropriate.
Script: [Question 95 script](interview-scripts/095-how-do-you-promote-immutable-artifacts-between-environm.yml)
96. How do you prevent rebuilding an artifact during promotion?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 96 script](interview-scripts/096-how-do-you-prevent-rebuilding-an-artifact-during-promot.yml)
97. How do you implement canary deployment in GitLab?
**Answer:** Bound concurrency, preserve a small failure domain, verify health between batches, and stop promotion when the error budget is exceeded.
Script: [Question 97 script](interview-scripts/097-how-do-you-implement-canary-deployment-in-gitlab.yml)
98. How do you gate production on health metrics?
**Answer:** Check a meaningful dependency or application endpoint, fail the operation when the check fails, and use the result to stop or roll back promotion.
Script: [Question 98 script](interview-scripts/098-how-do-you-gate-production-on-health-metrics.yml)
99. How do you automate rollback after a failed smoke test?
**Answer:** Check a meaningful dependency or application endpoint, fail the operation when the check fails, and use the result to stop or roll back promotion.
Script: [Question 99 script](interview-scripts/099-how-do-you-automate-rollback-after-a-failed-smoke-test.yml)
100. How do child pipelines improve pipeline scalability?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
Script: [Question 100 script](interview-scripts/100-how-do-child-pipelines-improve-pipeline-scalability.yml)
101. How do dynamic child pipelines work?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
Script: [Question 101 script](interview-scripts/101-how-do-dynamic-child-pipelines-work.yml)
102. How do multi-project pipelines coordinate dependencies?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
Script: [Question 102 script](interview-scripts/102-how-do-multi-project-pipelines-coordinate-dependencies.yml)
103. How do you version shared pipeline templates?
**Answer:** Extract the behavior behind a small documented interface, keep inputs and outputs explicit, and test the reusable unit independently.
Script: [Question 103 script](interview-scripts/103-how-do-you-version-shared-pipeline-templates.yml)
104. How do you prevent breaking changes in a shared template?
**Answer:** Extract the behavior behind a small documented interface, keep inputs and outputs explicit, and test the reusable unit independently.
Script: [Question 104 script](interview-scripts/104-how-do-you-prevent-breaking-changes-in-a-shared-templat.yml)
105. How do you implement deployment concurrency control?
**Answer:** Bound concurrency, preserve a small failure domain, verify health between batches, and stop promotion when the error budget is exceeded.
Script: [Question 105 script](interview-scripts/105-how-do-you-implement-deployment-concurrency-control.yml)
106. How do you model change freezes?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 106 script](interview-scripts/106-how-do-you-model-change-freezes.yml)
107. How do you create a release from a tag?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
Script: [Question 107 script](interview-scripts/107-how-do-you-create-a-release-from-a-tag.yml)
108. How do you sign release artifacts?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
Script: [Question 108 script](interview-scripts/108-how-do-you-sign-release-artifacts.yml)
109. How do you verify image provenance in CI?
**Answer:** Build a minimal immutable image, pin dependencies, scan and sign it, publish it to a controlled registry, and deploy by digest when possible.
Script: [Question 109 script](interview-scripts/109-how-do-you-verify-image-provenance-in-ci.yml)
110. How do you integrate SBOM generation and vulnerability gates?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 110 script](interview-scripts/110-how-do-you-integrate-sbom-generation-and-vulnerability.yml)
111. How do you design disaster recovery for GitLab itself?
**Answer:** Keep the previous known-good version, validate the replacement, and automate a tested rollback or restore path with clear ownership and audit output.
Script: [Question 111 script](interview-scripts/111-how-do-you-design-disaster-recovery-for-gitlab-itself.yml)
112. How do you back up repositories, registry data, and CI configuration?
**Answer:** Keep environment-specific values outside reusable logic, validate them at the boundary, and provide safe defaults only where appropriate.
Script: [Question 112 script](interview-scripts/112-how-do-you-back-up-repositories-registry-data-and-ci-co.yml)
113. How do you test GitLab backup restoration?
**Answer:** Automate syntax, static analysis, unit, and integration checks in CI; fail early and publish useful diagnostics as artifacts.
Script: [Question 113 script](interview-scripts/113-how-do-you-test-gitlab-backup-restoration.yml)
114. How do you observe pipeline health at organization scale?
**Answer:** Check a meaningful dependency or application endpoint, fail the operation when the check fails, and use the result to stop or roll back promotion.
Script: [Question 114 script](interview-scripts/114-how-do-you-observe-pipeline-health-at-organization-scal.yml)
115. Which DORA metrics can GitLab provide?
**Answer:** Emit structured, correlation-aware telemetry with enough context to diagnose duration, failures, deployment version, and affected environment.
Script: [Question 115 script](interview-scripts/115-which-dora-metrics-can-gitlab-provide.yml)
116. How do you reduce pipeline lead time without reducing safety?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
Script: [Question 116 script](interview-scripts/116-how-do-you-reduce-pipeline-lead-time-without-reducing-s.yml)
117. How do you handle flaky tests without hiding defects?
**Answer:** Automate syntax, static analysis, unit, and integration checks in CI; fail early and publish useful diagnostics as artifacts.
Script: [Question 117 script](interview-scripts/117-how-do-you-handle-flaky-tests-without-hiding-defects.yml)
118. How do you design a regulated production approval workflow?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
Script: [Question 118 script](interview-scripts/118-how-do-you-design-a-regulated-production-approval-workf.yml)
119. How do you connect GitLab deployment events to incident management?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
Script: [Question 119 script](interview-scripts/119-how-do-you-connect-gitlab-deployment-events-to-incident.yml)
120. Design a secure, reusable, observable GitLab platform for Azure, AWS, and on-premises delivery.
**Answer:** Emit structured, correlation-aware telemetry with enough context to diagnose duration, failures, deployment version, and affected environment.
Script: [Question 120 script](interview-scripts/120-design-a-secure-reusable-observable-gitlab-platform-for.yml)

## HackerRank-Style CI/CD Challenges: 121-150

121. Write a pipeline with lint, test, build, and deploy stages.
**Answer:** Test the happy path, invalid input, timeout, retry exhaustion, and partial failure with mocks for external systems and an assertion on the final result.
Script: [Question 121 script](interview-scripts/121-write-a-pipeline-with-lint-test-build-and-deploy-stages.yml)
122. Store a generated report as an artifact.
**Answer:** Separate validation, build, promotion, and verification jobs; use immutable artifacts, protected variables or OIDC, and manual approval for production.
Script: [Question 122 script](interview-scripts/122-store-a-generated-report-as-an-artifact.yml)
123. Cache Python dependencies with a branch-safe key.
**Answer:** Implement the solution with validated inputs, deterministic behavior, clear failure handling, tests, and an example execution command for GitLab CI/CD.
Script: [Question 123 script](interview-scripts/123-cache-python-dependencies-with-a-branch-safe-key.yml)
124. Run deployment only on the default branch.
**Answer:** Deploy an immutable version, run a health or smoke check, promote only on success, and invoke a tested rollback while preserving the failure in logs.
Script: [Question 124 script](interview-scripts/124-run-deployment-only-on-the-default-branch.yml)
125. Add a manual production job with a protected environment.
**Answer:** Parse with the platform's structured data tool, validate required fields and types at the boundary, and return a clear nonzero failure for malformed input.
Script: [Question 125 script](interview-scripts/125-add-a-manual-production-job-with-a-protected-environmen.yml)
126. Build and push an immutable commit-SHA Docker tag.
**Answer:** Use declarative manifests with pinned images, probes, resource controls, least-privilege identity, and a rollout strategy that can be observed and rolled back.
Script: [Question 126 script](interview-scripts/126-build-and-push-an-immutable-commit-sha-docker-tag.yml)
127. Test two Python versions and two database engines with a matrix.
**Answer:** Test the happy path, invalid input, timeout, retry exhaustion, and partial failure with mocks for external systems and an assertion on the final result.
Script: [Question 127 script](interview-scripts/127-test-two-python-versions-and-two-database-engines-with.yml)
128. Build a DAG so independent tests run in parallel.
**Answer:** Use a bounded worker pool, collect each success and exception separately, and fail the operation when the defined error threshold is exceeded.
Script: [Question 128 script](interview-scripts/128-build-a-dag-so-independent-tests-run-in-parallel.yml)
129. Create a review app and manual stop job.
**Answer:** Separate validation, build, promotion, and verification jobs; use immutable artifacts, protected variables or OIDC, and manual approval for production.
Script: [Question 129 script](interview-scripts/129-create-a-review-app-and-manual-stop-job.yml)
130. Always upload JUnit test results.
**Answer:** Test the happy path, invalid input, timeout, retry exhaustion, and partial failure with mocks for external systems and an assertion on the final result.
Script: [Question 130 script](interview-scripts/130-always-upload-junit-test-results.yml)
131. Include SAST and dependency scanning templates.
**Answer:** Implement the solution with validated inputs, deterministic behavior, clear failure handling, tests, and an example execution command for GitLab CI/CD.
Script: [Question 131 script](interview-scripts/131-include-sast-and-dependency-scanning-templates.yml)
132. Include secret detection and fail on a finding.
**Answer:** Implement the solution with validated inputs, deterministic behavior, clear failure handling, tests, and an example execution command for GitLab CI/CD.
Script: [Question 132 script](interview-scripts/132-include-secret-detection-and-fail-on-a-finding.yml)
133. Add a Helm lint job.
**Answer:** Separate validation, build, promotion, and verification jobs; use immutable artifacts, protected variables or OIDC, and manual approval for production.
Script: [Question 133 script](interview-scripts/133-add-a-helm-lint-job.yml)
134. Add a Terraform validate and plan job.
**Answer:** Express the desired state with typed inputs, stable addresses, policy validation, protected state, and a reviewed plan before apply.
Script: [Question 134 script](interview-scripts/134-add-a-terraform-validate-and-plan-job.yml)
135. Obtain Azure credentials through OIDC.
**Answer:** Separate validation, build, promotion, and verification jobs; use immutable artifacts, protected variables or OIDC, and manual approval for production.
Script: [Question 135 script](interview-scripts/135-obtain-azure-credentials-through-oidc.yml)
136. Obtain AWS identity through OIDC.
**Answer:** Separate validation, build, promotion, and verification jobs; use immutable artifacts, protected variables or OIDC, and manual approval for production.
Script: [Question 136 script](interview-scripts/136-obtain-aws-identity-through-oidc.yml)
137. Generate a child pipeline from an artifact.
**Answer:** Separate validation, build, promotion, and verification jobs; use immutable artifacts, protected variables or OIDC, and manual approval for production.
Script: [Question 137 script](interview-scripts/137-generate-a-child-pipeline-from-an-artifact.yml)
138. Wait for an infrastructure project with a multi-project pipeline.
**Answer:** Separate validation, build, promotion, and verification jobs; use immutable artifacts, protected variables or OIDC, and manual approval for production.
Script: [Question 138 script](interview-scripts/138-wait-for-an-infrastructure-project-with-a-multi-project.yml)
139. Serialize production deployments with `resource_group`.
**Answer:** Parse the input into structured records, use a map or counter for aggregation, sort only when ranking is required, and test empty, duplicate, and boundary inputs.
Script: [Question 139 script](interview-scripts/139-serialize-production-deployments-with-resource-group.yml)
140. Create a canary, smoke-test, and manual promotion flow.
**Answer:** Test the happy path, invalid input, timeout, retry exhaustion, and partial failure with mocks for external systems and an assertion on the final result.
Script: [Question 140 script](interview-scripts/140-create-a-canary-smoke-test-and-manual-promotion-flow.yml)
141. Create a tag-based release job.
**Answer:** Deploy an immutable version, run a health or smoke check, promote only on success, and invoke a tested rollback while preserving the failure in logs.
Script: [Question 141 script](interview-scripts/141-create-a-tag-based-release-job.yml)
142. Run a job only from a scheduled pipeline.
**Answer:** Separate validation, build, promotion, and verification jobs; use immutable artifacts, protected variables or OIDC, and manual approval for production.
Script: [Question 142 script](interview-scripts/142-run-a-job-only-from-a-scheduled-pipeline.yml)
143. Block production changes during a deployment freeze.
**Answer:** Deploy an immutable version, run a health or smoke check, promote only on success, and invoke a tested rollback while preserving the failure in logs.
Script: [Question 143 script](interview-scripts/143-block-production-changes-during-a-deployment-freeze.yml)
144. Add a manual rollback job for a previous artifact.
**Answer:** Deploy an immutable version, run a health or smoke check, promote only on success, and invoke a tested rollback while preserving the failure in logs.
Script: [Question 144 script](interview-scripts/144-add-a-manual-rollback-job-for-a-previous-artifact.yml)
145. Send a failure notification from `after_script`.
**Answer:** Implement the solution with validated inputs, deterministic behavior, clear failure handling, tests, and an example execution command for GitLab CI/CD.
Script: [Question 145 script](interview-scripts/145-send-a-failure-notification-from-after-script.yml)
146. Publish pipeline duration metrics.
**Answer:** Separate validation, build, promotion, and verification jobs; use immutable artifacts, protected variables or OIDC, and manual approval for production.
Script: [Question 146 script](interview-scripts/146-publish-pipeline-duration-metrics.yml)
147. Retain a backup artifact for 30 days.
**Answer:** Separate validation, build, promotion, and verification jobs; use immutable artifacts, protected variables or OIDC, and manual approval for production.
Script: [Question 147 script](interview-scripts/147-retain-a-backup-artifact-for-30-days.yml)
148. Protect cloud credentials without plaintext secrets.
**Answer:** Implement the solution with validated inputs, deterministic behavior, clear failure handling, tests, and an example execution command for GitLab CI/CD.
Script: [Question 148 script](interview-scripts/148-protect-cloud-credentials-without-plaintext-secrets.yml)
149. Build a reusable YAML component for security gates.
**Answer:** Separate validation, build, promotion, and verification jobs; use immutable artifacts, protected variables or OIDC, and manual approval for production.
Script: [Question 149 script](interview-scripts/149-build-a-reusable-yaml-component-for-security-gates.yml)
150. Build a secure pipeline with OIDC, immutable artifacts, canary, rollback, and metrics.
**Answer:** Deploy an immutable version, run a health or smoke check, promote only on success, and invoke a tested rollback while preserving the failure in logs.
Script: [Question 150 script](interview-scripts/150-build-a-secure-pipeline-with-oidc-immutable-artifacts-c.yml)

## Executable Answers

- [Beginner answers](interview-answers/beginner.yml): stages, dependencies, and artifacts.
- [Intermediate answers](interview-answers/intermediate.yml): matrix testing and review apps.
- [Advanced answers](interview-answers/advanced.yml): canary promotion, smoke tests, and deployment locking.
