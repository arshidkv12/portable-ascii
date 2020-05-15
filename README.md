[![Build Status](https://travis-ci.org/voku/portable-ascii.svg?branch=master)](https://travis-ci.org/voku/portable-ascii)
[![Build status](https://ci.appveyor.com/api/projects/status/gnejjnk7qplr7f5t/branch/master?svg=true)](https://ci.appveyor.com/project/voku/portable-ascii/branch/master)
[![Coverage Status](https://coveralls.io/repos/voku/portable-ascii/badge.svg?branch=master&service=github)](https://coveralls.io/github/voku/portable-ascii?branch=master)
[![Codacy Badge](https://api.codacy.com/project/badge/Grade/997c9bb10d1c4791967bdf2e42013e8e)](https://www.codacy.com/app/voku/portable-ascii)
[![Latest Stable Version](https://poser.pugx.org/voku/portable-ascii/v/stable)](https://packagist.org/packages/voku/portable-ascii) 
[![Total Downloads](https://poser.pugx.org/voku/portable-ascii/downloads)](https://packagist.org/packages/voku/portable-ascii)
[![License](https://poser.pugx.org/voku/portable-ascii/license)](https://packagist.org/packages/voku/portable-ascii)
[![Donate to this project using Paypal](https://img.shields.io/badge/paypal-donate-yellow.svg)](https://www.paypal.me/moelleken)
[![Donate to this project using Patreon](https://img.shields.io/badge/patreon-donate-yellow.svg)](https://www.patreon.com/voku)

# 🔡 Portable ASCII

## Description

It is written in PHP (PHP 7+) and can work without "mbstring", "iconv" or any other extra encoding php-extension on your server. 

The benefit of Portable ASCII is that it is easy to use, easy to bundle.

The project based on ...
+ Portable UTF-8 work (https://github.com/voku/portable-utf8) 
+ Daniel St. Jules's work (https://github.com/danielstjules/Stringy) 
+ Johnny Broadway's work (https://github.com/jbroadway/urlify)
+ and many cherry-picks from "github"-gists and "Stack Overflow"-snippets ...

## Index

* [Alternative](#alternative)
* [Install](#install-portable-ascii-via-composer-require)
* [Why Portable ASCII?](#why-portable-ascii)
* [Requirements and Recommendations](#requirements-and-recommendations)
* [Usage](#usage)
* [Class methods](#class-methods)
* [Unit Test](#unit-test)
* [License and Copyright](#license-and-copyright)

## Alternative

If you like a more Object Oriented Way to edit strings, then you can take a look at [voku/Stringy](https://github.com/voku/Stringy), it's a fork of "danielstjules/Stringy" but it used the "Portable ASCII"-Class and some extra methods. 

```php
// Portable ASCII
use voku\helper\ASCII;
ASCII::to_transliterate('déjà σσς iıii'); // 'deja sss iiii'

// voku/Stringy
use Stringy\Stringy as S;
$stringy = S::create('déjà σσς iıii');
$stringy->toTransliterate();              // 'deja sss iiii'
```

## Install "Portable ASCII" via "composer require"
```shell
composer require voku/portable-ascii
```

##  Why Portable ASCII?[]()
I need ASCII char handling in different classes and before I added this functions into "Portable UTF-8",
but this repo is more modular and portable, because it has no dependencies.

## Requirements and Recommendations

*   No extensions are required to run this library. Portable ASCII only needs PCRE library that is available by default since PHP 4.2.0 and cannot be disabled since PHP 5.3.0. "\u" modifier support in PCRE for ASCII handling is not a must.
*   PHP 7.0 is the minimum requirement

## Usage

Example: ASCII::to_ascii()
```php
  echo ASCII::to_ascii('�Düsseldorf�', 'de');
  
  // will output
  // Duesseldorf

  echo ASCII::to_ascii('�Düsseldorf�', 'en');
  
  // will output
  // Dusseldorf
```

# Portable ASCII | API

The API from the "ASCII"-Class is written as small static methods.


## Class methods

<table><tr><td><a href="#charsarraybool-replace_extra_symbols-array">charsArray</a>
</td><td><a href="#charsarraywithmultilanguagevaluesbool-replace_extra_symbols-array">charsArrayWithMultiLanguageValues</a>
</td><td><a href="#charsarraywithonelanguagestring-language-bool-replace_extra_symbols-bool-asorigreplacearray-array">charsArrayWithOneLanguage</a>
</td><td><a href="#charsarraywithsinglelanguagevaluesbool-replace_extra_symbols-bool-asorigreplacearray-array">charsArrayWithSingleLanguageValues</a>
</td></tr><tr><td><a href="#cleanstring-str-bool-normalize_whitespace-bool-keep_non_breaking_space-bool-normalize_msword-bool-remove_invisible_characters-string">clean</a>
</td><td><a href="#getalllanguages-string">getAllLanguages</a>
</td><td><a href="#is_asciistring-str-bool">is_ascii</a>
</td><td><a href="#normalize_mswordstring-str-string">normalize_msword</a>
</td></tr><tr><td><a href="#normalize_whitespacestring-str-bool-keepnonbreakingspace-bool-keepbidiunicodecontrols-string">normalize_whitespace</a>
</td><td><a href="#remove_invisible_charactersstring-str-bool-url_encoded-string-replacement-string">remove_invisible_characters</a>
</td><td><a href="#to_asciistring-str-string-language-bool-remove_unsupported_chars-bool-replace_extra_symbols-bool-use_transliterate-boolnull-replace_single_chars_only-string">to_ascii</a>
</td><td><a href="#to_filenamestring-str-bool-use_transliterate-string-fallback_char-string">to_filename</a>
</td></tr><tr><td><a href="#to_slugifystring-str-string-separator-string-language-string-replacements-bool-replace_extra_symbols-bool-use_str_to_lower-bool-use_transliterate-string">to_slugify</a>
</td><td><a href="#to_transliteratestring-str-stringnull-unknown-bool-strict-string">to_transliterate</a>
</td></tr></table>

#### charsArray(bool $replace_extra_symbols): array
<a href="#class-methods">↑</a>
Returns an replacement array for ASCII methods.

EXAMPLE: <code>
$array = ASCII::charsArray();
var_dump($array['ru']['б']); // 'b'
</code>

**Parameters:**
- `bool $replace_extra_symbols [optional] <p>Add some more replacements e.g. "£" with " pound ".</p>`

**Return:**
- `array`

--------

#### charsArrayWithMultiLanguageValues(bool $replace_extra_symbols): array
<a href="#class-methods">↑</a>
Returns an replacement array for ASCII methods with a mix of multiple languages.

EXAMPLE: <code>
$array = ASCII::charsArrayWithMultiLanguageValues();
var_dump($array['b']); // ['β', 'б', 'ဗ', 'ბ', 'ب']
</code>

**Parameters:**
- `bool $replace_extra_symbols [optional] <p>Add some more replacements e.g. "£" with " pound ".</p>`

**Return:**
- `array <p>An array of replacements.</p>`

--------

#### charsArrayWithOneLanguage(string $language, bool $replace_extra_symbols, bool $asOrigReplaceArray): array
<a href="#class-methods">↑</a>
Returns an replacement array for ASCII methods with one language.

For example, German will map 'ä' to 'ae', while other languages
will simply return e.g. 'a'.

EXAMPLE: <code>
$array = ASCII::charsArrayWithOneLanguage('ru');
$tmpKey = \array_search('yo', $array['replace']);
echo $array['orig'][$tmpKey]; // 'ё'
</code>

**Parameters:**
- `string $language [optional] <p>Language of the source string e.g.: en, de_at, or de-ch.
(default is 'en') | ASCII::*_LANGUAGE_CODE</p>`
- `bool $replace_extra_symbols [optional] <p>Add some more replacements e.g. "£" with " pound ".</p>`
- `bool $asOrigReplaceArray [optional] <p>TRUE === return thr {orig: string[], replace: string[]}
array</p>`

**Return:**
- `array <p>An array of replacements.</p>`

--------

#### charsArrayWithSingleLanguageValues(bool $replace_extra_symbols, bool $asOrigReplaceArray): array
<a href="#class-methods">↑</a>
Returns an replacement array for ASCII methods with multiple languages.

EXAMPLE: <code>
$array = ASCII::charsArrayWithSingleLanguageValues();
$tmpKey = \array_search('hnaik', $array['replace']);
echo $array['orig'][$tmpKey]; // '၌'
</code>

**Parameters:**
- `bool $replace_extra_symbols [optional] <p>Add some more replacements e.g. "£" with " pound ".</p>`
- `bool $asOrigReplaceArray [optional] <p>TRUE === return thr {orig: string[], replace: string[]}
array</p>`

**Return:**
- `array <p>An array of replacements.</p>`

--------

#### clean(string $str, bool $normalize_whitespace, bool $keep_non_breaking_space, bool $normalize_msword, bool $remove_invisible_characters): string
<a href="#class-methods">↑</a>
Accepts a string and removes all non-UTF-8 characters from it + extras if needed.

**Parameters:**
- `string $str <p>The string to be sanitized.</p>`
- `bool $normalize_whitespace [optional] <p>Set to true, if you need to normalize the
whitespace.</p>`
- `bool $keep_non_breaking_space [optional] <p>Set to true, to keep non-breaking-spaces, in
combination with
$normalize_whitespace</p>`
- `bool $normalize_msword [optional] <p>Set to true, if you need to normalize MS Word chars
e.g.: "…"
=> "..."</p>`
- `bool $remove_invisible_characters [optional] <p>Set to false, if you not want to remove invisible
characters e.g.: "\0"</p>`

**Return:**
- `string <p>A clean UTF-8 string.</p>`

--------

#### getAllLanguages(): string[]
<a href="#class-methods">↑</a>
Get all languages from the constants "ASCII::.*LANGUAGE_CODE".

**Parameters:**
__nothing__

**Return:**
- `string[]`

--------

#### is_ascii(string $str): bool
<a href="#class-methods">↑</a>
Checks if a string is 7 bit ASCII.

EXAMPLE: <code>
ASCII::is_ascii('白'); // false
</code>

**Parameters:**
- `string $str <p>The string to check.</p>`

**Return:**
- `bool <p>
<strong>true</strong> if it is ASCII<br>
<strong>false</strong> otherwise
</p>`

--------

#### normalize_msword(string $str): string
<a href="#class-methods">↑</a>
Returns a string with smart quotes, ellipsis characters, and dashes from
Windows-1252 (commonly used in Word documents) replaced by their ASCII
equivalents.

EXAMPLE: <code>
ASCII::normalize_msword('„Abcdef…”'); // '"Abcdef..."'
</code>

**Parameters:**
- `string $str <p>The string to be normalized.</p>`

**Return:**
- `string <p>A string with normalized characters for commonly used chars in Word documents.</p>`

--------

#### normalize_whitespace(string $str, bool $keepNonBreakingSpace, bool $keepBidiUnicodeControls): string
<a href="#class-methods">↑</a>
Normalize the whitespace.

EXAMPLE: <code>
ASCII::normalize_whitespace("abc-\xc2\xa0-öäü-\xe2\x80\xaf-\xE2\x80\xAC", true); // "abc-\xc2\xa0-öäü- -"
</code>

**Parameters:**
- `string $str <p>The string to be normalized.</p>`
- `bool $keepNonBreakingSpace [optional] <p>Set to true, to keep non-breaking-spaces.</p>`
- `bool $keepBidiUnicodeControls [optional] <p>Set to true, to keep non-printable (for the web)
bidirectional text chars.</p>`

**Return:**
- `string <p>A string with normalized whitespace.</p>`

--------

#### remove_invisible_characters(string $str, bool $url_encoded, string $replacement): string
<a href="#class-methods">↑</a>
Remove invisible characters from a string.

e.g.: This prevents sandwiching null characters between ascii characters, like Java\0script.

copy&past from https://github.com/bcit-ci/CodeIgniter/blob/develop/system/core/Common.php

**Parameters:**
- `string $str`
- `bool $url_encoded`
- `string $replacement`

**Return:**
- `string`

--------

#### to_ascii(string $str, string $language, bool $remove_unsupported_chars, bool $replace_extra_symbols, bool $use_transliterate, bool|null $replace_single_chars_only): string
<a href="#class-methods">↑</a>
Returns an ASCII version of the string. A set of non-ASCII characters are
replaced with their closest ASCII counterparts, and the rest are removed
by default. The language or locale of the source string can be supplied
for language-specific transliteration in any of the following formats:
en, en_GB, or en-GB. For example, passing "de" results in "äöü" mapping
to "aeoeue" rather than "aou" as in other languages.

EXAMPLE: <code>
ASCII::to_ascii('�Düsseldorf�', 'en'); // Dusseldorf
</code>

**Parameters:**
- `string $str <p>The input string.</p>`
- `string $language [optional] <p>Language of the source string.
(default is 'en') | ASCII::*_LANGUAGE_CODE</p>`
- `bool $remove_unsupported_chars [optional] <p>Whether or not to remove the
unsupported characters.</p>`
- `bool $replace_extra_symbols [optional]  <p>Add some more replacements e.g. "£" with " pound
".</p>`
- `bool $use_transliterate [optional]  <p>Use ASCII::to_transliterate() for unknown chars.</p>`
- `bool|null $replace_single_chars_only [optional]  <p>Single char replacement is better for the
performance, but some languages need to replace more then one char
at the same time. | NULL === auto-setting, depended on the
language</p>`

**Return:**
- `string <p>A string that contains only ASCII characters.</p>`

--------

#### to_filename(string $str, bool $use_transliterate, string $fallback_char): string
<a href="#class-methods">↑</a>
Convert given string to safe filename (and keep string case).

EXAMPLE: <code>
ASCII::to_filename('שדגשדג.png', true)); // 'shdgshdg.png'
</code>

**Parameters:**
- `string $str`
- `bool $use_transliterate <p>ASCII::to_transliterate() is used by default - unsafe characters are
simply replaced with hyphen otherwise.</p>`
- `string $fallback_char`

**Return:**
- `string <p>A string that contains only safe characters for a filename.</p>`

--------

#### to_slugify(string $str, string $separator, string $language, string[] $replacements, bool $replace_extra_symbols, bool $use_str_to_lower, bool $use_transliterate): string
<a href="#class-methods">↑</a>
Converts the string into an URL slug. This includes replacing non-ASCII
characters with their closest ASCII equivalents, removing remaining
non-ASCII and non-alphanumeric characters, and replacing whitespace with
$separator. The separator defaults to a single dash, and the string
is also converted to lowercase. The language of the source string can
also be supplied for language-specific transliteration.

**Parameters:**
- `string $str`
- `string $separator [optional] <p>The string used to replace whitespace.</p>`
- `string $language [optional] <p>Language of the source string.
(default is 'en') | ASCII::*_LANGUAGE_CODE</p>`
- `array<string, string> $replacements [optional] <p>A map of replaceable strings.</p>`
- `bool $replace_extra_symbols [optional]  <p>Add some more replacements e.g. "£" with "
pound ".</p>`
- `bool $use_str_to_lower [optional] <p>Use "string to lower" for the input.</p>`
- `bool $use_transliterate [optional]  <p>Use ASCII::to_transliterate() for unknown
chars.</p>`

**Return:**
- `string <p>A string that has been converted to an URL slug.</p>`

--------

#### to_transliterate(string $str, string|null $unknown, bool $strict): string
<a href="#class-methods">↑</a>
Returns an ASCII version of the string. A set of non-ASCII characters are
replaced with their closest ASCII counterparts, and the rest are removed
unless instructed otherwise.

EXAMPLE: <code>
ASCII::to_transliterate('déjà σσς iıii'); // 'deja sss iiii'
</code>

**Parameters:**
- `string $str <p>The input string.</p>`
- `null|string $unknown [optional] <p>Character use if character unknown. (default is '?')
But you can also use NULL to keep the unknown chars.</p>`
- `bool $strict [optional] <p>Use "transliterator_transliterate()" from PHP-Intl`

**Return:**
- `string <p>A String that contains only ASCII characters.</p>`

--------



## Unit Test

1) [Composer](https://getcomposer.org) is a prerequisite for running the tests.

```
composer install
```

2) The tests can be executed by running this command from the root directory:

```bash
./vendor/bin/phpunit
```

### Support

For support and donations please visit [Github](https://github.com/voku/portable-ascii/) | [Issues](https://github.com/voku/portable-ascii/issues) | [PayPal](https://paypal.me/moelleken) | [Patreon](https://www.patreon.com/voku).

For status updates and release announcements please visit [Releases](https://github.com/voku/portable-ascii/releases) | [Twitter](https://twitter.com/suckup_de) | [Patreon](https://www.patreon.com/voku/posts).

For professional support please contact [me](https://about.me/voku).

### Thanks

- Thanks to [GitHub](https://github.com) (Microsoft) for hosting the code and a good infrastructure including Issues-Managment, etc.
- Thanks to [IntelliJ](https://www.jetbrains.com) as they make the best IDEs for PHP and they gave me an open source license for PhpStorm!
- Thanks to [Travis CI](https://travis-ci.com/) for being the most awesome, easiest continous integration tool out there!
- Thanks to [StyleCI](https://styleci.io/) for the simple but powerful code style check.
- Thanks to [PHPStan](https://github.com/phpstan/phpstan) && [Psalm](https://github.com/vimeo/psalm) for really great Static analysis tools and for discover bugs in the code!

### License and Copyright

Released under the MIT License - see `LICENSE.txt` for details.
