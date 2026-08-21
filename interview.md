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
2. What is a GitLab project?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
3. What is a repository?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
4. What is a commit?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
5. What is a branch?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
6. What is a merge request?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
7. What is a protected branch?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
8. What is a `.gitlab-ci.yml` file?
**Answer:** Use structured filesystem APIs, validate paths, quote inputs, handle missing resources deliberately, and avoid unsafe traversal or shell expansion.
9. What is a pipeline?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
10. What is a stage?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
11. What is a job?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
12. What is a runner?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
13. What is an executor?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
14. What is the purpose of an image in a job?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
15. What does the `script` keyword define?
**Answer:** Keep the value in a protected secret store or workload identity, pass it at runtime, redact it from logs, and never commit it to source control.
16. What is the difference between `before_script` and `after_script`?
**Answer:** Encapsulate the operation behind validated inputs, explicit exit behavior, safe argument handling, logging, and a testable return value.
17. What is an artifact?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
18. What is a cache?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
19. How do artifacts differ from cache?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
20. What are predefined CI/CD variables?
**Answer:** Keep environment-specific values outside reusable logic, validate them at the boundary, and provide safe defaults only where appropriate.
21. What is `CI_COMMIT_SHA`?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
22. What is `CI_COMMIT_REF_NAME`?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
23. How do you define a custom variable?
**Answer:** Keep environment-specific values outside reusable logic, validate them at the boundary, and provide safe defaults only where appropriate.
24. What is a manual job?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
25. What does `when: manual` do?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
26. What is a pipeline environment?
**Answer:** Keep environment-specific values outside reusable logic, validate them at the boundary, and provide safe defaults only where appropriate.
27. How do you name a staging environment?
**Answer:** Keep environment-specific values outside reusable logic, validate them at the boundary, and provide safe defaults only where appropriate.
28. What is a pipeline rule?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
29. What does `workflow: rules` control?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
30. How do you run a job only on the default branch?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
31. What is a Docker-in-Docker service?
**Answer:** Define the smallest required traffic path, restrict it with policy and identity, and verify connectivity from the same network boundary as the workload.
32. How do you build a Docker image in GitLab CI?
**Answer:** Build a minimal immutable image, pin dependencies, scan and sign it, publish it to a controlled registry, and deploy by digest when possible.
33. What is the GitLab Container Registry?
**Answer:** Build a minimal immutable image, pin dependencies, scan and sign it, publish it to a controlled registry, and deploy by digest when possible.
34. How do you authenticate to the registry?
**Answer:** Build a minimal immutable image, pin dependencies, scan and sign it, publish it to a controlled registry, and deploy by digest when possible.
35. Where should passwords be stored?
**Answer:** Keep the value in a protected secret store or workload identity, pass it at runtime, redact it from logs, and never commit it to source control.
36. What is a masked variable?
**Answer:** Keep environment-specific values outside reusable logic, validate them at the boundary, and provide safe defaults only where appropriate.
37. What is a protected variable?
**Answer:** Keep environment-specific values outside reusable logic, validate them at the boundary, and provide safe defaults only where appropriate.
38. How do you inspect a failed job log?
**Answer:** Emit structured, correlation-aware telemetry with enough context to diagnose duration, failures, deployment version, and affected environment.
39. What is a retry and when is it appropriate?
**Answer:** Retry only transient failures, use bounded exponential backoff with jitter, and return the final error when the retry budget is exhausted.
40. How do you cancel a running pipeline?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.

## Intermediate: 41-80

41. How do jobs move through stages?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
42. What does `needs` change about pipeline execution?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
43. How do you construct a directed acyclic pipeline graph?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
44. What is `parallel:matrix`?
**Answer:** Bound concurrency, preserve a small failure domain, verify health between batches, and stop promotion when the error budget is exceeded.
45. How do you test multiple language versions?
**Answer:** Automate syntax, static analysis, unit, and integration checks in CI; fail early and publish useful diagnostics as artifacts.
46. How do you pass artifacts between jobs?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
47. How do you set artifact expiration?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
48. How do you cache language dependencies?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
49. How do cache keys affect correctness?
**Answer:** Keep the value in a protected secret store or workload identity, pass it at runtime, redact it from logs, and never commit it to source control.
50. How do `rules` differ from legacy `only` and `except`?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
51. How do you prevent duplicate branch and merge-request pipelines?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
52. How do you create a review app?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
53. How do you stop a review app?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
54. What is a protected environment?
**Answer:** Keep environment-specific values outside reusable logic, validate them at the boundary, and provide safe defaults only where appropriate.
55. How do deployment approvals work?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
56. What is a resource group?
**Answer:** Declare requests and limits, measure real usage, set explicit capacity bounds, and test behavior under saturation and recovery.
57. How do you prevent concurrent production deployments?
**Answer:** Bound concurrency, preserve a small failure domain, verify health between batches, and stop promotion when the error budget is exceeded.
58. How do you publish JUnit test reports?
**Answer:** Automate syntax, static analysis, unit, and integration checks in CI; fail early and publish useful diagnostics as artifacts.
59. What is a dotenv report?
**Answer:** Define the smallest required traffic path, restrict it with policy and identity, and verify connectivity from the same network boundary as the workload.
60. How do you publish code-quality results?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
61. How do SAST templates work?
**Answer:** Extract the behavior behind a small documented interface, keep inputs and outputs explicit, and test the reusable unit independently.
62. How does dependency scanning work?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
63. How does secret detection work?
**Answer:** Keep the value in a protected secret store or workload identity, pass it at runtime, redact it from logs, and never commit it to source control.
64. How do you scan container images?
**Answer:** Build a minimal immutable image, pin dependencies, scan and sign it, publish it to a controlled registry, and deploy by digest when possible.
65. How do you lint Helm charts in CI?
**Answer:** Automate syntax, static analysis, unit, and integration checks in CI; fail early and publish useful diagnostics as artifacts.
66. How do you run Terraform validate and plan?
**Answer:** Automate syntax, static analysis, unit, and integration checks in CI; fail early and publish useful diagnostics as artifacts.
67. How do you prevent Terraform plan secrets leaking in artifacts?
**Answer:** Keep the value in a protected secret store or workload identity, pass it at runtime, redact it from logs, and never commit it to source control.
68. What is an environment URL?
**Answer:** Keep environment-specific values outside reusable logic, validate them at the boundary, and provide safe defaults only where appropriate.
69. How do you define a deployment rollback job?
**Answer:** Keep the previous known-good version, validate the replacement, and automate a tested rollback or restore path with clear ownership and audit output.
70. How do you use `allow_failure` responsibly?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
71. What is a scheduled pipeline?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
72. How do you identify the pipeline source?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
73. What are GitLab CI includes?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
74. How do you reuse YAML with anchors and extends?
**Answer:** Extract the behavior behind a small documented interface, keep inputs and outputs explicit, and test the reusable unit independently.
75. What is a CI/CD component?
**Answer:** Extract the behavior behind a small documented interface, keep inputs and outputs explicit, and test the reusable unit independently.
76. How do you share templates across projects?
**Answer:** Extract the behavior behind a small documented interface, keep inputs and outputs explicit, and test the reusable unit independently.
77. How do you use runner tags?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
78. What are protected runners?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
79. How do you troubleshoot a job stuck pending?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
80. How do you design a pipeline for a monorepo?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.

## Advanced: 81-120

81. Design a secure enterprise GitLab runner architecture.
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
82. How do shared and group runners differ?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
83. How do you isolate untrusted merge-request code?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
84. How do you secure privileged Docker runners?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
85. What are the risks of Docker-in-Docker?
**Answer:** Build a minimal immutable image, pin dependencies, scan and sign it, publish it to a controlled registry, and deploy by digest when possible.
86. How do rootless or Kaniko-style builds change the threat model?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
87. How do you implement Azure OIDC federation from GitLab?
**Answer:** Use provider-native identity with least privilege, explicit environment boundaries, tagging, policy controls, and repeatable infrastructure definitions.
88. How do you implement AWS OIDC federation from GitLab?
**Answer:** Use provider-native identity with least privilege, explicit environment boundaries, tagging, policy controls, and repeatable infrastructure definitions.
89. Why are short-lived cloud credentials preferable?
**Answer:** Keep the value in a protected secret store or workload identity, pass it at runtime, redact it from logs, and never commit it to source control.
90. How do you restrict a federated role to one project and branch?
**Answer:** Use a structured client, explicit timeouts, status handling, pagination, schema validation, and safe authentication rather than string parsing.
91. How do you manage protected secrets across environments?
**Answer:** Keep the value in a protected secret store or workload identity, pass it at runtime, redact it from logs, and never commit it to source control.
92. How do you rotate a credential without pipeline downtime?
**Answer:** Keep the value in a protected secret store or workload identity, pass it at runtime, redact it from logs, and never commit it to source control.
93. How do you design a multi-account AWS deployment pipeline?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
94. How do you design a multi-subscription Azure deployment pipeline?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
95. How do you promote immutable artifacts between environments?
**Answer:** Keep environment-specific values outside reusable logic, validate them at the boundary, and provide safe defaults only where appropriate.
96. How do you prevent rebuilding an artifact during promotion?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
97. How do you implement canary deployment in GitLab?
**Answer:** Bound concurrency, preserve a small failure domain, verify health between batches, and stop promotion when the error budget is exceeded.
98. How do you gate production on health metrics?
**Answer:** Check a meaningful dependency or application endpoint, fail the operation when the check fails, and use the result to stop or roll back promotion.
99. How do you automate rollback after a failed smoke test?
**Answer:** Check a meaningful dependency or application endpoint, fail the operation when the check fails, and use the result to stop or roll back promotion.
100. How do child pipelines improve pipeline scalability?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
101. How do dynamic child pipelines work?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
102. How do multi-project pipelines coordinate dependencies?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
103. How do you version shared pipeline templates?
**Answer:** Extract the behavior behind a small documented interface, keep inputs and outputs explicit, and test the reusable unit independently.
104. How do you prevent breaking changes in a shared template?
**Answer:** Extract the behavior behind a small documented interface, keep inputs and outputs explicit, and test the reusable unit independently.
105. How do you implement deployment concurrency control?
**Answer:** Bound concurrency, preserve a small failure domain, verify health between batches, and stop promotion when the error budget is exceeded.
106. How do you model change freezes?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
107. How do you create a release from a tag?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
108. How do you sign release artifacts?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
109. How do you verify image provenance in CI?
**Answer:** Build a minimal immutable image, pin dependencies, scan and sign it, publish it to a controlled registry, and deploy by digest when possible.
110. How do you integrate SBOM generation and vulnerability gates?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
111. How do you design disaster recovery for GitLab itself?
**Answer:** Keep the previous known-good version, validate the replacement, and automate a tested rollback or restore path with clear ownership and audit output.
112. How do you back up repositories, registry data, and CI configuration?
**Answer:** Keep environment-specific values outside reusable logic, validate them at the boundary, and provide safe defaults only where appropriate.
113. How do you test GitLab backup restoration?
**Answer:** Automate syntax, static analysis, unit, and integration checks in CI; fail early and publish useful diagnostics as artifacts.
114. How do you observe pipeline health at organization scale?
**Answer:** Check a meaningful dependency or application endpoint, fail the operation when the check fails, and use the result to stop or roll back promotion.
115. Which DORA metrics can GitLab provide?
**Answer:** Emit structured, correlation-aware telemetry with enough context to diagnose duration, failures, deployment version, and affected environment.
116. How do you reduce pipeline lead time without reducing safety?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
117. How do you handle flaky tests without hiding defects?
**Answer:** Automate syntax, static analysis, unit, and integration checks in CI; fail early and publish useful diagnostics as artifacts.
118. How do you design a regulated production approval workflow?
**Answer:** A strong answer should define the concept, show a small GitLab CI/CD implementation, explain failure behavior, and describe how it would be tested in CI.
119. How do you connect GitLab deployment events to incident management?
**Answer:** Separate validation, build, promotion, and verification; use immutable artifacts, protected production controls, and an observable rollback path.
120. Design a secure, reusable, observable GitLab platform for Azure, AWS, and on-premises delivery.
**Answer:** Emit structured, correlation-aware telemetry with enough context to diagnose duration, failures, deployment version, and affected environment.

## HackerRank-Style CI/CD Challenges: 121-150

121. Write a pipeline with lint, test, build, and deploy stages.
**Answer:** Test the happy path, invalid input, timeout, retry exhaustion, and partial failure with mocks for external systems and an assertion on the final result.
122. Store a generated report as an artifact.
**Answer:** Separate validation, build, promotion, and verification jobs; use immutable artifacts, protected variables or OIDC, and manual approval for production.
123. Cache Python dependencies with a branch-safe key.
**Answer:** Implement the solution with validated inputs, deterministic behavior, clear failure handling, tests, and an example execution command for GitLab CI/CD.
124. Run deployment only on the default branch.
**Answer:** Deploy an immutable version, run a health or smoke check, promote only on success, and invoke a tested rollback while preserving the failure in logs.
125. Add a manual production job with a protected environment.
**Answer:** Parse with the platform's structured data tool, validate required fields and types at the boundary, and return a clear nonzero failure for malformed input.
126. Build and push an immutable commit-SHA Docker tag.
**Answer:** Use declarative manifests with pinned images, probes, resource controls, least-privilege identity, and a rollout strategy that can be observed and rolled back.
127. Test two Python versions and two database engines with a matrix.
**Answer:** Test the happy path, invalid input, timeout, retry exhaustion, and partial failure with mocks for external systems and an assertion on the final result.
128. Build a DAG so independent tests run in parallel.
**Answer:** Use a bounded worker pool, collect each success and exception separately, and fail the operation when the defined error threshold is exceeded.
129. Create a review app and manual stop job.
**Answer:** Separate validation, build, promotion, and verification jobs; use immutable artifacts, protected variables or OIDC, and manual approval for production.
130. Always upload JUnit test results.
**Answer:** Test the happy path, invalid input, timeout, retry exhaustion, and partial failure with mocks for external systems and an assertion on the final result.
131. Include SAST and dependency scanning templates.
**Answer:** Implement the solution with validated inputs, deterministic behavior, clear failure handling, tests, and an example execution command for GitLab CI/CD.
132. Include secret detection and fail on a finding.
**Answer:** Implement the solution with validated inputs, deterministic behavior, clear failure handling, tests, and an example execution command for GitLab CI/CD.
133. Add a Helm lint job.
**Answer:** Separate validation, build, promotion, and verification jobs; use immutable artifacts, protected variables or OIDC, and manual approval for production.
134. Add a Terraform validate and plan job.
**Answer:** Express the desired state with typed inputs, stable addresses, policy validation, protected state, and a reviewed plan before apply.
135. Obtain Azure credentials through OIDC.
**Answer:** Separate validation, build, promotion, and verification jobs; use immutable artifacts, protected variables or OIDC, and manual approval for production.
136. Obtain AWS identity through OIDC.
**Answer:** Separate validation, build, promotion, and verification jobs; use immutable artifacts, protected variables or OIDC, and manual approval for production.
137. Generate a child pipeline from an artifact.
**Answer:** Separate validation, build, promotion, and verification jobs; use immutable artifacts, protected variables or OIDC, and manual approval for production.
138. Wait for an infrastructure project with a multi-project pipeline.
**Answer:** Separate validation, build, promotion, and verification jobs; use immutable artifacts, protected variables or OIDC, and manual approval for production.
139. Serialize production deployments with `resource_group`.
**Answer:** Parse the input into structured records, use a map or counter for aggregation, sort only when ranking is required, and test empty, duplicate, and boundary inputs.
140. Create a canary, smoke-test, and manual promotion flow.
**Answer:** Test the happy path, invalid input, timeout, retry exhaustion, and partial failure with mocks for external systems and an assertion on the final result.
141. Create a tag-based release job.
**Answer:** Deploy an immutable version, run a health or smoke check, promote only on success, and invoke a tested rollback while preserving the failure in logs.
142. Run a job only from a scheduled pipeline.
**Answer:** Separate validation, build, promotion, and verification jobs; use immutable artifacts, protected variables or OIDC, and manual approval for production.
143. Block production changes during a deployment freeze.
**Answer:** Deploy an immutable version, run a health or smoke check, promote only on success, and invoke a tested rollback while preserving the failure in logs.
144. Add a manual rollback job for a previous artifact.
**Answer:** Deploy an immutable version, run a health or smoke check, promote only on success, and invoke a tested rollback while preserving the failure in logs.
145. Send a failure notification from `after_script`.
**Answer:** Implement the solution with validated inputs, deterministic behavior, clear failure handling, tests, and an example execution command for GitLab CI/CD.
146. Publish pipeline duration metrics.
**Answer:** Separate validation, build, promotion, and verification jobs; use immutable artifacts, protected variables or OIDC, and manual approval for production.
147. Retain a backup artifact for 30 days.
**Answer:** Separate validation, build, promotion, and verification jobs; use immutable artifacts, protected variables or OIDC, and manual approval for production.
148. Protect cloud credentials without plaintext secrets.
**Answer:** Implement the solution with validated inputs, deterministic behavior, clear failure handling, tests, and an example execution command for GitLab CI/CD.
149. Build a reusable YAML component for security gates.
**Answer:** Separate validation, build, promotion, and verification jobs; use immutable artifacts, protected variables or OIDC, and manual approval for production.
150. Build a secure pipeline with OIDC, immutable artifacts, canary, rollback, and metrics.
**Answer:** Deploy an immutable version, run a health or smoke check, promote only on success, and invoke a tested rollback while preserving the failure in logs.

## Executable Answers

- [Beginner answers](interview-answers/beginner.yml): stages, dependencies, and artifacts.
- [Intermediate answers](interview-answers/intermediate.yml): matrix testing and review apps.
- [Advanced answers](interview-answers/advanced.yml): canary promotion, smoke tests, and deployment locking.
