---
layout: post
title: How to build a github page
categories: [Project, Github]
---

# Setting Up My Personal Homepage with GitHub Pages and Jekyll (Reverie Template)

## Introduction

I recently set up my personal homepage using GitHub Pages along with the Reverie Jekyll template. In this blog post, I'll walk you through the steps I took to get everything up and running, including automatic deployment using GitHub Actions.

## Prerequisites

Before starting, make sure you have the following installed on your local machine:
- Ruby
- Jekyll
- Bundler

You can install Jekyll and Bundler using the following commands:
```bash
gem install bundler jekyll
```

## Step-by-Step Guide

### 1. Choosing the Reverie Template

I opted for the Reverie Jekyll template for its clean design and ease of customization. You can find the Reverie template [here](https://github.com/amitmerchant1990/reverie).

### 2. Setting Up GitHub Repository

- Create a new repository on GitHub named `sunmaize.github.io`.
- Clone the repository to your local machine.

### 3. Configuring Jekyll

- Navigate to the cloned repository and initialize Jekyll:
  ```bash
  bundle install
  ```

### 4. Customizing Your Site

- Customize the `_config.yml` file to personalize your site settings.
- Modify the content in the `_posts` directory to include your own blog posts.

### 5. Local Testing

- Run the Jekyll server locally to preview your site:
  ```bash
  bundle exec jekyll serve
  ```
- Open your browser and go to `http://127.0.0.1:4000/` to view your site.

### 6. Automating Deployment with GitHub Actions

To automate deployment on GitHub Pages:
- Ensure your GitHub Pages setup is configured properly following the [GitHub Pages Quick Start guide](https://pages.github.com/).
- Commit and push to trigger GitHub Actions to build and deploy your site automatically whenever you push changes to the `main` branch.

## Conclusion

Setting up my personal homepage with GitHub Pages and the Reverie Jekyll template was straightforward, thanks to Jekyll's flexibility and GitHub Actions for seamless deployment. I'm excited to continue customizing and expanding my site to showcase my work and interests.

Feel free to explore the repository for this site at https://sunmaize.github.io/.

Happy coding!



