# wppool-coding-standard
Coding Standard for WPPOOL WordPress Plugins and Themes.

# Get Started

### Install dependencies (Globally)
- Install [PHP_CodeSniffer](https://github.com/squizlabs/PHP_CodeSniffer)
- Install [WordPress Coding Standard](https://github.com/WordPress/WordPress-Coding-Standards) (Install from GitHub Master branch)
- Install [PHPCompatibility](https://github.com/PHPCompatibility/PHPCompatibility)

### Add paths to PHP_CodeSniffer configuration
You can set multiple paths at a time
```bash
phpcs --config-set installed_paths /path/to/wpcs,/path/to/PHPCompatibility
```

Now test your installation
```bash
phpcs -i
```

If it shows like bellow, then you are GOOD TO GO

<code>The installed coding standards are PSR1, Zend, PEAR, PSR12, Squiz, MySource, PSR2, WordPress, WordPress-Core, WordPress-Docs, WordPress-Extra and PHPCompatibility
</code>

# Configurating VSCode
1. Go to Settings.json (Settings -> Edit in Settings.json)
2. Add this snippet to your JSON file
```json
{
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
},
```

### NOTE: The `PHPCS_BIN_PATH` is relative, you have to change it. To know the absolute path of PHPCS on your local machine, follow this command
```bash
which phpcs
```
and
```bash
which phpcbf
```
On example, I used Linux (almost same for Mac).

The location in Windows 10 maybe `C:\Users\{user_name}\AppData\Roaming\Composer\vendor\bin\
`

3. Install PHPCS (shevaua.phpcs) VSCode Extention
# Add WPCS to your project
1. Create a file named `phpcs.xml` at the root of your project.
2. [Optional] Add these commands to your project
   
```json
{ 
	"php-report" : "phpcs . > report.txt",
	"php-format" : "phpcbf ."
}
```

# First report
```bash
phpcs .
```

To save all report to a file, type
```bash
php-report
```
or
```bash
phpcs . > report.txt
```

### Don't forget to add report.txt to project's `.gitignore`

## Contributions
These WordPress Coding Standard is generated and maintained by WPPOOL Developers.
