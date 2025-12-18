---
title: Quickstart
slug: docs/quickstart
description: |
  How to quickly spin-up your website with ScissorHands.NET
---

You've [setup the development environment](/docs/setup). Let's quickly build a website using ScissorHands.NET!

## Scaffolding App

1. Create a new empty web app.

    ```bash
    dotnet new web -n MyScissorHandsApp
    ```

1. Add a NuGet package to the app.

    ```bash
    dotnet add ./MyScissorHandsApp package ScissorHands.Web --prerelease
    ```

   > **NOTE**: ScissorHands.NET is currently in public preview. Therefore, make sure to add the `--prerelease` option when adding the `ScissorHands.Web` package.

1. Open `Program.cs` file and replace all the code lines with the following code snippet.

    ```csharp
    using ScissorHands.Web;
    
    var app = await new ScissorHandsApplication<MainLayout, IndexView, PostView, PageView>(args)
                        .VerifyCommandArguments()
                        .BuildAsync();
    await app.RunAsync();
    ```

1. Build the app.

    ```bash
    dotnet restore && dotnet build
    ```

That's it!

## Running App

1. Run the app. To run the app locally, always use the `--preview` option.

    ```bash
    dotnet run --project ./MyScissorHandsApp -- --preview
    ```

   You'll be able to see the web app URL on the terminal. The default URL is `http://localhost:5000`, but it may vary depending on your `Properties/launchSettings.json`.

1. Open a web browser and navigate to the web app. Then, you'll be able to see the following screen.

   ![Screenshot of "Welcome onboard ScissorHands.NET"](/images/quickstart-01.jpg)

Congratulations! You've just run your first ScissorHands.NET app!

## Adding First Post

1. Let's add a blog post. Create a `contents/posts` directory.

    ```bash
    # zsh/bash
    mkdir -p ./MyScissorHandsApp/contents/posts
    ```

    ```powershell
    # PowerShell
    New-Item -ItemType Directory -Path ./MyScissorHandsApp/contents/posts -Force
    ```

1. Create a markdown file, `hello-world.md` under the `posts` directory.

    ```bash
    # zsh/bash
    touch ./MyScissorHandsApp/contents/posts/hello-world.md
    ```

    ```powershell
    # PowerShell
    New-Item -iTemType File -Path ./MyScissorHandsApp/contents/posts/hello-world.md -Force
    ```

1. Open `hello-world.md` and add the following contents.

    ```md
    ---
    title: Hello, world
    slug: hello-world
    description: My first blog post
    author: The ScissorHands
    ---
    
    ## It's my first blog post
    
    How exciting!
    ```

1. Run the app again.

    ```bash
    dotnet run --project ./MyScissorHandsApp -- --preview
    ```

1. Open a web browser and navigate to the web app. Then, you'll be able to see your list of blog posts.

   ![Screenshot of blog post list](/images/quickstart-02.jpg)

1. Click the blog post title, `Hello, world`. Then you'll be able to see the blog post content.

   ![Screenshot of blog post content](/images/quickstart-03.jpg)

Congratulations! You've just added your first blog post to ScissorHands.NET!

---

👈 [Setup](/docs/setup) | 👆 [Documentation](/docs) | [Build](/docs/build) 👉
