# Note: Due to old API is no longer support. Please use new [official Cloudflare's Wrangler 3](https://github.com/cloudflare/wrangler-action) action instead.

## cf-pages-action [customized]

## Usage

1. Create an API token in the Cloudflare dashboard with the "Cloudflare Pages — Edit" permission.
2. Add that API token as a secret to your GitHub repository, `CLOUDFLARE_API_TOKEN`.
3. Create a `.github/workflows/spok.yml` file in your repository:

   ```yml
   on: [push]

   jobs:
     publish:
       runs-on: ubuntu-latest
       permissions:
         contents: read
         deployments: write
       name: Checkout repository
       steps:
         - name: Checkout
           uses: actions/checkout@v3

         # Run a build step here if your project requires

         - name: Publish
           uses: pickyzz/cf-pages-action@v1
           with:
             apiToken: ${{ secrets.CLOUDFLARE_API_TOKEN }}
             accountId: YOUR_ACCOUNT_ID
             projectName: YOUR_PROJECT_NAME
             directory: YOUR_BUILD_OUTPUT_DIRECTORY
             # Optional: Enable this if you want to have GitHub Deployments triggered
             gitHubToken: ${{ secrets.GITHUB_TOKEN }}
             # Optional: Switch what branch you are publishing to.
             # By default this will be the branch which triggered this workflow
             branch: main
             # Optional: Change the working directory
             workingDirectory: my-site
             # Optional: Change the Wrangler version, allows you to point to a specific version or a tag such as `beta` default 3
             wranglerVersion: "3"
             # Generate logs when deploying fail
             logsOnFailure: false
   ```

**Replace `YOUR_ACCOUNT_ID`, `YOUR_PROJECT_NAME` and `YOUR_BUILD_OUTPUT_DIRECTORY` with the appropriate values to your Pages project.**
