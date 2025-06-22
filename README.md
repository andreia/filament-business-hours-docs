# Filament Business Hours Plugin

A powerful and flexible Filament plugin for managing business hours in your application. Built on top of [spatie/opening-hours](https://github.com/spatie/opening-hours), this plugin provides a complete solution for handling business hours with an elegant Filament interface.

![Filament Business Hours Form Field With Exceptions](https://raw.githubusercontent.com/andreia/filament-business-hours-docs/main/art/business_hours_form_field1.png)

## Features

### Rich Form Field
- **Global Enable/Disable**: Toggle to quick enable/disable existing business hours
- **Dynamic Time Slots**: Add multiple time ranges per day
- **Timezone Support**: Built-in timezone selection with searchable dropdown
- **Quick Toggles**: Enable/disable specific days with a single click
- **Visual Feedback**: Clear visual indicators for open/closed status
- **Flexible Layout**: Use Filament's available layout components for a responsive and customizable layout

### Exception Management
- **Date-based Exceptions**: Handle holidays, special hours, and closures
- **Recurring Exceptions**: Set up annual recurring exceptions (e.g., Christmas)
- **Date Ranges**: Define exceptions for specific date ranges
- **Custom Labels**: Add descriptions to exceptions for better organization

### Display Components
- **Table Column**: Business days displayed as interactive circles with tooltips showing opening/closing times and distinct color for opening days.
- **InfoList Entry**: Display formatted business hours with timezone and exceptions
- **Widget Support**: Use as a standalone widget in your dashboard

### Developer-Friendly
- **Trait-based Integration**: Quick add business hours to any model with `HasBusinessHours` trait
- **Cache Support**: Built-in caching for optimal performance
- **Flexible Data Retrieving**: Rich set of methods for querying business hours with Spatie Opening Hours

## Video

Take a look at what Filament Business Hours can do in this short feature-packed video!  
[![Filament Business Hours Youtube Video](https://raw.githubusercontent.com/andreia/filament-business-hours-docs/main/art/youtube_cover.jpg)](https://www.youtube.com/watch?v=5gXI0v3BwAU)

## Screenshots

Form Field

![Filament Business Hours Form Field](https://raw.githubusercontent.com/andreia/filament-business-hours-docs/main/art/business_hours_form_field.png)

Form Field with Exceptions

![Filament Business Hours Form Field With Exceptions](https://raw.githubusercontent.com/andreia/filament-business-hours-docs/main/art/business_hours_form_field_exceptions.png)

Exceptions Modal

![Filament Business Hours Form Field Exceptions Modal](https://raw.githubusercontent.com/andreia/filament-business-hours-docs/main/art/business_hours_form_field_exceptions_modal.png)

Table Column

![Filament Business Hours Table Column](https://raw.githubusercontent.com/andreia/filament-business-hours-docs/main/art/business_hours_table_column.png)

![Filament Business Hours Table Column](https://raw.githubusercontent.com/andreia/filament-business-hours-docs/main/art/business_hours_table_column1.png)

![Filament Business Hours Table Column](https://raw.githubusercontent.com/andreia/filament-business-hours-docs/main/art/business_hours_table_column2.png)

Infolist Entry

![Filament Business Hours Infolist Entry](https://raw.githubusercontent.com/andreia/filament-business-hours-docs/main/art/business_hours_infolist.png)

## Requirements

- PHP 8.2+
- Filament 3

## Dependencies

This package use the following dependencies:

- [Spatie Opening Hours](https://github.com/spatie/opening-hours)
- [Filament Timezone Field](https://github.com/TappNetwork/filament-timezone-field)
- [Filament Table Repeater](https://github.com/awcodes/filament-table-repeater)

Before install the Business Hours Plugin, make sure the Table Repeater Filament plugin is configured according to the the docs:
https://github.com/awcodes/filament-table-repeater?tab=readme-ov-file#installation

For more information about Spatie Opening Hours, please refer to the official [Spatie Opening Hours documentation](https://github.com/spatie/opening-hours).

## Installation

## Activating Your License on AnyStack

Filament Business Hours uses AnyStack to handle payment, licensing, and distribution. [You can buy it here](https://checkout.anystack.sh/filament-business-hours).

During the purchasing process, AnyStack will provide you with a license key. Once your license key is activated, you can proceed with the Composer installation described below.

## Installing with Composer

Add the the Filament Business Hours package to repositories section of your `composer.json` file:

```
{
    "repositories": [
        {
            "type": "composer",
            "url": "https://filament-business-hours.composer.sh"
        }
    ]
}
```

Once the repository has been added to the `composer.json` file, you can install like any other Composer package using the `composer require` command:

### Filament 3

Install the package via Composer:
```bash
composer require andreia/filament-business-hours
```

Next, you will be prompted to provide your username and password.

```
Loading composer repositories with package information
Authentication required (filament-business-hours.composer.sh):
Username: [license-email]
Password: [license-key]
```

Your username will be your email address and the password will be your license key. For example, let's say we have the following email and license activation:

```
Contact email: your@email.com
License key: 04c21df8f-4890-7024-y2vk-6bny143ta642
```

You will need to enter the above information as follows when prompted for your credentials:

```
Loading composer repositories with package information
Authentication required (filament-business-hours.composer.sh):
Username: your@email.com
Password: 04c21df8f-4890-7024-y2vk-6bny143ta642
```

### Filament 4

Coming soon

### Publish and run the migrations

```bash
php artisan vendor:publish --tag="filament-business-hours-migrations"
php artisan migrate
```

### Publish the config file (optional)

You can publish the config file with:

```bash
php artisan vendor:publish --tag="filament-business-hours-config"
```

### Publish Views (optional)

Optionally, you can publish the views using:

```bash
php artisan vendor:publish --tag="filament-business-hours-views"
```

### Plublish Translations (optional)

The package comes with English translations out of the box. Publish the language files to customize:

```bash
php artisan vendor:publish --tag="filament-business-hours-translations"
```

### Add the Business Hours path in your Tailwind config file

Filament recommends developers create a custom theme to better support plugin's additional TailwindCSS classes. After you have created your [custom theme](https://filamentphp.com/docs/3.x/panels/themes), add the Business Hours vendor views directory to your theme's `tailwind.config.js` file usually located in `resources/css/filament/admin/tailwind.config.js`:

```js
// ...

export default {
    content: [
        // ...
        './vendor/andreia/filament-business-hours/resources/**/*.blade.php',
    ],
}
```

## Usage

### Add Business Hours to Your Model

The `HasBusinessHours` Trait provides the `businessHours` relationship and convenient methods to quick build business/opening hours Spatie object. 

Add the included `HasBusinessHours` trait to the model (e.g., `User`, `Team`, `Company` etc.) that you want to add business hours:

```php
use Andreia\FilamentBusinessHours\Concerns\HasBusinessHours;

class Business extends Model
{
    use HasBusinessHours;
}
```

It gives you:

- A `morphOne` relationship to `BusinessHours`
- An accessor to get `OpeningHours` as an instance
- Helper methods to query if the entity is currently open, next opening time, next closing time, and more
- Fully compatible with Spatie’s Opening Hours

### Query Business Hours

```php
$modelWithBusinessHours = Company::find($companyId);

// Check if business is open
$modelWithBusinessHours->isOpen();

// Get next opening time
$nextOpen = $modelWithBusinessHours->nextOpen();

// Get current open range
$range = $modelWithBusinessHours->currentOpenRange();

// Check specific date/time
$isOpen = $modelWithBusinessHours->isOpen(now()->addDays(2));
```

You can also use all Spatie's Opening Hours methods available to query and format the set of business/opening hours.

### Use in Forms

```php
use Andreia\FilamentBusinessHours\Forms\Components\BusinessHoursField;

BusinessHoursField::make('businessHours')
    ->allowExceptions()
```

Any Form layout can be used to wrap the business hours, for example, using `Section`:

```php
use Andreia\FilamentBusinessHours\Forms\Components\BusinessHoursField;

Forms\Components\Section::make('Business Hours')
    ->description('Control the availability of hours on each weekday')
    ->icon('heroicon-o-clock')
    ->schema([
        BusinessHoursField::make('businessHours')
            ->allowExceptions(),
    ]),
```

#### Options

**Allow Exceptions**

To allow the user provide exceptions to the business hours added, use the `->allowExceptions()` method. It will show the button to set up exceptions.

```php
use Andreia\FilamentBusinessHours\Forms\Components\BusinessHoursField;

$form->schema([
    // ...
    BusinessHoursField::make('businessHours')
        ->allowExceptions(),
]),
```

The exceptions can be added through a modal UI opened by the “Set up” button in the form.

The exceptions will be saved in Spatie-style on `exceptions` database column:

```php
'exceptions' => [
    '2025-11-11' => ['09:00-12:00'],
    '2025-07-04' => [],                  // closed all day
    '01-01'      => [],                  // recurring annually
    '12-25'      => ['09:00-12:00'],     // recurring annually
    '12-25 to 12-25' => [
        'hours' => [],
        'data' => 'Holidays',
    ],
    '2025-06-25 to 2025-07-01' => [
        'hours' => [],
        'data' => 'Closed for works',
    ],
]
```

### Display in Tables

```php
use Andreia\FilamentBusinessHours\Tables\Columns\BusinessHoursColumn;

// businessHours is the name of the relationship
BusinessHoursColumn::make('businessHours')
```

### Show in InfoLists

```php
use Andreia\FilamentBusinessHours\Infolists\Components\BusinessHoursEntry;

// businessHours is the name of the relationship
BusinessHoursEntry::make('businessHours')
```

Any Infolist layout can be used to wrap the business hours, for example, using `Section`:

```php
use Andreia\FilamentBusinessHours\Infolists\Components\BusinessHoursEntry;
use Filament\Infolists;

Infolists\Components\Section::make('Business Hours')
    ->description('Control the availability of hours on each weekday')
    ->icon('heroicon-o-clock')
    ->schema([
        BusinessHoursEntry::make('businessHours')
            ->hiddenLabel()
            ->columnSpanFull(),
    ]),
```

## Testing

```bash
composer test
```

## Changelog

Please see [CHANGELOG](https://changelog.anystack.sh/filament-business-hours) for more information on what has changed recently.

## Contributing

Users with active licenses may access the private repo to contribute by visiting the `Licenses` tab of your AnyStack account. 

## Need Assistance?

If you have any questions, find a bug, need support, or have a feature request or suggestion, please don't hesitate to reach out to me at [andreiabohner@gmail.com](mailto:andreiabohner@gmail.com). I'd love to hear from you.

## Licensing Information

### Single Project License

The Single Project license allows for the utilization of Filament Business Hours within a single project hosted on
one domain or subdomain. It is suitable for personal websites or websites tailored to specific clients.

If you intend to incorporate Filament Business Hours into a SaaS application, you must obtain an Unlimited Projects or
Lifetime license.

Under the Single Project license, you are authorized to activate Filament Business Hours up to 4 times (development,
test, staging, and production).

You will receive updates and bug fixes for one year from the purchase date. If you choose not to renew your license, you
can only install the plug-in up to the latest version available before the license expiration. Renewing the license at a
discounted price allows you to continue receiving updates and new features.

### Unlimited Projects License

The Unlimited Projects license permits the utilization of Filament Business Hours on **unlimited** domains, subdomains,
and even in SaaS applications.

You will receive updates and bug fixes for one year from the purchase date. If you choose not to renew your license, you
can only install the plug-in up to the latest version available before the license expiration. Renewing the license at a
discounted price allows you to continue receiving updates and new features.

### Code Distribution

Please note that the licenses for Filament Business Hours does not allow the public distribution of its source code. Hence,
you cannot build and distribute applications publicly using Filament Business Hours source code on open-source platforms.

### Questions About Licensing?

If you're uncertain about which license is appropriate for your needs, don't hesitate to reach out. Contact me at
[andreiabohner@gmail.com](mailto:andreiabohner@gmail.com), and I'll be glad to assist you.
