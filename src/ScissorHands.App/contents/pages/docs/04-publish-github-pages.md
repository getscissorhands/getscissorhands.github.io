---
title: Publish to GitHub Pages
slug: docs/publish/github-pages
description: |
  How to publish the artifact to GitHub Pages
---

Publishing your ScissorHands.NET app to [GitHub Pages](https://docs.github.com/pages/getting-started-with-github-pages/what-is-github-pages) requires a [GitHub Actions](https://docs.github.com/actions/get-started/understand-github-actions) workflow.

## Configure to publish GitHub Pages

1. [Configure your GitHub repository to publish your app to GitHub Pages through GitHub Actions](https://docs.github.com/pages/getting-started-with-github-pages/configuring-a-publishing-source-for-your-github-pages-site#publishing-with-a-custom-github-actions-workflow).
1. Add [GitHub Secrets](https://docs.github.com/actions/how-tos/write-workflows/choose-what-workflows-do/use-secrets) to the repository.
   - `GH_PACKAGE_USERNAME`
   - `GH_PACKAGE_TOKEN`

## Write a GitHub Actions workflow

1. Create a GitHub Actions workflow file under the `.github/workflows` directory. Let's say the filename is `main.yaml`.
1. Add the following workflow details. You can customise it if you want.

    ```yml
    name: Publish GitHub Pages
    
    on:
      push:
        branches:
        - main
    
    env:
      GH_PACKAGE_USERNAME: '${{ secrets.GH_PACKAGE_USERNAME }}'
      GH_PACKAGE_TOKEN: '${{ secrets.GH_PACKAGE_TOKEN }}'
    
    jobs:
      build_and_test:
        name: Build and test packages
    
        runs-on: ubuntu-latest
    
        steps:
        - name: Checkout the repository
          uses: actions/checkout@v6
    
        - name: Setup .NET SDK
          uses: actions/setup-dotnet@v5
          with:
            dotnet-version: '10.x'
      
        - name: Build and publish artifact
          shell: bash
          run: |
            dotnet restore
            dotnet build -c Release
            dotnet run --project <YOUR_SCISSORHANDS_APP_DIRECTORY> -- --build
    
        - name: Upload artifact for web
          uses: actions/upload-pages-artifact@v4
          with:
            path: <YOUR_SCISSORHANDS_APP_DIRECTORY>/dist
    
      publish:
        name: Publish preview site
        needs:
        - build_and_test
    
        runs-on: ubuntu-latest
    
        environment:
          name: github-pages
          url: ${{ steps.deployment.outputs.page_url }}
    
        permissions:
          contents: write
          pages: write
          id-token: write
    
        steps:
        - name: Deploy to GitHub Pages
          id: deployment
          uses: actions/deploy-pages@v4
    ```

1. Commit and push the GitHub Actions workflow.
1. Once published, you can find out your app on `https://<GITHUB_USERNAME>.github.io/<GITHUB_REPOSITORY_NAME>`.

   > **NOTE**: If you configure your [GitHub Pages with a custom domain](https://docs.github.com/pages/configuring-a-custom-domain-for-your-github-pages-site/about-custom-domains-and-github-pages) like `contoso.com`, you can visit your website by `https://contoso.com` instead of `https://<GITHUB_USERNAME>.github.io/<GITHUB_REPOSITORY_NAME>`.

Congratulations! You've just published your ScissorHands.NET app to GitHub Pages!

---

👈 [Publish](/docs/publish) | 👆 [Documentation](/docs) | [Publish to Netlify](/docs/publish/netlify) 👉
