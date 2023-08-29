# WPPOOL Coding Standard 3
Coding Standard for WPPOOL WordPress Plugins and Themes.
Compatible with WPCS 3.0


## Prerequisites
1. **PHP 7.4**^
2. [**Composer**](https://getcomposer.org/)

<br>

# Step 1 : Install Packages

Follow all the steps one by one

## (i) Install PHP Code Sniffer

```bash
composer global require "squizlabs/php_codesniffer=*"
```

[See other ways to install](https://github.com/squizlabs/PHP_CodeSniffer)

<br>

## (ii) Install WPCS
Run this command to install
```bash
composer global config allow-plugins.dealerdirect/phpcodesniffer-composer-installer true
composer global require --dev wp-coding-standards/wpcs:"^3.0"
```

or run this to upgrade
```bash
composer global update wp-coding-standards/wpcs --with-dependencies
```

[See other ways to install](https://github.com/WordPress/WordPress-Coding-Standards)


<br>

## (iii) Install PHPCompatibility
Run this command
```bash
composer global require --dev phpcompatibility/php-compatibility
```


[See other ways to install](https://github.com/PHPCompatibility/PHPCompatibility)


<br>

## (iv) Set Environment Paths

### For Windows

After installing Composer, it sets up a global bin directory where Composer-installed tools are placed. This directory needs to be added to your system's PATH so that you can run the tools from any command prompt.

- Search for "Environment Variables" in the Windows Start menu and open the "Edit the system environment variables" option.
- In the System Properties window, click the "Environment Variables" button.
- In the "System Variables" section, scroll down and find the "Path" variable. Select it and click the "Edit" button.
- Click the "New" button and add the path to Composer's global bin directory. The default path is `C:\Users\<your-username>\AppData\Roaming\Composer\vendor\bin`, but - it might vary based on your setup.
- Click "OK" to close the windows and apply the changes.


## For Linux/mac
Composer's global bin directory is usually `~/.composer/vendor/bin`. To run Composer-installed tools from any terminal window, you need to ensure that this directory is added to your system's PATH. You can do this by adding the following line to your shell's configuration file (~/.bashrc for Bash users, ~/.zshrc for Zsh users):

```bash
export PATH="$PATH:$HOME/.composer/vendor/bin"
```
After adding the line, save the file and either restart your terminal or run `source ~/.bashrc` (or `source ~/.zshrc` for Zsh) to apply the changes.

<br>

# Step 2 : Configure Installed Paths
 
Add WordPress Coding Standard and PHPCompatibility paths to PHP_CodeSniffer.

Basic format
```bash
phpcs --config-set installed_paths /path/to/wpcs,/path/to/phpextra,path/to/phpcsutils,/path/to/PHPCompatibility
```

WPCS and PHPCompatibility path will be different on different machines. So try finding the exact location of these two packages. 

### Windows
```bash
phpcs --config-set installed_paths C:\Users\<your-username>\AppData\Roaming\Composer\vendor\phpcompatibility\php-compatibility,C:\Users\<your-username>\AppData\Roaming\Composer\vendor\phpcsstandards\phpcsextra,C:\Users\<your-username>\AppData\Roaming\Composer/vendor\phpcsstandards\phpcsutils,C:\Users\<your-username>\AppData\Roaming\Composer/vendor\wp-coding-standards\wpcs
```

### Linux/Mac
```bash
phpcs --config-set installed_paths ~/.composer/vendor/phpcompatibility/php-compatibility,~/.composer/vendor/phpcsstandards/phpcsextra,~/.composer/vendor/phpcsstandards/phpcsutils,~/.composer/vendor/wp-coding-standards/wpcs
```

<br/>

## Check installation
```
phpcs -i
```
If it shows like this

`The installed coding standards are MySource, PEAR, PSR1, PSR2, PSR12, Squiz, Zend, PHPCompatibility, Modernize, NormalizedArrays, Universal, PHPCSUtils, WordPress, WordPress-Core, WordPress-Docs and WordPress-Extra`

Then you have successfully installed WPCS 3 and PHPCompatibility

<br><br>


# Step 3 : Configure WPCS in VSCode
## i. Install PHPCS [VSCode Extension](https://marketplace.visualstudio.com/items?itemName=shevaua.phpcs)
- Launch VS Code Quick Open (Ctrl+P), paste the following command, and press enter.
- `ext install shevaua.phpcs`
  
## ii. Modify Settings
- Go to Settings.json (Settings -> Edit in Settings.json)
- Add this snippet to your JSON file **(Modify first)**
```json
    "phpcs.enable": true,
    "phpcs.executablePath": "PHPCS_BIN_PATH",
    "phpcs.standard": "WordPress",
    "phpcbf.documentFormattingProvider": true,
    "phpcbf.onsave": false,
    "phpcbf.executablePath":"PHPCBF_BIN_PATH",
    "phpcbf.standard": "WordPress",
    "phpcs.showSources": true,
    "[php]": {
        "editor.defaultFormatter": "persoderlind.vscode-phpcbf"
	}
```

### `PHPCS_BIN_PATH` and `PHPCBF_BIN_PATH` is different on different machine. So you have to find the right path of these files.

### Linux / MacOS
```bash
which phpcs
# Output : /usr/bin/phpcs
which phpcbf
# Output : /usr/bin/phpcbf
```

### Windows
```bash
where phpcs
# or
where phpcbf
```
If you have installed PHP_CodeSniffer using composer, your default path should be `C:\Users\%USERNAME%\AppData\Roaming\Composer\phpcs` and `C:\Users\%USERNAME%\AppData\Roaming\Composer\phpcbf`

<br>

## iii. Add RuleSet to your project
1. Open your project in VSCode and copy the `phpcs3.xml` file to root of your project as `phpcs.xmlpu
2. Modify `Excludes` sections as you need
3. Update `text-domain` value in **19** line
4. [Optional] Add these commands to your project (package.json or composer.json)
   
```json
{ 
	"php-report" : "phpcs . > report.txt",
	"php-format" : "phpcbf ."
}
```
<br>

### Run PHPCS!
```bash
phpcs .
```

To save all report to a file `report.txt`, type and hit enter
```bash
php-report
```
or
```bash
phpcs . > report.txt
```

### Well done. You have successfully installed WPCS in your project. Now you may continue if you want to do more advanced thing with that.
<br>

# Use a Global RuleSet
If you want to use phpcbf (php code beautifier) for VSCode or from CLI with WordPress Standard, you can follow this hacks.

1. Copy `phpcs3.xml` file to root of your machine as `phpcs.xml` (or somewhere you trust). 
2. Modify the VSCode Settings for a little bit
```json
{
    "phpcs.enable": true,
    "phpcs.executablePath": "PHPCS_BIN_PATH",
    "phpcs.standard": "/path/to/your/phpcs.xml",
    "phpcbf.documentFormattingProvider": true,
    "phpcbf.onsave": false,
    "phpcbf.executablePath":"PHPCBF_BIN_PATH",
    "phpcbf.standard": "/path/to/your/phpcs.xml",
    "phpcs.showSources": true,
    "[php]": {
        "editor.defaultFormatter": "persoderlind.vscode-phpcbf"
	}
},
```
You can use directly phps.xml path instead of the standard name as configuration.

Now you can open a PHP file and right click on mouse -> `Format Document` to format the php file.
### Don't forget to add report.txt to project's `.gitignore`

## Contributions
These WordPress Coding Standard is generated and maintained by WPPOOL Developers.
