# Meshack's Portfolio

A high-performance personal portfolio and blog built for a Senior Full Stack Engineer.

**Live Site**: [https://meshack-vs-you-all.github.io/meshack-hugo-portfolio/](https://meshack-vs-you-all.github.io/meshack-hugo-portfolio/)

## 🚀 Tech Stack

-   **Framework**: [Hugo](https://gohugo.io/) (Fastest SSG)
-   **Theme**: [Blowfish](https://blowfish.page/) (Tailwind CSS based)
-   **Hosting**: GitHub Pages
-   **CI/CD**: GitHub Actions

## 🛠️ Local Development

1.  **Clone the repository**:
    ```bash
    git clone --recursive git@github.com:meshack-vs-you-all/meshack-hugo-portfolio.git
    cd meshack-hugo-portfolio
    ```

2.  **Install Hugo**:
    -   Ensure you have `hugo-extended` installed.

3.  **Run the server**:
    ```bash
    hugo server -D
    ```
    Visit `http://localhost:1313`.

## 📦 Deployment

This project uses **GitHub Actions** for deployment.

1.  Push changes to the `main` branch.
2.  The workflow `.github/workflows/hugo.yaml` will automatically:
    -   Install dependencies.
    -   Build the site using Hugo.
    -   Deploy the `public/` folder to GitHub Pages.

### Important Configuration
-   **`hugo.toml`**: Contains the `baseURL` setting. This MUST match the repository name for assets to load correctly on GitHub Pages.
-   **`content/`**: Markdown files for pages and blog posts.

## 📝 Managing Content

-   **Posts**: Create new articles in `content/posts/`.
-   **Projects**: Managed in `content/projects/`.
-   **About**: Edit `content/about/index.md`.
