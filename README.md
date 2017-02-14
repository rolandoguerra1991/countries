# Countries
## A Laravel Countries package, with lots of information  

[![Latest Stable Version](https://img.shields.io/packagist/v/pragmarx/countries.svg?style=flat-square)](https://packagist.org/packages/pragmarx/countries) [![License](https://img.shields.io/badge/license-BSD_3_Clause-brightgreen.svg?style=flat-square)](LICENSE) [![Downloads](https://img.shields.io/packagist/dt/pragmarx/countries.svg?style=flat-square)](https://packagist.org/packages/pragmarx/countries) [![Code Quality](https://img.shields.io/scrutinizer/g/antonioribeiro/countries.svg?style=flat-square)](https://scrutinizer-ci.com/g/antonioribeiro/countries/?branch=master) [![StyleCI](https://styleci.io/repos/74829244/shield)](https://styleci.io/repos/74829244)

### What does it gives you?

This package is a collection of some other packages with information on:

- Countries
    - name (common and native)
    - tld
    - multiple ISO codes
    - currency
    - calling code
    - capital
    - alternate spellings
    - region & sub region
    - languages
    - translations (country name translated to some other languages)
    - latitude and logitude
    - borders (countries) - you can hydrate those borders (like relatioships)
    - area
    - flags (sprites, flag icons, svg)
    - states
    - topology 
    - geometry

- Currencies
    - sign
    - ISO codes
    - title
    - subunits
    - usage (dates)
    
- States 
    - adm codes
    - name & alt name
    - type (state, city, province, canton, department, district, etc.)
    - latitude & longitude
    - language
    - (and many more)

## Getting the information
 
The package is based on Laravel Collections, so you basically have access to all methods in Collections, like 

    $all = Countries::all();
     
This filter

    Countries::where('name.common', 'Brazil')

Will find Brazil by its common name, which is a 

      #items: array:22 [▼
        "name" => array:3 [▼
          "common" => "Brazil"
          "official" => "Federative Republic of Brazil"
          "native" => array:1 [▼
            "por" => array:2 [▼
              "official" => "República Federativa do Brasil"
              "common" => "Brasil"
            ]
          ]
        ]
        
And, you can go deepeer
         
     Countries::where('name.native.por.common', 'Brasil')
     
Or search by the country top level domain
     
     Countries::where('tld.0', '.ch')
     
To get

    "name" => array:3 [▼
      "common" => "Switzerland"
      "official" => "Swiss Confederation"
      "native" => array:4 [▶]
    ]
    "tld" => array:1 [▼
      0 => ".ch"
    ]
    
And use things like pluck

    Countries::where('cca3', 'USA')->first()->states->pluck('name', 'postal')

To get

    "MA" => "Massachusetts"
    "MN" => "Minnesota"
    "MT" => "Montana"
    "ND" => "North Dakota"
    "HI" => "Hawaii"
    "ID" => "Idaho"
    "WA" => "Washington"
    "AZ" => "Arizona"
    "CA" => "California"
    "CO" => "Colorado"
    "NV" => "Nevada"
    "NM" => "New Mexico"
    "OR" => "Oregon"
    "UT" => "Utah"
    "WY" => "Wyoming"
    "AR" => "Arkansas"
    "IA" => "Iowa"
    "KS" => "Kansas"
    "MO" => "Missouri"
    "NE" => "Nebraska"
    "OK" => "Oklahoma"
    "SD" => "South Dakota"
    "LA" => "Louisiana"
    "TX" => "Texas"
    "CT" => "Connecticut"
    "NH" => "New Hampshire"
    "RI" => "Rhode Island"
    "VT" => "Vermont"
    "AL" => "Alabama"
    "FL" => "Florida"
    "GA" => "Georgia"
    "MS" => "Mississippi"
    "SC" => "South Carolina"
    "IL" => "Illinois"
    "IN" => "Indiana"
    "KY" => "Kentucky"
    "NC" => "North Carolina"
    "OH" => "Ohio"
    "TN" => "Tennessee"
    "VA" => "Virginia"
    "WI" => "Wisconsin"
    "WV" => "West Virginia"
    "DE" => "Delaware"
    "DC" => "District of Columbia"
    "MD" => "Maryland"
    "NJ" => "New Jersey"
    "NY" => "New York"
    "PA" => "Pennsylvania"
    "ME" => "Maine"
    "MI" => "Michigan"
    "AK" => "Alaska"
          
The package uses a modified Collection which allows you to access properties and methods as objects:
         
    Countries::where('cca3', 'FRA')->first()->borders->first()->first()->name->official
    
Should give
    
    Principality of Andorra
         
Borders hydration is disabled by default, but you can have your borders hydrated easily by calling the hydrate method:
 
    Countries::getRepository()->hydrate(
        Countries::where('cca3', 'GBR'), ['borders' => true]
    )->first()->borders->reverse()->first()->first()->name->common      

## Sample file

Take a look at the [sample.json](sample.json) file to see an example of country with all fields hydrated.
         
## Requirements

- PHP 7.0+
- Laravel 5.3+

## Installing

Use Composer to install it:

    composer require pragmarx/countries

## Installing on Laravel

Add the Service Provider and Facade alias to your `app/config/app.php` (Laravel 4.x) or `config/app.php` (Laravel 5.x):

    PragmaRX\Countries\ServiceProvider::class,

## Author

[Antonio Carlos Ribeiro](http://twitter.com/iantonioribeiro)

## License

Countries is licensed under the BSD 3-Clause License - see the `LICENSE` file for details

## Contributing

Pull requests and issues are more than welcome.



