# Google Autocomplete

I am sharing this component because I was overwhelmed of complicated examples to achieve this simple duty. So, I will try to be as easier as I can during my explanation.

Google Autocomplete component is not more than a ```Vue.js``` wrapper around the google official API. In spite of the demo was written in ```Vue.js```,  the Autocomplete object can be pulled in from any ***JS framework***.


# Requirements
You will have to install Vue & Vuemit, as so:

```js
npm install vue --save
```

```js
npm install vuemit --save
```

The Vuemit library is used to manage the events between the google component its parent one.


# Installation
To install this package you just need to open your console line and type ```npm i google-autocomplete-vue --save```. If there is any problems during the installation, you can try again using the ```force param```, as so ```npm i -f google-autocomplete-vue --save```


# Gettings started

***First of all***, you have to sign up in ***Google API Console*** in order for you to configure your app information, as API key, app name, etc. This can be addressed on <a href="https://console.developers.google.com">https://console.developers.google.com</a>. Once this has been done, you will have to copy the ***API KEY given by google*** and paste in your JS file entry point. Example:

- Bootstrap File: <a href="https://github.com/goblindaydream/Vue-Google-Auto-Complete/blob/master/src/js/bootstrap.js">bootstrap.js</a>. You will have to ***require Vuemit*** in this file to have the events handler set as globaly. As so: <a href="https://github.com/goblindaydream/Vue-Google-Auto-Complete/blob/master/src/js/bootstrap.js#L23">Example</a>

- Entry point file: <a href="https://github.com/goblindaydream/Vue-Google-Auto-Complete/blob/master/src/js/demo.js">demo.js</a>

> **Note:** Important keys have to be kept within an .env file, so be aware of this while pushing your code to your git control.


***Second of all***, you will have to import the component in your application entry point, so you will be able to call it as global when need it. Example:

```js
import GoogleAutocomplete from 'google-autocomplete-vue';
```


# Validation on server side

Places validation is a ***laravel library*** that will help you out to handle your user addresses. Its aim is making sure addresses submitted by users are valid through 3rd party services, as google.

Take a look at its repository on <a href="https://github.com/gocanto/places-validation"> Places Validation </a>


# Illustration

![example](https://github.com/goblindaydream/Vue-Google-Auto-Complete/blob/master/src/images/example.gif)


# Guide

* First of all, you have to create an entry point in order for you to compile the component out and generate your bundle file. An illustration is posted <a href="https://github.com/goblindaydream/Vue-Google-Auto-Complete/blob/master/src/js/demo.js" target="_blank">here</a>


* Second of all, you will have to create your vue object to control the component mentioned, as so:

```javascript

require('./bootstrap');


new Vue({

    el: '#demo',


    data:
    {
        output: {}, address: {}, sent: false, response: {}, config: {}
    },


    mounted()
    {
        //Set an event listener for 'setAddress'.
        Vuemit.listen('setAddress', this.onAddressChanged);
        Vuemit.listen('addressWasCleared', this.onAddressCleared);
    },


    methods:
    {
        /**
         * Submit the data to be evaluated.
         *
         * @return {Void}
         */
        submit()
        {
            this.sent = true;
            this.output = this.address;
            this.address = {};
        },


        /**
         * Checks whether the output data is valid.
         *
         * @return {Bool}
         */
        isValid()
        {
            return Object.keys(this.output).length > 0;
        },


        /**
         * Checks whether the output data is not valid.
         *
         * @return {Bool}
         */
        isNotValid()
        {
            return ! this.isValid();
        },


        /**
         * The callback fired when the autocomplete address change event was fired.
         *
         * @param {Object}
         * @return {Void}
         */
        onAddressChanged(payload)
        {
            if (Object.keys(paypload.place).length > 0) {
                this.address = payload.address;
                this.response = payload.response;
            }
        }

        /**
         * The callback fired when the autocomplete clear event was fired.
         *
         * @param {Object}
         * @return {Void}
         */
        onAddressCleared()
        {
            this.address = {};
            this.response = {};
        }
    }
});
```

See the example <a href="https://github.com/goblindaydream/Vue-Google-Auto-Complete/blob/master/src/js/demo.js" target="_blank">here</a>


* Third of all, you have to compile these two files with **browserify or webpack** and **laravel-elixir-vue-2** to make them readable for every browser. Example:

```javascript
require('laravel-elixir-vue-2');
var elixir = require('laravel-elixir');

elixir.config.sourcemaps = false;
elixir.config.assetsPath = 'src';

elixir(function(mix)
{
    mix.webpack('demo.js', 'dist/demo.js');
});
```

See the example <a href="https://github.com/goblindaydream/Vue-Google-Auto-Complete/blob/master/gulpfile.js#L10" target="_blank">here</a>


* Finally, you can use the component in your **HTML** file using this syntax:

```HTML
<google-autocomplete
    class = "input"
    input_id = "txtAutocomplete"
    :config = "{type: ['geocode']}"
    placeholder = "type your address"
>
</google-autocomplete>
```

***:config*** is the config passed to the Autocomplete constructor of the places API. See <a href="https://developers.google.com/maps/documentation/javascript/places-autocomplete#add_autocomplete">documentation</a>. Config corresponds to the `options` argument in the doc.

See the example <a href="https://github.com/goblindaydream/Vue-Google-Auto-Complete/blob/master/demo/index.html#L50-L54" target="_blank">here</a>


Also, You can pass any ```css class``` through "class" prop.


# Contributing

Please feel free to fork this package and contribute by submitting a pull request to enhance the functionalities.
