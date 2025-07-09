# GitHub Actions Workflows

## release-apk.yml

This workflow automatically builds and releases the Android APK when a new version tag is pushed.

### Trigger
- Runs on push to tags matching the pattern `v*.*.*` (e.g., `v1.0.0`, `v2.1.3`)

### Steps
1. **Checkout code** - Retrieves the repository code
2. **Set up Java 17** - Configures Java environment for Android builds
3. **Setup Gradle** - Configures Gradle with caching for faster builds
4. **Grant execute permission** - Makes gradlew executable
5. **Build Release APK** - Builds the release APK using `./gradlew assembleRelease`
6. **Upload APK as artifact** - Uploads the built APK as a GitHub Actions artifact

### Optional Features (Commented Out)

#### APK Signing
Uncomment the "Sign APK" step to enable automatic APK signing. You'll need to configure the following secrets:
- `SIGNING_KEY` - Base64-encoded signing key file
- `ALIAS` - Key alias
- `KEY_STORE_PASSWORD` - Keystore password
- `KEY_PASSWORD` - Key password

#### GitHub Release
Uncomment the "Create GitHub Release" step to automatically attach the APK to a GitHub Release. This uses the built-in `GITHUB_TOKEN` and creates a release with the tag name.

### Usage
To trigger a release:
```bash
git tag v1.0.0
git push origin v1.0.0
```

The workflow will automatically build and upload the APK as an artifact. If signing and release steps are enabled, it will also sign the APK and create a GitHub Release.