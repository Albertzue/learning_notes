A key issue in the introduction of GitOps is the design of the GitOps process and associated repositories. This raises questions about:

1. The structure of the repositories,
2. implementation of stages/environments,
3. use of branches,
4. ratio of the number of GitOps operators to the number of clusters and/or namespaces and
5. how everything should be wired in the end.
 ![image](https://github.com/user-attachments/assets/e344264d-f363-4dbc-ae4d-2e29795c548e)


Categories of GitOps patterns
---

GitOps patterns are named and described in the following categories:

1. Operator Deployment – Ratio of number of GitOps operators to Kubernetes clusters and namespaces.
2. Repository – How many GitOps repos are used?
3. Promotion – How are stages/environments modeled?
4. Wiring – Bootstrapping the operator, connecting the repos, branches and folders, grouping resources.
