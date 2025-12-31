# SearchWiz Project Context

## Quick Reference

| Item | Value |
|------|-------|
| **Repo** | andyvadul/search_wiz |
| **Branch** | master |
| **Dev URL** | https://wp-dev-683-php84.searchwiz.ai |
| **Admin** | https://wp-dev-683-php84.searchwiz.ai/wp-admin/ |
| **Deploy** | `./scripts/deploy.sh dreamhost` |
| **Build** | `cd src/searchwiz && npm run build` |

## Active Projects (Priority Order)

1. **searchwiz** - WordPress plugin under WordPress.org review
2. **crosswalk** - FHIR budget mapping (separate repo: andyvadul/crosswalk)
3. **searchwiz.AI** - Paid AI upgrade features
4. **unwebsite.AI** - Serverless website automation (concept phase)

## Deployment Flows

### 1. Development Deployment (Automatic)
When changes are pushed to `master` in `src/searchwiz/`:
- Automated workflow: `.github/workflows/deploy-on-success.yml`
- Deploys to dev site: `wp-dev-683-php84.searchwiz.ai`
- Triggered by: Successful test runs

### 2. Demo Site Deployment (Manual)
To deploy to demo site `wpdemo.searchwiz.ai`:
- Add `deploy:demo` label to any GitHub issue
- Automated workflow: `.github/workflows/deploy-to-demo.yml`
- Requires user approval via issue label

### 3. WordPress.org SVN Deployment (Automatic)
When changes are pushed to `master` in `src/searchwiz/`:
- Automated workflow: `.github/workflows/sync-wporg.yml`
- Deploys to: `https://plugins.svn.wordpress.org/searchwiz/`
- Creates version tags automatically
- Requires secrets: `WORDPRESS_SVN_USER`, `WORDPRESS_SVN_PASS`

### Manual Local Deployment
```bash
# Build and deploy to dev site
./scripts/deploy.sh dreamhost

# Deploy directly to WordPress.org SVN (requires credentials)
./scripts/deploy-wporg.sh
```

## Common Commands

```bash
# Build plugin assets
cd src/searchwiz && npm run build && cd ../..

# Deploy to test server (local script)
./scripts/deploy.sh dreamhost

# Full commit + deploy cycle
git add -A && git commit -m "type: message" && git push origin master && ./scripts/deploy.sh dreamhost

# Check GitHub issues
gh issue list -R andyvadul/search_wiz

# View specific issue
gh issue view <number> -R andyvadul/search_wiz --comments
```

## Code Style

- **PHP**: WordPress Coding Standards, prefix functions with `searchwiz_`
- **JavaScript**: ESLint, use `searchWiz` namespace
- **CSS**: Stylelint, BEM naming
- **Commits**: `type(scope): message` (feat, fix, docs, refactor, test, chore)

## WordPress Plugin Structure

```
src/searchwiz/
├── searchwiz.php          # Main plugin file
├── includes/              # Core functionality
├── admin/                 # Admin interface
│   ├── class-sw-admin.php
│   ├── js/               # Admin JavaScript
│   └── partials/         # Admin templates
├── public/               # Frontend
│   ├── js/              # Public JavaScript
│   └── css/             # Public styles
└── languages/           # i18n
```

## Key Classes

- `SearchWiz` - Main plugin class
- `SearchWiz_Admin` - Admin functionality
- `SearchWiz_Settings_Fields` - Settings API
- `SearchWiz_Ajax_Handler` - AJAX endpoints

## Testing

- **PHP**: PHPUnit (run from src/searchwiz)
- **JS**: Jest (run from src/searchwiz)
- **Manual**: Test on https://wp-dev-683-php84.searchwiz.ai

## WordPress.org Review

- Check email: andy@searchwiz.ai for review feedback
- Key requirements: No external requests without consent, proper escaping, nonce verification
- See: `docs/open_items/WordPress_Plugin_Resubmission_Response.md`

## Pro Features (docs/pro-specs/)

12 planned features for paid version:
1. Complete mockup screens
2. Licensing (Freemius)
3. ChatGPT conversational search (frontend)
4. Conversational action config (backend)
5. Multi-language/multi-site
6. Advanced analytics dashboard
7. Synonym/stopword management
8. Performance optimization
9. Advanced custom field indexing
10. Custom result templates
11. Faceted search filters
12. Smart search widgets

## Owner Availability

- **Mon, Tue, Fri, Sat, Sun**: At home, full local infrastructure access
- **Wed, Thu**: In office, limited access (Dreamhost only during breaks)
- **Escalate**: Only for critical decisions, blockers >4 hours, or security issues
