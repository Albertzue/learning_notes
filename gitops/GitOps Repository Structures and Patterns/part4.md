This part is about Promotion Patterns.
The promotion patterns describe different ways to implement environments (also known as stages, for example "QA", "Staging" and "Production") with GitOps. 
We refer to this process as promotion.
Sometimes the term promotion is preceded by a word such as release, application, environment, workload, or change. 
This article uses the terms environment and promotion in the following.

Branch vs Folder per Environment
---
 We are talking about the Branch per Environment (also Environment per Branch) pattern. 
 The entire config, which is located on a branch, is always deployed to an environment. 
 The promotion then takes place by a merge in Git. Interestingly, there are few success stories for this pattern.
 Instead, they recommend the Folder per Environment pattern (also "Environment per Folder" or with the term "directory" instead of "folder"). 
 Here the environments are realized as folders on a branch (trunk-based). For the promotion, short-lived branches are created in which the changes are copied from one environment folder to the next.
 These short-lived branches contain only one feature at a time and are deleted again with the merge. 
 Since environments differ only in a few areas, there is often a lot of duplication.
 However, with tools like Helm and Kustomize, this duplication can be prevented.
