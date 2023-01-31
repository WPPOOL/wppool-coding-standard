# WPPOOL Coding Standard
Coding Standard for WPPOOL WordPress Plugins and Themes.


## Prerequisites
1. **PHP 7.4***
2. [**Composer**](https://getcomposer.org/) / Homebrew / Curl

<br>

### Installation guidelines Step by Step

# Step 1 : Install PHP_CodeSniffer

### Linux
```bash
curl -OL https://squizlabs.github.io/PHP_CodeSniffer/phpcs.phar
curl -OL https://squizlabs.github.io/PHP_CodeSniffer/phpcbf.phar
```
### MacOS
```bash
brew doctor
brew install php-code-sniffer
```
### Windows
```bash
composer global require "squizlabs/php_codesniffer=*"
```

#### Run this command to verify installation.
```bash
phpcs -i
```
If it shows like this

`The installed coding standards are PSR1, Zend, PEAR, PSR12, Squiz, MySource, PSR2`

Means, you have installed PHP_CodeSniffer successfully.

<br>

# Step 2 : Install WordPress Coding Standard
Go to your global working directory (such as `cd /Users/$USER/` or `cd ~` in Linux, MacOS and `cd C:\Users\%USERNAME%`) open Terminal/Command Prompt and run this command
```bash
 git clone -b master https://github.com/WordPress/WordPress-Coding-Standards.git wpcs
```

<br>

# Step 3 : Install PHPCompatibility
Go to your global working directory (such as `cd /Users/$USER/` or `cd ~` in Linux, MacOS and `cd C:\Users\%USERNAME%`) open Terminal/Command Prompt and run this command

```bash
git clone https://github.com/PHPCompatibility/PHPCompatibility.git PHPCompatibility
```

<br>

# Step 4 : Configure Paths
 
Add WordPress Coding Standard and PHPCompatibility paths to PHP_CodeSniffer.

Basic format
```bash
phpcs --config-set installed_paths /path/to/wpcs,/path/to/PHPCompatibility
```

WPCS and PHPCompatibility path will be different on different machines. So try finding the exact location of these two packages. 

The home directory should be `/Users/$USER` in Linux, MacOS.
And `C:\\Users\\%USERNAME%` in Windows. 

So

### Linux / MacOS
```bash
phpcs --config-set installed_paths /home/$USER/wpcs,/home/$USER/PHPCompatibility
```

### Windows
```bash
phpcs --config-set installed_paths C:\\Users\\%USERNAME%\\wpcs,C:\\Users\\%USERNAME%\\PHPCompatibility
```

#### Check installation
```
phpcs -i
```
If it shows like this

`The installed coding standards are PSR1, Zend, PEAR, PSR12, Squiz, MySource, PSR2, WordPress, WordPress-Core, WordPress-Docs, WordPress-Extra and PHPCompatibility`

Then you have successfully installed WordPress Coding Standard and PHPCompatibility

<br>

# Step 5 : Configure VSCode
### 1. Install PHPCS [VSCode Extension](https://marketplace.visualstudio.com/items?itemName=shevaua.phpcs)
- Launch VS Code Quick Open (Ctrl+P), paste the following command, and press enter.
- `ext install shevaua.phpcs`
  
### 2. Modify Settings
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

# Step 6 : Add WPCS to your project
1. Open your project in VSCode and copy the `phpcs.xml` file to root of your project.
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

## Run PHPCS!
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

# Use PHPCBF Globally
If you want to use phpcbf (php code beautifier) for VSCode or from CLI with WordPress Standard, you can follow this hacks.

1. Copy `phpcs.xml` file to root of your machine (or somewhere you trust). 
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
