# XCode-Deploy 1.4
This action will archive, export, and upload your project or workspace to App Store Connect (TestFlight). 
It is designed to run on a containerized VM, such as a GitHub Hosted Runner.
If self-hosting, some of these steps may be unnecessary or redundant. 

## Inputs

### `xcode-version`

The version of XCode to use, in SemVer. Default is latest stable release: `xcode-latest`. See also [setup-xcode][0].

### `configuration`

The configuration to archive. Default is `Release`. See also `xcodebuild`'s `-configuration`. 

### `scheme`

The scheme to archive. If left blank, the action will search the project or workspace file for a default scheme. See also `xcodebuild`'s `-scheme`.

### `path-to-export-options`

The path to the `ExportOptions.plist` file, required for `-exportArchive`. Will default to `ExportOptions.plist` in the `${{ github.workspace }}` directory. See also `xcodebuild`'s `-exportArchive`.

### `update-build`

A boolean value that will set the `version-number` to the commit depth.  If false, nothing happens. See also `agvtool`'s `-new-version`.

### `distribution-certificate-p12`

The `base64` representation of your Apple/iOS Distribution Certificate and private key pair. 

### `distribution-certificate-password`

The password to unlock the Distribution Certificate and private key pair.

### `app-store-provisioning-profile`

The `base64` representation of your App Store Provisioning Profile. 

### `auth-key-id`

The ID of the Authentication Key provided by App Store Connect.

### `auth-key-issuer-id`

The Issuer ID provided by App Store Connect.

### `auth-key-p8`

The `base64` representation of the private key provided by App Store Connect.

Additionally, an `ExportOptions.plist` file must be included in the repository at the location and filename that matches `path-to-export-options`.
You can generate one of these by doing a local export in XCode and then copy it into your repository, or use `/usr/libexec/PlistBuddy`. 

## Sample Usage
```yml
- name: Deploy
  uses: vfrascello/xcode-deploy@v1.4
  with:
    xcode-version: '14.0'
    configuration: 'Release'
    scheme: 'MyScheme'
    path-to-export-options: 'ExportOptions.plist'
    update-build: true
    distribution-certificate-p12: ${{ secrets.DISTRIBUTION_CERTIFICATE_P12 }}
    distribution-certificate-password: ${{ secrets.DISTRIBUTION_CERTIFICATE_PASSWORD }}
    app-store-provisioning-profile: ${{ secrets.APPSTORE_PROVISIONING_PROFILE}}
    auth-key-id: ${{ secrets.AUTH_KEY_ID }}
    auth-key-issuer-id: ${{ secrets.AUTH_KEY_ISSUER_ID }}
    auth-key-p8: ${{ secrets.AUTH_KEY_P8 }}
```

See [action.yml][1] for more details.

## Contributions

This composite action was written by me, Vincent Frascello, but uses actions by other open-source contributors: 

[Maxim Lobanov][0]

[Oliver Jones][2]

[Florian Fried][3]

[Akio Jinsenji][4]

[Github Actions Team][5]

## License
Any contributions made under this project will be governed by the [MIT License][6].

[0]: https://github.com/maxim-lobanov/setup-xcode
[1]: https://github.com/vfrascello/xcode-deploy/blob/main/action.yml
[2]: https://github.com/orj
[3]: https://github.com/ffried
[4]: https://github.com/akiojin
[5]: https://github.com/actions
[6]: https://github.com/vfrascello/xcode-deploy/blob/main/LICENSE
