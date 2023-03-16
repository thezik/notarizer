# Notarizer

This is a simple bash script that I wrote to quickly sign, zip, notarize and staple a macOS app for distribution:

1. Signs the app using `codesign`
2. Zips the app using `ditto` to prepare to send package to Apple for notarization
3. Sends package to Apple for notarization using `notarytool` and waits for result
4. Staples the app using `stapler` so it's ready to be distributed

## Example

```
notarizer -d "Developer ID Application: My Company" -k my_appstoreconnect_profile "MyApplication.app"
```

## Prerequisites

Notarizer requires a valid Developer ID certificate to be installed in the keychain. Also, since it uses `notarytool`, you need to store App Store connect credentials in a profile on your keychain:

```
xcrun notarytool store-credentials --apple-id <app store connect username> --team-id <team id>
```

Notice that this will ask you for an app-specific Apple ID password and for a name to save the profile, that you will later use in notarizer.

To discover Developer Identity Name and team id use

```
security find-identity -p basic -v
```