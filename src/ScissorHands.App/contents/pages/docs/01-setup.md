---
title: Setup
slug: docs/setup
description: |
  Setting up a development environment to build a website with ScissorHands.NET
---

To build a website with ScissorHands.NET, you should have the following prerequisites.

## Development Environment

- [.NET 10 SDK](https://dotnet.microsoft.com/download/dotnet/10.0) or later
- [Visual Studio 2026](https://visualstudio.microsoft.com/downloads/) or [VS Code](https://code.visualstudio.com/download) with [C# DevKit](https://marketplace.visualstudio.com/items?itemName=ms-dotnettools.csdevkit)
- [GitHub account (free)](http://github.com/signup)

## Access to GitHub NuGet Package Registry

Currently ScissorHands.NET can be downloaded only from [GitHub NuGet Package Registry](https://docs.github.com/packages/working-with-a-github-packages-registry/working-with-the-nuget-registry), which requires authentication with [PAT (Personal Access Token)](https://docs.github.com/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens#creating-a-personal-access-token-classic).

1. Create a PAT (classic) containing the `read:packages` scope.
1. Set environment variables for GitHub NuGet Package Registry.

    ```bash
    # zsh/bash
    source ./scripts/setup-gh-auth.sh \
        --username "<GITHUB_USERNAME>" --token "<GITHUB_TOKEN>"
    ```

    ```powershell
    # PowerShell
    . ./scripts/setup-gh-auth.ps1 `
        -Username "<GITHUB_USERNAME>" -Token "<GITHUB_TOKEN>"
    ```

   > **NOTE**: Make sure to **sourcing** the script instead of executing it.

1. Make sure that you've got a `NuGet.config` file that registers the GitHub NuGet Package Registry for ScissorHands.NET. Here's the example of `NuGet.config`.

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <configuration>
      <packageSources>
        <add key="github"
             value="https://nuget.pkg.github.com/getscissorhands/index.json" />
      </packageSources>
      <packageSourceCredentials>
        <github>
            <add key="Username" value="%GH_PACKAGE_USERNAME%" />
            <add key="ClearTextPassword" value="%GH_PACKAGE_TOKEN%" />
          </github>
      </packageSourceCredentials>
    </configuration>
    ```

Congratulations! You're ready to use ScissorHands.NET!

---

👆 [Documentation](/docs) | [Quickstart](/docs/quickstart) 👉
