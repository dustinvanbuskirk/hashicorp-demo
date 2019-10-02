# Codefresh Pipeline - HashiCorp Packer as a step

https://www.packer.io/

Steps:
1. Create [GIT Integration](https://codefresh.io/docs/docs/integrations/git-providers/#adding-more-git-providers-to-your-codefresh-account).
1. Create a Codefresh Pipeline.
1. Create [GIT Trigger](https://codefresh.io/docs/docs/configure-ci-cd-pipeline/triggers/git-triggers/).
1. Add YAML (codefresh.yml) to your pipeline to clone the repository your packer templates exist in and execute packer.

```
version: '1.0'
stages:
  - clone
  - packer
steps:
  main_clone:
    title: Cloning main repository...
    stage: clone
    type: git-clone
    repo: ${{CF_REPO_OWNER}}/${{CF_REPO_NAME}}
    revision: ${{CF_REVISION}}
  PackerAzureBuilder:
    title: Building Azure ARM Image 
    stage: packer
    image: hashicorp/packer:light
    commands:
      - packer build ./packer/azure-arm-ubuntu.json
```
