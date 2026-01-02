---
title: Plugins
slug: docs/plugins
description: |
  How to add a plugin to ScissorHands.NET app and how to write my own plugin
---

Plugins provide additional contexts while building an app with ScissorHands.NET. A plugin may add extra HTML tag elements, replace existing HTML elements with something else or convert a placeholder to something else.

## Plugin Structure

Each plugin has at least the following structure:

```text
.
├── README.md
│
├── MyAwesomePlugin.sln
│
└── MyAwesomePlugin/
    ├── MyAwesomePlugin.csproj
    ├── _Imports.razor
    ├── MyAwesomePluginComponent.razor
    └── MyAwesomePlugin.cs
```

- `README.md`: README document of the plugin
- `*.sln`: A solution file for the plugin
- `*.csproj`: A project file that contains the plugin
- `_Imports.razor`: Defines global using directives
- `*Component.razor`: Defines the UI component representing the plugin
- `*Plugin.cs`: Defines the placeholder replacement representing the plugin

## Getting Started

1. Set environment variables for GitHub NuGet Package Registry.

    ```bash
    # zsh/bash
    export GH_PACKAGE_USERNAME="<GITHUB_USERNAME>"
    export GH_PACKAGE_TOKEN="<GITHUB_TOKEN>"
    ```

    ```powershell
    # PowerShell
    $env:GH_PACKAGE_USERNAME = "<GITHUB_USERNAME>"
    $env:GH_PACKAGE_TOKEN = "<GITHUB_TOKEN>"
    ```

1. Create a Razor class library project.

    ```bash
    dotnet new razorclasslib -n MyAwesomePlugin
    ```

1. Add a NuGet package.

    ```bash
    dotnet add package ScissorHands.Plugin --prerelease
    ```

1. Create a plugin class inheriting the `ScissorHands.Plugin.ContentPlugin` class.

    ```csharp
    public class MyAwesomePlugin : ContentPlugin
    {
        public override string Name => "My Awesome ScissorHands Plugin";
    
        public override async Task<ContentDocument> PreMarkdownAsync(
            ContentDocument document,
            PluginManifest plugin, 
            SiteManifest site,
            CancellationToken cancellationToken = default)
        {
            // ADD LOGIC HERE
        }
    
        public override async Task<ContentDocument> PostMarkdownAsync(
            ContentDocument document,
            PluginManifest plugin,
            SiteManifest site,
            CancellationToken cancellationToken = default)
        {
            // ADD LOGIC HERE
        }
    
        public override async Task<string> PostHtmlAsync(
            string html,
            ContentDocument document,
            PluginManifest plugin,
            SiteManifest site,
            CancellationToken cancellationToken = default)
        {
            // ADD LOGIC HERE
        }
    }
    ```

1. Create a plugin component inheriting the `ScissorHands.Plugin.PluginComponentBase` class.

    ```razor
    @* MyAwesomePluginComponent.razor *@
    @inherits ScissorHands.Plugin.PluginComponentBase
    
    <!-- ADD HTML ELEMENTS HERE -->
    
    @code {
        // ADD UI COMPONENT LOGIC HERE
    }
    ```

## Properties of Plugin Component

Since a plugin component inherits `ScissorHands.Plugin.PluginComponentBase`, it exposes the following properties for plugin developers to use:

- `Name`: **Parameter**. Name of the plugin.
- `Documents`: **Cascading Parameter**. List of content documents &ndash; used by `IndexView.razor`
- `Document`: **Cascading Parameter**. Content document &ndash; used by `PostView.razor` and `PageView.razor`
- `Plugins`: **Cascading Parameter**. List of plugins defined in the [Plugins section of `appsettings.json`](/docs/plugins#plugin-configuration)
- `Plugin`: Plugin matches to the component, filtered by its name when it's being initialised.
- `Theme`: **Cascading Parameter**. Theme configuration defined in [`theme.json`](/docs/themes#theme.json)
- `Site`: **Cascading Parameter**. Site configuration defined in the [Site section of `appsettings.json`](/docs/configuration#site-configuration)

## Use Plugin

To use a plugin, it MUST be configured in `appsettings.json` beforehand.

### Plugin Configuration

Open `appsettings.json` and add the plugin configurations to the `Plugins` section:

```jsonc
{
  "Plugins": [
    {
      "Name": "My Awesome ScissorHands Plugin",
      "Options": {
        "Option1": "value1",
        "Option2": "value2"
      }
    }
  ]
}
```

> **NOTE**: Make sure to have the same plugin name in the settings to the one defined in the plugin package.

### Plugin as Component

You can add the plugin as a Razor component. Put your plugin component to `MainLayout.razor`, `IndexView.razor`, `PostView.razor` or `PageView.razor` of your theme. Here's an example putting the plugin to `MainLayout.razor`.

```razor
@* MainLayout.razor *@
...

<MyAwesomePluginComponent Name="My Awesome Plugin" />

...
```

### Plugin as Placeholder

You can add the plugin as a placeholder. Put your plugin placeholder to `MainLayout.razor`, `IndexView.razor`, `PostView.razor` or `PageView.razor` of your theme. Here's an example putting the plugin to `MainLayout.razor`.

```razor
@* MainLayout.razor *@
...

<plugin:my-awesome-plugin />

...
```

### Plugin as Markdown

TBD

## List of Plugins

Here are the list of plugins you can currently use &ndash; either official or community contributed.

### Official Plugins

- [Google Analytics](https://github.com/getscissorhands/plugins/tree/main/src/ScissorHands.Plugin.GoogleAnalytics)
- [Open Graph](https://github.com/getscissorhands/plugins/tree/main/src/ScissorHands.Plugin.OpenGraph)

### Community Plugins

TBD

---

👈 [Themes](/docs/themes) | 👆 [Documentation](/docs)
