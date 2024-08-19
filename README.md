# versioning
name: Deploy

on:
  push:
    branches:
      - 'REL'
      - 'master'
      - 'HTX'

jobs:
  deploy:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v3

      - name: Set up variables
        id: vars
        run: |
          BRANCH_NAME=${GITHUB_REF##*/}
          COMMIT_HASH=${GITHUB_SHA:0:7}
          echo "BRANCH_NAME=$BRANCH_NAME" >> $GITHUB_ENV
          echo "COMMIT_HASH=$COMMIT_HASH" >> $GITHUB_ENV
          echo "VERSION=$(echo $BRANCH_NAME | sed 's/[^a-zA-Z0-9]//g')-$(echo $COMMIT_HASH)" >> $GITHUB_ENV

      - name: Display version
        run: echo "Version: $VERSION"
