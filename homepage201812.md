homepage201812.md

Quick setup — if you’ve done this kind of thing before
or

Get started by creating a new file or uploading an existing file. We recommend every repository include a README, LICENSE, and .gitignore.
…or create a new repository on the command line

echo "# homepage201812" >> README.md
git init
git add README.md
git commit -m "first commit"
git remote add origin https://github.com/josonchen/homepage201812.git
git push -u origin master

----------


Checking for existing SSH keys

    mac
    windows
    linux

Before you generate an SSH key, you can check to see if you have any existing SSH keys.

Note: DSA keys were deprecated in OpenSSH 7.0. If your operating system uses OpenSSH, you'll need to use an alternate type of key when setting up SSH, such as an RSA key. For instance, if your operating system is MacOS Sierra, you can set up SSH using an RSA key.

    Open Terminal.

    Enter ls -al ~/.ssh to see if existing SSH keys are present:

    ls -al ~/.ssh
    # Lists the files in your .ssh directory, if they exist

    Check the directory listing to see if you already have a public SSH key.

By default, the filenames of the public keys are one of the following:

    id_dsa.pub
    id_ecdsa.pub
    id_ed25519.pub

    id_rsa.pub

    If you don't have an existing public and private key pair, or don't wish to use any that are available to connect to GitHub, then generate a new SSH key.
    If you see an existing public and private key pair listed (for example id_rsa.pub and id_rsa) that you would like to use to connect to GitHub, you can add your SSH key to the ssh-agent.

Tip: If you receive an error that ~/.ssh doesn't exist, don't worry! We'll create it when we generate a new SSH key.

Article versions

    GitHub.com
    GitHub Enterprise 2.15
    GitHub Enterprise 2.14
    GitHub Enterprise 2.13
    GitHub Enterprise 2.12

---------


Authenticating to GitHub / Generating a new SSH key and adding it to the ssh-agent
Generating a new SSH key and adding it to the ssh-agent

    mac
    windows
    linux

After you've checked for existing SSH keys, you can generate a new SSH key to use for authentication, then add it to the ssh-agent.

If you don't already have an SSH key, you must generate a new SSH key. If you're unsure whether you already have an SSH key, check for existing keys.

If you don't want to reenter your passphrase every time you use your SSH key, you can add your key to the SSH agent, which manages your SSH keys and remembers your passphrase.
Generating a new SSH key

    Open Terminal.

    Paste the text below, substituting in your GitHub email address.

    ssh-keygen -t rsa -b 4096 -C "your_email@example.com"

    This creates a new ssh key, using the provided email as a label.

    Generating public/private rsa key pair.

    When you're prompted to "Enter a file in which to save the key," press Enter. This accepts the default file location.

    Enter a file in which to save the key (/Users/you/.ssh/id_rsa): [Press enter]

    At the prompt, type a secure passphrase. For more information, see "Working with SSH key passphrases".

    Enter passphrase (empty for no passphrase): [Type a passphrase]
    Enter same passphrase again: [Type passphrase again]

Adding your SSH key to the ssh-agent

Before adding a new SSH key to the ssh-agent to manage your keys, you should have checked for existing SSH keys and generated a new SSH key. When adding your SSH key to the agent, use the default macOS ssh-add command, and not an application installed by macports, homebrew, or some other external source.

    Start the ssh-agent in the background.

    eval "$(ssh-agent -s)"
    Agent pid 59566

    If you're using macOS Sierra 10.12.2 or later, you will need to modify your ~/.ssh/config file to automatically load keys into the ssh-agent and store passphrases in your keychain.

    Host *
     AddKeysToAgent yes
     UseKeychain yes
     IdentityFile ~/.ssh/id_rsa

    Add your SSH private key to the ssh-agent and store your passphrase in the keychain. If you created your key with a different name, or if you are adding an existing key that has a different name, replace id_rsa in the command with the name of your private key file.

    ssh-add -K ~/.ssh/id_rsa

    Note: The -K option is Apple's standard version of ssh-add, which stores the passphrase in your keychain for you when you add an ssh key to the ssh-agent.

    If you don't have Apple's standard version installed, you may receive an error. For more information on resolving this error, see "Error: ssh-add: illegal option -- K."

    Add the SSH key to your GitHub account.

-----
Adding a new SSH key to your GitHub account

    mac
    windows
    linux

To configure your GitHub account to use your new (or existing) SSH key, you'll also need to add it to your GitHub account.

Before adding a new SSH key to your GitHub account, you should have:

    Checked for existing SSH keys
    Generated a new SSH key and added it to the ssh-agent

After adding a new SSH key to your GitHub account, you can reconfigure any local repositories to use SSH. For more information, see "Switching remote URLs from HTTPS to SSH."

Note: DSA keys were deprecated in OpenSSH 7.0. If your operating system uses OpenSSH, you'll need to use an alternate type of key when setting up SSH, such as an RSA key. For instance, if your operating system is MacOS Sierra, you can set up SSH using an RSA key.

    Copy the SSH key to your clipboard.

    If your SSH key file has a different name than the example code, modify the filename to match your current setup. When copying your key, don't add any newlines or whitespace.

    pbcopy < ~/.ssh/id_rsa.pub
    # Copies the contents of the id_rsa.pub file to your clipboard

    Tip: If pbcopy isn't working, you can locate the hidden .ssh folder, open the file in your favorite text editor, and copy it to your clipboard.

    Settings icon in the user bar

In the upper-right corner of any page, click your profile photo, then click Settings.

Authentication keys

In the user settings sidebar, click SSH and GPG keys.

SSH Key button

Click New SSH key or Add SSH key.
In the "Title" field, add a descriptive label for the new key. For example, if you're using a personal Mac, you might call this key "Personal MacBook Air".
The key field
Paste your key into the "Key" field.
The Add key button
Click Add SSH key.
Sudo mode dialog

    If prompted, confirm your GitHub password.

Further reading

    "Authorizing an SSH key for use with a SAML single sign-on organization"
--------

如果是第一次使用Git，则需要设置用户名和邮箱：

    $ git config --global user.name "用户名"
    $ git config --global user.email "电子邮箱"
你可以在GitHub上新建免费的公开仓库，并按照GitHub的文档配置SSH Key，然后将代码仓库克隆到本地，其实就是将代码复制到你的机器里，并交由Git来管理：

    $ git clone git@github.com:username/repository.git
或使用HTTPS地址进行克隆：

    $ git clone https://username:password@github.com/username/repository.git
你可以修改复制到本地的代码了（symfony-docs-chs项目里都是rst格式的文档）。当你觉得完成了一定的工作量，想做一个阶段性的提交，并向这个本地的代码仓库添加当前目录的所有改动：

    $ git add .
或者只是按需要来添加修改的内容：

    $ git add -p
可以输入：

    $ git status
来看现在的状态，图1-7是添加之前的，图1-8是添加之后的情况
----
