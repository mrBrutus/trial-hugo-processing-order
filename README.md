# Trial-hugo-processing-order

## About

This trial repository was created to see in which order Hugo processes the content.

The reason is that I would like to add some `Scratch` data to *every* page *before the pages
are rendered*. Since Hugo does most of the processing in parallel this is not so trivial.

In this repo I tried four ways to run the partial which adds the `Scratch` data:

1. Using a loop in the home page layout ([demo](https://trial-hugo-processing-order-homelayout.netlify.app/)).
1. Using a loop in a [custom output]( /custom-output.html ) layout for the home page ([demo](https://trial-hugo-processing-order-homecustomoutput.netlify.app/)).
1. As the page is processed by its corresponding layout ([demo](https://trial-hugo-processing-order-perlayout.netlify.app/)).
1. Using a loop in a custom layout, which is used by a dedicated content page ([demo](https://trial-hugo-processing-order-customlayout.netlify.app/)).
   This page has the `weight` set such that it will be processed first.

The selection takes place in `config.yaml`:

```yaml
params:
  # scratchProcessing: # homeLayout / homeCustomOutput / perLayout / customLayout
  # Process the partial for adding some Scratch data to the page:
  #   "homeLayout" - using a loop in the home layout (`/index.html`)
  #   "homeCustomOutput" - using a loop in the home custom output layout (`/index.custom-output.html`)
  #   "perLayout" - as the page is processed by its corresponding layout (`_default/single.html` etc.)
  #   "customLayout" - using a loop in a custom layout (`_default/custom-layout.html`)
  scratchProcessing: customLayout
```

## Inspect

To inspect the order a number (or time stamp) is added to the scratch.

- This number is then rendered next to the page title.
- A sidebar lists all pages recursively. Here the numbers are rendered too.
- The goal is that at any given page, the numbers are available and consistent.
