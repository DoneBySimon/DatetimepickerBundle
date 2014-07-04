#DatetimepickerBundle

This bundle implements the [Bootstrap DateTime Picker](https://github.com/smalot/bootstrap-datetimepicker) in a Form Type for Symfony 2.*. 

Demo : http://www.malot.fr/bootstrap-datetimepicker/demo.php

keeping this best practice in mind
http://stackoverflow.com/a/6227488/1006760

So get the smalot-bootstrap-datetimepicker in your project using your favourite frontend package manager (Boweer/Copy+paste/...)


### Step 1: Install DatetimepickerBundle

Add the following dependency to your composer.json file:

``` json
{
    "require": {

        "donebysimon/datetimepicker-bundle": "dev-master"
    }
}
```

and then run

```bash
php composer.phar update donebysimon/datetimepicker-bundle
```

### Step 2: Enable the bundle

``` php
<?php
// app/AppKernel.php

public function registerBundles()
{
    $bundles = array(
        // ...
        new DBS\DatetimepickerBundle\DatetimepickerBundle(),
    );
}
```

### Step 3: assetic setup

``` yml
assetic:
    bundles:        [..., DatetimepickerBundle ]
    assets:
      bootstrap_datetimepicker_css:
        inputs:
          - [the path where you keep your frontend stuff]/smalot-bootstrap-datetimepicker/css/bootstrap-datetimepicker.min.css
      bootstrap_datetimepicker_js:
        inputs:
          - [the path where you keep your frontend stuff]/smalot-bootstrap-datetimepicker/js/bootstrap-datetimepicker.min.js
```

## Usages

``` php
<?php
// ...
public function buildForm(FormBuilder $builder, array $options)
{
    $builder
        // defaut options
        ->add('createdAt', 'collot_datetime') 
        
        // full options
        ->add('updatedAt', 'collot_datetime', array( 'pickerOptions' =>
            array('format' => 'mm/dd/yyyy',
                'weekStart' => 0,
                'startDate' => date('m/d/Y'), //example
                'endDate' => '01/01/3000', //example
                'daysOfWeekDisabled' => '0,6', //example
                'autoclose' => false,
                'startView' => 'month',
                'minView' => 'hour',
                'maxView' => 'decade',
                'todayBtn' => false,
                'todayHighlight' => false,
                'keyboardNavigation' => true,
                'language' => 'en',
                'forceParse' => true,
                'minuteStep' => 5,
                'pickerReferer ' => 'default', //deprecated
                'pickerPosition' => 'bottom-right',
                'viewSelect' => 'hour',
                'showMeridian' => false,
                'initialDate' => date('m/d/Y', 1577836800), //example
                ))) ; 

}
```

Add form_javascript and form_stylesheet

The principle is to separate the javascript, stylesheet and html.
This allows better integration of web pages.

### Example:

``` twig
{% block stylesheets %}
    <link href="{{ asset('css/bootstrap.min.css') }}" rel="stylesheet" />
    
    {{ form_stylesheet(form) }}
{% endblock %}

{% block javascripts %}
    <script src="{{ asset('js/jquery.min.jss') }}"></script>
    <script src="{{ asset('js/bootstrap.min.js') }}"></script>
    
    {{ form_javascript(form) }}
{% endblock %}

{% block body %}
    <form action="{{ path('my_route_form') }}" type="post" {{ form_enctype(form) }}>
        {{ form_widget(form) }}

        <input type="submit" />
    </form>
{% endblock %}
```

## Documentation

The documentation of the datetime picker is here : http://www.malot.fr/bootstrap-datetimepicker/#options

## Thanx

credits to Stephane Collot
https://github.com/stephanecollot/DatetimepickerBundle