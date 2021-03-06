## Couchbase Mobile Portal

The website for Couchbase Mobile.

The site is using [Hexo](http://hexo.io).

### Getting started

1. Install Hexo CLI: `npm install hexo-cli -g`
2. Run `npm install` to install dependencies
3. Run `hexo server` to generate the site. Hexo automatically detects when a file changed and rebuilds the site. Just reload your browser to see the changes.

### Deployment

A version of the site is hosted on the project page of the [mobile-staging](https://github.com/jamiltz/mobile-staging) repo (GitHub looks for the generated files on the `gh-pages` branch).

The url is [jamiltz.github.io/mobile-staging/](http://jamiltz.github.io/mobile-staging/).

To generate and deploy the site to the GitHub page:
```bash
$ hexo generate
$ hero deploy
```

**Note:** In `_config.yml`, the deploy property holds the info such as the git repo to push to and the branch. The url and root properties need to have the `mobile-staging` root path appended. Hexo provides [other plugins](http://hexo.io/docs/deployment.html) for deployment. This section will likely change when we have a better solution to get the tip of master automatically deployed somewhere.

### General Project Structure

- **scripts**: helper functions, you generally won’t have to look into it
- **source**: that’s where all the `.md` files are, you can write the documentation in Markdown as you would on GitHub
- **theme**: holds the couchbase theme. You might want to look into it to style the theme.

### Adding an App to the App Showcase

1. Add an entry in `source/_data/apps.yml` with the following properties:
	* name
	* description
	* link
	* ios
	* android
	The ios and android properties are optional, the app store/play store images will be visible if you add these properties.
2. Add a banner image for the app in `source/community/images`:
	* size `175x175`
	* format `png`
	The filename should be the same as the **name** property you defined in `apps.yml`.

### Navigation items

A couple of files hold the site index and localisation of the navigation items.

The **Docs** and **API** page have a sidebar. `source/_data/sidebar.yml` is doing the mapping between the sidebar items and files. So when adding/removing an `.md` file, you should check `sidebar.yml` to update the reference.

That’s only the mapping between item and file, we haven’t given the item a title.

You can find the text for each navigation item in `themes/couchbase/languages/en.yml`. You’ll find the mapping for other languages in the same folder.

For the header menu items (main navigation), you can just edit `source/_data/menu.yml`.

So to recap: `menu.yml` is responsible for declaring the top level nav items, `sidebar.yml` for the nav item in the sidebar (on the Guides & API pages). `en.yml` is the mapping between the nav item and text in English.

![](http://cl.ly/aQFY/Screen%20Shot%202015-03-28%20at%2015.13.58.png)


Hexo has a concept of `data-files` to make some data available to any template, think of the properties in those files as being attached to the global scope.

Read more about [data files](http://hexo.io/docs/data-files.html).

### Helper files

The scripts folder holds additional logic for converting the `yml` navigation files to `html` tags.

Dependencies for this folder are the `lodash`, `cheerio` and `lunr` modules.

### Layouts and Partials

There is a pre-existing theme called **couchbase** in the themes folder. Layout and templates are following the [Swig](http://paularmstrong.github.io/swig/) template engine.

##### Syntax highlighting in WebStorm

You can follow this StackOverflow [answer](http://stackoverflow.com/a/27389727/1908348) to have syntax highlighting for Swig templates.

### Logo

The logo is used as the home button in the upper right corner. Hexo picks up the `logo.svg` file in the source folder, you can change this file to change the logo.

### Color Palette

The colour palette used is available [here](http://app.coolors.co/e40121-717579-d3f3ee-85908e-9a9aa1).

You can change the CSS colours accordingly in `themes/couchbase/source/css/_variables.styl`.

### Other dependencies in package.json

Removed **hexo-generator-index** because we have a special way of generating the index page, with the `index.jade` in the source folder.

Added **hexo-generator-jade** for the jade template we have in the source folder.
