The first step in this is to bootstrap the GitOps operator. 
This involves installing the GitOps operator in the cluster and setting it up to point to an initial GitOps repo.
Ideally, the configuration of the GitOps operator is also stored in Git, 
so that updates and changes to the configuration of the GitOps operator can be made via GitOps in the future. 
Bootstrapping can be implemented via kubectl, 
but usually there are special command line tools for the respective GitOps operators that are easier to use.

Bootstrapping is followed by linking, i.e. connecting further repositories, folders or branches.
This is often accompanied by grouping, i.e. the grouping of certain resources, for example everything that belongs to an application or an environment. 
Both linking and grouping are typically done using specific CRDs,
for example, the Kustomization in Flux and the Application in Argo CD.
