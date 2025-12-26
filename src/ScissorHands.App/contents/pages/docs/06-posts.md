---
title: Posts
slug: docs/posts
description: |
  How to write blog posts
---

Use [markdown](https://daringfireball.net/projects/markdown/) to write blog posts.

> **NOTE**: If you learn more about markdown, follow this [markdown basics](https://www.markdownguide.org/basic-syntax/).

## Directory structure

- All blog posts MUST be located under the `contents/posts` directory. Any markdown files outside this directory are not considered as blog posts.
- As long as all the blog posts are located under the `contents/posts` directory, they're published. But the following structure setup is recommended:

    ```text
    contents/
    └── posts/
        └── year/
            ├── month-1/
            │   ├── yyyy-mm-dd-post-1.md
            │   └── yyyy-mm-dd-post-2.md
            └── month-2/
                ├── yyyy-mm-dd-post-3.md
                └── yyyy-mm-dd-post-4.md
    ```

  By structuring like above, you can easily find out what you've published in a chronological order.
  
  > **NOTE**: The directory structure doesn't affect the post URL's segment structure.

## Post structure

Each blog post consists of two sections &ndash; [front matter](/docs/front-matter) and content.

```md
---
title: Placeholder
slug: placeholder
description: Lorem ipsum dolor sit amet, consectetur adipiscing elit.
author: The ScissorHands
hero_image: /images/hello-world.png
published: 2025-12-15
tags:
  - blazor
  - static-site
  - preview
---

## Lorem ipsum dolor sit amet

Lorem ipsum dolor sit amet, consectetur adipiscing elit. 
Proin consequat porttitor ullamcorper. Nullam sed fringilla ex, 
non condimentum nibh. Vestibulum sit amet urna sed sem viverra 
dignissim vel quis purus. Pellentesque nec urna nec dolor feugiat 
ullamcorper. Cras luctus vel neque eget commodo. Nulla aliquam felis nulla, 
vitae rutrum lacus bibendum in. Nulla id est dui. Quisque tempus erat tortor, 
non tempor turpis scelerisque sed. Nam id posuere felis. Cras fermentum 
tristique dui, a lobortis odio ornare vitae.
```

### Front Matter

It contains all the metadata of the specific blog post including title, slug, date published and tags. It's located in the beginning of the markdown document and surrounded by the `---` separator. For more details, refer to the [front matter](/docs/front-matter) page.

### Content

This is the main blog post content. Write anything you want. It's strongly recommended to avoid using the `H1` tag element in the content section. It's because the title from the front matter section will use the `H1` tag element, when it's converted to HTML.

### Media

All the media files should be stored under the `content` directory. Here are the recommended directory structure:

```text
contents/
├── images/
│   ├── image-1.jpg
│   ├── image-2.png
│   └── image-3.gif
├── videos/
│   └── video-1.mp4
└── audios/
    └── audio-1.mp3
```

Each directory will be published to `/images`, `/videos`, `/audios` respectively.

---

👈 [Configuration](/docs/configuration) | 👆 [Documentation](/docs) | [Pages](/docs/pages) 👉
