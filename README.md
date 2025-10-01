# Personal Portfolio Website

A modern, responsive personal portfolio website built with [Hugo](https://gohugo.io/) and the [Toha](https://github.com/hugo-toha/toha) theme. This site is deployed on GitHub Pages and showcases professional experiences, projects, skills, and blog posts.

🌐 **Live Site**: [https://kaleby.github.io/](https://kaleby.github.io/)

![Hugo](https://img.shields.io/badge/Hugo-FF4088?style=flat&logo=hugo&logoColor=white)
![GitHub Pages](https://img.shields.io/badge/GitHub%20Pages-222222?style=flat&logo=github&logoColor=white)
![License](https://img.shields.io/badge/License-MIT-blue.svg)

## 📋 Table of Contents

- [Features](#-features)
- [Tech Stack](#-tech-stack)
- [Prerequisites](#-prerequisites)
- [Quick Start](#-quick-start)
- [Project Structure](#-project-structure)
- [Customization Guide](#-customization-guide)
- [Deployment](#-deployment)
- [Common Commands](#-common-commands)
- [Learning Resources](#-learning-resources)
- [Contributing](#-contributing)

## ✨ Features

- **Responsive Design**: Mobile-first design that looks great on all devices
- **Multi-Section Portfolio**: Includes sections for About, Skills, Experience, Education, Projects, and Blog
- **Dark/Light Mode**: Theme switching capability
- **Markdown Blog**: Write blog posts in Markdown with syntax highlighting
- **SEO Optimized**: Built-in SEO best practices and OpenGraph support
- **Fast Performance**: Static site generation for lightning-fast page loads
- **Easy Customization**: YAML-based configuration for easy content management

## 🛠 Tech Stack

- **[Hugo](https://gohugo.io/)** - Fast and flexible static site generator
- **[Toha Theme](https://github.com/hugo-toha/toha)** - Beautiful portfolio theme
- **[Bootstrap 5](https://getbootstrap.com/)** - CSS framework
- **[Font Awesome](https://fontawesome.com/)** - Icons
- **[GitHub Pages](https://pages.github.com/)** - Free hosting

## 📦 Prerequisites

Before you begin, ensure you have the following installed:

- **Hugo Extended** (v0.118.0 or later)
  ```bash
  # macOS
  brew install hugo
  
  # Windows (using Chocolatey)
  choco install hugo-extended
  
  # Linux (using Snap)
  snap install hugo
  ```

- **Git** (for cloning and submodule management)
  ```bash
  # Verify installation
  git --version
  ```

- **Node.js** (v16 or later, optional - for theme development)
  ```bash
  node --version
  ```

## 🚀 Quick Start

### 1. Clone the Repository

```bash
git clone https://github.com/kaleby/personal-website.git
cd personal-website
```

### 2. Initialize Submodules

The Toha theme is included as a Git submodule, so you need to initialize it:

```bash
git submodule update --init --recursive
```

### 3. Install Dependencies (Optional)

If you want to modify the theme:

```bash
cd personal
npm install
```

### 4. Run Local Development Server

```bash
cd personal
hugo server -D
```

Your site will be available at `http://localhost:1313/`

The `-D` flag includes draft content. Remove it to see only published content.

## 📁 Project Structure

```
personal-website/
├── personal/                  # Main Hugo site directory
│   ├── archetypes/           # Content templates
│   ├── assets/               # Raw assets (images, CSS, JS)
│   │   ├── css/             # Custom stylesheets
│   │   └── images/          # Site images
│   ├── content/              # Content files
│   │   ├── posts/           # Blog posts
│   │   └── notes/           # Note pages
│   ├── data/                 # Data files
│   │   └── en/              # English content data
│   │       ├── author.yaml  # Author information
│   │       ├── site.yaml    # Site metadata
│   │       └── sections/    # Section configurations
│   │           ├── about.yaml
│   │           ├── experiences.yaml
│   │           ├── projects.yaml
│   │           ├── skills.yaml
│   │           ├── education.yaml
│   │           ├── accomplishments.yaml
│   │           └── recent-posts.yaml
│   ├── layouts/              # Custom layouts (overrides)
│   ├── public/               # Generated site (don't edit)
│   ├── static/               # Static files (copied as-is)
│   ├── themes/               # Hugo themes
│   │   └── toha/            # Toha theme (submodule)
│   ├── hugo.toml            # Hugo configuration
│   └── package.json         # Node dependencies
├── CV_Kaleby_US.pdf         # Resume/CV file
└── README.md                # This file
```

## 🎨 Customization Guide

### Editing Site Configuration

Edit `personal/hugo.toml` to configure:

```toml
baseURL = 'https://yourusername.github.io/'  # Your GitHub Pages URL
title = 'Your Name - Personal Portfolio'     # Site title
theme = 'toha'

[params]
  background = "images/hero.jpg"              # Hero background image
  accent = "blue"                             # Theme color
  gitRepo = "https://github.com/yourusername/personal-website"
```

### Updating Personal Information

Edit `personal/data/en/author.yaml`:

```yaml
name: "Your Name"
designation: "Your Title"
location: "Your City, Country"
image: "images/author/your-photo.png"
```

### Adding Projects

Edit `personal/data/en/sections/projects.yaml`:

```yaml
projects:
  - name: Project Name
    logo: /images/sections/projects/project-logo.png
    role: Your Role
    timeline: "Jan 2024 - Present"
    repo: https://github.com/username/project
    summary: Project description
    tags: ["tag1", "tag2"]
```

### Adding Experience

Edit `personal/data/en/sections/experiences.yaml`:

```yaml
experiences:
  - company:
      name: Company Name
      url: "https://company.com"
      logo: /images/sections/companies/company-logo.png
    positions:
      - designation: Your Position
        start: Jan 2024
        responsibilities:
          - Responsibility 1
          - Responsibility 2
```

### Adding Blog Posts

Create a new markdown file in `personal/content/posts/`:

```markdown
---
title: "Your Post Title"
date: 2025-10-01
description: "Post description"
tags: ["tag1", "tag2"]
---

Your content here...
```

### Customizing Styles

Add custom CSS to `personal/assets/css/custom.css`:

```css
/* Your custom styles */
.custom-section {
  background-color: #f5f5f5;
}
```

## 🚀 Deployment

### GitHub Pages Deployment

#### Option 1: Manual Deployment

1. Build the site:
   ```bash
   cd personal
   hugo --minify
   ```

2. The generated files will be in `personal/public/`

3. Push to `gh-pages` branch or configure GitHub Pages to use the `main` branch

#### Option 2: GitHub Actions (Recommended)

Create `.github/workflows/hugo.yml`:

```yaml
name: Deploy Hugo site to GitHub Pages

on:
  push:
    branches: ["main"]
  workflow_dispatch:

permissions:
  contents: read
  pages: write
  id-token: write

concurrency:
  group: "pages"
  cancel-in-progress: false

defaults:
  run:
    shell: bash

jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v4
        with:
          submodules: recursive
          fetch-depth: 0

      - name: Setup Hugo
        uses: peaceiris/actions-hugo@v2
        with:
          hugo-version: 'latest'
          extended: true

      - name: Build with Hugo
        run: |
          cd personal
          hugo --minify --baseURL "${{ steps.pages.outputs.base_url }}/"

      - name: Upload artifact
        uses: actions/upload-pages-artifact@v3
        with:
          path: ./personal/public

  deploy:
    environment:
      name: github-pages
      url: ${{ steps.deployment.outputs.page_url }}
    runs-on: ubuntu-latest
    needs: build
    steps:
      - name: Deploy to GitHub Pages
        id: deployment
        uses: actions/deploy-pages@v4
```

#### Configure GitHub Pages

1. Go to your repository **Settings** → **Pages**
2. Under "Build and deployment":
   - **Source**: GitHub Actions
3. Save and wait for the workflow to complete

Your site will be available at `https://yourusername.github.io/`

## 💻 Common Commands

```bash
# Start development server
hugo server -D

# Start server with live reload
hugo server --disableFastRender

# Build production site
hugo --minify

# Create new blog post
hugo new posts/my-new-post.md

# Update theme
git submodule update --remote --merge

# Check Hugo version
hugo version

# Clean generated files
rm -rf public resources
```

## 📚 Learning Resources

### Hugo Documentation
- [Hugo Official Docs](https://gohugo.io/documentation/)
- [Hugo Quick Start](https://gohugo.io/getting-started/quick-start/)
- [Hugo Content Management](https://gohugo.io/content-management/)

### Toha Theme
- [Toha Documentation](https://toha-guides.netlify.app/)
- [Toha GitHub Repository](https://github.com/hugo-toha/toha)
- [Toha Examples](https://toha-guides.netlify.app/posts/)

### GitHub Pages
- [GitHub Pages Docs](https://docs.github.com/en/pages)
- [Custom Domain Setup](https://docs.github.com/en/pages/configuring-a-custom-domain-for-your-github-pages-site)

### Tutorials
- [Hugo + GitHub Pages Tutorial](https://gohugo.io/hosting-and-deployment/hosting-on-github/)
- [Markdown Guide](https://www.markdownguide.org/)

## 🤝 Contributing

This is a personal website, but if you find any issues or have suggestions for improvements, feel free to:

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/improvement`)
3. Commit your changes (`git commit -am 'Add some improvement'`)
4. Push to the branch (`git push origin feature/improvement`)
5. Open a Pull Request

## 📄 License

This project is open source and available under the [MIT License](LICENSE).

The Toha theme is also licensed under the MIT License. See the [theme license](personal/themes/toha/LICENSE) for more information.

## 🙏 Acknowledgments

- [Hugo](https://gohugo.io/) - The world's fastest framework for building websites
- [Toha Theme](https://github.com/hugo-toha/toha) - Beautiful and feature-rich portfolio theme
- [GitHub Pages](https://pages.github.com/) - Free hosting for static sites

## 📞 Contact

Feel free to reach out if you have questions or want to connect!

---

**Note**: This README serves as both documentation for this specific site and as a learning resource for anyone wanting to create their own portfolio website using Hugo and GitHub Pages. Feel free to use this as a template for your own projects!

Made with ❤️ using Hugo and GitHub Pages
