# Dr Ecco Website

This is the source code for the Dr Ecco Omniheurist website for hosting final projects for *Heuristic Problem Solving* at NYU.

A draft version of this website exists at [https://cims.nyu.edu/~jw8710/drecco/](https://cims.nyu.edu/~jw8710/drecco/). 

**NOTE**: none of the actual games are stored in this repository. Games must be added into the `content/games` folder (see Adding Games below) and the site must then be rebuilt (see Development below - it's just one command). 

# Development

This version of the Dr Ecco website is a static site generated with [Zola](https://www.getzola.org/). Install Zola first. 

Then clone the repo:

```
git clone https://github.com/wjmn/drecco
```

You must then create a `config.toml` file in this directory, e.g. (making sure to change `base_url` to the URL you will deploy to):

```
# The URL the site will be built for
base_url = "https://example.com"

# Whether to automatically compile all Sass files in the sass directory
compile_sass = true

# Whether to build a search index to be used later on by a JavaScript library
build_search_index = false

[markdown]
# Whether to do syntax highlighting
# Theme can be customised by setting the `highlight_theme` variable to a theme supported by Zola
highlight_code = true

[extra]
# Put all your custom variables here

```

Add your games into `content/games` under a subdirectory for each year (and ensure each subdirectory has a `_index.md` file). 

To run the live development server:

```
zola serve
```

To build/rebuild for deployment:

```
zola build
```

# Adding Games


First, create a directory for the year if it doesn't already exists under `content/games` (e.g. `content/games/2024/`). 

Then add a file `_index.md` inside that directory which must contain frontmatter with a title e.g. make a file `content/games/2024/_index.md` with:

```md
+++
title = "2024"
sort_by = "title"
+++
```

You can then add games as subdirectories inside that year (e.g. `content/games/2024/MyGame/`). Each game directory must contain:
    1. `index.md`: a Markdown file describing the game (which gets shown on the description page for the game).
    2. `iframe.html`: the actual game, bundled as a single static HTML file (if you open the HTML file, it should start the game!)
    3. `thumbnail.png`: a thumbnail of the game, shown on the homepage at about 150px width.

The `index.md` markdown file must have the following frontmatter:

```md
+++
title="My Game Title"

[extra]
team="My Team Name"
thumbnail="thumbnail.png"
+++

See the [Elm game template](https://github.com/wjmn/drecco-game-template) and [an example of a completed game with this template](https://github.com/wjmn/gomoku). 

Once you've added your games, rebuild the site with `zola build`. 

# Deployment

The built site is contained in the `public` folder. Simply copy the folder to your web server. Done! You will probably need to modify the permissions on the directory to make these files accessible by the web server.

# Other Notes

1. Use the extension `.markdown` for any extra markdown files in the game directory (e.g. a README). `index.md` should be the only file with the extension `.md` in the game directory. This is because Zola treats any `.md` files as pages to be rendered in the website. 

