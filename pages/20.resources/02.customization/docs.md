---
title: Learn2 Grav Skeleton Customization
---

>>> [learn2 on github](https://github.com/getgrav/grav-theme-learn2)

[grav documents](https://learn.getgrav.org/troubleshooting)

### github "edit this link implementation 
- [Theme template on gitHub](https://github.com/hibbitts-design/grav-skeleton-learn2-with-git-sync)
 - blueprints.yaml
 - mytheme.yaml
- languages.yaml [sets variable 'THEME_LEARN2_GITHUB_EDIT_THIS_PAGE'] ->  github_link.html.twig -> base.html.twig [see below]
```
<blockquote id="github-contrib"><blockquote><blockquote><blockquote><blockquote>
<p>
    {{ 'THEME_LEARN2_GITHUB_NOTE'|t }}

    {% include 'partials/github_link.html.twig' %}
</p>
</blockquote></blockquote></blockquote></blockquote></blockquote>
```
### files to modify for site customizations

[div class="table table-striped"]
|route|route L2|route L3|route L4|route L5|
|--- | --- | --- | --- | --- |
/assets|
/bin|
/cache|
/config|site.yaml|system.yaml|security.yaml|media.yaml
/images|doNotUseThis|
/logs|
/user |blueprint.yaml|screenshot.jpg|![](/user/screenshot.jpg)|
| |/accounts |
| |/assets |
| |/config |site.yaml|system.yaml|security.yaml|media.yaml|
| | |/plugins|admin.yaml|git-sync.yaml|login.yaml|etc|
| |  |
| |/data |
| |/images |![techdogs(small).png](/user/images/techdogs(small).png)
| |/pages |
| |/plugins |
| |/themes |
| | |/mytheme|mytheme.yaml|
| | | |/css |[custom.css](/user/themes/mytheme/css/custom.css)|
| | | |/images|favicon.png|![favicon.png](/user/themes/mytheme/images/favicon.png)|
| | | |/templates |/partials|[base.html.twig]|
| | | | | | [sidebar.html.twig]|
| | | | || [logo.html.twig]|
/vendor |
/webconfig |web.config
[/div]

#### logo.html.twig

```html
<img src="/images/techdogs(small).png" alt="logo">
```
#### site.yaml

```yaml
title: techDogs
default_lang: 'United States'
author:
  name: 'Richard Hoppel'
  email: rhoppel@gmail.com
taxonomies:
  - category
  - tag
  - author
metadata:
  description: techDogs
summary:
  enabled: true
  format: short
  size: 300
  delimiter: '==='
blog:
  route: /blog

```
#### custom.css

```css
/*
===============================================================================================================================
Put your custom CSS in this file.
===============================================================================================================================
*/

/* CSS to hide sidebar numbering (uncomment to enable) */
/*
#sidebar ul.topics > li > a b
{
    visibility: hidden;
}
*/

/* CSS to hide clipboard icon (uncomment to enable) */
/*
.copy-to-clipboard {
    display:none;
}
*/
#body { 
    background-color:#82624b;

    color: white;
}
#header {
    background-color: #7faedb;
    color: black;
}
#sidebar {
    background-color: #2d3b45;
}
#logo {
//background-color:white;
}

.searchbox {
    //background-color:white;
}

/* Links */
body a {
    color: #ed7d31;
}

/* Atom buttons */
.button {
    background: #ed7d31;
    color: #fff;
    box-shadow: 0 3px 0 #1380ae;
}

/* Searchbox */
.searchbox input {
    display: inline-block;
    color: #fff;
    width: 100%;
    height: 30px;
    background: #ed7d31;
    border: 0;
    padding: 0 25px 0 30px;
    margin: 0;
    font-weight: 400;
}
```

#### base.html.twig

```twig
{% set theme_config = attribute(config.themes, config.system.pages.theme) %}
<!DOCTYPE html>
<html lang="{{ grav.language.getLanguage ?: 'en' }}">
<head>
    {% block head %}
    <meta charset="utf-8" />
    <title>{% if header.title %}{{ header.title }} | {% endif %}{{ site.title }}</title>
    {% include 'partials/metadata.html.twig' %}
    <meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1, user-scalable=no, shrink-to-fit=no" />
    <link rel="alternate" type="application/atom+xml" href="{{ base_url_absolute}}/feed.atom" title="Atom Feed" />
    <link rel="alternate" type="application/rss+xml" href="{{ base_url_absolute}}/feed.rss" title="RSS Feed" />
    <link rel="icon" type="image/png" href="{{ url('theme://images/favicon.png') }}">

    {% block stylesheets %}
        {% do assets.addCss('theme://css-compiled/nucleus.css',102) %}
        {% do assets.addCss('theme://css-compiled/theme.css',101) %}
        {% do assets.addCss('theme://css/custom.css',100) %}
        {% do assets.addCss('theme://css/font-awesome.min.css',100) %}
        {% do assets.addCss('theme://css/featherlight.min.css') %}

        {% if browser.getBrowser == 'msie' and browser.getVersion >= 8 and browser.getVersion <= 9 %}
            {% do assets.addCss('theme://css/nucleus-ie9.css') %}
            {% do assets.addCss('theme://css/pure-0.5.0/grids-min.css') %}
            {% do assets.addJs('theme://js/html5shiv-printshiv.min.js') %}
        {% endif %}

        {{ assets.css() }}
    {% endblock %}

    {% block javascripts %}
        {% do assets.addJs('jquery',101) %}
        {% do assets.addJs('theme://js/modernizr.custom.71422.js',100) %}
        {% do assets.addJs('theme://js/featherlight.min.js') %}
        {% do assets.addJs('theme://js/clipboard.min.js') %}
        {% do assets.addJs('theme://js/jquery.scrollbar.min.js') %}
        {% do assets.addJs('theme://js/learn.js') %}
        {{ assets.js() }}
    {% endblock %}

    {% endblock %}
</head>
<body class="searchbox-hidden {{ page.header.body_classes }}" data-url="{{ page.route }}">
    {% block sidebar %}
    <nav id="sidebar">
        <div id="header-wrapper">
            <div id="header">
                <a id="logo" href="{{ theme_config.home_url ?: base_url_absolute }}">{% include 'partials/logo.html.twig' %}</a>
                <div class="searchbox">
                    <label for="search-by"><i class="fa fa-search"></i></label>
                    <input id="search-by" type="text" placeholder="{{ 'SEARCH'|t }}"
                           data-search-input="{{ base_url_relative }}/search.json/query"/>
                    <span data-search-clear><i class="fa fa-close"></i></span>
                </div>
            </div>
        </div>
        {% include 'partials/sidebar.html.twig' %}
    </nav>
    {% endblock %}

    {% block body %}
    <section id="body">
        <div id="overlay"></div>

        <div class="padding highlightable">
            <a href="#" id="sidebar-toggle" data-sidebar-toggle><i class="fa fa-2x fa-bars"></i></a>

            {% block topbar %}{% if theme_config.github.position == 'top' or config.plugins.breadcrumbs.enabled %}
            <div id="top-bar">
                {% if theme_config.github.position == 'top' %}
                <div id="top-github-link">
                {% include 'partials/github_link.html.twig' %}
                </div>
                {% endif %}

                {% if config.plugins.breadcrumbs.enabled %}
                {% include 'partials/breadcrumbs.html.twig' %}
                {% endif %}
            </div>
            {% endif %}{% endblock %}

            {% block content %}{% endblock %}

            {% block footer %}
                {% if theme_config.github.position == 'bottom' %}
                {% include 'partials/github_note.html.twig' %}
                {% endif %}
            {% endblock %}

        </div>
        {% block navigation %}{% endblock %}
    </section>
    {% endblock %}
    {% block analytics %}
        {% if theme_config.google_analytics_code %}
        {% include 'partials/analytics.html.twig' %}
        {% endif %}
    {% endblock %}
 </body>
</html>
```

#### sidebar.html.twig

```twig
{% macro loop(page, parent_loop) %}
    {% if parent_loop|length > 0 %}
        {% set data_level = parent_loop %}
    {% else %}
        {% set data_level = 0 %}
    {% endif %}
    {% for p in page.children.visible %}
        {% set parent_page = p.activeChild ? ' parent' : '' %}
        {% set current_page = p.active ? ' active' : '' %}
        <li class="dd-item{{ parent_page }}{{ current_page }}" data-nav-id="{{ p.route }}">
            <a href="{{ p.url }}" {% if p.header.class %}class="{{ p.header.class }}"{% endif %}>
                <i class="fa fa-check read-icon"></i>
                <span><b>{% if data_level == 0 %}{{ loop.index }}. {% endif %}</b>{{ p.menu }}</span>
            </a>
            {% if p.children.count > 0 %}
            <ul>
                {{ _self.loop(p, parent_loop|default(0)+loop.index) }}
            </ul>
            {% endif %}
        </li>
    {% endfor %}
{% endmacro %}
 
{% macro version(p) %}
    {% set parent_page = p.activeChild ? ' parent' : '' %}
    {% set current_page = p.active ? ' active' : '' %}
    <h5 class="{{ parent_page }}{{ current_page }}">
        {% if p.activeChild or p.active %}
        <i class="fa fa-chevron-down fa-fw"></i>
        {% else %}
        <i class="fa fa-plus fa-fw"></i>
        {% endif %}
        <a href="{{ p.url }}">{{ p.menu }}</a>
    </h5>
{% endmacro %}
 
<div class="scrollbar-inner">
    <div class="highlightable">
        {% if theme_config.top_level_version %}
            {% for slug, ver in pages.children %}
                {{ _self.version(ver) }}
                <ul id="{{ slug }}" class="topics">
                {{ _self.loop(ver, '') }}
                </ul>
            {% endfor %}
        {% else %}
            <ul class="topics">
                {% if theme_config.root_page %}
                    {{ _self.loop(page.find(theme_config.root_page), '') }}
                {% else %}
            {{ _self.loop(pages, '') }}
                {% endif %}
            </ul>
        {% endif %}
        <hr />

        <a class="padding" href="#" data-clear-history-toggle><i
                    class="fa fa-fw fa-history"></i> {{ 'THEME_LEARN2_CLEAR_HISTORY'|t }}</a><br/>

        <section id="footer">
            {% if config.plugins.feed.enabled and pages.find('/feed') %}
              <a class="button" href="{{ base_url }}/feed.atom"><i class="fa fa-rss-square"></i> Atom 1.0</a>
              <a class="button" href="{{ base_url }}/feed.rss"><i class="fa fa-rss-square"></i> RSS</a><br><br>
            {% endif %}
            <p>{{ 'built by Ricky'|t }}</p>
        </section>
    </div>
</div>
```

#### mytheme.yaml

```yaml
enabled: true
root_page: 					                        # optional: set root page of documentation
top_level_version: false                            # Use versions for top level navigation
google_analytics_code:                              # Enter your `UA-XXXXXXXX-X` code here
home_url:                                           # http://getgrav.org
github:
    position: top                                   # top | bottom | off
    icon:                                           # FontAwesome icon
    tree:

streams:
 schemes:
   theme:
     type: ReadOnlyStream
     prefixes:
       '':
       - user/themes/mytheme
       - user/themes/learn2-git-sync
       - user/themes/learn2
```

#### tree structure

```
├───assets
├───backup
├───bin
├───cache
│   ├───compiled
│   │   ├───blueprints
│   │   ├───config
│   │   ├───files
│   │   └───languages
│   ├───doctrine
│   ├───gpm

│   ├───login
│   │   └───login_attempts
│
│   └───twig
│ 
├───images
├───logs
│   └───popularity
├───system
│   ├───assets
│   │   ├───jquery
│   │   └───responsive-overlays
│   ├───blueprints
│   │   ├───config
│   │   ├───pages
│   │   └───user
│   ├───config
│   ├───images
│   │   └───media
│   ├───languages
│   ├───pages
│   ├───src
│   │   └───Grav
│   │       ├───Common
│   │       │   ├───Backup
│   │       │   ├───Config
│   │       │   ├───Data
│   │       │   ├───Errors
│   │       │   │   └───Resources
│   │       │   ├───File
│   │       │   ├───Filesystem
│   │       │   ├───GPM
│   │       │   │   ├───Common
│   │       │   │   ├───Local
│   │       │   │   └───Remote
│   │       │   ├───Helpers
│   │       │   ├───Language
│   │       │   ├───Markdown
│   │       │   ├───Page
│   │       │   │   └───Medium
│   │       │   ├───Processors
│   │       │   ├───Service
│   │       │   ├───Twig
│   │       │   │   ├───Node
│   │       │   │   └───TokenParser
│   │       │   └───User
│   │       ├───Console
│   │       │   ├───Cli
│   │       │   ├───Gpm
│   │       │   └───TerminalObjects
│   │       └───Framework
│   │           ├───Cache
│   │           │   ├───Adapter
│   │           │   └───Exception
│   │           ├───Collection
│   │           ├───ContentBlock
│   │           ├───Object
│   │           │   ├───Access
│   │           │   ├───Base
│   │           │   ├───Interfaces
│   │           │   └───Property
│   │           ├───Psr7
│   │           ├───Route
│   │           └───Uri
│   └───templates
│       └───partials
├
├───tmp
├───user
│   ├───accounts
│   ├───assets
│   ├───config
│   │   ├───plugins
│   │   └───themes
│   ├───data
│   ├───pages
│   │   ├───01.basics
│   │   │   ├───01.overview
│   │   │   ├───02.requirements
│   │   │   │   └───01.sub-topic
│   │   │   │       └───01.sub-sub-topic
│   │   │   └───03.installation
│   │   ├───02.intermediate
│   │   │   ├───01.topic-1
│   │   │   ├───02.topic-2
│   │   │   ├───03.topic-3
│   │   │   └───04.topic-4
│   │   ├───03.advanced
│   │   │   ├───01.adv-topic-1
│   │   │   └───02.adv-topic-2
│   │   ├───04.ricks-admin-page
│   │   └───feed
│   ├───plugins
│   │   ├───admin
│   │   │   ├───assets
│   │   │   ├───blueprints
│   │   │   │   ├───admin
│   │   │   │   │   └───pages
│   │   │   │   └───config
│   │   │   ├───classes
│   │   │   │   └───Twig
│   │   │   ├───languages
│   │   │   ├───pages
│   │   │   │   └───admin
│   │   │   ├───tests
│   │   │   │   ├───unit
│   │   │   │   │   └───classes
│   │   │   │   └───_support
│   │   │   │       └───Helper
│   │   │   ├───themes
│   │   │   │   └───grav
│   │   │   │       ├───app
│   │   │   │       │   ├───dashboard
│   │   │   │       │   ├───forms
│   │   │   │       │   │   └───fields
│   │   │   │       │   │       └───editor
│   │   │   │       │   ├───media
│   │   │   │       │   ├───pages
│   │   │   │       │   │   └───page
│   │   │   │       │   ├───plugins
│   │   │   │       │   ├───themes
│   │   │   │       │   ├───updates
│   │   │   │       │   └───utils
│   │   │   │       ├───css
│   │   │   │       │   ├───codemirror
│   │   │   │       │   └───pure-0.5.0
│   │   │   │       ├───css-compiled
│   │   │   │       ├───fonts
│   │   │   │       │   └───rockettheme-apps
│   │   │   │       ├───images
│   │   │   │       ├───js
│   │   │   │       ├───scss
│   │   │   │       │   ├───configuration
│   │   │   │       │   │   ├───fonts
│   │   │   │       │   │   ├───nucleus
│   │   │   │       │   │   └───template
│   │   │   │       │   ├───nucleus
│   │   │   │       │   │   ├───functions
│   │   │   │       │   │   ├───mixins
│   │   │   │       │   │   └───particles
│   │   │   │       │   ├───template
│   │   │   │       │   │   └───modules
│   │   │   │       │   └───vendor
│   │   │   │       │       ├───bourbon
│   │   │   │       │       │   ├───addons
│   │   │   │       │       │   ├───css3
│   │   │   │       │       │   ├───functions
│   │   │   │       │       │   ├───helpers
│   │   │   │       │       │   └───settings
│   │   │   │       │       └───color-schemer
│   │   │   │       │           └───color-schemer
│   │   │   │       └───templates
│   │   │   │           ├───email
│   │   │   │           ├───forms
│   │   │   │           │   └───fields
│   │   │   │           │       ├───array
│   │   │   │           │       ├───blueprint
│   │   │   │           │       ├───colorpicker
│   │   │   │           │       ├───column
│   │   │   │           │       ├───columns
│   │   │   │           │       ├───dateformat
│   │   │   │           │       ├───datetime
│   │   │   │           │       ├───editor
│   │   │   │           │       ├───fieldset
│   │   │   │           │       ├───file
│   │   │   │           │       ├───filepicker
│   │   │   │           │       ├───frontmatter
│   │   │   │           │       ├───iconpicker
│   │   │   │           │       ├───ignore
│   │   │   │           │       ├───key
│   │   │   │           │       ├───list
│   │   │   │           │       ├───markdown
│   │   │   │           │       ├───mediapicker
│   │   │   │           │       ├───multilevel
│   │   │   │           │       ├───order
│   │   │   │           │       ├───pagemedia
│   │   │   │           │       ├───pagemediaselect
│   │   │   │           │       ├───pages
│   │   │   │           │       ├───parents
│   │   │   │           │       ├───permissions
│   │   │   │           │       ├───range
│   │   │   │           │       ├───section
│   │   │   │           │       ├───selectize
│   │   │   │           │       ├───selectunique
│   │   │   │           │       ├───tab
│   │   │   │           │       ├───tabs
│   │   │   │           │       ├───taxonomy
│   │   │   │           │       ├───themeselect
│   │   │   │           │       ├───toggle
│   │   │   │           │       └───userinfo
│   │   │   │           └───partials
│   │   │   ├───twig
│   │   │   └───vendor
│   │   │       ├───bin
│   │   │       ├───composer
│   │   │       │   └───semver
│   │   │       │       └───src
│   │   │       │           └───Constraint
│   │   │       ├───fguillot
│   │   │       │   └───picofeed
│   │   │       │       └───lib
│   │   │       │           └───PicoFeed
│   │   │       │               ├───Client
│   │   │       │               ├───Config
│   │   │       │               ├───Encoding
│   │   │       │               ├───Filter
│   │   │       │               ├───Generator
│   │   │       │               ├───Logging
│   │   │       │               ├───Parser
│   │   │       │               ├───Processor
│   │   │       │               ├───Reader
│   │   │       │               ├───Rules
│   │   │       │               ├───Scraper
│   │   │       │               ├───Serialization
│   │   │       │               └───Syndication
│   │   │       └───zendframework
│   │   │           └───zendxml
│   │   │               └───src
│   │   │                   └───Exception
│   │   ├───email
│   │   │   ├───classes
│   │   │   ├───cli
│   │   │   ├───templates
│   │   │   │   └───email
│   │   │   └───vendor
│   │   │       ├───composer
│   │   │       └───swiftmailer
│   │   │           └───swiftmailer
│   │   │               └───lib
│   │   │                   ├───classes
│   │   │                   │   └───Swift
│   │   │                   │       ├───ByteStream
│   │   │                   │       ├───CharacterReader
│   │   │                   │       ├───CharacterReaderFactory
│   │   │                   │       ├───CharacterStream
│   │   │                   │       ├───Encoder
│   │   │                   │       ├───Events
│   │   │                   │       ├───KeyCache
│   │   │                   │       ├───Mailer
│   │   │                   │       ├───Mime
│   │   │                   │       │   ├───ContentEncoder
│   │   │                   │       │   ├───HeaderEncoder
│   │   │                   │       │   └───Headers
│   │   │                   │       ├───Plugins
│   │   │                   │       │   ├───Decorator
│   │   │                   │       │   ├───Loggers
│   │   │                   │       │   ├───Pop
│   │   │                   │       │   └───Reporters
│   │   │                   │       ├───Signers
│   │   │                   │       ├───StreamFilters
│   │   │                   │       └───Transport
│   │   │                   │           └───Esmtp
│   │   │                   │               └───Auth
│   │   │                   └───dependency_maps
│   │   ├───external_links
│   │   │   ├───assets
│   │   │   │   ├───css
│   │   │   │   └───images
│   │   │   ├───blueprints
│   │   │   ├───classes
│   │   │   └───docs
│   │   ├───feed
│   │   │   ├───assets
│   │   │   ├───blueprints
│   │   │   └───templates
│   │   ├───form
│   │   │   ├───app
│   │   │   ├───assets
│   │   │   ├───classes
│   │   │   ├───templates
│   │   │   │   ├───forms
│   │   │   │   │   ├───default
│   │   │   │   │   ├───dropzone
│   │   │   │   │   └───fields
│   │   │   │   │       ├───avatar
│   │   │   │   │       ├───captcha
│   │   │   │   │       ├───checkbox
│   │   │   │   │       ├───checkboxes
│   │   │   │   │       ├───color
│   │   │   │   │       ├───column
│   │   │   │   │       ├───columns
│   │   │   │   │       ├───conditional
│   │   │   │   │       ├───date
│   │   │   │   │       ├───datetime
│   │   │   │   │       ├───display
│   │   │   │   │       ├───email
│   │   │   │   │       ├───fieldset
│   │   │   │   │       ├───file
│   │   │   │   │       ├───formname
│   │   │   │   │       ├───hidden
│   │   │   │   │       ├───honeypot
│   │   │   │   │       ├───month
│   │   │   │   │       ├───number
│   │   │   │   │       ├───password
│   │   │   │   │       ├───radio
│   │   │   │   │       ├───range
│   │   │   │   │       ├───select
│   │   │   │   │       ├───select_optgroup
│   │   │   │   │       ├───signature
│   │   │   │   │       ├───spacer
│   │   │   │   │       ├───switch
│   │   │   │   │       ├───tel
│   │   │   │   │       ├───text
│   │   │   │   │       ├───textarea
│   │   │   │   │       ├───time
│   │   │   │   │       ├───uniqueid
│   │   │   │   │       ├───url
│   │   │   │   │       └───week
│   │   │   │   ├───modular
│   │   │   │   └───partials
│   │   │   └───vendor
│   │   │       └───composer
│   │   ├───git-sync
│   │   │   ├───app
│   │   │   │   └───wizard
│   │   │   ├───classes
│   │   │   ├───cli
│   │   │   ├───css-compiled
│   │   │   ├───images
│   │   │   │   └───repos
│   │   │   ├───js
│   │   │   ├───scss
│   │   │   │   ├───configuration
│   │   │   │   ├───plugin
│   │   │   │   └───vendor
│   │   │   │       └───bourbon
│   │   │   │           ├───addons
│   │   │   │           ├───css3
│   │   │   │           ├───functions
│   │   │   │           ├───helpers
│   │   │   │           └───settings
│   │   │   ├───templates
│   │   │   │   ├───forms
│   │   │   │   │   └───fields
│   │   │   │   │       ├───enc-password
│   │   │   │   │       └───git-wizard
│   │   │   │   └───partials
│   │   │   └───vendor
│   │   │       ├───composer
│   │   │       ├───defuse
│   │   │       │   └───php-encryption
│   │   │       │       ├───dist
│   │   │       │       ├───docs
│   │   │       │       │   └───classes
│   │   │       │       └───src
│   │   │       │           └───Exception
│   │   │       ├───paragonie
│   │   │       │   └───random_compat
│   │   │       │       ├───dist
│   │   │       │       ├───lib
│   │   │       │       └───other
│   │   │       └───sebastian
│   │   │           └───git
│   │   │               └───src
│   │   │                   └───Exception
│   │   ├───highlight
│   │   │   ├───assets
│   │   │   ├───css
│   │   │   └───js
│   │   ├───login
│   │   │   ├───classes
│   │   │   │   ├───Events
│   │   │   │   ├───RememberMe
│   │   │   │   └───TwoFactorAuth
│   │   │   ├───cli
│   │   │   ├───css
│   │   │   ├───languages
│   │   │   ├───pages
│   │   │   ├───templates
│   │   │   │   ├───forms
│   │   │   │   │   └───fields
│   │   │   │   │       └───2fa_secret
│   │   │   │   └───partials
│   │   │   └───vendor
│   │   │       ├───bacon
│   │   │       │   └───bacon-qr-code
│   │   │       │       ├───src
│   │   │       │       │   ├───BaconQrCode
│   │   │       │       │   │   ├───Common
│   │   │       │       │   │   ├───Encoder
│   │   │       │       │   │   ├───Exception
│   │   │       │       │   │   └───Renderer
│   │   │       │       │   │       ├───Color
│   │   │       │       │   │       ├───Image
│   │   │       │       │   │       │   └───Decorator
│   │   │       │       │   │       └───Text
│   │   │       │       │   ├───Common
│   │   │       │       │   ├───Encoder
│   │   │       │       │   ├───Exception
│   │   │       │       │   └───Renderer
│   │   │       │       │       ├───Color
│   │   │       │       │       ├───Eye
│   │   │       │       │       ├───Image
│   │   │       │       │       ├───Module
│   │   │       │       │       │   └───EdgeIterator
│   │   │       │       │       ├───Path
│   │   │       │       │       └───RendererStyle
│   │   │       │       └───tests
│   │   │       │           └───BaconQrCode
│   │   │       │               ├───Common
│   │   │       │               ├───Encoder
│   │   │       │               └───Renderer
│   │   │       │                   └───Text
│   │   │       ├───birke
│   │   │       │   └───rememberme
│   │   │       │       ├───example
│   │   │       │       │   ├───css
│   │   │       │       │   ├───templates
│   │   │       │       │   └───tokens
│   │   │       │       ├───src
│   │   │       │       │   └───Rememberme
│   │   │       │       │       └───Storage
│   │   │       │       └───test
│   │   │       │           └───Storage
│   │   │       ├───composer
│   │   │       ├───dasprid
│   │   │       │   └───enum
│   │   │       │       ├───src
│   │   │       │       │   └───Exception
│   │   │       │       └───test
│   │   │       ├───paragonie
│   │   │       │   └───random_compat
│   │   │       │       ├───dist
│   │   │       │       ├───lib
│   │   │       │       └───other
│   │   │       │           └───ide_stubs
│   │   │       └───robthree
│   │   │           └───twofactorauth
│   │   │               ├───demo
│   │   │               ├───lib
│   │   │               │   └───Providers
│   │   │               │       ├───Qr
│   │   │               │       ├───Rng
│   │   │               │       └───Time
│   │   │               └───tests
│   │   └───youtube
│   │       ├───admin
│   │       │   └───editor-button
│   │       │       └───js
│   │       ├───classes
│   │       │   └───Twig
│   │       ├───css
│   │       └───templates
│   │           └───partials
│   └───themes
│       ├───learn2
│       │   ├───blueprints
│       │   ├───css
│       │   │   └───pure-0.5.0
│       │   ├───css-compiled
│       │   ├───fonts
│       │   ├───images
│       │   ├───js
│       │   ├───scss
│       │   │   ├───configuration
│       │   │   │   ├───nucleus
│       │   │   │   └───theme
│       │   │   ├───nucleus
│       │   │   │   ├───functions
│       │   │   │   ├───mixins
│       │   │   │   └───particles
│       │   │   ├───theme
│       │   │   │   └───modules
│       │   │   └───vendor
│       │   │       ├───bourbon
│       │   │       │   ├───addons
│       │   │       │   ├───css3
│       │   │       │   ├───functions
│       │   │       │   ├───helpers
│       │   │       │   └───settings
│       │   │       └───color-schemer
│       │   │           └───color-schemer
│       │   └───templates
│       │       └───partials
│       ├───learn2-git-sync
│       │   ├───blueprints
│       │   ├───css
│       │   ├───css-compiled
│       │   └───templates
│       │       └───partials
│       └───mytheme
│           ├───css
│           ├───images
│           └───templates
│               └───partials
├───vendor
│   ├───antoligy
│   │   └───dom-string-iterators
│   │       └───src
│   ├───bin
│   ├───composer
│   │   └───ca-bundle
│   │       ├───res
│   │       └───src
│   ├───doctrine
│   │   ├───cache
│   │   │   └───lib
│   │   │       └───Doctrine
│   │   │           └───Common
│   │   │               └───Cache
│   │   └───collections
│   │       └───lib
│   │           └───Doctrine
│   │               └───Common
│   │                   └───Collections
│   │                       └───Expr
│   ├───donatj
│   │   └───phpuseragentparser
│   │       └───Source
│   ├───erusev
│   │   ├───parsedown
│   │   └───parsedown-extra
│   ├───filp
│   │   └───whoops
│   │       └───src
│   │           └───Whoops
│   │               ├───Exception
│   │               ├───Handler
│   │               ├───Resources
│   │               │   ├───css
│   │               │   ├───js
│   │               │   └───views
│   │               └───Util
│   ├───gregwar
│   │   ├───cache
│   │   │   └───Gregwar
│   │   │       └───Cache
│   │   └───image
│   │       └───Gregwar
│   │           └───Image
│   │               ├───Adapter
│   │               ├───Exceptions
│   │               ├───images
│   │               └───Source
│   ├───guzzlehttp
│   │   └───psr7
│   │       └───src
│   ├───league
│   │   └───climate
│   │       └───src
│   │           ├───Argument
│   │           ├───ASCII
│   │           ├───Decorator
│   │           │   ├───Component
│   │           │   └───Parser
│   │           ├───Settings
│   │           ├───TerminalObject
│   │           │   ├───Basic
│   │           │   ├───Dynamic
│   │           │   │   ├───Animation
│   │           │   │   └───Checkbox
│   │           │   ├───Helper
│   │           │   └───Router
│   │           └───Util
│   │               ├───Reader
│   │               ├───System
│   │               └───Writer
│   ├───matthiasmullie
│   │   ├───minify
│   │   │   ├───data
│   │   │   │   └───js
│   │   │   └───src
│   │   │       └───Exceptions
│   │   └───path-converter
│   │       └───src
│   ├───maximebf
│   │   └───debugbar
│   │       └───src
│   │           └───DebugBar
│   │               ├───Bridge
│   │               │   ├───SwiftMailer
│   │               │   └───Twig
│   │               ├───DataCollector
│   │               │   └───PDO
│   │               ├───DataFormatter
│   │               │   └───VarDumper
│   │               ├───Resources
│   │               │   └───widgets
│   │               │       ├───mails
│   │               │       ├───sqlqueries
│   │               │       └───templates
│   │               └───Storage
│   ├───miljar
│   │   └───php-exif
│   │       └───lib
│   │           └───PHPExif
│   │               ├───Adapter
│   │               ├───Hydrator
│   │               ├───Mapper
│   │               └───Reader
│   ├───monolog
│   │   └───monolog
│   │       └───src
│   │           └───Monolog
│   │               ├───Formatter
│   │               ├───Handler
│   │               │   ├───Curl
│   │               │   ├───FingersCrossed
│   │               │   ├───Slack
│   │               │   └───SyslogUdp
│   │               └───Processor
│   ├───pimple
│   │   └───pimple
│   │       └───src
│   │           └───Pimple
│   │               ├───Exception
│   │               └───Psr11
│   ├───psr
│   │   ├───container
│   │   │   └───src
│   │   ├───http-message
│   │   │   └───src
│   │   ├───log
│   │   │   └───Psr
│   │   │       └───Log
│   │   │           └───Test
│   │   └───simple-cache
│   │       └───src
│   ├───rockettheme
│   │   └───toolbox
│   │       ├───ArrayTraits
│   │       │   └───src
│   │       ├───Blueprints
│   │       │   ├───src
│   │       │   └───tests
│   │       │       └───data
│   │       │           ├───blueprint
│   │       │           │   └───partials
│   │       │           ├───form
│   │       │           │   └───items
│   │       │           ├───input
│   │       │           └───schema
│   │       │               ├───defaults
│   │       │               ├───extra
│   │       │               ├───init
│   │       │               ├───merge
│   │       │               └───state
│   │       ├───DI
│   │       │   └───src
│   │       ├───Event
│   │       │   └───src
│   │       ├───File
│   │       │   └───src
│   │       ├───ResourceLocator
│   │       │   ├───src
│   │       │   └───tests
│   │       │       └───data
│   │       │           ├───base
│   │       │           │   └───all
│   │       │           ├───local
│   │       │           │   └───all
│   │       │           └───override
│   │       │               └───all
│   │       ├───Session
│   │       │   ├───src
│   │       │   └───tests
│   │       └───StreamWrapper
│   │           └───src
│   ├───seld
│   │   └───cli-prompt
│   │       ├───res
│   │       └───src
│   ├───symfony
│   │   ├───console
│   │   │   ├───Command
│   │   │   ├───Descriptor
│   │   │   ├───Event
│   │   │   ├───Exception
│   │   │   ├───Formatter
│   │   │   ├───Helper
│   │   │   ├───Input
│   │   │   ├───Logger
│   │   │   ├───Output
│   │   │   ├───Question
│   │   │   ├───Resources
│   │   │   │   └───bin
│   │   │   └───Style
│   │   ├───debug
│   │   │   ├───Exception
│   │   │   └───FatalErrorHandler
│   │   ├───event-dispatcher
│   │   │   ├───Debug
│   │   │   └───DependencyInjection
│   │   ├───polyfill-ctype
│   │   ├───polyfill-iconv
│   │   │   └───Resources
│   │   │       └───charset
│   │   ├───polyfill-mbstring
│   │   │   └───Resources
│   │   │       └───unidata
│   │   ├───var-dumper
│   │   │   ├───Caster
│   │   │   ├───Cloner
│   │   │   ├───Dumper
│   │   │   ├───Exception
│   │   │   └───Resources
│   │   │       └───functions
│   │   └───yaml
│   │       └───Exception
│   └───twig
│       └───twig
│           ├───lib
│           │   └───Twig
│           │       ├───Cache
│           │       ├───Error
│           │       ├───Extension
│           │       ├───Filter
│           │       ├───Function
│           │       ├───Loader
│           │       ├───Node
│           │       │   └───Expression
│           │       │       ├───Binary
│           │       │       ├───Filter
│           │       │       ├───Test
│           │       │       └───Unary
│           │       ├───NodeVisitor
│           │       ├───Profiler
│           │       │   ├───Dumper
│           │       │   ├───Node
│           │       │   └───NodeVisitor
│           │       ├───Sandbox
│           │       ├───Test
│           │       ├───TokenParser
│           │       └───Util
│           └───src
│               ├───Cache
│               ├───Error
│               ├───Extension
│               ├───Loader
│               ├───Node
│               │   └───Expression
│               │       ├───Binary
│               │       ├───Filter
│               │       ├───Test
│               │       └───Unary
│               ├───NodeVisitor
│               ├───Profiler
│               │   ├───Dumper
│               │   ├───Node
│               │   └───NodeVisitor
│               ├───RuntimeLoader
│               ├───Sandbox
│               ├───Test
│               ├───TokenParser
│               └───Util
```
