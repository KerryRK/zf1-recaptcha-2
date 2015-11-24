ZF1 reCAPTCHA2 - Google reCAPTCHA integration
==============================

ZF1 ships with Google reCAPTCHA version 1.  Now that version 2 is available
you will probably want to use an up-to-date element for your Zend Framework installations.

Installation
-----

#### Composer Install

    "require": {
        "cgsmith/zf1-recaptcha-2": "~1.0"
    }


Usage
-----

Install the latest version (1.0.1) and setup your plugins and form abstract with the following information:

* On your application.ini or where you want

```ini
recaptcha.sitekey = "YOUR SITE KEY GIVED BY GOOGLE"
recaptcha.secretkey = "YOUR SECRET KEY GIVED BY GOOGLE"
```

* In your controller or bootsrap:

```php
<?php
// important view settings that you will have to place
// pulls in google js api
$view->headScript()->appendFile('//www.google.com/recaptcha/api.js'); 
```

* In your bootstrap

```php
// setup your helper path
$view->addHelperPath('/src/Cgsmith/View/Helper', 'Cgsmith\\View\\Helper\\'); 

```

* In the init() function of your Form

```php
// setup prefix path for form element (form abstract) 
$this->addPrefixPath('Cgsmith\\Form\\Element', '/src/Cgsmith/Form/Element', Zend_Form::ELEMENT);
$this->addElementPrefixPath('Cgsmith\\Validate\\', '/src/Cgsmith/Validate/', Zend_Form_Element::VALIDATE);

```

* Below is what you would setup in your form.

```php
<?php

// create your element and pass through your site key and secret key
$this->addElement('Recaptcha', 'g-recaptcha-response', [
    'siteKey'   => Zend_Registry::get('application')->recaptcha->sitekey,
    'secretKey' => Zend_Registry::get('application')->recaptcha->secretkey,
]);

```

* On your controller, after "validate the post data"

```php
$values = $form->getValues();
unset($values['g-recaptcha-response']);

```

About
=====

Requirements
------------

- ZF1 reCAPTCHA2 works with PHP 5.5 or above.

Submitting bugs and feature requests
------------------------------------

Bugs and feature request are tracked on [GitHub](https://github.com/cgsmith/zf1-recaptcha-2/issues)

Author
------

Chris Smith - <chris@cgsmith.net> - <http://twitter.com/cgsmith105>

License
-------

ZF1 reCAPTCHA2 is licensed under the MIT License - see the `LICENSE` file for details
