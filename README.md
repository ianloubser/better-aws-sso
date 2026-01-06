# AWS SSO Login

A lightweight, bash-native AWS SSO login tool. No additional dependencies beyond the AWS CLI—just pure bash.

## Features

- **Zero dependencies** — Uses only AWS CLI, works anywhere bash runs
- **Interactive account & role selection** — Browse and select from your available AWS accounts and roles
- **Session management** — Check TTL, refresh credentials, or deactivate cleanly
- **Visual prompt** — Shows current role and account in your shell prompt
- **Cross-platform** — Works on macOS, Linux, and WSL

## Quick Start

### 1. Download the script

```bash
curl -fsSL https://raw.githubusercontent.com/ianloubser/better-aws-sso/main/aws-sso -o ~/bin/aws-sso
chmod +x ~/bin/aws-sso
```

> **Note:** Replace `YOUR_USERNAME` with your GitHub username, and adjust the path if needed.

### 2. Configure your SSO settings

Open the script and update the configuration section at the top:

```bash
SSO_START_URL='https://your-org.awsapps.com/start'
SSO_REGION='us-east-1'
SSO_ISSUER_URL='https://identitycenter.amazonaws.com/ssoins-xxxxxxxx'
```

### 3. Add the alias to your shell

Add this line to your `~/.zshrc` or `~/.bashrc`:

```bash
alias aws-sso='eval "$(~/bin/aws-sso/aws-sso)"'
```

Then reload your shell:

```bash
source ~/.zshrc  # or source ~/.bashrc
```

### 4. Authenticate

```bash
aws-sso
```

Your browser will open for SSO authentication. After approving, select your account and role interactively.

## Usage

Once authenticated, you'll have these commands available:

| Command      | Description                                    |
|--------------|------------------------------------------------|
| `ttl`        | Show remaining session time                    |
| `refresh`    | Refresh credentials without re-authenticating  |
| `deactivate` | Clear AWS credentials and restore prompt       |

Your shell prompt will update to show the current role and account:

```
AdministratorAccess@production ~ %
```

## Requirements

- **AWS CLI v2** — [Installation guide](https://docs.aws.amazon.com/cli/latest/userguide/getting-started-install.html)
- **bash** — Version 4.0+ recommended (ships with most systems)

## How It Works

1. Registers an OIDC client with AWS SSO
2. Initiates device authorization and opens browser for approval
3. Polls for access token after user approves
4. Lists available accounts and roles
5. Fetches temporary credentials for the selected role
6. Exports credentials as environment variables in your current shell

## License

MIT

