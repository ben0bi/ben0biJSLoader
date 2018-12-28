# ben0biJSLoader
Load all your JS files from a single JSON file.

Intended to be used when several html pages need the same chunk of JS-files.
(These pages should reside in the same folder.)

I don't really get how Require.js works. Instead of learning it, I wrote my own JS loader.
You can put all your JS-files (names & path) in a single JSON file and load them into each of your pages with one command.
No PHP and jQuery is needed - I made it work without jQuery so you can load it (jQuery) along with the other files.

It simply loads the filenames and adds some SCRIPT tags to the HEAD tag of your page.

A script tag of a json key-value pair looks like this then:    
<script id="JSFILE_[key]" src="[value]"></script>    
where the values between the [ brackets ] will vary depending on the json file.    

## Usage:
Create a JSON file with a one-level structure.  
The key values do not matter except for "//" which is a comment.  
The last entry should be "//":0 so the comment key will be cleared.  
In your page, just load this script and call the loader. See example below.  

## Example:

#### JSON File:
{  
   "//": "Those are my files and this is a comment..",  
   
   "JQUERY": "js/jquery.min.js",  
   "SomeLib": "js/mylib_01.js",  
   
   "//": "Assume Lib2 depends SomeLib and both depend on jQuery.",  
   "//": The File order is important, not the keys!",  
   "Lib2": "js/mylib_02.js",  
   
   "//":0  
}  

##### Loading it:
After that, you only need to call the loader with the right path and your main function.  
You NEED to put your code into a main function, whereelse it will try to execute it before all the stuff is loaded.  

&lt;script src="js/ben0biJSLoader.js"&gt;&lt;/script&gt;  
&lt;script&gt;  
  
function main()  
{  
   // Do your whole stuff here, when the JS files finished loading.  
}  

ben0biJSLoader.recursiveLoad('config/mypaths.json', main);  
&lt;/script&gt;  

Aaaaand...it should work.

## COMPOSER
To download the ben0biJSLoader into your project with composer, add those lines to your composer.json:

{
	...	

    "repositories": [

	...,

        {
            "type": "vcs",
            "url": "https://github.com/ben0bi/ben0biJSLoader.git"
        }
    ],
    "require": {
	...,
        "ben0bienterprises/ben0biJSLoader" : "dev-master@dev"
    },

	...
}

Now you can load the ben0biJSLoader by typing "composer update" into your console.

