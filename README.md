# Personal Flatpak Repository

Self-hosted Flatpak repository for distributing my Linux applications with automatic updates.

## Hosted Applications

- **s-art** - Steam Art Manager
- **cryptomator-gtk** - GTK frontend for Cryptomator

## For Users

### Add the repository

```bash
flatpak remote-add --user --if-not-exists ljam96-repo https://ljam96.github.io/flatpak-repo/repo
```

### Install applications

```bash
flatpak install ljam96-repo io.github.ljam96.sart
flatpak install ljam96-repo io.github.ljam96.cryptomatorgtk
```

### Update applications

```bash
flatpak update
```

## For Maintainer

### Build and publish new versions

The repository automatically builds applications from the main branches when triggered:

```bash
# Manual trigger via GitHub Actions UI
# Or trigger via API:
curl -X POST \
  -H "Accept: application/vnd.github.v3+json" \
  -H "Authorization: token YOUR_TOKEN" \
  https://api.github.com/repos/YOURUSERNAME/flatpak-repo/actions/workflows/build-repo.yml/dispatches \
  -d '{"ref":"gh-pages"}'
```

### Repository structure

```
flatpak-repo/
├── repo/           # OSTree repository (hosted via GitHub Pages)
├── index.html      # Repository info page
└── .github/
    └── workflows/
        └── build-repo.yml
```

## Technical Details

- **OSTree repository** format: archive-z2
- **Branch**: stable
- **Runtime**: GNOME 47
- **Hosting**: GitHub Pages
- **Build**: GitHub Actions with flatpak-builder

## Advantages Over Bundle Files

- ✅ Automatic updates via `flatpak update`
- ✅ Delta updates (only download changes)
- ✅ Easier installation (one-time remote add)
- ✅ Familiar Flatpak workflow for users
- ✅ No manual download/reinstall needed

## Future Improvements

- [ ] Add GPG signing for repository security
- [ ] Implement versioned branches (stable/beta)
- [ ] Add more applications
- [ ] Set up automatic builds on upstream releases
- [ ] Consider applying to Flathub when applications mature
