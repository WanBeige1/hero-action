# hero-action-test

[![test-action](https://github.com/unfor19/hero-action-test/workflows/test-action/badge.svg)](https://github.com/unfor19/hero-action-test/actions?query=workflow%3Atest-action)

This repository is meant for testing the master branch of the action - [unfor19/hero-action](https://github.com/marketplace/actions/hero-action)
name: testing
on:
  push:
    branches: [master]
    paths-ignore:
      - "README.md"
  workflow_dispatch:

jobs:
  dispatch_test_action:
    name: Dispatch Test Action
    runs-on: ubuntu-20.04
    steps:
      - uses: actions/checkout@v2
      - name: Workflow Dispatch Status
        uses: unfor19/hero-action@v1.0.2
        with:
          action: "dispatch-status"
          src_repository: ${{ github.repository }}
          src_workflow_name: ${{ github.workflow }}
          src_sha: ${{ github.sha }}
          target_repository: ${{ github.repository }}-test
          target_workflow_name: "test-action.yml"
          gh_token: ${{ secrets.GH_TOKEN }} # scope: repo + workflow
