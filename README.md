# Scripts to use with git-credential-libsecret

Git includes a [libsecret](https://wiki.gnome.org/Projects/Libsecret) credential helper (git-credential-libsecret`) under `/usr/share/doc/git/contrib/credential/libsecret` (Debian/Ubuntu) that can be used to interface Git with the `libsecret` keyring.

This repository contains a simple script `git-credential-libsecret-add-https` that can be used to add passwords to the libsecret keyring using the `git-credential-libsecret` credential helper.

**NOTE:** You don't need this if you use [Git Credential Manager](https://github.com/GitCredentialManager/git-credential-manager).

# Requirements

* `git-credential-libsecret` should be in `$PATH`
* `zenity` (for the gtk form)
* `seahorse` (optional)

# Example: Adding a GitHub PAT

## Step 1: Configure the credential helper

Use `git config --global credential.helper $(which git-credential-libsecret)` to configure the libsecrets credential helper globally or `git config --credential.helper $(which git-credential-libsecret)` to configure it locally for the project you're in.

## Step 2: Add the credentials to the keyring

Run `./git-credential-libsecret-add-https` and fill out the form like this to add a github PAT:

| Host (e.g GitHub.com) | github.com  |
|-----------------------|-------------|
| Username              | mygithubuser|
| Password              | myPAT!2232_ |

Click on **OK** afterwards. On success, the GNOME keyring GUI (seahorse) will be opened where you can inspect the added key.

That's it, now `git push` operations should read credentials from the `libsecrets` keyring instead of displaying a CLI prompt.

# Wishlist/Notes

Eventually, this script will be rendered obselete if `seahorse` or a different libsecrets frontend provides built-in functionality to add custom authentication keys.
