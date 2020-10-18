# WinDevTools

There are many good options for local web development environment on Windows (Acquia DevDesktop, MAMP, XAMPP), but personally I find IIS to be the most convenient option (*after it has been properly configured*).

These are the steps I take to setup local development.

## Directory Structure

Create a directory for each language you choose to install in either the root directory or a `lang` subdirectory on root. This will make it easier to reference paths and support multiple versions.

Create a local project directory (i.e. `C:\dev`) to contain subdirectories for all projects.  Place the `index.php` from this repo here to return phpinfo.

Each project will go into its own subdirectory (i.e. `C:\dev\drupal7`, `C:\dev\wordpress`). Either `cd C:\dev` before cloning/installing with package manager, or create the project directory manually and extract files.

## Internet Information Services (IIS)

1. Enable IIS in Windows

   - In a file explorer window, navigate to `Control Panel\Programs`
   - Select `Turn Windows features on or off`
   - Tick the box for Internet Information Services & "OK"

2. Download & Install the [FastCGI Extension]('https://www.iis.net/downloads/microsoft/fastcgi-for-iis')

3. Download & Install PHP Manager for IIS (*in this repo*)

4. Set the Windows hosts file

   - **Run Notepad (or your preferred editor) as Administrator** Find the program, right-click > Run as administrator
   - Open the file `C:\Windows\System32\drivers\etc\hosts` 
     
      \* `hosts` **is not** a "Text Document" - look for "All Files"
   - To listen for http://dev.local, add `127.0.0.1       dev.local`

5. Setup a new site in IIS

   - Open IIS, Expand root directory, Right click on Sites > Add Website
   - Site name = `dev.local`
   - Physical path = `C:\dev`
   - Host name = `dev.local`

6. Test server configuration by navigating to `http://dev.local` in a browser- phpinfo should be returned by `C:\dev\index.php`.

## Version Control

1. Download & install [git]('https://git-scm.com/download/win') & [Sourcetree]('https://www.sourcetreeapp.com/')

2. Download & install [PuttyGen]('https://www.puttygen.com/download-putty')

3. Generate private keys with PuttyGen, save to local machine & upload to your git server.

## PHP

1. [Download desired PHP versions]('https://windows.php.net/download/') (*non-thread-safe for IIS*) and extract to `C:\PHP\*version*`

2. Create a new directory `C:\PHP\Temp`

3. Open IIS PHP Manager and register each PHP version under the PHP Setup section.

4. Update each `php.ini` to set configuration and enable extensions

\* *The `php.ini` in this repo is for v.7.4.11 nts with recommended settings*

```
extension_dir = "C:\PHP\7.4.11\ext\"

error_log = "C:\PHP\php-7.4.11_errors.log"

upload_tmp_dir = "C:\PHP\Temp\"

; Recommended Opcache settings
opcache.enable=1
opcache.enable_cli=1
opcache.memory_consumption=128
opcache.interned_strings_buffer=8
opcache.max_accelerated_files=4000
opcache.revalidate_freq=60
opcache.fast_shutdown=1
```

5. Download & install [Composer]('https://getcomposer.org/Composer-Setup.exe')

## Nodejs

1. Download & install [Nodejs]('https://nodejs.org/en/')

2. Install NPM packages globally
   - `npm install -g grunt-cli gulp `

## Python

1. Download & install [Python](https://www.python.org/downloads/) (*recommend both 2 & 3, but only add v3 to Windows system Path*)

2. Install global packages
   - `pip install pandas pandasgui `

## Ruby

1. Download & install [Ruby]('https://rubyinstaller.org/downloads/')

2. Install global packages
   - `gem install rails sass`

## Database

1. Download & install [MariaDB]('https://mariadb.com/downloads/') & [PostgreSQL]('https://www.postgresql.org/download/windows/')

2. Download & install a database manager
   - [HeidiSQL]('https://www.heidisql.com/download.php'), [Adminer]('https://www.adminer.org/'), [phpMyAdmin]('https://www.phpmyadmin.net/downloads/')
  
3. Create empty databases for each system to be developed (django, drupal7, drupal9, wordpress)

## Setup

1. Download & extract  [Drupal]('https://www.drupal.org/project/drupal/releases') and [Wordpress]('https://wordpress.org/download/') to the dev directory

   - i.e. `C:\dev\drupal7`, `C:\dev\wordpress`)

2. Install & manage Drupal with git & composer:

    - `cd C:\dev`
    - `git clone --branch 7.x https://git.drupalcode.org/project/drupal.git d7`
    - `git clone --branch 9.2.x https://git.drupalcode.org/project/drupal.git d9`

3. Navigate to the correct subdirectory from the local dev directory in a browser (i.e. `http://dev.local/drupal7`, `http://dev.local/wordpress`) to install the CMS.

4. Check the php_error.log to confirm configuration is correct (*if no log file is present, all is well*)