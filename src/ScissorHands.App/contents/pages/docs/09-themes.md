---
title: Themes
slug: docs/themes
description: |
  How to add a theme to ScissorHands.NET app and how to write my own theme
---

Themes take a crucial part while building an app with ScissorHands.NET. It looks after all UI including the landing page, blog posts and pages. Since ScissorHands.NET uses the [Blazor](https://blazor.net)'s [Razor syntax](https://learn.microsoft.com/aspnet/core/mvc/views/razor), you can easily build page components and UI components for your theme.

## Theme Template &ndash; Starter Pack

If you're unsure, you can start from the [theme template repository](https://github.com/getscissorhands/theme-template). It includes all the basic page components including `_Imports.razor`, `MainLayout.razor`, `IndexView.razor`, `PostView.razor` and `PageView.razor` as well as `theme.json` that describes the metadata of the theme.

## Theme Structure

Each theme has at least the following structure:

```text
.
├── README.md
│
└── src/
    ├── theme.json
    │
    ├── favicon.ico
    │
    ├── assets/
    │   ├── css/
    │   │   └── theme.css
    │   ├── js/
    │   │   └── theme.js
    │   └── images/
    │       └── theme.png
    │
    ├── _Imports.razor
    ├── MainLayout.razor
    ├── IndexView.razor
    ├── PostView.razor
    ├── PageView.razor
    └── NotFoundView.razor
```

- `README.md`: README document of the theme
- `src/theme.json`: Theme metadata
- `src/favicon.ico`: Favicon
- `src/assets/css/*.css`: CSS files used in the theme
- `src/assets/js/*.js`: JavaScript files used in the theme
- `src/assets/images/*`: Image files used in the theme
- `src/_Imports.razor`: Defines global using directives
- `src/MainLayout.razor`: Defines the main layout
- `src/IndexView.razor`: Defines the landing page view layout
- `src/PostView.razor`: Defines blog post view layout
- `src/PageView.razor`: Defines page view layout
- `src/NotFoundView.razor`: Defines 404 (not found) page view layout

## `theme.json`

`theme.json` declares the metadata of the theme used by ScissorHands.NET app.

```jsonc
{
  "name": "Theme Template",
  "version": "1.0.0",
  "description": "A theme template for ScissorHands.NET",
  "slug": "theme-template",
  "stylesheets": [
    "/assets/css/theme.css"
  ],
  "scripts": [
    "/assets/js/theme.js"
  ]
}
```

- `name`: Name of the theme.
- `version`: Version of the theme.
- `description`: Theme description.
- `slug`: Slug of the theme. This MUST be equal to the `Theme` value of the [site configuration](/docs/configuration#site-configuration).
- `stylesheets`: The list of CSS files used in the theme.
- `scripts`: The list of JavaScript files used in the theme.

## `_Imports.razor`

`_Imports.razor` declares the global using directives and the namespace of the theme.

## `MainLayout.razor`

`MainLayout.razor` defines the overall layout of the theme. It calls the other view files like `IndexView.razor`, `PostView.razor` and `PageView.razor` as well as other UI components defined in the theme. It MUST declare inheritance of `ScissorHands.Theme.MainLayoutBase` by adding `@inherits ScissorHands.Theme.MainLayoutBase`.

### Properties of `MainLayout.razor`

Since `MainLayout.razor` inherits `ScissorHands.Theme.MainLayoutBase`, it exposes the following properties for theme developers to use:

- `PageTitle`: Calculated page title by [`CalculatePageTitle()`](/docs/themes#calculatepagetitle)
- `PageDescription`: Calculated page description by [`CalculatePageDescription()`](/docs/themes#calculatepagedescription)
- `PageLocale`: Calculated page locale by [`CalculatePageLocale()`](/docs/themes#calculatepagelocale)
- `Documents`: **Parameter**. List of content documents &ndash; used by `IndexView.razor`
- `Document`: **Parameter**. Content document &ndash; used by `PostView.razor` and `PageView.razor`
- `Plugins`: **Parameter**. List of plugins defined in the [Plugins section of `appsettings.json`](/docs/plugins#plugin-configuration)
- `Theme`: **Parameter**. Theme configuration defined in [`theme.json`](/docs/themes#theme.json)
- `Site`: **Parameter**. Site configuration defined in the [Site section of `appsettings.json`](/docs/configuration#site-configuration)

These properties are passed to `IndexView.razor`, `PostView.razor`, `PageView.razor` and UI components as cascading parameters.

### Methods for Overriding

Both `PageTitle` and `PageDescription` property values are calculated from the methods, `CalculatePageTitle()` and `CalculatePageDescription()` respectively. You can override these two methods to change the property values.

#### `CalculatePageTitle()`

```csharp
protected virtual string CalculatePageTitle()
{
    var title = Site?.Title;
    if (Document is not null && string.IsNullOrWhiteSpace(Document.Metadata.Title) == false)
    {
        title = $"{Document.Metadata.Title} | {title}";
    }

    return title ?? string.Empty;
}
```

#### `CalculatePageDescription()`

```csharp
protected virtual string CalculatePageDescription()
{
    var description = Site?.Description ?? string.Empty;

    if (Document is not null && string.IsNullOrWhiteSpace(Document.Metadata.Description) == false)
    {
        description = Document.Metadata.Description;
    }

    return description ?? string.Empty;
}
```

#### `CalculatePageLocale()`

```csharp
protected virtual string CalculatePageLocale()
{
    var locale = Site?.Locale ?? string.Empty;

    if (Document is not null && string.IsNullOrWhiteSpace(Document.Metadata.Locale) == false)
    {
        locale = Document.Metadata.Locale;
    }

    return locale.ToLowerInvariant() ?? string.Empty;
}
```

## `IndexView.razor`

`IndexView.razor` describes the landing page view. It also calls other UI components defined in the theme. It MUST declare inheritance of `ScissorHands.Theme.IndexViewBase` by adding `@inherits ScissorHands.Theme.IndexViewBase`.

### Properties of `IndexView.razor`

Since `IndexView.razor` inherits `ScissorHands.Theme.IndexViewBase`, it exposes the following properties for theme developers to use:

- `Documents`: **Cascading Parameter**. List of content documents &ndash; used by `IndexView.razor`
- `Plugins`: **Cascading Parameter**. List of plugins defined in the [Plugins section of `appsettings.json`](/docs/plugins#plugins-configuration)
- `Theme`: **Cascading Parameter**. Theme configuration defined in [`theme.json`](#themejson)
- `Site`: **Cascading Parameter**. Site configuration defined in the [Site section of `appsettings.json`](/docs/configuration#site-configuration)

These properties are passed from `MainLayout.razor` as cascading parameters.

## `PostView.razor`

`PostView.razor` describes the blog post view. It also calls other UI components defined in the theme. It MUST declare inheritance of `ScissorHands.Theme.PostViewBase` by adding `@inherits ScissorHands.Theme.PostViewBase`.

### Properties of `PostView.razor`

Since `PostView.razor` inherits `ScissorHands.Theme.PostViewBase`, it exposes the following properties for theme developers to use:

- `Document`: **Cascading Parameter**. Content document &ndash; used by `PostView.razor`
- `Plugins`: **Cascading Parameter**. List of plugins defined in the [Plugins section of `appsettings.json`](/docs/plugins#plugins-configuration)
- `Theme`: **Cascading Parameter**. Theme configuration defined in [`theme.json`](#themejson)
- `Site`: **Cascading Parameter**. Site configuration defined in the [Site section of `appsettings.json`](/docs/configuration#site-configuration)

These properties are passed from `MainLayout.razor` as cascading parameters.

## `PageView.razor`

`PageView.razor` describes the page view. It also calls other UI components defined in the theme. It MUST declare inheritance of `ScissorHands.Theme.PageViewBase` by adding `@inherits ScissorHands.Theme.PageViewBase`.

### Properties of `PageView.razor`

Since `PageView.razor` inherits `ScissorHands.Theme.PageViewBase`, it exposes the following properties for theme developers to use:

- `Document`: **Cascading Parameter**. Content document &ndash; used by `PageView.razor`
- `Plugins`: **Cascading Parameter**. List of plugins defined in the [Plugins section of `appsettings.json`](/docs/plugins#plugins-configuration)
- `Theme`: **Cascading Parameter**. Theme configuration defined in [`theme.json`](#themejson)
- `Site`: **Cascading Parameter**. Site configuration defined in the [Site section of `appsettings.json`](/docs/configuration#site-configuration)

These properties are passed from `MainLayout.razor` as cascading parameters.

## `NotFoundView.razor`

`NotFoundView.razor` describes the 404 page view. It also calls other UI components defined in the theme. It MUST declare inheritance of `ScissorHands.Theme.NotFoundViewBase` by adding `@inherits ScissorHands.Theme.NotFoundViewBase`.

### Properties of `NotFoundView.razor`

Since `NotFoundView.razor` inherits `ScissorHands.Theme.NotFoundViewBase`, it exposes the following properties for theme developers to use:

- `Document`: **Cascading Parameter**. Content document &ndash; used by `NotFoundView.razor`
- `Plugins`: **Cascading Parameter**. List of plugins defined in the [Plugins section of `appsettings.json`](/docs/plugins#plugins-configuration)
- `Theme`: **Cascading Parameter**. Theme configuration defined in [`theme.json`](#themejson)
- `Site`: **Cascading Parameter**. Site configuration defined in the [Site section of `appsettings.json`](/docs/configuration#site-configuration)

These properties are passed from `MainLayout.razor` as cascading parameters.

## Additional UI Components

In addition to the mandatory page layout components &ndash; `MainLayout`, `IndexView`, `PostView`, `PageView` and `NotFoundView`, you can add as many UI component as you want. Here's a very simple component you can write up:

```razor
@* Component: `AdditionalComponent.razor` *@
@namespace MyAwesomeTheme.Components
<div class="@CssClass">
  <p>This is an additional component.</p>
</div>

@code {
    [Parameter]
    public string? CssClass { get; set; }

    [CascadingParameter]
    public IEnumerable<ContentDocument>? Documents { get; set; }

    [CascadingParameter]
    public ContentDocument? Document { get; set; }

    [CascadingParameter]
    public IEnumerable<PluginManifest>? Plugins { get; set; }

    [CascadingParameter]
    public ThemeManifest? Theme { get; set; }

    [CascadingParameter]
    public SiteManifest? Site { get; set; }
}
```

Then, place this component wherever you like. Make sure that `Documents`, `Document`, `Plugins`, `Theme` and `Site` properties are cascading parameters. Therefore, you only need to pass `CssClass` value in this example. Here's an example of using this component in `IndexView.razor`:

```razor
@* View: `IndexView.razor` *@
@inherits ScissorHands.Theme.IndexViewBase
@layout MainLayout

<section class="home">
    <AdditionalComponent CssClass="additional-component" />
    ...
</section>

```

## List of Themes

Here are the list of themes you can currently use &ndash; either official or community contributed.

### Official Themes

- [Theme Template](https://github.com/getscissorhands/theme-template)
- [Minimal Blog](https://github.com/getscissorhands/minimal-blog)

### Community Themes

TBD

---

👈 [Front Matter](/docs/front-matter) | 👆 [Documentation](/docs) | [Plugins](/docs/plugins) 👉
