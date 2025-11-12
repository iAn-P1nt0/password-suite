# Publishing Guide

## Pre-Publication Checklist

- [x] All tests passing (59/59)
- [x] Build successful (ESM + CJS)
- [x] TypeScript types generated
- [x] README complete
- [x] LICENSE file present
- [x] package.json configured correctly
- [x] CI/CD workflows in place

## Publishing to npm

### First Time Setup

1. **Login to npm:**
   ```bash
   npm login
   ```

2. **Verify package name is available:**
   ```bash
   npm search @trustvault/password-utils
   ```

### Publishing

1. **Dry run to verify package contents:**
   ```bash
   npm pack --dry-run
   ```

2. **Publish the package:**
   ```bash
   npm publish --access public
   ```

### Automated Publishing (Recommended)

The repository includes a GitHub Actions workflow that automatically publishes to npm when you create a release:

1. **Create a GitHub release:**
   - Go to GitHub repository → Releases → Create new release
   - Tag version: `v1.0.0`
   - Release title: `v1.0.0 - Initial Release`
   - Add release notes

2. **Add NPM_TOKEN secret:**
   - Go to npm → Account → Access Tokens
   - Generate new token (Automation type)
   - Go to GitHub repository → Settings → Secrets → Actions
   - Add secret: `NPM_TOKEN` = your token

3. **Workflow will automatically:**
   - Run tests
   - Build package
   - Publish to npm with provenance

## Version Management

Update version in `package.json` following semantic versioning:
- Patch: `1.0.1` - Bug fixes
- Minor: `1.1.0` - New features (backward compatible)
- Major: `2.0.0` - Breaking changes

```bash
npm version patch  # 1.0.0 → 1.0.1
npm version minor  # 1.0.0 → 1.1.0
npm version major  # 1.0.0 → 2.0.0
```

## Post-Publication

### Verify Installation

```bash
npm install @trustvault/password-utils
```

### Test the Published Package

```javascript
// test-published.mjs
import { generatePassword, getDefaultOptions } from '@trustvault/password-utils';

const result = generatePassword(getDefaultOptions());
console.log(result.password);
```

### Update Documentation

- Add npm badge to README
- Update version references
- Announce on relevant channels

## Package Stats

- **Size**: ~19 KB (gzipped)
- **Dependencies**: 2 (zxcvbn, @noble/hashes)
- **Exports**: 15+ functions
- **Test Coverage**: 59 tests

## Support

For issues or questions:
- GitHub Issues: https://github.com/indi-gamification-initiative/TrustVault-password-utils/issues
- npm: https://www.npmjs.com/package/@trustvault/password-utils
