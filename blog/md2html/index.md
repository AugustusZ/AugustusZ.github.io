---
title: How to convert Markdown to HTML
date: Jun 30, 2025
lang: en
---

Requirements:

- HTML template
- Custom CSS
- Breadcrumbs

## Basic convert

Start with a `.md` file.

```sh
pandoc ./index.md  -o ./export-1.html --standalone
```

See [./export-1.html](./export-1.html)

## Use template

Now let's add the template `template.html` for wrapping the Markdown content between header and footer:

<details>
<summary><code>template.html</code></summary>

```
<!DOCTYPE html>
<html lang="$lang$">
  <head>
    <meta charset="utf-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <title>Yankuan Zhang | Blog | $title$</title>
    <link rel="preload" href="/img/zyk.jpg" as="image" />
    <link rel="icon" href="/img/favicon.ico" sizes="32x32">
    <link rel="apple-touch-icon" href="/img/apple-touch-icon.png">
    <link rel="stylesheet" href="/styles.css" />
     <style>
      p, li, a {
        font-family: Verdana, Geneva, Tahoma, sans-serif;
        line-height: 2;
      }

      h2 {
        margin-top: 32px;
      }

      a {
        color: #567;
      }

      main {
        max-width: 960px;
        margin: 32px auto;
        padding: 32px;
      }
    </style>
  </head>
  <body>
    <header>
      <a href="/" title="Home">
        <img class="logo" src="/img/zyk.jpg" alt="Home" />
      </a>
      <nav aria-label="Site">
        <ul>
          <li><a href="/about">About</a></li>
          <li><a href="/blog" aria-current="page">Blog</a></li>
        </ul>
      </nav>
    </header>
    <main>
      <nav class="breadcrumbs" aria-label="Breadcrumbs">
        <ol>
          <li>
            <a href="/">Home</a>
          </li>
          <li>
            <a href="/blog">Blog</a>
          </li>
          <li>
            <a href="#" aria-current="page">$title$</a>
          </li>
        </ol>
      </nav>
      $body$
    </main>
    <footer>
      <p>©2024–2025</p>
      <p>​Logo「張延寬」by Yuerong Xia</p>
    </footer>
  </body>
</html>
```

</details>


And add some metadata at the beginning of the `.md` file in YAML

```YAML
---
title: How to convert Markdown to HTML
lang: en
---
```

And run

```sh
pandoc ./index.md  -o ./export-2.html --standalone --template ../template.html 
```

See [./export-2.html](./export-2.html)

And I think that's it!