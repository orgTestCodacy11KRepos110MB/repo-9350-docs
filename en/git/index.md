# Git setup

What you need to config?

- Git repo URL to clone
- Access permission for private Git repo
- Webhook that can trigger CI job
- Git provider host
- Access permission to write job status back

![structure](../../_images/git/structure.png)


## Clone Git repo

flow.ci clones git repo via [git clone](https://github.com/flowci-plugins/gitclone) plugin

```yaml
envs:
  FLOWCI_GIT_URL: "https://github.com/FlowCI/spring-petclinic-sample.git" ## Git repo address, support https or ssh

steps:
- name: clone
  docker:
    image: flowci/debian-git ## other images with git command can be applied here as well!
  plugin: 'gitclone'
```


## Access permission for private Git repo

The __SSH-RSA__ `secret` is required if git url is __SSH__ based, for example `git@github.com:FlowCI/docs.git`

1. Create SSH-RSA secret

   - Go to `Settings -> Secret -> +` from Admin page
   - Input a secret name, for example `ras-test`
   - Select `SSH key` category
   - Click `create a new` ssh key pair or paste exsiting public and private key
   - Save

    ![how to create ssh-rsa secret](../../_images/secret/create_ssh_key.gif)

2. Config secret in the flow

   `FLOWCI_GIT_CREDENTIAL` variable is applied for git access permisison in [Git clone plugin](https://github.com/flowci-plugins/gitclone). 
   
   For example:

   ```yaml
    envs:
      FLOWCI_GIT_CREDENTIAL: "rsa-test"

    steps:
    - name: clone
      docker:
        image: flowci/debian-git
      plugin: 'gitclone'
   ```

## Setup Git provider

Different Git provider has different way to setup access permission and webhook

flow.ci currenlty supports:

- [GitHub](en/git/github.md)
- [GitLab](en/git/gitlab.md)
- [Gogs](en/git/gogs.md)
- [Gitee](en/git/gitee.md)
- [Gerrit](en/git/gerrit.md)

please click around the links for more detail
