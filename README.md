# izi Hugo Theme

> 'izi' name come from Croatian spelling of the English work 'eazy'

A fast (no JS), minimalist (text based), responsive and highly customisable hugo theme.

![./images/screenshot.png](https://raw.githubusercontent.com/tophatcroat/izi-hugo-theme/master/images/screenshot.png)

- [Example site](https://martinovic.blog)

Features:

- Fast
- Minimalist
- Responsive
- Archive
- Tags

## 1. Installation

### 1.1 As Git Submodule (Easy)

1. Inside the folder of your Hugo site run:
    ```bash
    git submodule add https://github.com/tophatcroat/izi-hugo-theme.git themes/izi
    ```

2. Add the theme's directory to your `config.yaml`:

    ```yaml
   theme: izi
    ```

### 1.2 As a Hugo Module

> Hugo Modules require Go to be installed.

1. From your project's root directory, initiate the hugo module system if you haven't already:

    ```bash
    $ hugo mod init github.com/<your_user>/<your_project>
    ```

2. Add the theme's repo to your `config.yaml`:

    ```yaml
    module:
      imports:
        - path: github.com/tophatcroat/izi-hugo-theme
    ```

For more information read the official [setup guide](//gohugo.io/overview/installing/) of Hugo.

### 1.3 Install Go With mise

If you use [`mise`](https://mise.jdx.dev/), install the latest Go runtime globally with:

```bash
mise use -g go@latest
```

To pin Go for just this project instead, run this from the site root:

```bash
mise use go@latest
```

That creates or updates `mise.toml` so the project uses that Go version automatically.


## 2. Getting started

After installing the theme successfully it requires a just a few more steps to get your site running.


### 2.1 The config file

Take a look inside the [`exampleSite`](https://github.com/tophatcroat/izi-hugo-theme/tree/master/exampleSite) folder of
this theme. You'll find a file called
[`config.yaml`](https://github.com/tophatcroat/izi-hugo-theme/blob/master/exampleSite/config.yaml).
To use it, copy the [`config.yaml`](https://github.com/tophatcroat/izi-hugo-theme/blob/master/exampleSite/config.yaml)
in the root folder of your Hugo site. Feel free to change the strings in this theme.

> ⚠️ You should delete the line: `themesDir: ../../`

### 2.2 Default Content Language

You can set default content language by `defaultContentLanguage`:

```yaml
defaultContentLanguage: en-us
```

Default is `en-gb`. Supported languages are:

- `en-gb`: English
- `en-us`: American English

- More about multiple languages: [Multilingual Mode](https://gohugo.io/content-management/multilingual/).


### 2.3 Nearly finished

In order to see your site in action, run Hugo's built-in local server.

```bash
$ hugo server
```

Now enter http://localhost:1313 in the address bar of your browser.

### 2.6 Production

To run in production, run HUGO_ENV=production before your build command.
For example:

```bash
HUGO_ENV=production hugo
```

Note: The above command will not work on Windows. If you are running a Windows OS, use the below command:

```bash
set HUGO_ENV=production
hugo
```

## 3. Optional Configuration

### 3.1 Add a favicon

To add a favicon, just paste it into the `static/` directory and configure it's path in `config.yaml:
```yaml
params:
  favicon: 'image/favicon.svg'
```

### 3.2 Add an avatar image

Just as easy to add an avatar, just paste it into the `static/` directory and configure it's path in `config.yaml:
```yaml
params:
  avatar: 'image/avatar.png'
```

### 3.3 Custom CSS and JS

You can put your custom css and js files to `static` directory, or use remote css and js files which start with
`http://` or `https://`.

For example:

```yaml
customCSS:
  - css/custom.css # local css in `static/css/custom.css`
  - https://example.com/custom.css # remote css
customJS:
  - js/custom.js # local js in `static/js/custom.js`
  - https://example.com/custom.js # remote js
```

### 3.3.1 Custom Social Icons

Built-in social icons are rendered from SVG partials.

If you want full control over `fill`, `width`, `height`, and the same styling behavior as built-in icons, create a site-level partial override:

```text
layouts/partials/svgs/bluesky.svg
```

This overrides the theme icon automatically.

If you only want to provide an image fallback, you can place a custom icon in your site's `static/` directory.

For example:

```yaml
params:
  social:
    - name: bluesky
      url: https://bsky.app/profile/example.com
  socialIconsPath: image/social
```

Then add one of these files:

```text
static/image/social/bluesky.svg
static/image/social/bluesky.png
static/image/social/bluesky.jpg
static/image/social/bluesky.jpeg
static/image/social/bluesky.webp
```

Use the list form for `params.social` so icons render in the same order as your configuration.

Resolution order is:

1. `layouts/partials/svgs/<key>.svg` from your site
2. custom image from `static/<socialIconsPath>/<key>.*`
3. built-in theme SVG partial
4. text label fallback

### 3.4 Post Summary in Home Page

Set `hiddenPostSummaryInHomePage` to `true` to show the first paragraph on the index page, default is `false`.

For example:

```yaml
hiddenPostSummaryInHomePage: true
```

Alternatively, you can add a `description` in the Front Matter to provide bespoke summary.


### 3.5 Fonts

Use `params.fonts` to load font stylesheets, then set the actual font families in your CSS variables.

```yaml
params:
  fonts:
    useGoogleFonts: true
    urls:
      - https://fonts.googleapis.com/css?family=Unna
      - https://fonts.googleapis.com/css?family=Open+Sans
```

How it works:

- `fonts.urls` is an array of stylesheet URLs to load
- `fonts.useGoogleFonts: true` adds these preconnect tags:

```html
<link rel="preconnect" href="https://fonts.googleapis.com">
<link rel="preconnect" href="https://fonts.gstatic.com" crossorigin>
```

Then choose the actual font families in your custom CSS:

```css
:root {
  --title-font: Unna, serif;
  --text-font: 'Open Sans', sans-serif;
  --code-font: 'JetBrains Mono', monospace;
}
```

If you self-host or download fonts, put your custom font family first in these CSS variables.

For example:

```yaml
params:
  fonts:
    urls:
      - /fonts/my-fonts.css
```

```css
:root {
  --title-font: 'My Title Font', Unna, serif;
  --text-font: 'My Body Font', 'Open Sans', sans-serif;
  --code-font: 'My Code Font', monospace;
}
```

### 3.6 Colours

If you wish to change the overall colours of the blogs, simply overwrite the CSS variables in your `customCSS` file
as such:

```css
:root {
    --accent-color: #8e24aa;
    --accent-color-light: #ab47bc;
    --text-primary: #0a0908;
    --text-secondary: #22333b;
    --background: #ffffff;
    --background-secondary: #f6fff8;
    --border: #6c757d;
}
```

If you want to add dark colour scheme support, for those who have it selected as preferred in their browser:
```css
@media (prefers-color-scheme: dark) {
  :root {
    --accent-color-light: #ffd60a;
    --text-primary: #f8f9fa;
    --text-secondary: #dee2e6;
    --background: #001d3d;
    --background-secondary: #003566;
    --border: #6c757d;
  }
}
```

#### 3.6.1 Syntax highlighting

If you want to change the colours of the syntax highlighter you can find the supported themes 
[here](https://xyproto.github.io/splash/docs/all.html) and generate the CSS with `hugo gen chromastyles --style=github` and
paste the output into your `customCSS` file.

```css
/* Background */ .bg { background-color: #ffffff; }
/* PreWrapper */ .chroma { background-color: #ffffff; }
/* Other */ .chroma .x {  }
/* Error */ .chroma .err { color: #a61717; background-color: #e3d2d2 }

/*
    ...
    omitted for brevity
*/
```

If you are using a different light and dark themes then it's recommended to use a different theme that will look good
with dark colours, it's also a good idea to wrap your light syntax with with `@media (prefers-color-scheme: light)`
because some colours can overwrite one another
```css
@media (prefers-color-scheme: light) {
    /* Background */ .bg { background-color: #ffffff; }
    /* PreWrapper */ .chroma { background-color: #ffffff; }
    /* Other */ .chroma .x {  }
    /* Error */ .chroma .err { color: #a61717; background-color: #e3d2d2 }

    /*
        ...
        omitted for brevity
    */
}

@media (prefers-color-scheme: dark) {
    /* Background */ .bg { color: #f8f8f2; background-color: #282a36; }
    /* PreWrapper */ .chroma { color: #f8f8f2; background-color: #282a36; }
    /* Other */ .chroma .x {  }
    /* Error */ .chroma .err {  }

    /*
        ...
        omitted for brevity
    */
}
```

### 3.7 Spacing

Changing the spacing is just as easy, simply overwrite the CSS variables in your `customCSS` file
as such:

```css
:root {
    --line-height-scalar: 2;

    --space-base: 1.5rem;

    --space-page-width: calc(var(--space-base) * 64);
    --space-page-vertical: calc(var(--space-base) * 2);

    --space-content-vertical: calc(var(--space-base) * 3);
}
```

### 3.8 Analytics

To add Google Analytics provide your tracking ID in your configuration file:

```yaml
googleAnalytics: UA-PROPERTY_ID
```

### 3.9 Edit article link

You can add a link to edit article in your repository by adding `editUrl` in your configuration file:

```yaml
params:
  editUrl: 'https://github.com/<your username>/<your repository>/tree/master'
```
