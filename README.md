# Pi4J website

##

## GoHugo

This website is created with the static site generator [Hugo](https://gohugo.io/).

### Test locally

To test the site locally, first install Hugo as described on ["Install Hugo"](https://gohugo.io/getting-started/installing/).

Example, for Mac:

```
brew install hugo
```

To run the site, open the terminal in the directory with the sources of this site and run the following command:

```
cd pi4j.github.io
hugo serve
```

The website is now available on [localhost:1313](http://localhost:1313/).

### Build and run on GitHub Pages

Using a GitHub Action, the site is published on each commit into the main branch of this repository.

This process is described here:

* [Automate your GitHub Pages Deployment using Hugo and Actions](https://medium.com/@asishrs/automate-your-github-pages-deployment-using-hugo-and-actions-518b959a51f9)
* [Deploy Hugo project to GitHub Pages with GitHub Actions](https://discourse.gohugo.io/t/deploy-hugo-project-to-github-pages-with-github-actions/20725)
