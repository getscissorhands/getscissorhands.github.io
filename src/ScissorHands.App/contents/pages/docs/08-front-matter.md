---
title: Front Matter
slug: docs/front-matter
description: |
  Understand the front matter in ScissorHands.NET
---

Front matter includes all the metadata of each blog post or page. It's written in a YAML format and surrounded by the `---` separator in each markdown document.

## Structure

Here are properties of front matter used in ScissorHands.NET.

```yml
title: My Awesome Post
description: Did you know my awesome blog post?
slug: my-awesome-post
author: Scissor Hands
twitter_handle: @scissor_hands
hero_image: /images/hello-world.png
published: 2025-12-15
tags:
  - tag-1
  - tag-2
  - tag-3
```

- `title`: The title of the blog post or page.
- `description`: The description of the blog post or page.
- `slug`: The slug of the blog post or page, which will be part of the page URL. You can use any format like `PascalCased`, `camelCased`, `snake_cased` or `kebab-cased`, but `kebab-cased` is recommended to avoid any confusion.
- `author`: The author of the blog post. The default site author will be used if it's omitted.
- `twitter_handle`: The Twitter handle of the author. It won't be appearing if it's omitted.
- `hero_image`: The hero image of the blog post or page. The default hero image will be used if it's omitted.
- `published`: The date of published in the [ISO 8601 format](https://www.iso.org/iso-8601-date-and-time-format.html), `yyyy-mm-dd`.
- `tags`: The list of tags of the blog post. Like `slug`, it's recommended to use the `kebab-cased` format.

## Limitations

There's no custom front matter properties supported yet.

---

👈 [Pages](/docs/pages) | 👆 [Documentation](/docs) | [Themes](/docs/themes) 👉
