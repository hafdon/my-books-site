# README

## Multilingual Book Translation Site with Hugo and OmegaT

This project is a multilingual website designed to display multiple books translated into English and Irish (Gaelic). It leverages the [Hugo](https://gohugo.io/) static site generator and [OmegaT](https://omegat.org/) for translation management.

---

## Table of Contents

- [README](#readme)
  - [Multilingual Book Translation Site with Hugo and OmegaT](#multilingual-book-translation-site-with-hugo-and-omegat)
  - [Table of Contents](#table-of-contents)
  - [Prerequisites](#prerequisites)
  - [Setup Instructions](#setup-instructions)
    - [1. Create a New Hugo Site](#1-create-a-new-hugo-site)
    - [2. Install the Hugo Book Theme](#2-install-the-hugo-book-theme)
  - [Content Organization](#content-organization)
    - [Content Files](#content-files)
    - [Front Matter Configuration](#front-matter-configuration)
  - [Translation Workflow with OmegaT](#translation-workflow-with-omegat)
    - [1. Set Up OmegaT Project](#1-set-up-omegat-project)
    - [2. Configure File Filters in OmegaT](#2-configure-file-filters-in-omegat)
    - [3. Translate Content](#3-translate-content)
    - [4. Export Translated Files](#4-export-translated-files)
  - [Multilingual Configuration](#multilingual-configuration)
  - [Running the Site Locally](#running-the-site-locally)
    - [Verify](#verify)
  - [Deployment](#deployment)
  - [Additional Resources](#additional-resources)
  - [Tips and Best Practices](#tips-and-best-practices)
  - [Running](#running)
  - [Specific issues](#specific-issues)
    - [Language Switcher Help](#language-switcher-help)
  - [Contributing](#contributing)
  - [License](#license)

---

## Prerequisites

- **Hugo** installed (version 0.92.0 or higher recommended)
  - [Installation Guide](https://gohugo.io/getting-started/installing/)
- **Git** for cloning and updating themes
- **OmegaT** for managing translations (Not integrated yet)
  - [Download OmegaT](https://omegat.org/download)

## Setup Instructions

### 1. Create a New Hugo Site

```bash
hugo new site my-books-site
cd my-books-site
```

### 2. Install the Hugo Book Theme

```bash
git init
git submodule add https://github.com/alex-shpak/hugo-book themes/hugo-book
```

## Content Organization

Organize your content in language-specific directories under `content/[lang]/docs`.

```
content/
├── en/docs/
│   └── the_corpse/
│       ├── _index.md
│       ├── chapter1.md
│       └── chapter2.md
└── ga/docs/
    └── the_corpse/
        ├── _index.md
        ├── chapter1.md
        └── chapter2.md
```

### Content Files

- **`_index.md`**: Acts as the homepage for each book.
- **`chapterX.md`**: Individual chapters of the book.

### Front Matter Configuration

Include the following in the front matter of each content file:

- **`title`**: Title of the chapter or book (translated accordingly).
- **`translationKey`**: Unique identifier to link translations across languages.
- **`weight`**: Determines the order of items in the navigation.

**Example for English `chapter1.md`:**

```markdown
---
title: "Chapter 1: The Beginning"
translationKey: "chapter1"
weight: 1
---

# Chapter 1: The Beginning

Content of Chapter 1 in English.
```

**Example for Irish `chapter1.md`:**

```markdown
---
title: "Caibidil 1: An Tosú"
translationKey: "chapter1"
weight: 1
---

# Caibidil 1: An Tosú

Ábhar Caibidil 1 i nGaeilge.
```

## Translation Workflow with OmegaT

### 1. Set Up OmegaT Project

- Create a new OmegaT project.
- Add your source language (`en`) Markdown files to the `source` folder.

### 2. Configure File Filters in OmegaT

- Enable Markdown file filters in OmegaT.
- Protect non-translatable content (front matter, code blocks) using regular expressions in the segmentation rules.

### 3. Translate Content

- Translate segments using OmegaT's editor.
- Utilize translation memories and glossaries for consistency.

### 4. Export Translated Files

- OmegaT generates translated Markdown files in the `target` folder.
- A `launchctl` watcher / deploy script combo copies the `.md` files to the proper folder in `my-books-site`

## Multilingual Configuration

- Hugo automatically handles multilingual content based on the `languages` section in `hugo.toml`.
- Use the same filenames and `translationKey` in front matter to link translations.
- Titles can differ between languages; Hugo will associate content based on `translationKey`.

## Running the Site Locally

Start the Hugo development server:

```bash
hugo server -D
```

- **English Version:** `http://localhost:1313/en/`
- **Irish Version:** `http://localhost:1313/ga/`

### Verify

- Navigation menus display correctly.
- Language switcher is visible and functioning.
- Table of Contents (TOC) appears on content pages with headers.

## Deployment

When ready to deploy the site:

```bash
hugo
```

- The static site will be generated in the `public/` directory.
- Host the `public/` directory on a static site hosting service like Netlify, GitHub Pages, or any web server.

## Additional Resources

- **Hugo Documentation**
  - [Official Docs](https://gohugo.io/documentation/)
  - [Multilingual Mode](https://gohugo.io/content-management/multilingual/)
- **Hugo Book Theme**
  - [GitHub Repository](https://github.com/alex-shpak/hugo-book)
  - [Theme Documentation](https://github.com/alex-shpak/hugo-book#readme)
- **OmegaT**
  - [Official Website](https://omegat.org/)
  - [User Documentation](https://omegat.org/documentation)
- **Markdown Syntax**
  - [Markdown Guide](https://www.markdownguide.org/basic-syntax/)

## Tips and Best Practices

- **Consistency is Key**: Ensure filenames and `translationKey` values are consistent across languages to link translations effectively.
- **Front Matter**: Keep front matter organized and include all necessary parameters (`title`, `translationKey`, `weight`).
- **Content Structure**: Mirror the directory structure in each language to maintain a coherent navigation experience.
- **Testing**: Regularly test your site locally to catch and fix issues early.
- **Version Control**: Use Git to track changes in your project and manage theme updates.

## Running

`hugo server --minify --theme hugo-book`

Run without cache

`hugo server --ignoreCache`

## Specific issues

### Language Switcher Help

See relevant `docs/language-switcher-help.md`

## Contributing

Contributions are welcome! Please submit a pull request or open an issue for suggestions and improvements.

## License

This project is licensed under the [MIT License](LICENSE).
