# Updating from the al-folio Template

This site is based on [al-folio](https://github.com/alshedivat/al-folio). The template remote is already configured:

```bash
git remote -v
# template  https://github.com/alshedivat/al-folio.git
```

## Standard Update Process

Since the repository shares git history with the template (from v0.16.3 onwards), updating is a straightforward merge:

```bash
# 1. Fetch the latest template tags and branches
git fetch template

# 2. Check available versions
git tag --list 'v*' --sort=-v:refname | head -5

# 3. Merge the desired version
git merge v0.X.Y

# 4. Resolve any conflicts (your customizations vs template changes)
# 5. Test locally
docker compose up --build

# 6. Commit and push
```

## If the Template Remote Is Missing

```bash
git remote add template https://github.com/alshedivat/al-folio.git
git fetch template
```

## Conflict Resolution Tips

- **Your content files** (`_bibliography/papers.bib`, `assets/json/resume.json`, `_data/socials.yml`): always keep your version.
- **Template infrastructure** (`_layouts/`, `_includes/`, `_sass/`, `_plugins/`): prefer the template's version unless you made intentional customizations.
- **Config** (`_config.yml`): merge carefully — keep your site metadata but accept new template settings.
- **Docker files** (`Dockerfile`, `docker-compose.yml`): accept template updates but keep `FROM ruby:3.3-slim` (Ruby 4.0 has bundler compatibility issues).

## History

- **v0.14.6 → v0.16.3** (March 2026): Initial major update. Since the repo originally had unrelated histories, the update was done by creating a new branch from `v0.16.3` and cherry-picking the 12 custom commits on top. The old main was backed up as tag `backup-main-before-template-update`.
