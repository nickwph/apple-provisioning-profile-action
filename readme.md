# Apple Provisioning Profile Action

Installing an Apple certificate on macOS runners for Xcode development.

More information can be found in [GitHub official documentation](https://docs.github.com/en/actions/deployment/deploying-xcode-applications/installing-an-apple-certificate-on-macos-runners-for-xcode-development).

## Encode profile as action secret 

```shell
base64 -i PROVISIONING_PROFILE.mobileprovision
```

## Installing build certificates

It is recommended to use [apple-build-certificate-action](https://github.com/nickwph/apple-build-certificate-action) at the same time to install the needed build certificates.

## Samaple usage

```yml
jobs:
  test:
    runs-on: macos-latest
    steps:
      - uses: actions/checkout@v3
      - uses: nickwph/apple-provisioning-profile-action@v1
        with:
          profile-base64: ${{ secrets.PROFILE_BASE64 }}
          profile-file: ${{ secrets.CERTIFICATE_PATH }}      # Optional: Ignored if profile-base64 is defined
      - uses: nickwph/apple-build-certificate-action@v1      # Optional: Recommend to use with apple-build-certificate-action
        with:
          certificate-base64: ${{ secrets.CERTIFICATE_BASE64 }}
          certificate-password: ${{ secrets.CERTIFICATE_PASSWORD }}
          certificate-file: ${{ secrets.CERTIFICATE_PATH }}  # Optional: Ignored if certificate-base64 is defined
```

