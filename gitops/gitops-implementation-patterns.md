[Link](https://www.redhat.com/en/blog/gitops-implementation-patterns)

The CI/CD Controller pattern
---
In the CI/CD Controller pattern, an independent application or service is aware of the state of one or many source code repositories. 
It executes a CI/CD deployment automatically when code changes within a particular repository.

You may have heard of controller applications including ArgoCD, Jenkins, and TeamCity, 
and controller services such as Travis CI and CircleCI.
![image](https://github.com/user-attachments/assets/a0dfdb0c-7b82-45fe-a61f-3e9de056dda7)

The SCM Controller pattern
---
In the SCM Controller pattern, source code that controls CI/CD deployment activity is colocated in the same Git repository as the application source code. 
Under the SCM Controller, the SCM service can internally execute actions such as builds, tests, and the eventual release to a staging or production target. 
And, if it doesn't have the capabilities it needs for some of the work,
the SCM service has access to the required ancillary services the CI/CD process requires.
![image](https://github.com/user-attachments/assets/6a8207c3-a6ea-4d1a-808e-612e3a4caad3)

Pros and cons
---
The CI/CD Controller pattern's biggest pro is that it provides the versatility to monitor repositories among various SCM service providers. 
The con is that it incurs a greater maintenance burden.
Every repository has its own operational model and peculiarities that need to be accommodated.
This can get to be a chore when the CI/CD Controller manipulates a variety of SCM services.


On the SCM Controller pattern side of the fence, the basic pro is the unification of source control and deployment management. 
Adding deployment behavior into the SCM process makes the SCM system a one-stop-shop development experience. 
In addition to being the sole source of truth for code, 
the SCM also becomes the sole source of truth for deployment processing.

A significant con of the SCM Controller pattern is that repositories that do a lot of VM building and compute-intensive activity internally need to be hosted on machines that are much more powerful than those that do nothing more than simple source code management. 

Another con is that excess merge requests on a code repository not related to the application can result in unnecessary deployments. 
When different teams manage builds (ops) and apps (dev), it can get messy.


In terms of the pros and cons of the CI/CD Controller and SCM Controller patterns, it comes down to the eternal tradeoffs:

1. Price vs. performance
2. Ease of use vs. robust security
3. Central management vs. decentralized independence
