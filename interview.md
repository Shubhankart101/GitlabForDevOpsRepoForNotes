# GitLab DevOps Interview Question Bank

This bank contains 120 questions organized by difficulty. Use the pipeline examples in `scripts/` and `examples/` to build practical answers.

## Beginner: 1-40

1. What problem does GitLab CI/CD solve?
2. What is a GitLab project?
3. What is a repository?
4. What is a commit?
5. What is a branch?
6. What is a merge request?
7. What is a protected branch?
8. What is a `.gitlab-ci.yml` file?
9. What is a pipeline?
10. What is a stage?
11. What is a job?
12. What is a runner?
13. What is an executor?
14. What is the purpose of an image in a job?
15. What does the `script` keyword define?
16. What is the difference between `before_script` and `after_script`?
17. What is an artifact?
18. What is a cache?
19. How do artifacts differ from cache?
20. What are predefined CI/CD variables?
21. What is `CI_COMMIT_SHA`?
22. What is `CI_COMMIT_REF_NAME`?
23. How do you define a custom variable?
24. What is a manual job?
25. What does `when: manual` do?
26. What is a pipeline environment?
27. How do you name a staging environment?
28. What is a pipeline rule?
29. What does `workflow: rules` control?
30. How do you run a job only on the default branch?
31. What is a Docker-in-Docker service?
32. How do you build a Docker image in GitLab CI?
33. What is the GitLab Container Registry?
34. How do you authenticate to the registry?
35. Where should passwords be stored?
36. What is a masked variable?
37. What is a protected variable?
38. How do you inspect a failed job log?
39. What is a retry and when is it appropriate?
40. How do you cancel a running pipeline?

## Intermediate: 41-80

41. How do jobs move through stages?
42. What does `needs` change about pipeline execution?
43. How do you construct a directed acyclic pipeline graph?
44. What is `parallel:matrix`?
45. How do you test multiple language versions?
46. How do you pass artifacts between jobs?
47. How do you set artifact expiration?
48. How do you cache language dependencies?
49. How do cache keys affect correctness?
50. How do `rules` differ from legacy `only` and `except`?
51. How do you prevent duplicate branch and merge-request pipelines?
52. How do you create a review app?
53. How do you stop a review app?
54. What is a protected environment?
55. How do deployment approvals work?
56. What is a resource group?
57. How do you prevent concurrent production deployments?
58. How do you publish JUnit test reports?
59. What is a dotenv report?
60. How do you publish code-quality results?
61. How do SAST templates work?
62. How does dependency scanning work?
63. How does secret detection work?
64. How do you scan container images?
65. How do you lint Helm charts in CI?
66. How do you run Terraform validate and plan?
67. How do you prevent Terraform plan secrets leaking in artifacts?
68. What is an environment URL?
69. How do you define a deployment rollback job?
70. How do you use `allow_failure` responsibly?
71. What is a scheduled pipeline?
72. How do you identify the pipeline source?
73. What are GitLab CI includes?
74. How do you reuse YAML with anchors and extends?
75. What is a CI/CD component?
76. How do you share templates across projects?
77. How do you use runner tags?
78. What are protected runners?
79. How do you troubleshoot a job stuck pending?
80. How do you design a pipeline for a monorepo?

## Advanced: 81-120

81. Design a secure enterprise GitLab runner architecture.
82. How do shared and group runners differ?
83. How do you isolate untrusted merge-request code?
84. How do you secure privileged Docker runners?
85. What are the risks of Docker-in-Docker?
86. How do rootless or Kaniko-style builds change the threat model?
87. How do you implement Azure OIDC federation from GitLab?
88. How do you implement AWS OIDC federation from GitLab?
89. Why are short-lived cloud credentials preferable?
90. How do you restrict a federated role to one project and branch?
91. How do you manage protected secrets across environments?
92. How do you rotate a credential without pipeline downtime?
93. How do you design a multi-account AWS deployment pipeline?
94. How do you design a multi-subscription Azure deployment pipeline?
95. How do you promote immutable artifacts between environments?
96. How do you prevent rebuilding an artifact during promotion?
97. How do you implement canary deployment in GitLab?
98. How do you gate production on health metrics?
99. How do you automate rollback after a failed smoke test?
100. How do child pipelines improve pipeline scalability?
101. How do dynamic child pipelines work?
102. How do multi-project pipelines coordinate dependencies?
103. How do you version shared pipeline templates?
104. How do you prevent breaking changes in a shared template?
105. How do you implement deployment concurrency control?
106. How do you model change freezes?
107. How do you create a release from a tag?
108. How do you sign release artifacts?
109. How do you verify image provenance in CI?
110. How do you integrate SBOM generation and vulnerability gates?
111. How do you design disaster recovery for GitLab itself?
112. How do you back up repositories, registry data, and CI configuration?
113. How do you test GitLab backup restoration?
114. How do you observe pipeline health at organization scale?
115. Which DORA metrics can GitLab provide?
116. How do you reduce pipeline lead time without reducing safety?
117. How do you handle flaky tests without hiding defects?
118. How do you design a regulated production approval workflow?
119. How do you connect GitLab deployment events to incident management?
120. Design a secure, reusable, observable GitLab platform for Azure, AWS, and on-premises delivery.

## HackerRank-Style CI/CD Challenges: 121-150

121. Write a pipeline with lint, test, build, and deploy stages.
122. Store a generated report as an artifact.
123. Cache Python dependencies with a branch-safe key.
124. Run deployment only on the default branch.
125. Add a manual production job with a protected environment.
126. Build and push an immutable commit-SHA Docker tag.
127. Test two Python versions and two database engines with a matrix.
128. Build a DAG so independent tests run in parallel.
129. Create a review app and manual stop job.
130. Always upload JUnit test results.
131. Include SAST and dependency scanning templates.
132. Include secret detection and fail on a finding.
133. Add a Helm lint job.
134. Add a Terraform validate and plan job.
135. Obtain Azure credentials through OIDC.
136. Obtain AWS identity through OIDC.
137. Generate a child pipeline from an artifact.
138. Wait for an infrastructure project with a multi-project pipeline.
139. Serialize production deployments with `resource_group`.
140. Create a canary, smoke-test, and manual promotion flow.
141. Create a tag-based release job.
142. Run a job only from a scheduled pipeline.
143. Block production changes during a deployment freeze.
144. Add a manual rollback job for a previous artifact.
145. Send a failure notification from `after_script`.
146. Publish pipeline duration metrics.
147. Retain a backup artifact for 30 days.
148. Protect cloud credentials without plaintext secrets.
149. Build a reusable YAML component for security gates.
150. Build a secure pipeline with OIDC, immutable artifacts, canary, rollback, and metrics.

## Executable Answers

- [Beginner answers](interview-answers/beginner.yml): stages, dependencies, and artifacts.
- [Intermediate answers](interview-answers/intermediate.yml): matrix testing and review apps.
- [Advanced answers](interview-answers/advanced.yml): canary promotion, smoke tests, and deployment locking.
