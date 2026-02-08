# Keystore Configuration

This directory contains the keystore and signing configuration for building release APKs.

## Setup Instructions

### 1. Generate or Add Your Keystore

If you don't have a keystore yet, generate one:

```bash
keytool -genkey -v -keystore release.keystore -alias your_alias -keyalg RSA -keysize 2048 -validity 10000
```

Or copy your existing keystore file here:

```bash
cp /path/to/your/keystore.jks .github/workflows/keystore/release.keystore
```

### 2. Update Signing Configuration

Edit `signing.properties` and update the following values:

- **STORE_FILE**: Path to your keystore relative to the `app/` directory (default: `../.github/workflows/keystore/release.keystore`)
- **STORE_PASSWORD**: Your keystore password
- **KEY_ALIAS**: Your key alias
- **KEY_PASSWORD**: Your key password

Example:
```properties
# Note: Path must be relative to the app/ directory (hence the ../)
STORE_FILE=../.github/workflows/keystore/release.keystore
STORE_PASSWORD=MySecurePassword123
KEY_ALIAS=my_release_key
KEY_PASSWORD=MyKeyPassword123
```

### 3. Verify Setup

Make sure your `release.keystore` file exists in this directory and the `signing.properties` file has the correct credentials.

**Important**: The `STORE_FILE` path must be relative to the `app/` directory since that's where Gradle resolves file paths during the build. The `../` prefix navigates up from `app/` to the project root.

## How It Works

During the GitHub Actions release workflow:
1. The workflow loads `signing.properties` and appends it to `app/gradle.properties`
2. Gradle reads the signing config from `app/gradle.properties`
3. The `STORE_FILE` path is resolved relative to the `app/` directory
4. The keystore at `../.github/workflows/keystore/release.keystore` is used for signing

## Security Note

⚠️ **WARNING**: This approach stores your keystore and credentials in the repository. This is only suitable for:
- Personal projects
- Private repositories
- Development/testing purposes

For production apps or public repositories, use GitHub Secrets instead.

## Files in This Directory

- `release.keystore` - Your Android keystore file (ready to use with default credentials)
- `signing.properties` - Signing configuration (configured with default credentials)
- `README.md` - This file
