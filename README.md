# cd-tools
## Usage

apiVersion: automation.cloudbees.io/v1alpha1
kind: workflow
name: 'CD test'


on:
  push:
    branches:
      - '**'
jobs:
  build:
    steps:
    - id: cd-tools
        uses: docker://cloudbees/cbflow-tools:2023.12.0.171596_3.2.64_20231207
        with:
            cd-url: https://gradinsky-cd-ps.beescloud.com
            cd-user: admin
            cd-password: changeme
    
runs:
  using: composite
  steps:
    - id: cd-tools
      kind: scan
      uses: docker://cloudbees/cbflow-tools:2023.12.0.171596_3.2.64_20231207
      shell: sh
      run: |
        ectool login --server {{ inputs.cd-url }} admin {{ secrets.cd-password }}
