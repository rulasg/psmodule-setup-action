# TestingHelper Setup Action

[![Test TestingHelper Setup Action](https://github.com/rulasg/testinghelper-setup-action/actions/workflows/test-action.yml/badge.svg)](https://github.com/rulasg/testinghelper-setup-action/actions/workflows/test-action.yml)

An action that setups TestingHelper Powershell module to be used later in the workflow job.

Testing is key for a healthy and effitient development process.

[TestingHelper](https://github.com/rulasg/testingHelper#readme) will help you on different faces of the developmnet lifecycle of a powershell module including testing.

This Action will setup the module on the runner for later use on the job.

## Calling the action

This workflow will run `testinghelper-setup-action` to setup version 2.0 of TestingHelper for later to call `testinghelper-action` to run the tests of the checkout module.

```yaml
name: Test with TestingHelper-Action

on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]
  workflow_dispatch:

permissions:
  # To run test we only need to read the repository
  contents: read

jobs:
  test:
    runs-on: ubuntu-latest

    steps:
      - name: Checkout repository
        uses: actions/checkout@v3

      - name: Setup TestingHelper
        uses: rulasg/testinghelper-setup-action@v1
        with:
          Version: '2.0'
    
      - name: Run tests
        uses: rulasg/testinghelper-action@v1
```
