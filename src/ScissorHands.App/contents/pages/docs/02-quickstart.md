---
title: Quickstart
slug: docs/quickstart
description: |
  How to quickly spin-up your website with ScissorHands.NET
---

Let's quickly build a website using ScissorHands.NET!

## Prerequisites

- [Development environment setup](/docs/setup)

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

    var app = new ScissorHandsApplicationBuilder(args)
                  .AddLayouts<MainLayout, IndexView, PostView, PageView, NotFoundView>()
                  .Build();
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

1. For more details about writing blog posts, see the [Posts](/docs/posts) page.

## Adding Theme

ScissorHands.NET supports the [theme feature](/docs/themes) that makes your web app more user friendly. You can use any [official and community-contributed themes](/docs/themes#list-of-themes) available. Let's use the [Minimal Blog](https://github.com/getscissorhands/minimal-blog) theme for now.

1. Create a `themes` directory within your app.

    ```bash
    # zsh/bash
    mkdir -p ./MyScissorHandsApp/themes
    ```

    ```powershell
    # PowerShell
    New-Item -ItemType Directory -Path ./MyScissorHandsApp/themes -Force
    ```

1. Clone the theme repository under the `themes` directory.

    ```bash
    pushd ./MyScissorHandsApp/themes
    git clone https://github.com/getscissorhands/minimal-blog.git
    popd
    ```

   Alternatively, download the theme file directly from the repository and unzip under the `themes` directory.

    ```bash
    # zsh/bash
    version=$(curl -s https://api.github.com/repos/getscissorhands/minimal-blog/releases/latest | jq -r '.tag_name')
    zipfile="minimal-blog-$version.zip"
    curl -OL https://github.com/getscissorhands/minimal-blog/releases/download/$version/$zipfile
    unzip $zipfile -d ./MyScissorHandsApp/themes/minimal-blog
    ```

    ```powershell
    # PowerShell
    $version = (Invoke-RestMethod -Uri "https://api.github.com/repos/getscissorhands/minimal-blog/releases/latest").tag_name
    $zipfile = "minimal-blog-$version.zip"
    Invoke-WebRequest -Uri "https://github.com/getscissorhands/minimal-blog/releases/download/$version/$zipfile" -OutFile $zipfile
    Expand-Archive -Path $zipfile -DestinationPath "./MyScissorHandsApp/themes/minimal-blog" -Force
    ```

1. Add the `Site` section in `appsettings.json` and declare the theme directory.

    ```jsonc
    {
      "Site": {
        "Theme": "minimal-blog"
      }
    }
    ```

1. Run the app again.

    ```bash
    dotnet run --project ./MyScissorHandsApp -- --preview
    ```

1. You'll see the app with the theme applied!
1. For more details about themes, see the [Themes](/docs/themes) page.

## Adding Plugins

ScissorHands.NET supports the [plugin feature](/docs/plugins) that makes your web app more flexible and extensible. You can use any [official and community-contributed plugins](/docs/plugins#list-of-plugins) available. Let's use the [Google Analytics](https://github.com/getscissorhands/plugins/tree/main/src/ScissorHands.Plugin.GoogleAnalytics) plugin for now.

1. Update the `Plugins` section in `appsettings.json` and declare the Google Analytics plugin. You can acquire the `MeasurementId` value from the [Google Analytics](https://analytics.google.com) dashboard.

    ```jsonc
    {
      "Plugins": [
        {
          "Name": "Google Analytics",
          "Options": {
            "MeasurementId": "G-XXXXXXXX"
          }
        }
      ]
    }
    ```

1. Add a NuGet package.

    ```bash
    dotnet add ./MyScissorHandsApp package ScissorHands.Plugin.GoogleAnalytics --prerelease
    ```

1. Open the `MainLayout.razor` file of your theme and add the `GoogleAnalyticsCompoment` component right after the `<head>` tag.

    ```razor
    <head>
      <GoogleAnalyticsComponent Name="Google Analytics" />
      ...
    </head>
    ```

1. Run the app again

    ```bash
    dotnet run --project ./MyScissorHandsApp -- --preview
    ```

1. Open the HTML view page.
1. You'll see the app with the Google Analytics script applied!
1. For more details about plugins, see the [Plugins](/docs/plugins) page.

Congratulations! You've just added your first blog post to ScissorHands.NET!

---

👈 [Setup](/docs/setup) | 👆 [Documentation](/docs) | [Build](/docs/build) 👉
