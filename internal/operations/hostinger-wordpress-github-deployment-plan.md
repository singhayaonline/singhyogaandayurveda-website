# Hostinger WordPress + GitHub Deployment Plan

## Purpose

This document explains how Singhaya Online should connect GitHub with Hostinger safely for WordPress website work.

The goal is to use GitHub as the master source for website content, documentation, custom code, and future deployment workflows without risking the live WordPress website.

---

## Important Rule

Do not deploy the entire WordPress installation from GitHub.

WordPress contains dynamic files and private data that should not be stored or deployed from this repository, such as:

- wp-config.php
- database files
- uploads containing client or student data
- backups
- plugin cache files
- private certificates
- customer records
- payment records

GitHub should be used for safe assets only:

- Website content drafts
- Brand documentation
- Custom CSS
- Child theme files
- Landing page templates
- SOPs and change logs
- Deployment notes

---

## Recommended Phase 1: Safe Manual Publishing

Use GitHub as the master content source.

Workflow:

```text
GitHub content draft
↓
Review content
↓
Copy approved content into WordPress page editor
↓
Preview page
↓
Publish / update page
↓
Record update in docs/change-log.md
```

This is the safest method for the current stage.

Recommended page to publish first:

```text
content/singhaya-online-page.md
```

WordPress page name:

```text
Singhaya Online
```

---

## Recommended Phase 2: GitHub Deployment for Custom Code Only

After the website structure is stable, GitHub can deploy only safe custom code to Hostinger.

Recommended deploy targets:

```text
wp-content/themes/child-theme/
wp-content/custom-css/
wp-content/mu-plugins/
```

Do not deploy:

```text
wp-config.php
wp-content/uploads/
wp-content/cache/
database.sql
backup.zip
```

---

## Hostinger Preparation Checklist

Before using GitHub Actions or Git deployment, prepare:

- SSH access enabled in Hostinger
- Correct server hostname
- SSH username
- SSH port
- Correct website path, usually similar to:

```text
/home/username/domains/domain.com/public_html/
```

or

```text
/home/username/public_html/
```

Confirm the exact path inside Hostinger File Manager or SSH terminal.

---

## GitHub Secrets Needed for Future Auto Deploy

Store secrets only in GitHub repository secrets, never inside files.

Recommended secret names:

```text
HOSTINGER_HOST
HOSTINGER_USER
HOSTINGER_PORT
HOSTINGER_SSH_KEY
HOSTINGER_TARGET_PATH
```

These should be added under:

```text
GitHub Repository → Settings → Secrets and variables → Actions → New repository secret
```

---

## Future GitHub Actions Concept

A future workflow can deploy only selected safe folders to Hostinger through SSH/rsync.

Example concept:

```text
Push to main branch
↓
GitHub Actions runs
↓
Connects to Hostinger via SSH
↓
Deploys only selected theme/custom-code folders
↓
WordPress remains safe
```

Do not activate auto deploy until:

- Website backup is available
- Target path is confirmed
- Child theme or deploy folder is clearly separated
- Test deploy has been completed

---

## Current Recommendation

For now, use GitHub as the content and documentation master.

Publish the Singhaya Online page manually in WordPress first.

Only after the page is working should Singhaya Online consider GitHub Actions deployment for selected custom code.

Version 1.0  
19 June 2026
