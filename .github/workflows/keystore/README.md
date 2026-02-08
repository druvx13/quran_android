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

- **STORE_FILE**: Path to your keystore (default: `.github/workflows/keystore/release.keystore`)
- **STORE_PASSWORD**: Your keystore password
- **KEY_ALIAS**: Your key alias
- **KEY_PASSWORD**: Your key password

Example:
```properties
STORE_FILE=.github/workflows/keystore/release.keystore
STORE_PASSWORD=MySecurePassword123
KEY_ALIAS=my_release_key
KEY_PASSWORD=MyKeyPassword123
```

### 3. Verify Setup

Make sure your `release.keystore` file exists in this directory and the `signing.properties` file has the correct credentials.

## Security Note

⚠️ **WARNING**: This approach stores your keystore and credentials in the repository. This is only suitable for:
- Personal projects
- Private repositories
- Development/testing purposes

For production apps or public repositories, use GitHub Secrets instead.

## Files in This Directory

- `release.keystore` - Your Android keystore file (add your own)
- `signing.properties` - Signing configuration (update with your credentials)
- `README.md` - This file
