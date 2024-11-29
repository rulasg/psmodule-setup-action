# Powershell Module Setup Action

[![Test Powershell Setup Action](https://github.com/rulasg/psmodule-setup-action/actions/workflows/test-action.yml/badge.svg)](https://github.com/rulasg/psmodule-setup-action/actions/workflows/test-action.yml)

An action that setups a powershell module to be used later in the workflow job.

Testing is key for a healthy and effitient development process.

This Action will setup the module on the runner for later use on the job.

## Calling the action

This workflow will run `psmodule-setup-action` to setup version 2.0 of MyModule for later to be use on next scritps steps.

```yaml
name: Test psmodule-setup-action

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

      - name: PsModule Setup
        uses: rulasg/psmodule-setup-action@v1
        with:
          Name: TestingHelper
          Version: '4.0.1-preview'
    
      - name: Run tests
        run: |
          $module = Get-Module -ListAvailable -Name TestingHelper

          if ($module -eq $null) { throw "Module TestingHelper not found" }

          if($module.count -ne 1) { throw "More than one module found"}

          if($module[0].Name -ne 'TestingHelper') { throw "Module name mismatch" }

          if($module[0].version.ToString() -ne '4.0.1') { throw "Version mismatch" }

```
