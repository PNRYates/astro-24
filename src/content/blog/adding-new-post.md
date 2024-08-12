---
title: Adding new posts in AstroPaper theme
author: Sat Naing
description: Description
featured: false
draft: false
pubDatetime: 2022-09-23
modDatetime: 2023-12-22T12:00:00Z
---
Here are some rules/recommendations, tips & ticks for creating new posts in AstroPaper blog theme.

## Table of contents

## Image Example

![image-peter](@assets/images/og-peter.jpg)Frontmatter

image should be below

![](/src/assets/images/AstroPaper-v4.png)![](@assets/images/AstroPaper-v4.png)

Frontmatter is the main place to store some important information about the blog post (article). Frontmatter lies at the top of the article and is written in YAML format. Read more about frontmatter and its usage in [astro documentation](https://docs.astro.build/en/guides/markdown-content/).

Here is the list of frontmatter property for each post.

<table style="minWidth: 75px"><colgroup><col><col><col></colgroup><tbody><tr><th colspan="1" rowspan="1"><p>Property</p></th><th colspan="1" rowspan="1"><p>Description</p></th><th colspan="1" rowspan="1"><p>Remark</p></th></tr><tr><td colspan="1" rowspan="1"><p><strong><em>title</em></strong></p></td><td colspan="1" rowspan="1"><p>Title of the post. (h1)</p></td><td colspan="1" rowspan="1"><p>required*</p></td></tr><tr><td colspan="1" rowspan="1"><p><strong><em>description</em></strong></p></td><td colspan="1" rowspan="1"><p>Description of the post. Used in post excerpt and site description of the post.</p></td><td colspan="1" rowspan="1"><p>required*</p></td></tr><tr><td colspan="1" rowspan="1"><p><strong><em>pubDatetime</em></strong></p></td><td colspan="1" rowspan="1"><p>Published datetime in ISO 8601 format.</p></td><td colspan="1" rowspan="1"><p>required*</p></td></tr><tr><td colspan="1" rowspan="1"><p><strong><em>modDatetime</em></strong></p></td><td colspan="1" rowspan="1"><p>Modified datetime in ISO 8601 format. (only add this property when a blog post is modified)</p></td><td colspan="1" rowspan="1"><p>optional</p></td></tr><tr><td colspan="1" rowspan="1"><p><strong><em>author</em></strong></p></td><td colspan="1" rowspan="1"><p>Author of the post.</p></td><td colspan="1" rowspan="1"><p>default = SITE.author</p></td></tr><tr><td colspan="1" rowspan="1"><p><strong><em>slug</em></strong></p></td><td colspan="1" rowspan="1"><p>Slug for the post. This field is optional but cannot be an empty string. (slug: ""❌)</p></td><td colspan="1" rowspan="1"><p>default = slugified file name</p></td></tr><tr><td colspan="1" rowspan="1"><p><strong><em>featured</em></strong></p></td><td colspan="1" rowspan="1"><p>Whether or not display this post in featured section of home page</p></td><td colspan="1" rowspan="1"><p>default = false</p></td></tr><tr><td colspan="1" rowspan="1"><p><strong><em>draft</em></strong></p></td><td colspan="1" rowspan="1"><p>Mark this post 'unpublished'.</p></td><td colspan="1" rowspan="1"><p>default = false</p></td></tr><tr><td colspan="1" rowspan="1"><p><strong><em>tags</em></strong></p></td><td colspan="1" rowspan="1"><p>Related keywords for this post. Written in array yaml format.</p></td><td colspan="1" rowspan="1"><p>default = others</p></td></tr><tr><td colspan="1" rowspan="1"><p><strong><em>ogImage</em></strong></p></td><td colspan="1" rowspan="1"><p>OG image of the post. Useful for social media sharing and SEO.</p></td><td colspan="1" rowspan="1"><p>default = SITE.ogImage or generated OG image</p></td></tr><tr><td colspan="1" rowspan="1"><p><strong><em>canonicalURL</em></strong></p></td><td colspan="1" rowspan="1"><p>Canonical URL (absolute), in case the article already exists on other source.</p></td><td colspan="1" rowspan="1"><p>default = <code>Astro.site</code> + <code>Astro.url.pathname</code></p></td></tr></tbody></table>

> Tip! You can get ISO 8601 datetime by running `new Date().toISOString()` in the console. Make sure you remove quotes though.

Only `title`, `description` and `pubDatetime` fields in frontmatter must be specified.

Title and description (excerpt) are important for search engine optimization (SEO) and thus AstroPaper encourages to include these in blog posts.

`slug` is the unique identifier of the url. Thus, `slug` must be unique and different from other posts. The whitespace of `slug` should to be separated with `-` or `_` but `-` is recommended. Slug is automatically generated using the blog post file name. However, you can define your `slug` as a frontmatter in your blog post.

For example, if the blog file name is `adding-new-post.md` and you don't specify the slug in your frontmatter, Astro will automatically create a slug for the blog post using the file name. Thus, the slug will be `adding-new-post`. But if you specify the `slug` in the frontmatter, this will override the default slug. You can read more about this in [Astro Docs](https://docs.astro.build/en/guides/content-collections/#defining-custom-slugs).

If you omit `tags` in a blog post (in other words, if no tag is specified), the default tag `others` will be used as a tag for that post. You can set the default tag in the `/src/content/config.ts` file.

```ts
// src/content/config.ts
export const blogSchema = z.object({
  // ---
  draft: z.boolean().optional(),
  tags: z.array(z.string()).default(["others"]), // replace "others" with whatever you want
  // ---
});
```

### Sample Frontmatter

Here is the sample frontmatter for a post.

```yaml
# src/content/blog/sample-post.md
---
title: The title of the post
author: your name
pubDatetime: 2022-09-21T05:17:19Z
slug: the-title-of-the-post
featured: true
draft: false
tags:
  - some
  - example
  - tags
ogImage: ""
description: This is the example description of the example post.
canonicalURL: https://example.org/my-article-was-already-posted-here
---
```

## Adding table of contents

By default, a post (article) does not include any table of contents (toc). To include toc, you have to specify it in a specific way.

Write `Table of contents` in h2 format (## in markdown) and place it where you want it to be appeared on the post.

For instance, if you want to place your table of contents just under the intro paragraph (like I usually do), you can do that in the following way.

```md
---
# some frontmatter
---

Here are some recommendations, tips & ticks for creating new posts in AstroPaper blog theme.

## Table of contents

<!-- the rest of the post -->
```

## Headings

There's one thing to note about headings. The AstroPaper blog posts use title (title in the frontmatter) as the main heading of the post. Therefore, the rest of the heading in the post should be using h2 ~ h6.

This rule is not mandatory, but highly recommended for visual, accessibility and SEO purposes.

## Storing Images for Blog Content

Here are two methods for storing images and displaying them inside a markdown file.

> Note! If it's a requirement to style optimized images in markdown you should [use MDX](https://docs.astro.build/en/guides/images/#images-in-mdx-files).

### Inside `src/assets/` directory (recommended)

You can store images inside `src/assets/` directory. These images will be automatically optimized by Astro through [Image Service API](https://docs.astro.build/en/reference/image-service-reference/).

You can use relative path or alias path (`@assets/`) to serve these images.

Example: Suppose you want to display `example.jpg` whose path is `/src/assets/images/example.jpg`.

```md
![something](@assets/images/example.jpg)

<!-- OR -->

![something](../../assets/images/example.jpg)

<!-- Using img tag or Image component won't work ❌ -->
<img src="@assets/images/example.jpg" alt="something">
<!-- ^^ This is wrong -->
```

> Technically, you can store images inside any directory under `src`. In here, `src/assets` is just a recommendation.

### Inside `public` directory

You can store images inside the `public` directory. Keep in mind that images stored in the `public` directory remain untouched by Astro, meaning they will be unoptimized and you need to handle image optimization by yourself.

For these images, you should use an absolute path; and these images can be displayed using [markdown annotation](https://www.markdownguide.org/basic-syntax/#images-1) or [HTML img tag](https://developer.mozilla.org/en-US/docs/Web/HTML/Element/img).

Example: Assume `example.jpg` is located at `/public/assets/images/example.jpg`.

```md
![something](/assets/images/example.jpg)

<!-- OR -->

<img src="/assets/images/example.jpg" alt="something">
```

## Bonus

### Image compression

When you put images in the blog post (especially for images under `public` directory), it is recommended that the image is compressed. This will affect the overall performance of the website.

My recommendation for image compression sites.

*   [TinyPng](https://tinypng.com/)
    
*   [TinyJPG](https://tinyjpg.com/)
    

### OG Image

The default OG image will be placed if a post does not specify the OG image. Though not required, OG image related to the post should be specify in the frontmatter. The recommended size for OG image is **_1200 X 640_** px.

> Since AstroPaper v1.4.0, OG images will be generated automatically if not specified. Check out [the announcement](https://astro-paper.pages.dev/posts/dynamic-og-image-generation-in-astropaper-blog-posts/).
