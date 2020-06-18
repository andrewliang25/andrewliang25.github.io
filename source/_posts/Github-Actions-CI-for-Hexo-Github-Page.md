---
title: Github Actions - CI for Hexo Github Page
date: 2020-06-15 18:48:36
tags:
---

**Note: Already Built GitHub Pages with Hexo**

## Set up access key for repo

### Generate SSH keys
Open terminal and generate SSH keys by following command.
```
ssh-keygen -f github-deploy-key
```
Skip passphrase.

<!-- more -->

{% asset_img sshkeygen.png SSH key generated on terminal %}
After generating, there should be 2 files.
{% asset_img keyfile.png Private Key & Public Key %}

### Set up private key
blog repo → Settings → Secrets → New secret
{% asset_img newsecret.png Create new secret %}
Name: HEXO_DEPLOY_PRI
Value: All content in github-deploy-key
{% asset_img enterHexoDeployPri.png Add Private Key as secret %}
**⚠ Never upload or tell anyone Private Key. ⚠**

### Set up public key
blog repo → Settings → Deploy keys → add deploy key
{% asset_img addDeployKeys.png New deploy key %}
Name: HEXO_DEPLOY_PUB
Value: All content in github-deploy-key.pub
**Check "Allow write access" to enable push access**
{% asset_img deployKeysAddNew.png Add Public Key as deploy key %}

## Build new workflow in github action

### Create a workflow
Fisrt, set source branch as default branch.
Settings -> Branches -> Select your source branch -> Update
{% asset_img setDefaultBranch.png Set Blog Source branch as default branch %}

**Note: the workflow file will be created under default branch.**

Action ->  new workflow -> set up a workflow yourself
{% asset_img setWorkflowYourself.png Set up a workflow yourself %}

### Modify main.yml and commit

Replace "blog_source_branch", "username", "username@email.address" with your own info.
```
name: HEXO CI

on:
  push:
    branches:
    - <blog_source_branch>

jobs:
  build:
    runs-on: ubuntu-latest
    strategy:
      matrix:
        node-version: [10.x]

    steps:
      - uses: actions/checkout@v1

      - name: Use Node.js ${{ matrix.node-version }}
        uses: actions/setup-node@v1
        with:
          node-version: ${{ matrix.node-version }}

      - name: Configuration environment
        env:
          HEXO_DEPLOY_PRI: ${{secrets.HEXO_DEPLOY_PRI}}
        run: |
          mkdir -p ~/.ssh/
          echo "$HEXO_DEPLOY_PRI" | tr -d '\r' > ~/.ssh/id_rsa
          chmod 600 ~/.ssh/id_rsa
          ssh-keyscan github.com >> ~/.ssh/known_hosts
          git config --global user.name "<username>"
          git config --global user.email "<username@email.address>"
      - name: Install dependencies
        run: |
          npm i -g hexo-cli
          npm i
      - name: Deploy hexo
        run: |
          hexo generate && hexo deploy
```
**Note: Hexo CI creates a Virtual Machine and deploy website for you.**

Commit main.yml into default branch.
{% asset_img commitMainYAML.png Commit main.yml into default branch %}

### Config Hexo deploy
Open "_config.yml" on local.
Change git repositary from http form to ssh form.
Deploy branch should be "master".
{% asset_img configDeploySSH.png Deploy config %}

# Known Issues

## CI does not tiggered after push

* Check if source branch is set as trigger branch in main.yml
* Check if .github/workflows/main.yml locates under source branch
{% asset_img pushTriggerCheck.png Check branch %}

## CI deploy hexo failed with no access

* Make sure keys are entered correctly
* Allow write access on Public Key
{% asset_img checkDeployKeyAccess.png Check deploy key access %}

> Reference
> https://help.github.com/en/actions
> https://confluence.atlassian.com/bitbucketserver/creating-ssh-keys-776639788.html
> https://op30132.github.io/2020/02/05/github-action/
