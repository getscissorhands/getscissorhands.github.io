---
title: Configuration
slug: docs/configuration
description: |
  How to configure your ScissorHands.NET website.
---

You can customise ScissorHands.NET app by configuration. There are three places for configuration.

## Site Configuration

Open `appsettings.json` file and configure the `Site` section. Here's the default site configurations.

```jsonc
{
  "Site": {
    "Title": "ScissorHands.NET",
    "Description": "A Blazor-based static site generator",
    "Locale": "en-US",
    "Author": "The ScissorHands",
    "Theme": "default",
    "BaseUrl": "/",
    "HeroImage": "https://raw.githubusercontent.com/getscissorhands/Scissorhands.NET/refs/heads/vnext/assets/hero.jpg",
    "IncludeDateInPostUrl": false,
    "Debug": false
  }
}
```

- `Title`: Title of the website.
- `Description`: Description of the website.
- `Locale`: Default locale of the website. It can be either combination of language code ([ISO 639](https://www.iso.org/iso-639-language-code)) and country code ([ISO 3166](https://www.iso.org/iso-3166-country-codes.html)), or language code only.
- `Author`: Default author of the website contents.
- `Theme`: The theme directory.
- `BaseUrl`: The base URL of this app. It's particularly useful for GitHub Pages scenario.
- `HeroImage`: Default hero image consumed by Open Graph meta tags.
- `IncludeDateInPostUrl`: Value indicating whether to include the date in the post URL segment like `/yyyy/mm/dd/my-awesome-blog-post`.
- `Debug`: Value indicating whether to show debug message in the console while previewing.

## Plugin Configuration

Refer to the [Plugins](/docs/plugins) page.

## Theme Configuration

Refer to the [Themes](/docs/themes) page.

---

👈 [Publish to Azure Blob Storage](/docs/publish/azure-blob-storage) | 👆 [Documentation](/docs) | [Posts](/docs/posts) 👉
