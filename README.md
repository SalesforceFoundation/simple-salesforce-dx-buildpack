# Simple Salesforce DX Buildpack

A more stripped down buildpack for Salesforce DX intended for apps that need the CLI only. Used by [SFDO-Tooling's](https://github.com/SFDO-Tooling/) web applications. 

## Release Channel
This buildpack installs the Salesforce CLI using unversioned TAR file URLs for the [`stable`](https://developer.salesforce.com/media/salesforce-cli/sfdx/channels/stable/sfdx-linux-x64.tar.xz) release channel. Set the `SFDX_CLI_URL` config var to select a different release channel or install a specific version. Optionally, set the `SALESFORCE_BUILDPACK_VERBOSE` and `SALESFORCE_BUILDPACK_DEBUG` config vars to troubleshoot build failures.

## JWT Authorization Flow
The buildpack will authorize a default SFDX Dev Hub using the JWT flow if the following config vars are set:
- `SFDX_CLIENT_ID`: Connected App Consumer key (i.e., `--client-id`)
- `SFDX_HUB_KEY`: The contents of your RSA private key (i.e., `--jwt-key-file`)
- `SFDX_HUB_USERNAME`: The Dev Hub username (i.e., `--username`)
- `SFDX_LOGIN_URL` (Optional): value overrides the default login URL (login.salesforce.com) 

## Salesforce CLI "just-in-time" (JIT) Plugins
When you run a command in a [JIT plugin](https://developer.salesforce.com/docs/atlas.en-us.sfdx_setup.meta/sfdx_setup/sfdx_setup_plugins_overview.htm) for the first time, Salesforce CLI installs the latest released version of the plugin and then runs the command. If the JIT plugin is not present in the build slug this could result in worker dynos repeatedly downloading and installing it. By default, the buildpack will call `plugin install` for each plugin listed in the `oclif:jitPlugins` property of the @salesforce/cli plugin [package.json](https://github.com/salesforcecli/cli/blob/main/package.json). To disable this behavior, set the `$SALESFORCE_BUILDPACK_JIT_INSTALL` config var to `false`. 
