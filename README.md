# Basic Eleventy Demo

To get started, clone this repo, cd into it, and run `npm install`.

## Taking a step back

The steps to get it to this point ("step 1") were:

1. Make a new directory
2. cd into it
3. `npm init -y`
3. Install Eleventy with `npm install @11ty/eleventy`
4. Edit the package.json to add a `start` script of `npx @11ty/eleventy --serve` and a build script of `npx @11ty/eleventy`.
5. Create index.md
6. Run the start script. Eleventy processes index.md into the default output folder _site/ with the filename index.html.

## Step 2: Add a layout and styles

Checkout branch `2-layout-styles` to see this next step. In this step, I move our source code to a `/src/` folder, add a layout file, and add a CSS styles file.

To build it on your own:

**First, we move our source code to `/src/`:**

1. Create `/src/` and move `index.md` into it.
2. Create a `.eleventy.js` file in the root of the project with the following content:

```javascript
module.exports = function(eleventyConfig) {
  // Set custom directories for input, output, includes, and data
  return {
    dir: {
      input: "src",
      includes: "_includes",
      data: "_data",
      output: "_site"
    }
  };
};
```

Most of those are defaults - change their name in this file if you'd like to use a different name. You'll need to restart your dev server for any changes in this file to take effect.

**Next, add a layout:**

1. Create `/src/_includes/layout.njk`. This is a [Nunjucks](https://mozilla.github.io/nunjucks/) template, but you can use [many others](https://www.11ty.dev/docs/). The stuff in curly brackets are things that we will fill in at build time:
  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <!-- Grab title from the page data and dump it here -->
    <title>{{ title }}</title>
  </head>
  <body>
    <!-- Grab the content from the page data and dump it here, and mark it as safe -->
    <!-- Safe docs: https://mozilla.github.io/nunjucks/templating.html#safe -->
    {{ content | safe }}
  </body>
  </html>
  ```
2. Add [YAML frontmatter](https://www.11ty.dev/docs/data-frontmatter/) to the top of our `/src/index.md` file to tell it which layout to use and to set the `title` data attribute:
  ```yaml
  ---
  layout: layout.njk
  title: The Best Eleventy Demo TM
  ---
  ```


**Finally, add some CSS:**

1. Create `/src/style.css`. Add some CSS to that file.
2. Add `<link rel="stylesheet" href="./style.css">` to the head of `/src/_includes/layout.njk`.
3. Now we need to tell Eleventy to ["pass through"](https://www.11ty.dev/docs/copy/#manual-passthrough-file-copy-(faster)) any CSS files. We do this in `.eleventy.js`:
  ```diff
  module.exports = function(eleventyConfig) {
  +  // Copy `src/style.css` to `_site/style.css`
  +  eleventyConfig.addPassthroughCopy("src/style.css");

    return {
  +    // When a passthrough file is modified, rebuild the pages:
  +    passthroughFileCopy: true,
      dir: {
        input: "src",
        includes: "_includes",
        data: "_data",
        output: "_site"
      }
    };
  };
  ```
