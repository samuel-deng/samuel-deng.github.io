# Personal website

This website uses **Jekyll**, which combines page content, a shared HTML layout, and styling to generate the website.

## Page content

Each page has its own Markdown file in the project root:

| Page | Source file | URL | Contents |
| --- | --- | --- | --- |
| Me | [index.markdown](index.markdown) | `/` | Bio, Service, and Miscellaneous |
| Teaching | [teaching.markdown](teaching.markdown) | `/teaching/` | Teaching philosophy, courses, and experience |
| Research | [research.markdown](research.markdown) | `/research/` | Research overview and publications |

Previously, all the content lived in `index.markdown`. It has been split across these files while preserving the wording.

Each page begins with a settings block called **front matter**:

```yaml
---
layout: default
title: Teaching
permalink: /teaching/
---
```

- `layout` selects the shared layout.
- `title` sets the page title.
- `permalink` sets the page URL.

Everything below the front matter is page content written in Markdown. For example, `**bold text**` makes text bold, and `[link text](URL)` creates a link.

## Shared header and navigation

[_layouts/default.html](_layouts/default.html) contains the name, email, affiliation, photo, and navigation links shared by all three pages. Editing this file updates every page.

The layout inserts each page's rendered Markdown at this placeholder:

```liquid
{{ content }}
```

The navigation checks the current page's URL and adds `aria-current="page"` to the corresponding link. The stylesheet uses this attribute to highlight the active tab, and assistive technology can use it to identify the current page.

## Styling

[assets/css/style.scss](assets/css/style.scss) controls the centered column, fonts, spacing, photo size, colors, and adjustments for small screens.

The tab colors are defined by these rules:

```css
.page-nav a {
  color: #ddb56f; /* Pastel orange: inactive tabs */
}

.page-nav a:hover,
.page-nav a[aria-current="page"] {
  color: #d99a11; /* Original orange: active or hovered tab */
}
```

A separate rule underlines the active tab. Ordinary links have their own `a` and `a:hover` rules, so their colors can be adjusted independently of the tabs.

The `@media (max-width: 520px)` block adjusts spacing, text, and the photo for smaller screens.

## How the source becomes the website

Jekyll converts Markdown into HTML, inserts it into the shared layout, and compiles the stylesheet. It writes the browser-ready files into `_site`.

**Edit the source files, not `_site`.** Generated files are overwritten on the next build.

With the local Jekyll server running, save a source file, let Jekyll rebuild, and refresh the browser at [http://127.0.0.1:4000/](http://127.0.0.1:4000/). Changes to `_config.yml` require restarting the server.

## Where to make future updates

| Change | File |
| --- | --- |
| Bio or personal information | [index.markdown](index.markdown) |
| Teaching content | [teaching.markdown](teaching.markdown) |
| Research overview or publications | [research.markdown](research.markdown) |
| Name, shared affiliation, email, or navigation | [_layouts/default.html](_layouts/default.html) |
| Profile photo | [assets/img/face.jpg](assets/img/face.jpg) |
| Colors, typography, or layout | [assets/css/style.scss](assets/css/style.scss) |
| Site-wide title, email, description, or Jekyll settings | [_config.yml](_config.yml) |

For the NYU role update, edit the bio in `index.markdown`, the shared affiliation and email in `_layouts/default.html`, and the site metadata in `_config.yml`. The header currently contains its own email and affiliation text, so changing metadata alone does not update the visible header.

Editing or previewing files locally does not publish the website. Publishing requires a separate deployment step.
