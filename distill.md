# How to Create a Distill Article

This guide compiles examples and best practices for creating interactive, explanatory articles using the Distill web framework. It is based on the official [Distill Guide](https://distill.pub/guide/).

## Getting Started

Distill ships with a CSS framework and custom web components that make building interactive academic articles easier than with raw HTML, CSS, and JavaScript. At its simplest, a Distill post is a single HTML file with one special script tag.

```html
<!doctype html>
<meta charset="utf-8">
<script src="https://distill.pub/template.v2.js"></script>

<dt-article>
  <h1>Hello World</h1>
</dt-article>
```

This script tag transforms your page in the browser, adding Distill styling and functionality. A typical Distill post is much longer and contains more structured elements:

```html
<!doctype html>
<meta charset="utf-8">
<script src="https://distill.pub/template.v1.js"></script>

<script type="text/front-matter">
  title: "Article Title"
  description: "Description of the post"
  authors:
  - Chris Olah: http://colah.github.io
  - Shan Carter: http://shancarter.com
  affiliations:
  - Google Brain: http://g.co/brain
  - Google Brain: http://g.co/brain
</script>

<dt-article>
  <h1>Hello World</h1>
  <h2>A description of the article</h2>
  <dt-byline></dt-byline>
  <p>This is the first paragraph of the article.</p>
  <p>We can also cite <dt-cite key="gregor2015draw"></dt-cite> external publications.</p>
</dt-article>

<dt-appendix>
</dt-appendix>

<script type="text/bibliography">
  @article{gregor2015draw,
    title={DRAW: A recurrent neural network for image generation},
    author={Gregor, Karol and Danihelka, Ivo and Graves, Alex and Rezende, Danilo Jimenez and Wierstra, Daan},
    journal={arXivreprint arXiv:1502.04623},
    year={2015},
    url={https://arxiv.org/pdf/1502.04623.pdf}
  }
</script>
```

## Project Structure

Because all templating is delivered via a script tag, each article simply needs to be its own repository. The simplest setup is an HTML file and any required assets. In this setup, you can simply open the `index.html` file in your browser to preview it locally.

```text
image.jpg
index.html
script.js
```

If you have a more complicated build process or private files, you can place your output in a `public` folder. Only the contents of the `public` folder will be published.

## Front Matter

Describe metadata about your post (title, description, authors, affiliations, etc.) using the `<script type="text/front-matter">` tag.

```html
<script type="text/front-matter">
  title: "Article Title"
  description: "Description of the post"
  authors:
  - Chris Olah: http://colah.github.io
  - Shan Carter: http://shancarter.com
  affiliations:
  - Google Brain: http://g.co/brain
  - Google Brain: http://g.co/brain
</script>
```

## Citations

Distill supports BibTeX for academic citations. Define your citations globally using the `<script type="text/bibliography">` element. Populating the `url` field is strongly encouraged to provide links for citations.

```html
<script type="text/bibliography">
  @article{gregor2015draw,
    title={DRAW: A recurrent neural network for image generation},
    author={Gregor, Karol and Danihelka, Ivo and Graves, Alex and Rezende, Danilo Jimenez and Wierstra, Daan},
    journal={arXivreprint arXiv:1502.04623},
    year={2015},
    url={https://arxiv.org/pdf/1502.04623.pdf},
  }
</script>
```

Use the `<dt-cite>` tag in the article body to cite references. The `key` attribute corresponds to the BibTeX id, and can accept multiple comma-separated ids.

```html
<dt-cite key="gregor2015draw"></dt-cite>
```

Citations are presented inline as hoverable numbers. An appendix bibliography is automatically generated if an appendix is present.

## Footnotes

Wrap the text you want to show up in a footnote in a `<dt-fn>` tag. The footnote number will be automatically generated and display on hover.

```html
<dt-fn>This will become a hoverable footnote.</dt-fn>
```

## Code Blocks

Syntax highlighting is provided within `<dt-code>` tags. 

For inline code: 
```html
<dt-code language="html">let x = 10;</dt-code>
```

For large blocks of code, add the `block` attribute:
```html
<dt-code block language="javascript">
  var x = 25;
  function(x){
    return x * x;
  }
</dt-code>
```

## Equations

Use MathJax or KaTeX for equations.

## Diagrams

- **Static Diagrams**: Use vector graphics tools like Adobe Illustrator, Sketch, or Inkscape. For LaTeX equations inside SVGs, Inkscape has a supported plugin.
- **Dynamic Diagrams**: D3.js is recommended. For complex diagrams where only part of it should be animated, you can draw a static diagram, tag elements with classes/ids, and manipulate them with D3.

## Layouts

The main text column is assumed to be the body (`.l-body`) layout. Other layouts can be applied by adding the following classes to elements:

- `.l-middle`: Slightly wider than body text.
- `.l-page`: Much wider.
- `.l-screen`: Full browser width.

You can append `-outset` or `-inset` to some layouts:
- `.l-body-outset`
- `.l-middle-outset`
- `.l-page-outset`
- `.l-screen-inset`

For floating items to the side (e.g., smaller images or side-text):
- `.l-body.side`
- `.l-middle.side`
- `.l-page.side`

For marginalia, asides, and footnotes that live in the gutter:
- `.l-gutter`

To center the whole article, add the `centered` class to the `<dt-article>` tag:
```html
<dt-article class="centered">
  <h1>Hello World</h1>
</dt-article>
```

## Appendix

An appendix can be added after your article using the `<dt-appendix>` tag. This is automatically where bibliographies get generated.

```html
<dt-article>
  ...
</dt-article>

<dt-appendix>
  <h3>Appendix Section Title</h3>
  <p>section content</p>
</dt-appendix>
```

Common appendix sections include:
- **Acknowledgments**: Recognize people, institutions, or open-source software that made the work possible.
- **Author Contributions**: Describe what each author did.
