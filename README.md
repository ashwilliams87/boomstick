Markdown# Boomstick
## Description

Boomstick is a PHP library designed to generate JSON objects representing HTML forms, control elements, and tables. It is particularly useful for creating structured data for REST API responses that can be consumed by frontend frameworks like Angular to render dynamic user interfaces.

The library provides classes and interfaces to build form areas with various controls (buttons, checkboxes, selects, date ranges, etc.) and tables with customizable columns and actions.

## Features

- Generate JSON for form controls and areas.
- Build tables with headers, rows, columns, and actions.
- Supports PSR-4 autoloading.
- Tested with Codeception.

## Requirements

- PHP 7.0 to 8.0

## Installation

Since the package is not yet published on Packagist, you can install it by cloning the repository and requiring it locally, or add it as a repository in your `composer.json`.

1. Clone the repository:

   ```bash
   git clone https://github.com/ashwilliams87/boomstick.git

Add to your composer.json (in the requiring project):JSON"repositories": [
    {
        "type": "path",
        "url": "/path/to/boomstick"
    }
],
"require": {
    "lan/boomstick": "dev-main"
}
Run:Bashcomposer install

Alternatively, if published in the future:
Bashcomposer require lan/boomstick
Usage
Creating a JSON Control Area (Form)
The JsonControlArea class allows you to build a collection of form controls and render them as JSON.
Example:
PHP<?php

use Lan\Ebs\Boomstick\JsonControlArea;
use Lan\Ebs\Boomstick\Items\Button; // Example import; adjust based on actual usage

$area = new JsonControlArea('my_form_area');

$area->addButton('submit_button', 'Submit', function($button) {
    // Optional callback to configure the button further
    // e.g., $button->setAttribute('class', 'btn-primary');
});

$area->addCheckbox('agree', 'I agree', function($checkbox) {
    // Configure checkbox
});

$area->addSelect('options', 'default_value', 'Select Option', ['option1' => 'Value 1', 'option2' => 'Value 2']);

$json = $area->renderJson();

echo $json;
This will output a JSON structure like:
JSON{
    "my_form_area": [
        // Array of control objects
    ]
}
Creating a Table
The Table class helps generate JSON for tabular data.
Example:
PHP<?php

use Lan\Ebs\Boomstick\Table;
use Lan\Ebs\Boomstick\Items\Common\Column; // Example import

$rows = [
    ['id' => 1, 'name' => 'Item 1'],
    ['id' => 2, 'name' => 'Item 2']
];

$table = Table::create('My Table', $rows);

$table->setColumn('id', 'ID');
$table->setColumn('name', 'Name', function($column) {
    // Optional callback
    // e.g., $column->setStyle(...);
});

$json = $table->renderJson();

echo $json;
This produces JSON representing the table structure, including type, header, columns, and rows.
Testing
The library includes tests in the tests/ directory using Codeception.
To run the tests:

Install dev dependencies:Bashcomposer install --dev
Run Codeception:Bashvendor/bin/codecept run

Directory Structure

src/: Core library files
Interfaces/: Interfaces like Action, Area, Control, Item
Items/: Control items
Common/: Common elements like Action, Column, Style
Specific controls: AreaItem.php, Button.php, Checkbox.php, Daterange.php, Select.php, Tabs.php

JsonControlArea.php: Main class for form areas
Table.php: Main class for tables

tests/: Unit and functional tests
composer.json: Package definition
LICENSE: GPL-2.0-or-later license

Contributing
Contributions are welcome! Please fork the repository and submit a pull request with your changes. Ensure that tests pass and add new tests for any new features.
License
This library is licensed under the GPL-2.0-or-later.
Author

Emil Limarenko (ash_williams@mail.ru)
