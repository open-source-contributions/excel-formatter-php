[![Actions Status](https://github.com/renekorss/excel-formatter-php/workflows/build/badge.svg)](https://github.com/renekorss/excel-formatter-php/actions)
[![Coverage Status](https://coveralls.io/repos/renekorss/excel-formatter-php/badge.svg?branch=master&service=github)](https://coveralls.io/github/renekorss/excel-formatter-php?branch=master)
[![Latest Stable Version](https://poser.pugx.org/renekorss/phpexcelformatter/v/stable)](https://packagist.org/packages/renekorss/phpexcelformatter)
[![Total Downloads](https://poser.pugx.org/renekorss/phpexcelformatter/downloads)](https://packagist.org/packages/renekorss/phpexcelformatter)
[![License](http://img.shields.io/badge/license-MIT-blue.svg)](LICENSE)

# PHPExcelFormatter

PHPExcelFormatter is class to make getting data from Excel documents simpler.

* Read columns what you really need
* Set column names for documents what dosen't have column names on first row
* Set your DB field names for columns
* Retrieve data in array or MySQL query format
* Greate for importing files and then letting user to connect document columns with your DB fields :) (example coming)

## Install

	composer require renekorss/phpexcelformatter

## Usage

```php
// Require needed files
require __DIR__ . '/vendor/autoload.php';

use RKD\PHPExcelFormatter\PHPExcelFormatter;
use RKD\PHPExcelFormatter\Exception\PHPExcelFormatterException;

try{
  // Load file
  $formatter = new PHPExcelFormatter('example1.xls');

  // Output columns array (document must have column names on first row)
  $formatterColumns = array(
    'username' => 'username',
    'phone'    => 'phone_no',
    'email'    => 'email_address'
  );

  // Output columns array (document dosen't have column names on first row)
  // Skip fourth column (age) (third in array), because we don't need that data
  // NOTE: if document dosen't have column names on first line, second parameter for PHPExcelFormatter should be $readColumns = false, otherwise it will skip first line of data
  $formatterColumns = array(
    'username',
    'email_address',
    'phone',
    4 => 'sex'
  );

  // Set our columns
  $formatter->setFormatterColumns($formatterColumns);

  // Output as array
  $output = $formatter->output('a');
  // OR
  // $output = $formatter->output('array');

  // Print array
  echo '<pre>'.print_r($output, true).'</pre>';

  // Set MySQL table
  $formatter->setMySQLTableName('users');

  // Output as mysql query
  $output = $formatter->output('m');
  // OR
  // $output = $formatter->output('mysql');

  // Print mysql query
  echo '<pre>'.print_r($output, true).'</pre>';

}catch(PHPExcelFormatterException $e){
  echo 'Error: '.$e->getMessage();
}
```

View [examples](examples)

## License

PHPExcelFormatter is licensed under [MIT](LICENSE)
