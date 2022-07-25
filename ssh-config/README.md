# SSH Config setup for 1Password

The following steps are to setup the 1Password SSH agent on
macOS taken from the [1Password Documentation](https://developer.1password.com/docs/ssh/get-started) to act as a quicker reference when setting up a new environment.

## Step 1: Generate an SSH key

In your 1Password 8 desktop app, generate an SSH key for GitHub:

1. Open and unlock 1Password, then navigate to your Personal or Private vault.
2. Click `New Item` and choose `SSH Key`.
3. Click `Add Private Key` > `Generate New Key.`
4. Select an SSH key type: `Ed25519` or `RSA`, then click `Generate`.
5. When you're done, click `Save`.

## Step 2: Connect to Github, Gitlab etc

With your SSH key generated, you can connect it to your GitHub account.

If you're using 1Password in your browser, select the Title or Key field, click the 1Password icon in the field, and choose your GitHub SSH key. 1Password will automatically fill the public key and title. Then click Add SSH Key on the GitHub settings page.

## Step 3: Enable SSH Agent

Ensure 1Password keeps running in the background

1. Open 1Password and choose `1Password` > `Preferences` > `General`
1. Select the checkboxes to `Keep 1Password in the menu bar` and `Start at login`

Enable the SSH Agent

1. Open 1Password and choose  `1Password` > `Preferences` > `Developer`
1. Select the checkbox to `Use the SSH agent`
1. Optional: Select the checkbox to `Display key names when authorizing connections`.

## Step 4: Configuration

Add the `IdentityAgent snippet` to your `~/.ssh/config` file:

Identity Agent Snippet

```bash
Host *
  IdentityAgent "~/Library/Group Containers/2BUA8C4S2C.com.1password/t/agent.sock"
```

You can also set the `SSH_AUTH_SOCK` environment variable in the shell where your SSH command runs:

```bash
export SSH_AUTH_SOCK=~/Library/Group\ Containers/2BUA8C4S2C.com.1password/t/agent.sock
```

### RUN THIS COMMAND

For an agent path that's easier to type and is also consistent with Linux, you can run this command to create a symlink for `~/.1password/agent.sock`:

```bash
mkdir -p ~/.1password && ln -s ~/Library/Group\ Containers/2BUA8C4S2C.com.1password/t/agent.sock ~/.1password/agent.sock
```

Now your SSH clients will use the 1Password SSH agent for all hosts.
