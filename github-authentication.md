# Setting up HTTPS Access Tokens or SSH Keys for GitHub Authentication

If you want to use GitHub as a remote repository for your Git projects, you'll need to authenticate with the service to verify your identity before you can make changes. If you're using GitHub through your web browser, it's as easy as logging in with your username and password. However, if you're using Git from the command line to work on the project locally, you'll need to take a few extra steps to set up authentication with GitHub.

To start, you need to choose whether you're authenticating over HTTPS or SSH. You only need to choose one of them. If you're not sure which to choose, the setup process for HTTPS is slightly less complex for new users and doesn't require use of the command line.

This guide will walk you through the process for both styles of authentication, starting with HTTPS.

* [Generating a Personal Access Token for HTTPS Authentication](#generating-a-personal-access-token-for-https-authentication)
* [Generating SSH Keys for SSH Authentication](#generating-ssh-keys-for-ssh-authentication)
  * [Create an SSH Key Pair](#create-an-ssh-key-pair)
  * [Add the Private SSH Key to the SSH Agent](#add-the-private-ssh-key-to-the-ssh-agent)
  * [Add the Public SSH Key to GitHub](#add-the-public-ssh-key-to-github)
* [Put it to Use](#put-it-to-use)

## Generating a Personal Access Token for HTTPS Authentication

HTTPS authentication with GitHub requires you to create a *personal access token*. GitHub supports two types of personal access tokens: fine-grained and classic. You can read more about the differences [here](https://docs.github.com/en/authentication/keeping-your-account-and-data-secure/managing-your-personal-access-tokens#types-of-personal-access-tokens); the main ones to be aware of are that fine-grained access tokens can be scoped to specific repositories, whereas classic access tokens are for general use. GitHub recommends using fine-grained access tokens whenever possible, so that's what this guide will show you. 

Before you begin, verify your email address if you haven't done so already.

1. Log in to GitHub.
2. Click the profile icon in the upper-right corner, then click **Settings**.
3. Scroll down and select **Developer settings** from the left sidebar.
4. Under **Personal access tokens**, select **Fine-grained tokens**.
5. Click **Generate new token**.
6. Enter a **Token name**.
7. Add a **Description** as necessary.
8. Select the **Resource owner**. By default, your account is selected.
9. Select an **Expiration** period. The default option is 30 days, but you can select up to an infinite lifetime for the token (not recommended for security reasons).
10. Under **Repository access**, select which repositories you want the token to access. GitHub recommends choosing the minimal repository access that meets your needs.
11. If you selected **Only select repositories**, use the **Selected repositories** dropdown to choose which repositories you want the token to access.
12. Under **Permissions**, choose the minimal permissions necessary for your needs. You can learn more about permissions [here](https://docs.github.com/en/rest/authentication/permissions-required-for-fine-grained-personal-access-tokens).
13. Click **Generate token**.
14. Copy and store the personal access token somewhere safe. For security reasons, GitHub shows you the full token only once after it's been generated.

Now that you have a personal access token, you can use it in place of your password when prompted by Git as you remotely access the repository.

## Generating SSH Keys for SSH Authentication

SSH authentication with GitHub requires you to create a public/private SSH key pair. We can break it into three high-level steps:

1. Create an SSH key pair.
2. Add the private SSH key to the SSH Agent.
3. Add the public SSH key to your GitHub account.

Let's look at each of these in more detail.

### Create an SSH Key Pair

The first step is to generate an SSH key on your local machine. You'll do this using the Terminal (Mac, Linux) or Git Bash (Windows).

1. Open Terminal or Git Bash.
2. Paste the following command, substituting the email address you use to log in to GitHub for the example:

`ssh-keygen -t ed25519 -C "your_email@example.com"`

3. Press Enter to accept the default file location to save the key pair&mdash;a hidden folder called `.ssh` in your default user directory.
4. When prompted, enter a passphrase. If you leave the prompt empty, no passphrase will be used (not recommended).
5. Enter the passphrase again to confirm it.

When you execute these commands, you generate a pair of files in the hidden `.ssh` folder, as shown in this screenshot. The file without an extension is your private key. The `.pub` file is the public key.

![An example of a pair of SSH key files](https://www.natebee.com/portfolio/writing/images/gh-auth-ssh-key-pair.png)

Now that you have generated an SSH key pair, the next step is to add the private key to the SSH agent.

### Add the Private SSH Key to the SSH Agent

Under normal circumstances, you'll be prompted to enter the passphrase from step 4 above every time you use SSH to connect to your remote repository. To avoid this, you can use the SSH agent to manage your key and remember the passphrase for you.

1. Start the SSH agent with the following command:

`eval "$(ssh-agent -s)"`

2. Add your SSH private key to the SSH agent:

`ssh-add ~/.ssh/id_ed25519`

3. Enter the passphrase.

Now that the SSH agent is managing your private key, you can add your public key to your GitHub account.

### Add the Public SSH Key to GitHub

The first step to adding your public SSH key to your GitHub account is to copy the contents of the `id_ed25519.pub` file you created. You can access the contents by opening the file in a text editor, or by using the command `cat ~/.ssh/id_ed25519.pub`.

1. Copy the the content of the public SSH key to your clipboard.
2. Access your profile settings in GitHub by clicking the profile icon in the upper-right corner, then click **Settings**.
3. In the **Access** section of the sidebar, select **SSH and GPG keys**.
4. Click **New SSH Key**.
5. Enter a **Title** for the new key.
6. Make sure the Key type is **Authentication Key**. You can also use the key for commit signing, but that's beyond the scope of this guide.
7. Paste the contents of your public key into the **Key** field.
8. Click **Add SSH Key**.

> **NOTE**: You may be prompted to re-enter your password to confirm access to your GitHub account.

## Put it to Use

Now you're ready to start using Git with a remote repository hosted on GitHub. You can find the URL for the repository by clicking the **Code** dropdown and choosing **HTTPS** or **SSH**.

![Repository clone URLs for HTTPS and SSH](https://www.natebee.com/portfolio/writing/images/gh-auth-clone-urls.png)