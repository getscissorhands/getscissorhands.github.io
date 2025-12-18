---
title: Build
slug: docs/build
description: |
  How to build an artifact for publish
---

You've got a website up and running with ScissorHands.NET. Now, you need to build an artifact to publish your website.

## Building Artifact

When you're happy to publish your website, it's time for building an artifact. The artifact consists of HTML pages, CSS files, JavaScript files, images and other files related to the contents.

1. Let's assume that your ScissorHands.NET app project is `MyScissorHandsApp`. To build the artifact, run the following command. Make sure to add the `--build` option.

    ```bash
    dotnet run --project ./MyScissorHandsApp -- --build
    ```

   You'll be able to find your artifact under the `dist` directory.

Congratulations! You've just built the artifact for publish!

---

👈 [Quickstart](/docs/quickstart) | 👆 [Documentation](/docs) | [Publish](/docs/publish) 👉
