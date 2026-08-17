# Argon

Custom Fedora Atomic images built with [BlueBuild](https://blue-build.org) and based on [Universal Blue](https://universal-blue.org).

Includes extra packages, tweaks, and Flatpaks I use, so I don't have to set everything up manually after every reinstall or rebase.

## Usage

To rebase an existing Silverblue install onto this image:

1. Switch to the image (use `argon-nvidia` if you have an NVIDIA GPU):

   ```bash
   sudo bootc switch ghcr.io/azuriteflow/argon:latest
   ```

   ```bash
   sudo bootc switch ghcr.io/azuriteflow/argon-nvidia:latest
   ```

2. Reboot to complete the rebase:

   ```bash
   sudo systemctl reboot
   ```

## Updating

To update the image manually:

```bash
sudo bootc upgrade
```

### Firmware updates

```bash
ujust update-firmware
```

### Secure Boot

If Secure Boot is enabled, enroll the signing keys after the first rebase (required for the NVIDIA kernel module):

```bash
ujust enroll-secure-boot-key
```

## Build schedule

The image is rebuilt every 2 days at 06:15 UTC via GitHub Actions, or manually via the "Run workflow" button.

## Verification

These images are signed with Sigstore's cosign. To verify the signature, download `cosign.pub` from this repo and run (pick the image you use):

For NVIDIA systems:
```bash
cosign verify --key cosign.pub ghcr.io/azuriteflow/argon-nvidia
```
For non-NVIDIA systems:
```bash
cosign verify --key cosign.pub ghcr.io/azuriteflow/argon
```

> [!NOTE]
> This image is built for my own use. Feel free to fork it and adapt it to your needs, but don't expect it to work out of the box for your setup.
