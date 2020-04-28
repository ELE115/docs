# How to setup your programming environment

We will be guiding you through the installation and configuration process of all the necessary software and tools to program the drones in ELE115.

## 1: Register Github

> Estimated Time Cost: 3min

1. To begin with, visit [Join Github](https://github.com/join) to create a Github account (if you don't have one yet).
1. Type your username, email, and password.
1. Please remember which email you are using now to create Github account. It will be used later.
1. Click next. Select the *Free* plan and proceed.
1. Activate your account by following the link in your email.

1. After finishing the registration process, visit [New personal access token](https://github.com/settings/tokens/new).
1. Type `IntelliJ IDEA` for *Note*.
1. Check the checkbox `repo` and `gist` below (sub-checkbox shall be automatically checked for you).
1. Click `Generate token`.
1. Now you should see a long green string composed of random numbers and characters, called **token**.
Your token will be used later so please copy this token and store it to somewhere super secret.
Remember, NEVER SHARE YOUR TOKEN WITH ANYONE, including TAs.

Proceed to step 2 when finished.

## 2: Install local software

> Estimated Time Cost: 15min

Installation process is different among different operating systems,
so please choose your operating system:
* [Windows 10](https://github.com/ELE115/docs/blob/master/setup.md#windows-10)
* [Mac OS X](https://github.com/ELE115/docs/blob/master/setup.md#mac-os-x)
* Linux
  * [Ubuntu](https://github.com/ELE115/docs/blob/master/setup.md#ubuntu)
  * [Arch Linux](https://github.com/ELE115/docs/blob/master/setup.md#arch-linux)
  * [Other](https://github.com/ELE115/docs/blob/master/setup.md#other-linux)

### Windows 10

#### 2.1: Install git

1. Download [git 2.25.0](https://github.com/git-for-windows/git/releases/download/v2.25.0.windows.1/Git-2.25.0-64-bit.exe).
1. Double click to open it.
1. Click `Yes` if Windows asks "Do you want to allow this app to make changes to your device".
1. In the installation wizard, click `Next` **5** times.
1. In the `Adjusting your PATH environmen` page, choose the second option, `Git from the command line and also from 3rd-party software`.
Click `Next`.
1. In the `Choosing HTTPS transport backend` page, choose the first option, `Use the OpenSSL library`.
Click `Next`.
1. **Here is an important part:**
In the `Configuring the line ending conversions` page, choose the second option, `Checkout as-is, commit Unix-style line endings`.
Click `Next`.
1. In the `Configuring the terminal emulator to use with Git Bash` page, choose the first option, `Use MinTTY (the default terminal of MSYS2)`.
Click `Next`.
1. In the `Configuring extra options` page, check `Enable file system caching` and `Enable Git Credential Manager`. Uncheck `Enable symbolic links`.
Click `Install`.
1. Click `Next` when done.

#### 2.2: Install OpenJDK

1. Download [OpenJDK 11.0.6](https://github.com/AdoptOpenJDK/openjdk11-binaries/releases/download/jdk-11.0.6%2B10/OpenJDK11U-jdk_x64_windows_hotspot_11.0.6_10.msi).
1. Double click to open it.
1. In the installation wizard, click `Next`.
1. Check `I accept the terms in the License Agreement`. Click `Next`.
1. **Here is an important part:**
In the `Custom Setup` page, click on the red cross before `Set JAVA_HOME variable`,
and change it to the first option available (aka `Will be installed on local hard drive`).
1. Click `Next`.
1. Click `Install`.
1. Click `Yes` if Windows asks "Do you want to allow this app to make changes to your device".
1. Click `Finish` when done.

#### 2.3: Install IntelliJ IDEA

1. Download [IntelliJ IDEA](https://download.jetbrains.com/idea/ideaIC-2019.3.2.exe).
1. Click `Yes` if Windows asks "Do you want to allow this app to make changes to your device".
1. In the installation wizard, click `Next` **3** times.
1. Click `Install`.
1. Click `Finish` when done.

Now, [Configure your IntelliJ IDEA](https://github.com/ELE115/docs/blob/master/setup.md#3-configure-your-intellij-idea).

### Mac OS X

#### 2.1: Install git

1. Download [git 2.23.0](https://sourceforge.net/projects/git-osx-installer/files/git-2.23.0-intel-universal-mavericks.dmg/download?use_mirror=autoselect).
1. Double click to open it.
1. **RIGHT** click on the `git-2.23.0-intel-universal-mavericks.pkg`.
Pick `Open`.
1. In the new dialog asking for permission, click `Open`.
1. Now you shall see a window titled `Install git-2.23.0-intel-universal-mavericks`. Click continue, and then install.
1. If it asks for your password, just type in your password.
1. Click `Close` when finished.
1. Click `Move to trash bin`.

#### 2.2: Install OpenJDK

1. Download [OpenJDK 11.0.6](https://github.com/AdoptOpenJDK/openjdk11-binaries/releases/download/jdk-11.0.6%2B10/OpenJDK11U-jdk_x64_mac_hotspot_11.0.6_10.pkg).
1. Double click to open it.
1. Click `Next`.
1. Click `Next`, and click `Agree`.
1. Click `Install`.
1. If it asks for your password, just type in your password.
1. Click `Close` when finished.
1. Click `Move to trash bin`.

#### 2.3: Install IntelliJ IDEA

1. Download [IntelliJ IDEA](https://download.jetbrains.com/idea/ideaIC-2019.3.2.dmg?_ga=2.254120648.1392192374.1579719800-819754429.1579503100).
1. Double click to open it.
1. In the new window poped out, *drag* the `IntelliJ IDEA CE` icon into the folder on the right side.
1. Close the window when finished.

Now, [Configure your IntelliJ IDEA](https://github.com/ELE115/docs/blob/master/setup.md#3-configure-your-intellij-idea).

### Linux

#### Ubuntu

Launch Terminal.
Copy-paste the following code, one line by another, into your terminal.
Hit enter after each line.

*Note: if it prompts "[sudo] password for ....:", then type your login password here.*

```bash
cd
sudo apt-get update
sudo apt-get install -y git openjdk-11-jdk wget
wget https://download.jetbrains.com/idea/ideaIC-2019.3.2.tar.gz
sudo mkdir /usr/share/idea
sudo tar xzf ideaIC-2019.3.2.tar.gz -C /usr/share/idea --strip-components=1
sudo ln -s /usr/share/idea/bin/idea.sh /usr/bin/idea
```

Copy-paste the following code, **as a whole**, into your terminal.
```bash
sudo tee /usr/share/applications/idea.desktop <<EOF
[Desktop Entry]
Version=1.0
Type=Application
Name=IntelliJ IDEA Community Edition
Comment=Develop with pleasure!
Exec=/usr/bin/idea %f
Icon=idea
Terminal=false
StartupNotify=true
StartupWMClass=jetbrains-idea-ce
Categories=Development;IDE;Java;
EOF
```

The IntelliJ IDEA icon shall appear on your desktop.
Now, [Configure your IntelliJ IDEA](https://github.com/ELE115/docs/blob/master/setup.md#3-configure-your-intellij-idea).

#### Arch Linux

Launch Terminal.
Copy-paste the following code, one line by another, into your terminal.
Hit enter after each line.

*Note: if it prompts "[sudo] password for ....:", then type your login password here.*

```bash
sudo pacman -Syu --noconfirm # Recommanded, but not necessary
sudo pacman -Sy --noconfirm git jdk11-openjdk wget intellij-idea-community-edition
```

The IntelliJ IDEA icon shall appear on your desktop.
Now, [Configure your IntelliJ IDEA](https://github.com/ELE115/docs/blob/master/setup.md#3-configure-your-intellij-idea).

#### Other Linux

The procedure should be similar as above.
Google `install xxx on yyy` where `xxx` is one of the following and `yyy` is your opearting system and follow the instructions.
You need to install these:

* git
* OpenJDK 11.0.6
* IntelliJ IDEA 2019.3

If you still have trouble, please contact course instructors.

## 3: Configure your IntelliJ IDEA

> Estimated Time Cost: 10min

### 3.1: Launch IntelliJ IDEA for the first time

1. Open IntelliJ IDEA if you haven't done so.
1. Choose `Do not import settings`, and click `OK`.
1. Choose your preferred UI style, either dark or bright.
1. Click `Skip Remaining and Set Defaults.`

You should now see a dialog titled `Welcome to IntelliJ IDEA`.

### 3.2: Download ELE115 project template

Before we proceed to anything else, we need to download our project template.

1. Goto your IntelliJ IDEA configuration folder:
  * For Linux, it is `~/.IdeaIC2019.3/config/`.
  * For macOS, it is `~/Library/Preferences/IdeaIC2019.3/`. To go to this folder:
    * Open Finder.
    * Cilck *Go* menu, and click `Go to Folder...`.
    * Type `~/Library/Preferences/IdeaIC2019.3/` and click `Go`.
  * For Windows, it is `C:\Users\<username>\.IdeaIC2019.3\config\`.
1. Create a folder named `projectTemplates` (if not exists) in the above folder.
1. Download [ELE115 project template](https://github.com/ELE115/idea-gradle-template/releases/latest/download/ELE115.zip).
Put the downloaded zip file to the **projectTemplates** folder.
Override the existing `ELE115.zip` file *if there is one*.

**Note: DO NOT UNZIP THE FILE.** Put the zip file, not the unzipped folder, into the `projectTemplates` folder.

**Note:** For **mac OS** users: To download without unzipping in Safari, right click on the link and choose `Save as...`.

### 3.3: Link your Github account with IntelliJ IDEA

> Note: Some Linux users may have trouble with this step. Please consult course instructors if you are using Linux.

In the `Welcome to IntelliJ IDEA` dialog:
1. Click the `Configure` button at the bottom, and click `Settings` (or `Preferences` if you are using **mac OS**).
1. Click the triangle before `Version Control` on the left, and click `GitHub`.
1. Click `Add account` on the right.
1. Click `Use Token` on the top, and paste your **token** generated before into the box.
1. Check `Clone git repositories using ssh` **ONLY** if you are using Linux or mac OS.
1. Click `Log In`.
You shall now see your Github Account added to IntelliJ IDEA.

### 3.4: Setup terminal

**Note:** Only Windows users should do this. Non-windows users can simply skip this section.
1. Unfold `Tools`, and click `Terminal`.
1. In the `Shell path` text field, type: `"C:\Program Files\Git\bin\bash.exe"`.
Remember to **include** the quotes `"`...`"`.

### 3.5: Install plugins

In the Settings/Preferences dialog:
1. Click `Plugins`.
1. Search `Gradle Run with Arguments`.
1. Click `Install`, and click `Accept`.
1. Click `Restart IDE`, and click `Restart`.

### 3.6: Recommanded settings for IntelliJ IDEA

**Note:** It is **HIGHLY RECOMMANDED** that you follow these steps to tweak some IDE features.
These features add complexity to your coding experience, which, while good for experts, may harm newbies.

In the `Welcome to IntelliJ IDEA` dialog:
1. Click the `Configure` button at the bottom, and click `Settings` (or `Preferences` if you are using **mac OS**).
1. `Editor`/`General`/`Code Folding`, uncheck all checkboxes.
1. `Editor`/`General`/`Gutter Icons`, uncheck `Run line marker`.
1. `Editor`/`General`/`Postfix Completion`, uncheck `Enable postfix completion`.
1. `Editor`/`Live Templates`, uncheck all checkboxes.
1. `Editor`/`Intentions`, uncheck `Groovy` and `Java`.
1. `Editor`/`Inlay Hints`/`Java`, choose `Parameter hints`, and then uncheck `Show parameter hints for:`.
1. Click `OK`.

Congratulations!
You've successfully setup all the necessary programming environment in ELE115.
Wish you a good luck on your journey with drones.

## Appendix: Keep your project template updated

The ELE115 project template you just downloaded **MAY** be updated thorough the whole term by our TAs.
Upon notificated by TA, you shall upgrade your project template ASAP.

The process is extremely simple: you just go through the same process as
[above](https://github.com/ELE115/docs/blob/master/setup.md#32-download-ele115-project-template).

**Note:** If you do not upgrade your project template in a timely manner,
you may encounter weird bugs that makes your life much harder during the labs.
