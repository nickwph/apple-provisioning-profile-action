# Apple Certificate Github Action

Installing an Apple certificate on macOS runners for Xcode development.

You can sign Xcode apps within your continuous integration (CI) workflow 
by installing an Apple code signing certificate on GitHub Actions runners.

Basically wrapping code from official documentation into a package.

https://docs.github.com/en/actions/deployment/deploying-xcode-applications/installing-an-apple-certificate-on-macos-runners-for-xcode-development

## Samaple usage

```yml
name: Main testing workflow
on: [push]
jobs:
  test:
    runs-on: macos-latest
    steps:
      - name: Checkout
        uses: actions/checkout@v3
      - name: Install certificates and profiles
        uses: nickwph/apple-certificate-action@v1
        with:
          build-certificate-base64: ${{ secrets.IOS_BUILD_CERTIFICATE_P12_BASE64 }}
          p12-password: ${{ secrets.IOS_BUILD_CERTIFICATE_P12_PASSWORD }}
          build-provision-profile-base64: ${{ secrets.IOS_BUILD_PROVISION_PROFILE_BASE64 }}
          keychain-password: ${{ secrets.MAC_MACHINE_KEYCHAIN_PASSWORD }}

```