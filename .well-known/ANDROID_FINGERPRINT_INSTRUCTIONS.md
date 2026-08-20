# Android App Links Certificate Fingerprint

## Where to Get the SHA-256 Fingerprint

The `assetlinks.json` file currently contains a placeholder `SHA256_FINGERPRINT_HERE`. Replace it with the actual SHA-256 certificate fingerprint from one of these sources:

### Option 1: From Play Console (Recommended)
1. Go to Google Play Console
2. Navigate to **Release > Setup > App Signing**
3. Look for **App signing key certificate** section
4. Copy the **SHA-256 certificate fingerprint** (it will be a 64-character hex string with colons, like `AA:BB:CC:...`)
5. Replace `SHA256_FINGERPRINT_HERE` in `assetlinks.json` with this value (keep the colons)

### Option 2: From Local Keystore (Development)
If you have the keystore file locally:

```bash
keytool -list -v -keystore path/to/your-keystore.jks -alias your-key-alias
```

Look for the **SHA256** line in the output and copy the fingerprint.

### Option 3: From APK/AAB
If you have a signed APK or AAB:

```bash
# Extract signing certificate info
keytool -printcert -jarfile path/to/your-app.apk
```

## After Updating

Once you've replaced the placeholder with the real fingerprint:

1. Commit and push to the agreenow-web repo
2. Deploy to Cloudflare Pages (if not auto-deployed)
3. Verify the file is accessible at: `https://agreenow.app/.well-known/assetlinks.json`

## Testing

Test that Android App Links work:

```bash
adb shell am start -a android.intent.action.VIEW -d "https://agreenow.app/sign/test-agreement-id?token=test-token"
```

If configured correctly, this should open the AgreeNow app (if installed) instead of the browser.
