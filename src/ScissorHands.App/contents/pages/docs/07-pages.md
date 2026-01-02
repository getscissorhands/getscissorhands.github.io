---
title: Pages
slug: docs/pages
description: |
  How to write pages
---

Use [markdown](https://daringfireball.net/projects/markdown/) to write pages.

> **NOTE**: If you learn more about markdown, follow this [markdown basics](https://www.markdownguide.org/basic-syntax/).

## Directory structure

- All pages MUST be located under the `contents/pages` directory. Any markdown files outside this directory are not considered as pages.
- As long as all the pages are located under the `contents/pages` directory, they're published. But the following structure setup is recommended:

    ```text
    contents/
    └── pages/
        ├── section-1/
        │   ├── page-1.md
        │   └── page-2.md
        └── section-2/
            ├── page-3.md
            └── page-4.md
    ```

  By structuring like above, you can easily find out what you've published in a alphabetical order.
  
  > **NOTE**: The directory structure doesn't affect the page URL's segment structure.

## Page structure

Each page consists of two sections &ndash; [front matter](/docs/front-matter) and content.

```md
---
title: Placeholder
slug: placeholder
description: Lorem ipsum dolor sit amet, consectetur adipiscing elit.
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

It contains all the metadata of the specific page including title, description and slug. It's located in the beginning of the markdown document and surrounded by the `---` separator. For more details, refer to the [front matter](/docs/front-matter) page.

### Content

This is the main page content. Write anything you want. It's strongly recommended to avoid using the `H1` tag element in the content section. It's because the title from the front matter section will use the `H1` tag element, when it's converted to HTML.

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

## 404 page

The `404.html` is a special page shown when a requested URL doesn't exist. When a page markdown document declares its slug of `404.html`, the page content will be rendered in the `404.html` page.

---

👈 [Posts](/docs/posts) | 👆 [Documentation](/docs) | [Front Matter](/docs/front-matter) 👉
