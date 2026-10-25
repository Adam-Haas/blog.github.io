# Adam Haas's blog

A Hugo site using the Terminal theme, published at https://adamhaas.co.uk/.

## Local development

Install Hugo **0.160.0**, the version pinned in `.github/workflows/hugo.yaml`.
The current theme builds with the standard Hugo binary; Node.js is not required.

Clone with the theme submodule:

```sh
git clone --recurse-submodules git@github.com:Adam-Haas/blog.github.io.git
cd blog.github.io
```

For an existing checkout:

```sh
git submodule update --init --recursive
```

Preview the site, including drafts:

```sh
make up
```

This requires Make and starts Hugo at http://localhost:1313/. Press Ctrl+C to stop.
You can also run `hugo server --buildDrafts` directly.

Create a post with `hugo new content posts/my-post.md`, edit it in `content/posts/`,
and set `draft: false` when ready to publish. The working content directory is
currently empty, so the site builds without posts until content is added.

## Production build

```sh
hugo --environment production --minify --cleanDestinationDir
```

Hugo writes the site to `public/`. Build output, generated resources, and the
build lock are ignored; commit source files instead. Put files that should be
copied unchanged into `static/`, including the custom-domain `CNAME` file.

Configure the site in `hugo.yaml`. Add site-specific templates under `layouts/`
and assets under `assets/` rather than editing the theme submodule directly.
Only add menu entries once their target pages exist.

## Deployment

The GitHub Actions workflow checks production builds on pull requests and builds
and deploys pushes to `main`. It can also be run manually. Deployment requires
the repository's **Settings > Pages > Source** to be set to **GitHub Actions**
and its custom domain to be configured as `adamhaas.co.uk`.

The workflow follows [Hugo's GitHub Pages guide](https://gohugo.io/host-and-deploy/deploy-to-github-pages/).
When upgrading Hugo, update the workflow version and this README together, then
verify a production build before merging.
