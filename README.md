# GitLab CI Pipeline architectures and templates

## Basic
Good for straightforward projects.
- simpliest pipeline in GitLab
- Jobs run independently, sometimes on different runners
- All Jobs in a stage must complete successfully before proceeding to the next stage
- Control pipeline with pipeline options

## Directed Acyclic Graph
https://docs.gitlab.com/ee/ci/directed_acyclic_graph/ 
<br>Good for complex and large projects that need efficient execution.
- Define Job dependencies to optimize pipeline flow
- Jobs run independently, sometimes on different runners
- Dependent Jobs can proceed to next stage without waiting for other Jobs in stage to finish

## Parent/Child Pipelines
https://docs.gitlab.com/ee/ci/pipelines/downstream_pipelines.html#parent-child-pipelines 
<br>Good for monorepos and projects with lots of independently defined components.
- Run child pipelines independend from each other
- Separates entire pipeline configuration in multiple files to keep thins simple
- Useful to branch out long running tasks into separate pipelines
- Consider to use **maximum of 3** triggered child pipelines

## Dynamic Pipelines
Good to connect multiple repos.
- Generate pipeline configuration at build time
- Use the generated configuration at a later stage to run as a child pipeline
- Useful to use a single pipeline configuration with different settings to support a matrix of targets and architectures

## Multi-project Pipelines

https://docs.gitlab.com/ee/ci/pipelines/downstream_pipelines.html#multi-project-pipelines 
<br>Good for larger products that require cross-project interdependencies.
- A pipeline in one project can trigger a pipeline in another project
- You can specify a specific branch
- You can pass variables to downstream pipelines
- If downstream pipeline fails it will not fail upstream pipeline
- Useful then building / deployng large applications that are made up of different components that their own project and build pipeline