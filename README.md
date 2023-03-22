# Hightouch Github Action

This Github action allows users to trigger a Hightouch sync with a sync ID via the Hightouch API. Use it in your workflows to automate Hightouch syncs in your pipelines.

## Usage

### Inputs

`sync-id`: The ID of the sync you wish to trigger. You can find this in the Hightouch UI on the sync page.

### Environment variables

`HIGHTOUCH_API_KEY`: The API key for the workspace the sync belongs to. You can create one in Settings > API keys in the Hightouch app.

## Example

Here is an example workflow that utilizes the Hightouch Github action to run a sync whenever there is a push or PR to the `main` branch.

```
on:
  push:
    branches: [ "main" ]
  pull_request:
    branches: [ "main" ]

env:
  HIGHTOUCH_API_KEY: ${{ secrets.HIGHTOUCH_API_KEY }}

jobs:
  trigger-hightouch-sync:
    runs-on: ubuntu-latest
    name: Trigger Hightouch sync
    steps:
    - uses: // REPLACE THIS WITH THE LATEST VERSION
      with:
        sync-id: ${{ vars.HIGHTOUCH_SYNC_ID }}
```

## Handling Multiple Syncs

Include additional steps in the job to trigger multiple syncs with multiple sync IDs.
```
jobs:
  trigger-hightouch-sync:
    runs-on: ubuntu-latest
    name: Trigger Hightouch sync
    steps:
    - uses: hightouchio/hightouch-github-action@v1.0.1
      with:
        sync-id: 10000 
    - uses: hightouchio/hightouch-github-action@v1.0.1
      with:
        sync-id: 20000
```