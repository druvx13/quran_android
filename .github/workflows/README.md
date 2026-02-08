# GitHub Actions Workflows

This directory contains GitHub Actions workflows for automated building, testing, and deployment of the Quran for Android app.

## Workflows

### Build Release APK (`release_apk.yml`)

A manually triggered workflow that builds a release APK for distribution.

**Trigger**: Manual (workflow_dispatch)

**Features**:
- Builds either a `release` or `beta` APK variant
- Supports signing with keystore (requires GitHub secrets configuration)
- Uploads the built APK as a GitHub Actions artifact with 30-day retention

**Usage**:
1. Go to the [Actions tab](../../actions) in the GitHub repository
2. Select "Build Release APK" from the workflows list
3. Click "Run workflow"
4. Choose the build type (release or beta)
5. Click "Run workflow" to start the build
6. Once complete, download the APK from the workflow run artifacts

**Required Secrets** (for signed builds):
- `KEYSTORE_BASE64`: Base64-encoded keystore file
- `STORE_PASSWORD`: Keystore password
- `KEY_ALIAS`: Key alias
- `KEY_PASSWORD`: Key password

**Note**: If secrets are not configured, the build will use default values from `app/gradle.properties` and may fail for release builds. Ensure proper signing configuration is set up in repository secrets for production releases.

### Other Workflows

- **Pull Request (`build.yml`)**: Validates pull requests by building debug APK, running lint, and tests
- **Merge Queue (`merge.yml`)**: Builds debug APK for merge queue
- **Upload Dependency List and Debug App (`post_merge.yml`)**: Runs after merge to main branch, uploads debug APK and dependency list
- **Comment on Pull Request (`post_build.yml`)**: Posts APK diff and dependency diff comments on pull requests
