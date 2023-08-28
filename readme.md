# PHPUnit Test Setup on Windows for WordPress Plugins

Setting up PHPUnit tests for WordPress plugins on Windows involves several steps. Follow this guide to ensure a smooth setup.

### Install WP-CLI

1. You can install WPCLI using Composer with the following command:

	```sh
	composer global require wp-cli/wp-cli-bundle
	```

2. Verify if WPCLI is installed:
	```sh
	wp
	```
If you encounter any issues, refer to the [WordPress Official Documentation](https://make.wordpress.org/cli/handbook/guides/installing/) for additional installation options.

### Install SVN Command Line Interface

To install the SVN command line tools:

1. Download and install [TortoiseSVN Software](https://tortoisesvn.net/)
2. Install the command line client tools. Here's an image illustrating the process:

	<img src="https://i.ibb.co/FBFFQXx/image.png"/>


### Ensure MySQL Global Setup

1. To ensure MySQL is appropriately set up:
	```sh
	mysqladmin --version
	```

2. If the MySQL admin tool is not installed, but you are using a local server such as Laragon, WampServer, or XAMPP, add the MySQL bin directory to your system's environment variables.

2. If you're not using a local server, download MySQL from the [Official Website](https://dev.mysql.com/downloads/installer/) and install it.

###  Install PHPUnit Globally

PHPUnit can be installed globally using Composer:

1. Install using Composer with the following command:

	```sh
	composer global require phpunit/phpunit
	```

2. If you encounter version compatibility issues, visit [Packagist](https://packagist.org/packages/phpunit/phpunit) to find your required version. Install PHPUnit with your desired version using:

	```sh
	composer global require phpunit/phpunit:9.6.11
	```
### Setup test environment using install-wp-tests.sh

1. Run the Command

	Execute the following command, replacing `<db-name>`, `<db-user>`, `<db-pass>`, and `<db-host>` with your actual database details:

	```sh
	bash install-wp-tests.sh <db-name> <db-user> <db-pass> <db-host>	
	```
2. Example

	As an example, here's how you might run the command:
	```sh
	bash bin/install-wp-tests.sh wordpress_test root '' localhost latest
	```

### Generating Files for PHPUnit Tests in a Plugin

To generate the necessary files for running PHPUnit tests within a plugin, follow these steps:

1. Open the terminal on your plugin directory

2. Generate the files using the WP-CLI scaffold command:
	```sh
	wp scaffold plugin-tests my-plugin
	```
3. Install [Yoast/PHPUnit-Polyfills](https://github.com/Yoast/PHPUnit-Polyfills/)
	```sh
	composer require --dev yoast/phpunit-polyfills:"^2.0"
	```
4. Define the path to Polyfills in your phpunit.xml[.dist] file:
	```xml
	<php>
        <const name="WP_TESTS_PHPUNIT_POLYFILLS_PATH" value="vendor/yoast/phpunit-polyfills"/>
	</php>
	```
5. Run PHPUnit Tests:
	```sh
	phpunit
	```

### Fix Fatal Error
If you encounter a fatal error like the following:

	```
	Warning: require_once(/tmp/wordpress//wp-includes/class-phpmailer.php): failed to open stream: No such file or directory in /tmp/wordpress-tests-lib/includes/mock-mailer.php on line 2

	Fatal error: require_once(): Failed opening required '/tmp/wordpress//wp-includes/class-phpmailer.php' (include_path='.:/opt/lampp/lib/php') in /tmp/wordpress-tests-lib/includes/mock-mailer.php on line 2
	```
1. Open your `C:\Users\{USER\AppData\Local\Temp\wordpress-tests-lib\wp-tests-config.php` file and change the ABSPATH with the absolute path to your TEMP folder, for example: `C:/Users/{USER}/AppData/Local/Temp/wordpress-tests-lib/`.

By following these steps, you empower yourself to develop high-quality WordPress plugins with confidence. Automated testing not only prevents regressions and bugs but also fosters a culture of continuous improvement in your development process. So, take the time to set up your testing environment and enjoy the benefits of robust and reliable plugin development. Happy coding!
