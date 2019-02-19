# EHgrab

A shell script for automatically downloading image galleries from E-Hentai (https://e-hentai.org).

- [Installation](#installation)
- [Usage](#usage)
  - [Basic Usage](#basic-usage)
  - [Command Line Options](#command-line-options)
  - [Authenticated Mode](#authenticated-mode)
- [Configuration](#configuration)
- [Contributing](#contributing)

## Installation
It is recommended that you install EHgrab on your path by entering the following commands into your preferred terminal:

`cd <location of ehgrab file>`

`chmod +x ehgrab`

*To install EHgrab for all users:*

`cp ehgrab /usr/local/bin`

`[[ $PATH != *"/usr/local/bin"* ]] && PATH=$PATH:/usr/local/bin && echo PATH=$PATH:/usr/local/bin >> ~/.profile`

*Or, to install EHgrab for the current user, only:*

`mkdir -p ~/bin && cp ehgrab ~/bin`

`[[ $PATH != *"~/bin"* ]] && PATH=$PATH:~/bin && echo PATH=$PATH:~/bin >> ~/.profile`

#### Other Shells
EHgrab is currently designed to work with Bash. At this time, support for other Unix shells is not tested or supported. If you'd like to help add support for your favorite shell, or make EHgrab more shell-agnostic, please feel free to email me at code@cacocav.com, or open a pull request.

#### A Note for Windows Users
EHgrab is a Unix shell script. As such, it needs to run in a Unix terminal emulator. While Unix terminals are natively available on Mac OS and Linux-based systems, on Windows you will have to download one. There are many available, but I personally use Git Bash, which is installed when you [install Git for Windows.](https://git-scm.com/download/)

## Usage

### Basic Usage
The most basic usage of EHgrab is

`ehgrab URL`

where `URL` is an E-Hentai gallery or image page. This downloads all images from the gallery into the current working directory.

Optionally, a path to a different download location can be specified after the URL:

`ehgrab URL PATH`

### Command Line Options
The following command line options are currently supported by EHgrab:

|        Option       |                               Behavior                              |  Default  |
|---------------------|---------------------------------------------------------------------|-----------|
| -c, --config *FILE* | Specifies a path to a file to use as a configuration file.          | ~/.ehgrab |
| --debug             | Enables verbose output for debugging. Mostly useful for developers. |           |
| -f, --force         | Downloads files even if a file with that name already exists.       |           |
| -h, --help          | Displays a help message.                                            |           |
| -p, --pass *STRING* | Specifies a string to use as the password hash.                     |           |
| -q, --quiet         | Silences all output, including errors.                              |           |
| --sd                | Disables downloading of high definition images.                     |           |
| -u, --user *STRING* | Specifies a string to use as the user ID.                           |           |
| -v, --version       | Displays EHgrab's current version                                   |           |
| -z, --zero          | Enables zero-indexed file names.                                    |           |

### Authenticated Mode
By default, EHgrab will work in "unauthenticated mode". That is, it will function as if you are not logged into E-Hentai. E-Hentai requires you to be logged in to get access to high definition images, when they're available, and to access sister site ExHentai (exhentai.org). When operating in unauthenticated mode, EHgrab will download a lower-quality "standard definition" images in place of high definition images, and will be unable to access ExHentai.

EHgrab can download high definition images and access ExHentai by working in "authenticated mode". To use authenticated mode, you must allow EHgrab to authenticate as your user account by providing a user ID and password hash.

#### Acquiring Your E-Hentai Credentials
To get your user ID and password hash, follow these instructions:
1. Log into your E-Hentai account
2. While still on E-Hentai, open your web console
    - If you don't know how to open your web console, try right-clicking anywhere on the page, selecting "Inspect" or "Inspect element", and then switching to the "Console" tab
3. Enter `document.cookie` into the console. This should return a semi-colon-separated list of cookies for the current page in key=value format
4. Look for the "ipb_member_id" and "ipb_pass_hash" keys. The values of these keys are your user ID and password hash, respectively.

#### Providing Your E-Hentai Credentials on the Command Line
To provide your E-Hentai credentials for one use, use the `-u` and `-p` command line options:

`ehgrab -u USER_ID -p PASSWORD_HASH URL`

#### Store Your E-Hentai Credentials in the EHgrab Configuration File
You can store your user ID and password hash in the EHgrab configuration file (See below for details on setting up your EHgrab configuration file). By doing so, your credentials will be used to download high definition images, where available, by default. If storage space or download time is ever a concern, you can still force EHgrab to download standard definition images by using the `--sd` command line option.

> **WARNING:** If a malicious person got access to your E-Hentai user ID and password, they may be able to log into E-Hentai as you by manually setting their cookies. If this is a concern and/or if you use a shared computer account, you may not want to set your E-Hentai credentials in your EHgrab configuration file.

## Configuration

EHgrab can be configured using a configuration file to set default options for using EHgrab. Any command line options provided to EHgrab will override options set via the configuration file. EHgrab configuration files should be formatted as a list of key-value pairs, one pair per line, with the key and value separated by at least one white space character. You can specify the location of a configuration file at the command line using the `-c` or `--config` command line options. If no configuration file is provided on the command line, EHgrab will look in ~/.ehgrab for a configuration file by default.

The following key-value pairs are currently supported in EHgrab configuration files:

| Key  |     Value     | Overridden By |
|------|---------------|---------------|
| pass | Password hash | -p, --pass    |
| user | User ID       | -u, --user    |

## Contributing

#### Reporting Bugs
EHgrab is a somewhat fragile script that works by making assumptions about E-Hentai's page structure. If things change, it will likely break. It would be a big help if you report any bugs you encounter by [opening an issue][issues].

#### Requesting Features
If you have any features you'd like to see added, [open an issue][issues]. I can't guarantee I'll be able to add all requested features, but I'm happy to take a look.

#### Contributing Code
If you'd like to contribute some code, open a pull request or contact me via email at code@cacocav.com.

Please make sure your code style matches the rest of the script and include comments and debug messages as appropriate.

If you are trying to debug a problem you are having, you may find the `--debug` flag useful. Also, lines that make assumptions about E-Hentai's page structure have line comments that include the phrase "(FRAGILE)", which may be a good place to start looking for problems.

[issues]: https://gitlab.com/cacocav/ehgrab/issues
