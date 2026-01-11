# Setup Instructions

## Step 1: Push to GitHub

```bash
cd /var/home/luke/git/flatpak-repo

# Create a new repository on GitHub named "flatpak-repo"
# Then push:
git remote add origin https://github.com/YOURUSERNAME/flatpak-repo.git
git push -u origin gh-pages
```

## Step 2: Enable GitHub Pages

1. Go to your GitHub repo: `https://github.com/YOURUSERNAME/flatpak-repo`
2. Go to **Settings** → **Pages**
3. Under "Source", select:
   - **Branch**: `gh-pages`
   - **Folder**: `/ (root)`
4. Click **Save**
5. Wait a few minutes for deployment

## Step 3: Run the Workflow

1. Go to **Actions** tab in your repository
2. Click on "Build Flatpak Repository" workflow
3. Click **Run workflow** button
4. Select `gh-pages` branch
5. Click **Run workflow**

This will:
- Clone both s-art and cryptomator-gtk
- Build them as Flatpaks
- Commit them to the OSTree repository
- Push to gh-pages (GitHub Pages will serve it)

## Step 4: Use Your Repository

Once the workflow completes and GitHub Pages deploys:

```bash
# Add your repository
flatpak remote-add --user --if-not-exists ljam96-repo https://YOURUSERNAME.github.io/flatpak-repo/repo

# Install apps
flatpak install ljam96-repo io.github.ljam96.sart
flatpak install ljam96-repo io.github.ljam96.cryptomatorgtk

# Updates work automatically
flatpak update
```

## Troubleshooting

### Workflow fails on first run?
- The workflow needs to create the OSTree repo first
- Run it again - second run usually succeeds

### GitHub Pages not working?
- Check Settings → Pages is enabled
- Ensure gh-pages branch is selected
- Wait 5-10 minutes for initial deployment

### Can't add remote?
- Ensure GitHub Pages URL is correct: `https://USERNAME.github.io/flatpak-repo/repo`
- Check that workflow completed successfully
- Verify `repo/` directory exists in gh-pages branch

## Updating Apps

To publish new versions, just re-run the workflow manually:
- Go to Actions → Build Flatpak Repository → Run workflow

Or set up webhooks from s-art/cryptomator-gtk repos to trigger automatically on releases.

## Next Steps

- Add GPG signing for security
- Automate builds on upstream releases
- Add more applications
- Consider applying to Flathub once apps mature
