# GitHub Actions Workflows

This directory contains GitHub Actions workflows for automated building, testing, and deployment of the Quran for Android app.

## Workflows

### Build Release APK (`release_apk.yml`)

A manually triggered workflow that builds a release APK for distribution.

**Trigger**: Manual (workflow_dispatch)

**Features**:
- Builds either a `release` or `beta` APK variant
- Uses local keystore and signing configuration from `keystore/` directory
- Uploads the built APK as a GitHub Actions artifact with 30-day retention

**Setup**:
1. Add your keystore file to `.github/workflows/keystore/release.keystore`
2. Update `.github/workflows/keystore/signing.properties` with your signing credentials
3. See [keystore/README.md](keystore/README.md) for detailed setup instructions

**Usage**:
1. Go to the [Actions tab](../../actions) in the GitHub repository
2. Select "Build Release APK" from the workflows list
3. Click "Run workflow"
4. Choose the build type (release or beta)
5. Click "Run workflow" to start the build
6. Once complete, download the APK from the workflow run artifacts

**Note**: This workflow uses local files for signing configuration, which is suitable for personal/private repositories. The `keystore/` directory contains a placeholder keystore - replace it with your own for production builds.

### Other Workflows

- **Pull Request (`build.yml`)**: Validates pull requests by building debug APK, running lint, and tests
- **Merge Queue (`merge.yml`)**: Builds debug APK for merge queue
- **Upload Dependency List and Debug App (`post_merge.yml`)**: Runs after merge to main branch, uploads debug APK and dependency list
- **Comment on Pull Request (`post_build.yml`)**: Posts APK diff and dependency diff comments on pull requests

