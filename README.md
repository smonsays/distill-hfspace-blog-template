---
title: Minimal Distill Paper
emoji: 📄
colorFrom: blue
colorTo: green
sdk: static
pinned: false
license: apache-2.0
app_file: index.html
---

# Minimal Distill Blog Template

This is a minimal implementation of the [Distill.pub](https://distill.pub) academic publishing framework with Hugging Face Spaces.
See [distill.md](./distill.md) for how to use the distill framework.


## Local Development

Because the Distill Javascript dynamically fetches `bibliography.bib` via XMLHttpRequest (XHR), the bibliography won't show if you open the HTML file locally in a browser. 

You must serve the directory using a simple local web server.
If you have Python installed, you can simply run:

```bash
python3 -m http.server
```

Then visit [http://localhost:8000](http://localhost:8000) in your browser.

## Publishing to Hugging Face Spaces

This repository is already configured to be published directly as a Static Space. 
When you push changes to Hugging Face, it will automatically serve `index.html` directly from the root folder.
