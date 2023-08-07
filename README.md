# Simple Salesforce DX Buildpack

A more stripped down buildpack for Salesforce DX intended for apps that need the CLI only. Used by [SFDO-Tooling's](https://github.com/SFDO-Tooling/) web applications. This buildpack installs the Salesforce CLI using unversioned TAR file URLs for the [`stable`](https://developer.salesforce.com/media/salesforce-cli/sfdx/channels/stable/sfdx-linux-x64.tar.xz) release channel. Set the `SFDX_CLI_URL` config var to select a different release channel or install a specific version. Optionally, set the `SALESFORCE_BUILDPACK_VERBOSE` and `SALESFORCE_BUILDPACK_DEBUG` config vars to troubleshoot build failures.

The buildpack will authorize a default SFDX Dev Hub using the JWT flow if the following config vars are set:
- `SFDX_CLIENT_ID`: Connected App Consumer key (i.e., `--client-id`)
- `SFDX_HUB_KEY`: The contents of your RSA private key (i.e., `--jwt-key-file`)
- `SFDX_HUB_USERNAME`: The Dev Hub username (i.e., `--username`)
- `SFDX_LOGIN_URL` (Optional): value overrides the default login URL (login.salesforce.com) 
