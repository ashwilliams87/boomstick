# Boomstick

[![PHP Version](https://img.shields.io/badge/PHP-7.0%20--%208.0-blue.svg)](https://php.net)
[![License](https://img.shields.io/badge/License-GPL--2.0--or--later-green.svg)](LICENSE)

**Boomstick** is a PHP library designed to generate JSON objects representing HTML forms, control elements, and tables. It is particularly useful for creating structured data for REST API responses that can be consumed by frontend frameworks like Angular to render dynamic user interfaces.

The library provides classes and interfaces to build form areas with various controls (buttons, checkboxes, selects, date ranges, etc.) and tables with customizable columns and actions.

---

## Features

- **Dynamic JSON Generation** — Create JSON for form controls and areas on the fly
- **Table Builder** — Easily build tables with headers, rows, columns, and custom actions
- **PSR-4 Compliant** — Fully supports modern autoloading standards
- **Tested** — Built-in test suite using Codeception

---

## Requirements

- **PHP**: 7.0 to 8.0

---

## Installation

Since the package is not yet published on Packagist, you can install it by cloning the repository or adding it as a local repository in your `composer.json`.

### 1. Clone the repository

```bash
git clone https://github.com/ashwilliams87/boomstick.git
```

### 2. Add to your project's `composer.json`

```json
{
    "repositories": [
        {
            "type": "path",
            "url": "/path/to/boomstick"
        }
    ],
    "require": {
        "lan/boomstick": "dev-main"
    }
}
```

### 3. Install dependencies

```bash
composer install
```

---

## Usage

### Creating a JSON Control Area (Form)

The `JsonControlArea` class allows you to build a collection of form controls and render them as JSON.

```php
<?php

use Lan\Ebs\Boomstick\JsonControlArea;

$area = new JsonControlArea('my_form_area');

$area->addButton('submit_button', 'Submit', function($button) {
    $button->setAttribute('class', 'btn-primary');
});

$area->addCheckbox('agree', 'I agree', function($checkbox) {
    $checkbox->setChecked(true);
});

$area->addSelect(
    'options',
    'default_value',
    'Select Option',
    [
        'option1' => 'Value 1',
        'option2' => 'Value 2'
    ]
);

echo $area->renderJson();
```

### Creating a Table

The `Table` class helps generate JSON for tabular data.

```php
<?php

use Lan\Ebs\Boomstick\Table;
use Lan\Ebs\Boomstick\Items\Common\Column;

$rows = [
    ['id' => 1, 'name' => 'Item 1'],
    ['id' => 2, 'name' => 'Item 2']
];

$table = Table::create('My Table', $rows);
$table->setColumn('id', 'ID');
$table->setColumn('name', 'Name', function(Column $column) {
    $column->setStyle('font-weight', 'bold');
});

echo $table->renderJson();
```

---

## Directory Structure

```
src/
├── Interfaces/           # Core interfaces (Action, Area, Control, Item)
├── Items/                # Implementation of UI elements
│   ├── Common/           # Shared components (Column, Style)
│   └── ...               # Button, Checkbox, Select, etc.
├── JsonControlArea.php   # Main form builder
└── Table.php             # Main table builder
```

---

## Testing

The library uses [Codeception](https://codeception.com/) for unit and functional testing.

```bash
composer install --dev
vendor/bin/codecept run
```

---

## Contributing

1. Fork the repository
2. Create a feature branch (`git checkout -b feature/amazing-feature`)
3. Commit your changes (`git commit -m 'Add some amazing feature'`)
4. Push to the branch (`git push origin feature/amazing-feature`)
5. Open a Pull Request

---

## License

This library is licensed under the [GPL-2.0-or-later](LICENSE) license.

---

## Author

**Emil Limarenko** — [ash_williams@mail.ru](mailto:ash_williams@mail.ru)
