---
title: Troubleshooting
subtitle: Plugin creation
layout: guide
order: 0
---




### TypeScript without Jest

You'll need to take the following steps for danger to evaluate your `dangerfile.ts`:

* Install the `ts-jest` package - `yarn add ts-jest --dev`
* Add the following `jest` section to your `package.json`

```json
{
  "jest": {
    "transform": {
      ".(ts|tsx)": "<rootDir>/node_modules/ts-jest/preprocessor.js"
    }
  }
}
```

### I want to only run Danger for internal branches

Let's say you run Danger on the same CI service that deploys your code. If that's open source, you don't want to be letting anyone pull out your private env vars. The work around for this is to not simply call Danger on every test run:

``` sh
'[ ! -z $DANGER_GITHUB_API_TOKEN ] && yarn danger || echo "Skipping Danger for External Contributor"'
```  

This ensures that Danger only runs when you have the environment variables set up to run.
