hugo-uno-chairraver
===================

A responsive hugo theme with awesome font's, charts and light-box
galleries, the theme is based on [hugo-uno](https://github.com/SenjinDarashiva/hugo-uno)
based on [Uno](https://github.com/daleanthony/Uno) for ghost. A example site
is available at [ridderbusch.name](https://ridderbusch.name) (Not yet online)

## My Changes compared to Hugo-Uno from Fredrik Loch.

* Updated lightGallery to latest and full feature version (1.2.6 as of this writing).
* Include lightGallery Javascript by default in the `<head>`.
* Moved the activation for lightGallery into `/layouts/partitials/script.html`.
* Include Google Analytics via `.Site.Params.google_analytics` in `config.toml`.
* Created a new `tags.html` partial to show tags below the posts and in
the summary.
* Created a new `pagination.html` partial to facilitate paging through the
index.
* Use [jquery-localize](https://github.com/coderifous/jquery-localize)
for some minimal localization to German (located in `/static/js/lang`).
* Activation of localization is also in `/layouts/partitials/script.html`.
* Changed the date format through out to ISO 8601 (YYYY-MM-DD).
* Used my own backgound image.
* Switched to the Google fonts Nunito for headlines and Open Sans for
  the rest.
* Update the SASS and Bourbon description with actual theme directory
(basically removing `assets/` path component)
* Move the `scss` directory up one level so that `.sass-cache` and the directory
itself are not published.
* Change the `curl` invocation to write the output of the minifying
with the `-o` flag. The output redirection causes problems on Windows (LF/CR).

## Usage
The following is a short tutorial on the usage of some features in the theme.
Configuration
-

To take full advantage of the features in this theme you can add variables to your site config file, the following is the example config from the example site:
```
languageCode = "en-us"
builddrafts = false
baseurl = "https://ridderbusch.name/"
canonifyurls = true
title = "Frank Ridderbusch"
author = "Frank Ridderbusch"
copyright = "This work is licensed under a Creative Commons Attribution-ShareAlike 4.0 International License."


[indexes]
   category = "categories"
   tag = "tags"
[Params]
  AuthorName = "Frank"
  github = "chairraver"
  twitter = "FRidderbusch"
  google_analytics = "..."
  email = "..."
  description = ""
  cv = "..."
  muut = "..."
  linkedin = "..."
  cover = "/images/background-cover.jpg"
  logo = "/img/logo-1.jpg"
```

If you prefer to use discourse replace the "muut" line with the following(remember the trailing slash)

'''
  discourse = "http://discourse.yoursite.com/"
'''
Charts
-

To create charts I use [Chart.js](https://github.com/nnnick/Chart.js) which can be configured through basic js files. To add a chart to a post use the following short-code:
```
{{% chart id="basicChart" width=860 height=400 js="../../js/chartData.js" %}}
```
Where the javascript file specified contains the data for the chart, a basic example could look like this:
```
$(function(){
  var chartData = {
      labels: ["Jekyll", "Hugo", "Wintersmith"],
      datasets: [
          {
              label: "Mean build time",
              fillColor: "#E1EDD7",
              strokeColor: "#E1EDD7",
              highlightFill: "#C1D8AB",
              highlightStroke: "#C1D8AB",
              data: [784, 100, 5255]
          }
      ]
  };
  var ctx = $("#chartData").get(0).getContext("2d");
  var myBarChart = new Chart(ctx).Bar(data1, {
      scaleBeginAtZero : true,
      responsive: true,
      maintainAspectRatio: false,
    }
  );
```
A running example can be found in my comparison between [Jekyll, Hugo and Winthersmith](http://fredrikloch.me/post/2014-08-12-Jekyll-and-its-alternatives-from-a-site-generation-point-of-view/)
Gallery
-
To add a gallery to the site we use basic html together with
[lightGallery](http://sachinchoolur.github.io/lightGallery/index.html)
to create a responsive light-box gallery.

Within `/layouts/_default/single.html` the `<div>` with class `post`,
which basically wraps the actual content of the post also has the ID
`#post-gallery`. Each individual image is marked with class
`post-pic`. 

```
<div class="post-pic" data-src="/.../pathToImg1.jpg"
     data-sub-html="caption for pathToImg1">
<img src="/.../thumbnailPathToImg1.jpg" alt="..." width="xxx" height="yyy" />
</div>

<div class="post-pic" data-src="/.../pathToImg2.jpg"
     data-sub-html="caption for pathToImg2">
<img src="/.../thumbnailPathToImg2.jpg" alt="..." width="xxx" height="yyy" />
</div>
```

The lightGallery is then actually activated through the following
Javascript fragment in `/layout/partials/script.html`.

```
$("#post-gallery").lightGallery({ selector : ".post-pic" });
```
An example is this
[page](https://ridderbusch.name/post/2014-10-31-nascom-circuits/). (Not
yet online).

An alternative is defined in the short codes file
`/layouts/shortcodes/img.html`, which provides the `img`
template. This allow the inclusion of individual images into a post.

```
{{< img id="unique ID" href="/.../pathToImg.jpg"
src="/.../thumbnailPathToImg.jpg" width="xxx" heigth="yyy"
alt="alt text" class="floatright" >}}
```

An example is this
[page](https://ridderbusch.name/page/my-photo-gear/). (Not
yet online).

## Features

**Cover page**
The landing page for Hugo-Uno is a full screen 'cover' featuring your avatar, blog title, mini-bio and cover image.

**Built with SASS, using BEM**
If you know HTML and CSS making modifications to the theme should be super simple.

**Responsive**
Hugo-Uno looks great on all devices, even those weird phablets that nobody buys.

**Muutt comments**
[Muut](https://muut.com/) integration allows users to comment on your posts.

**Font-awesome icons**
For more information on available icons: [font-awesome](http://fortawesome.github.io/Font-Awesome/)

**No-JS fallback**
While JS is widely used, some themes and websites don't provide fallback for when no JS is available (I'm looking at you [Squarespace](http://blog.squarespace.com/)). If for some weird reason a visitor has JS disabled your blog will still be usable.

## License
[Creative Commons Attribution 4.0 International](http://creativecommons.org/licenses/by/4.0/)

## Development

In order to develop or make changes to the theme you will need to have the sass compiler and bourbon both installed.

To check installation run the following commands from a terminal and you should see the `> cli output` but your version numbers may vary.

**SASS**
```bash
$ sass -v
> Sass 3.3.4 (Maptastic Maple)
```
If for some reason SASS isn't installed follow the instructions from the [Sass install page](http://sass-lang.com/install)

**Bourbon**
```bash
$ bourbon help
> Bourbon 3.1.8
```
If Bourbon isn't installed follow the installation instructions on the [Bourbon website](http://bourbon.io)

Once installation is verified we will need to go mount the bourbon
mixins into the `scss` folder.

From the project root run `bourbon install` with the correct path (in
the theme main directory)

```bash
$ bourbon install --path scss
> bourbon files installed to scss/bourbon/
```

Now that we have the bourbon mixins inside of the `scss` src folder we
can now use the sass cli command to watch the scss files for changes
and recompile them.

```bash
$ sass --watch scss:static/css
>>>> Sass is watching for changes. Press Ctrl-C to stop.
```

To minify the css files use the following command in the assets folder

```bash
curl -X POST -s -o css/uno.min.css --data-urlencode 'input@css/uno.css' http://cssminifier.com/raw
```

On Windows and within PowerShell you explicitly need use `curl.exe`
(provided that you installed a `curl` program) otherwise the
PowerShell alias `curl` will be invoked, which of course will not
work.
