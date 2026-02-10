# Getting Dependabot Working on Your Juice Shop Fork

## The Issue

Forked this repo but Dependabot isn't opening any PRs? You're not alone - this is GitHub's default behavior for all forked repositories.

## Why This Happens

GitHub intentionally disables automated dependency tools on forks. Without this protection, every fork would receive automated PRs from bots, cluttering repositories that might just be for learning or experimentation. For Juice Shop forks used in training environments, you probably want this automation, so you'll need to opt-in.

## Activating Dependabot

Here's what to do on your fork:

**Step 1:** Open your repository on GitHub

**Step 2:** Click the "Settings" tab (rightmost tab in the repository navigation)

**Step 3:** Look for "Code security and analysis" in the left menu

**Step 4:** Toggle on these options:
- Dependabot alerts (notifies about vulnerable dependencies)
- Dependabot security updates (opens PRs for security patches)  
- Dependabot version updates (opens PRs for routine upgrades)

That's it! The `.github/dependabot.yml` file in this repo already contains the configuration.

## What Happens Next

Once activated:

- Dependabot scans `package.json` and `frontend/package.json`
- Checks run daily looking for updates
- PRs target the `develop` branch
- Each PR gets labeled with `dependencies`
- Updates appear for both backend and Angular frontend packages

You might see a burst of PRs initially if dependencies are outdated. This is normal.

## Important Note for Juice Shop

This project intentionally includes vulnerable dependencies for security training purposes. Check `.github/dependabot.yml` - you'll see several versions explicitly ignored:

```yaml
ignore:
  - dependency-name: "express-jwt"
    versions: ["0.1.3"]
  - dependency-name: "sanitize-html"
    versions: ["1.4.2"]
  # ... etc
```

These are learning exercises, not oversights. Don't update these manually.

## Still Having Problems?

**No PRs after 24 hours?**
Check Insights → Dependency graph → Dependabot to see job status and any error messages.

**Have an old config file?**
Delete `.dependabot/config.yml` if it exists - this legacy format conflicts with the newer `.github/dependabot.yml` and prevents it from running.

**Need help?**
Visit the [Gitter chat](https://gitter.im/bkimminich/juice-shop) or review [existing issues](https://github.com/juice-shop/juice-shop/issues) before opening a new one.

## Related Documentation

- [Juice Shop Contributing Guide](../CONTRIBUTING.md)
- [Troubleshooting in the companion book](https://pwning.owasp-juice.shop/companion-guide/latest/part4/troubleshooting.html)
