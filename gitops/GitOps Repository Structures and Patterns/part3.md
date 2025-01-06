This third part is about Repository Patterns, 
which answer the question about the number of GitOps repos. 
There are a few patterns to choose from in this category.
However, the choice does not have to be exclusive.
Some patterns can also be combined well. 

Monorepo
---
When the entire configuration is stored in a single repo, it is called "monorepo". 
It is questionable whether the typical advantages of monorepo in software development, as used by some big tech companies, 
for example easier refactoring and dependency management, also apply to GitOps. 
Disadvantages of monorepos are often more difficult to configure per-folder authorization and poor performance due to the large repo, due to the many commits. 
The opposite of monorepo is sometimes referred to as "polyrepo". However, the term polyrepo does not refer to a single pattern.

Repo per Team
---
When multiple repos are created, most people first think of the "repo per team" pattern.
More generalized, the term "tenant" is sometimes used instead of team. This offers the advantage that repo-level authorization is typically easy to handle in source code management (SCM). 
In addition, it often feels natural to mimic the structures of the organization, as mentioned at the outset (Conway's Law).
In addition, each team is also only shown what is relevant to them, 
which reduces complexity and "mental load."

![image](https://github.com/user-attachments/assets/87fdd0b5-4970-479b-a104-5d12e13fab86)

Repo per App
---
The "Repo per App" pattern offers an alternative. 
This pattern is often used for apps that are developed by the team itself. 
This is meant in contrast to off-the-shelf/3rd-party apps that are operated but not self-developed. 
The pattern has the advantage that everything that belongs to an application is in the same repo. 
This includes the application's code, documentation and config. 
Config means Kubernetes resources, for example; in some cases, this is referred to as "Infra As Code". 
Storing source code and config in the same repo is very popular, especially among developers. 
However, it is recommended (for example, according to Argo CD) to separate the source code of the application from the config. At this point, it makes sense to distinguish the terms app repo (contains source code) and GitOps repo.

Figure 1 shows a comparison and further synonyms. 
The separation of app repo and GitOps repo has, among other things, the advantage that the entire config (for example, of a team with multiple applications or of an entire cluster) is in a central location, where it can be better audited and searched. 
This separation also has advantages for automating the update of newly built image versions with the CI server, as it avoids endless loops of build jobs and Git pushes. On the other hand, this very thing is also a disadvantage, 
since there is no CI job to perform static code analysis, for example. What now?

Config Replication
---
![image](https://github.com/user-attachments/assets/17db35f8-d0e8-416a-9ec9-2dcbf8f56d12)
A compromise can be to implement the "Repo per App" pattern by "Config Replication". 
In this case, the config remains in the app repo and is then pushed from the CI server to the GitOps repo.
In this process, the CI server can also be used to implement Shift Left: It can perform static code analysis. 
Enclosed are some concrete tool suggestions: By means of yamllint simple syntax errors can be found early. 
Kubeconform prevents Kubernetes resources from using fields that are not present in the API server's schema. 
Helm Lint can be used to find errors in Helm Charts.

Of course, Config Replication does not only have advantages. 
One disadvantage is the complexity of the resulting pipelines. 
To avoid having to duplicate the logic for every application, it makes sense to develop something reusable here.
Examples of this are a GitHub Action or a Jenkins Shared Library.
Experience shows that quite a bit of effort is required before this all works resiliently. 
For example, concurrency in interaction with Git and automatic merges can be risky (retry strategies and risk of inconsistency) and the advanced features mentioned,
such as static code analysis and information in commits can cause additional effort.
So it is recommended to use something existing here instead of building it yourself.
An example is the GitOps-Build-Lib for Jenkins.
It was also used to build the commit shown in Figure 3. Another disadvantage is the redundancy of the config. 
It exists once in the app repo and once in the GitOps repo.

Repo Pointer
---
![image](https://github.com/user-attachments/assets/2fbe33d5-2d28-427b-a40e-82b654a7b8c2)
If the redundancy bothers you, 
you can alternatively implement the "repo per app" pattern with a "repo pointer" as shown schematically in Figure 4. 
In this case, the code is not replicated, but referenced from the GitOps repo to the app repo. 
This can be implemented, for example, with an Application Custom Resource (CR) in Argo CD or a Kustomization CR in Flux. 
The GitOps operator then pulls the config directly from the app repo. 
The Git-native way via submodules would also be possible. However, experience has shown that the use of CRs is more usable.
This approach also has its disadvantages. For example, 
the GitOps controller must be authorized on many repos and the GitOps repo is no longer the central location for Config, 
but only contains links.

Repo per Environment
----
A last pattern that is feasible with regard to repositories is "Repo per Environment" (also "Environment per Repo" or with the term "Stage" instead of "Environment"). 
Here, a repository is created for each environment (for example, development, staging, production). 
This pattern is rarely chosen because it leads to a large number of repositories and a less automated, more tedious GitOps process.
Reasons for choosing this are mostly organizational requirements.
For example, when developers are not allowed to access production or authorization on folders within a Git repo is not possible or isolated enough. 
Another use case is when releases need to be approved by a security team.
