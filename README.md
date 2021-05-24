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

Checkout branch `2-layout-styles` to see this next step. To build it on your own:
