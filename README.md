# cd-tools 1
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
            cd-url: https://cd-url.com
            cd-user: admin
            cd-password: changeme
            
