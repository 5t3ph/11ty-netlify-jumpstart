---
title: "About"
description: "Review feature info and customization details."
---

## Intro to Jumpstart

This jumpstart is intended to be _just enough_ to be a functional site/blog using 11ty, and also to introduce essential 11ty features.

[**Review the "Quick Start"**](/#quickstart) on the home page for how to get this starter up and running for your project.

### Colophon

Hi, I'm Stephanie Eckles - @5t3ph on [Twitter](https://twitter.com/5t3ph), [Github](https://github.com/5t3ph), [CodePen](https://codepen.com/5t3ph), and [DEV](https://dev.to/5t3ph). You may know me as the author of [ModernCSS.dev](https://moderncss.dev) or the creator of [StyleStage.dev](https://stylestage.dev). I can also be found on [egghead as an instructor](https://egghead.io/instructors/stephanie-eckles?af=2s65ms).

> Check out my extended collection of Eleventy resources available on [11ty.Rocks](https://11ty.rocks)!

I spent a decade creating WordPress themes and plugins then flipped to product development + leading development of a multi-platform enterprise design system. My intro to Jamstack was with Gatsby, but 11ty fills a special place that is so needed for truly static sites. I'm in love, and I think you will be, too.

### Jump to:

- [Global Site Data and .env](#global-site-data-and-env)
- [Template Languages Used](#template-languages-used)
- [Layout Hierarchy and Features](#layout-hierarchy-and-features)
- [Expected Frontmatter](#expected-frontmatter)
- [Permalink Style](#permalink-style)
- [Asset Handling](#asset-handling)
- [Linting](#linting)
- [Sass Framework](#sass-framework)
- [Anchor links](#anchor-links)
- [Sitemap](#sitemap)
- [RSS Feed](#rss-feed)
- [Social Share Preview Images](#social-share-preview-images)
- [Prism Syntax Highlighting](#prism-syntax-highlighting)
- [.eleventy.js Config Features](#eleventyjs-config-features)
- [VSCode Tips](#vscode-tips)

## Global Site Data and .env

As noted in the [Quick Start](/#quickstart), there are global site data variables in `src/_data/meta.json`.

Those include:

- `url` - should remain unchanged, reads from the single expected `.env` value of `URL`
- `siteName` - your "brand" if you will, appended to the `<title>` tag, shown in the `sitenav`, displayed in the "hero" for the `home` layout, in the footer by the copyright, as the "credit" for social share images, and as the identifier throughout the RSS feed
- `siteDescription` - used in the "description" meta tag, and below the `siteName` on the `home` layout
- `authorName` - Used in the RSS feed, intended to be your full name
- `twitterUsername` - without the "@", this value is used for the Twitter meta tags, and for the URL of the icon link in the footer

### .env

See `.env-sample` for the single expected value of `URL` which should be set to your localhost. The sample uses the default 11ty port, so you can simply rename the file to `.env` if you haven't changed the port.

The `URL` value is then available via the global data described previously, and can be used in templates with `meta.url`. You can see this used for the RSS feed and sitemap as well as meta tag links to the social share preview images to create the absolute URLs.

## Template Languages Used

Page templates are created as Nunjucks (`.njk`), and feature are added that expect Markdown for most page content.

The home page - `src/index.njk` - is set to process first as Markdown followed by Nunjucks. This allows mixing HTML with Markdown, with benefits being code syntax highlighting and ability to include classes on HTML elements. This functionality is provided by the `templateEngineOverride: md, njk` in the frontmatter.

A unique case uses Nunjucks to create the `json` that is used to generate the [social share preview images](#social-share-preview-images).

Review the list of [available templating languages](https://www.11ty.dev/docs/languages/) in the 11ty docs.

## Layout Hierarchy and Features

There are two layouts and one partial included.

**New in v1.1.0** - layouts are customized to be located in `src/_layouts`.

- `_layouts/base.njk` includes the standard HTML boilerplate including meta and "og" tags in `<head>`.

- `_layouts/page.njk` includes the `sitenav.njk` partial and chains up to `base`

The `src/index.njk` template chains to the `base` layout and includes a loop that will create "cards" for everything in `collections.pages`.

## Expected Frontmatter

There are only two fields expected:

- `title` - essentially required, by default is used in the page `<title>`, in the layout "hero", in social share preview images, and in social share meta tags.
- `description` - optional, by default appears below the title for the `page` template and is used as for the "description" meta tag and social share meta tag descriptions.

## Permalink Style

The default setup expects content - using any template language - within `pages/`.

The `pages.json` in that directory includes a `permalink` setting so that the file name is used directly to prevent 'pages' being the base of the URL.

You can [override permalinks per file](https://www.11ty.dev/docs/permalinks/).

## Asset Handling

In the `.eleventy.js` config, there are included "pass-throughs" for an `img/` directory as well as `favicon.png`.

You can replace the included favicon, and create an `img` directory or remove the `addPassthroughCopy` if you do not have need of images.

Creating an `img` directory and keeping the pass-through directive will make images available at `/img/[image-file-path]` relative to the site root.

## Linting

For Sass, [stylelint](https://stylelint.io/) is included. If you want to keep it, you may want to do a find/replace for `tdbc` to the prefix of your choice. If not, you'll want to remove the related files at the project root as well as the related items in the `package.json`.

A `prettier` config is included, with the only update being `printWidth: 100`.

## Sass Framework

Review the [styling documentation](https://5t3ph.github.io/html-sass-jumpstart/) for the included minimal Sass framework, particularly the theme variables, to quickly customize the starter.

The only notable differences are:

1. `sitenav` - adjust the styles for the navigation header that appears on pages
1. `tdbc-anchor` - styles for the `#` anchor that appears next to page headings ([or turn that feature off](#anchor-links)) can be adjusted in `sass/_utilities`
1. Additional `article`-scoped styling for typography as it appears on `pages`
1. A theme for the [`prism` syntax highlighting](#prism-syntax-highlighting) for code blocks. You can adjust or replace the theme in `sass/_prism`.

### Fonts

The default font is [Baloo 2](https://fonts.google.com/specimen/Baloo+2) and is locally hosted with files in `fonts/`. If you swap to a different font, be sure to remove the font files as well as the `@font-face` rules at the top of `sass/_fonts.scss`, and update the `$tdbc-font-family` Sass variable.

## Anchor Links

Anchor links next to headings throughout Markdown content are generated by an add-on plugin for `markdownIt`.

This feature can be adjusted or removed in the `.eleventy.js` config file.

## Generated Features

### Sitemap

A `sitemap.xml` is generated from all available content.

To exclude non-page or non-public content from the sitemap, include `eleventyExcludeFromCollections: true` in frontmatter, or [create a custom filter](https://www.11ty.dev/docs/collections/#advanced-custom-filtering-and-sorting).

### RSS Feed

An RSS feed is included, and output at `[siteurl]/feed/feed.xml`.

If publishing from Netlify, the included `netlify.toml` file will create a redirect so that the feed becomes available at `[siteurl]/feed`.

### Social Share Preview Images

Upon use of the build command, social share preview images are generated for each page + the home page, and available in `public/previews/[title-as-slug].png`.

Here's an example of the default template:

![default social share preview image template](/previews/hello-world.png)

As of v0.5.0, these images now use my Eleventy plugin - `@11tyrocks/eleventy-plugin-social-images` - with the default blue theme and a customized template.

Any changes made can be previewed by running the build command and reviewing the contents of `public/previews/`.

[Review the plugin docs](https://www.npmjs.com/package/@11tyrocks/eleventy-plugin-social-images) for the full details of how to customize the behavior, and read on to learn how this starter is currently setup for the social images.

#### Update social image template HTML

HTML can be changed in `_generate/socialtemplate.njk` - be sure to leave the `<style>` block and the template tag within so that the plugin can insert your styles.

The only requirement for the generator to work is to keep an `<h1>` to populate with the content title, but the rest of the template is up to you!

#### Update social image template style

There are two options:

1. Select a different theme to use from the plugin's [predefined theme options](https://github.com/5t3ph/eleventy-plugin-social-images/tree/main/themes) and amend the `social-images` script to set the `--theme` option
2. Create a custom stylesheet (such as social.scss) and add the included `build:sass-social` script at the end of the `build:sass` command

If choosing to create your own styles for option #2, the CSS will be output in `social/style.css` with provided stubbed out script. You will need to add this as the value for the `--stylesPath` option within the `social-images` script to ensure your custom styles are used.

#### Change included pages OR available data

Adjust the collections loop in `_generate/pagesjson.njk`, but keep the defined keys of `title` and `imgName`.

## Prism Syntax Highlighting

Syntax highlighting of inline or code blocks found within Markdown content is provided by Prism via `@11ty/eleventy-plugin-syntaxhighlight`.

You can change the theme used in `sass/_prism.scss`.

Or, remove the plugin if you are not in need of code highlighting.

## .eleventy.js Config Features

### Overrides

- **Input directory**: `src`
- **Output directory**: `public`
- **Layout directory**: `_layouts`

Also, `markdownLibrary` is extended to add the `markdownItAnchor` plugin for [anchor links](#anchor-links).

### Shortcode: `year`

Returns the current `YYYY` year, used by the footer copyright.

### Filter: `slug`

Makes the default `slug` function more strict to ensure things like excluding emojis and enforcing lowercase.

## VSCode Tips

### Nunjucks

If you haven't previously worked with Nunjucks, you will want a syntax highlighting extension: [Nunjucks](https://marketplace.visualstudio.com/items?itemName=ronnidc.nunjucks)

In addition, you may want to ensure Emmet works on `.njk` files by updating/adding the following in the `settings.json`:

```json
"emmet.includeLanguages": {
	"nunjucks": "html",
},
```

### Formatting

As noted previously, a `prettier` config is included, and you may want to get the
Prettier extension and update your VSCode settings to "Format on Save".

However, to format template files Prettier doesn't recognize like `.njk`, you can update the "Language Mode" on the currently open file from "Nunjucks" (or other current templating language) to "HTML" to allow formatting to be applied. Then, flip it back to re-allow the syntax highlighting if needed.

This is located in the VSCode bottom toolbar near the right-hand side and will display the value of the current file's detected language. Click the name to open the selector.
