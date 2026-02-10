# johnseverini.github.io

Personal academic website built with [Quarto](https://quarto.org/), hosted on GitHub Pages.

## Prerequisites

1. **Install Quarto**: Download from [https://quarto.org/docs/get-started/](https://quarto.org/docs/get-started/)
2. **Install Git**: Download from [https://git-scm.com/downloads](https://git-scm.com/downloads)
3. **VSCode** (recommended): Install the [Quarto extension](https://marketplace.visualstudio.com/items?itemName=quarto.quarto)

## Initial Setup

### Step 1: Add your images

Download these files from your WordPress site and place them in the `images/` folder:

- `hero.png` — The full Siege of La Rochelle painting (used as homepage hero background)
- `banner.png` — The cropped banner version (used on subpages)
- `headshot.jpg` — Your headshot photo

To download from WordPress:
1. Log in to your WordPress admin panel
2. Go to **Media → Library**
3. Click each image and download the original file
4. Rename and place them in `images/`

### Step 2: Add your CV

Place your CV PDF in the `files/` folder as `John_Severini-CV.pdf`.

### Step 3: Preview locally

Open a terminal in the project folder and run:

```bash
quarto preview
```

This will open the site in your browser at `localhost:4000` (or similar). Changes you make to `.qmd` files will auto-refresh.

### Step 4: Render the site

```bash
quarto render
```

This generates the static HTML in the `docs/` folder.

## Deploying to GitHub Pages

### Step 5: Create the GitHub repository

1. Go to [github.com/new](https://github.com/new)
2. Name the repository **`johnseverini.github.io`** (must match your GitHub username exactly)
3. Set it to **Public**
4. Do **not** initialize with a README (you already have one)
5. Click **Create repository**

### Step 6: Push to GitHub

In your terminal, from the project folder:

```bash
git init
git add .
git commit -m "Initial commit"
git branch -M main
git remote add origin https://github.com/JohnSeverini/johnseverini.github.io.git
git push -u origin main
```

### Step 7: Configure GitHub Pages

1. Go to your repository on GitHub
2. Navigate to **Settings → Pages**
3. Under **Source**, select **Deploy from a branch**
4. Set Branch to **main** and folder to **/docs**
5. Click **Save**

Your site will be live at `https://johnseverini.github.io` within a few minutes.

## Pointing Your Custom Domain

Once the GitHub Pages site is working:

### Step 8: Configure the custom domain in GitHub

1. In your repo, go to **Settings → Pages**
2. Under **Custom domain**, enter `johnseverini.com`
3. Click **Save**
4. Check **Enforce HTTPS** once DNS propagates

### Step 9: Update your DNS

At your domain registrar (wherever you bought `johnseverini.com`), update your DNS records:

**Option A — Apex domain (`johnseverini.com`):**

Create A records pointing to GitHub's IPs:
```
185.199.108.153
185.199.109.153
185.199.110.153
185.199.111.153
```

**Option B — Also add www subdomain:**

Create a CNAME record:
```
www → johnseverini.github.io
```

DNS propagation can take up to 48 hours, but usually completes within a few hours.

### Step 10: Create a CNAME file

Create a file called `CNAME` (no extension) in the `docs/` folder containing:

```
johnseverini.com
```

Alternatively, add this to `_quarto.yml` under the `website:` section so Quarto generates it automatically:

```yaml
website:
  site-url: https://johnseverini.com
```

And create the file `CNAME` in the project root — Quarto will copy it to `docs/` on render if you add it to `resources`:

```yaml
project:
  type: website
  output-dir: docs
  resources:
    - CNAME
```

## Updating Content

To update the site (e.g., adding a new publication):

1. Edit the relevant `.qmd` file in VSCode
2. Preview with `quarto preview`
3. Render with `quarto render`
4. Commit and push:

```bash
git add .
git commit -m "Added new publication"
git push
```

GitHub Pages will automatically redeploy.

## Project Structure

```
johnseverini.github.io/
├── _quarto.yml          # Site configuration
├── styles.css           # Custom CSS
├── index.qmd            # Homepage
├── about.qmd            # About page
├── cv.qmd               # CV page
├── research.qmd         # Research page
├── data.qmd             # Data page
├── policy-writing.qmd   # Policy Writing page
├── contact.qmd          # Contact page
├── images/              # Image assets
│   ├── hero.png         # Homepage hero image
│   ├── banner.png       # Subpage banner image
│   └── headshot.jpg     # About page headshot
├── files/               # Downloadable files
│   └── John_Severini-CV.pdf
├── docs/                # Rendered output (GitHub Pages serves this)
└── .nojekyll            # Tells GitHub not to process with Jekyll
```
