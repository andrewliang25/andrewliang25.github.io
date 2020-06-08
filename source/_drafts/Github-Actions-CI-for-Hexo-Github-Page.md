---
title: Github Actions - CI for Hexo Github Page
tags:
---

# Lets start it

**Note: Please read my previous article fisrt**

## Set up access key for repo

### Generate keys
```
ssh-keygen -f github-deploy-key
```
### Set up private key
blog repo → settings → Secrets → add a new secret
### Set up public key
blog repo → settings → Deploy keys → add deploy key

## Build new workflow in github action

### Create a workflow
**Set source branch as default**
Action ->  new workflow -> set up a workflow yourself
### Modify main.yml
```
name: HEXO CI

on:
  push:
    branches:
    - master

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
### Commit to master
**Note: .github/workflows/main.yml will be created under default branch (master).**
**Make sure "source branch" has been set as default branch.**

### Set up Hexo config
http -> ssh

# Known Issues

## CI does not tiggered after push

### Check if trigger branch is source branch

### Check if .github/workflows/main.yml locates under source branch

## CI deploy hexo failed with no access

### Make sure keys are entered correctly

### Allow write access on Public Key

## Blank Website

### Set deploy branch as default branch

> Reference
> Winnie's Blog: https://op30132.github.io/2020/02/05/github-action/
