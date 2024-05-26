# My Trusted Package: NPM Lifecycle Script Example

![Ladybug in a box labeled "my trusted package"](https://github.com/jonchurch/my-trusted-package/raw/main/my-trusted-bug.jpg)

## It is a pleasure to have your trust.

`my-trusted-package` demonstrates the execution of npm lifecycle scripts during various stages of the npm package lifecycle. It is specifically designed for developers who want to understand and how these lifecycle events are triggered.

## Lifecycle Scripts

This package contains the following npm lifecycle scripts:

- **`preinstall`**: Triggered before the package installation begins.
  ```json
  "preinstall": "echo 'Trust preinstalling!' # (Running preinstall script)"
  ```

- **`postinstall`**: Triggered immediately after the package is installed.
  ```json
  "postinstall": "echo 'Trust Installed!' # (Running postinstall script)"
  ```

- **`preuninstall`**: Triggered before the package is uninstalled.
  ```json
  "preuninstall": "echo 'Trust preuninstalling!' # (Running preuninstall script)"
  ```

- **`postuninstall`**: Triggered after the package is uninstalled.
  ```json
  "postuninstall": "echo 'Trust postuninstalling!' # (Running postuninstall script)"
  ```

- **`prepare`**: Triggered in two scenarios: after the package is installed locally (not through the registry) and before the package is packed and published (e.g., during `npm publish` or `npm pack`).
  ```json
  "prepare": "echo 'Preparing Trust!' # (Running prepare script)"
  ```

## Installation

`npm@7` and above do not foreground output from dependency scripts, so you won't know that they've run unless you use `--foreground-scripts`:

```bash
npm install --foreground scripts my-trusted-package
```

Monitor the console to see the execution of lifecycle scripts and verify they ran.

## Disabling Lifecycle Scripts

To ensure that installation scripts do not execute, install the package with scripts disabled:

```bash
npm install my-trusted-package --ignore-scripts
```

## Importance of Disabling Install Scripts

As noted by [socket.dev](https://socket.dev/alerts/installScripts), install scripts are a common vector for malware distribution within the npm ecosystem. The majority of malware found in npm packages leverages these scripts, which often execute without thorough vetting by users.

Allowing install scripts to run automatically during npm installations introduces significant security risks. Install scripts execute with the same level of access as the user running the npm install command, which can lead to several severe security threats, including:

- **Modification or theft of data:** Scripts can alter or steal files accessible to the user.
- **Installation of malicious software:** Scripts can download and install additional malicious packages or software without the user's consent.
- **Unauthorized access to system resources:** Scripts may open backdoors for further exploitation by attackers.

### Suggested Practices

To effectively manage security risks associated with npm install scripts, you can employ the following technical configurations:

- **Use `--ignore-scripts`**: This command-line option prevents npm from executing any scripts defined in the package's `package.json` file during the installation process.
  ```bash
  npm install some-package --ignore-scripts
  ```
- **Persistently disable scripts**: You can set a global configuration in your `.npmrc` file to consistently prevent the execution of scripts during npm installations. This is done by adding the following line to your `.npmrc` file:
  ```plaintext
  ignore-scripts=true
  ```
