

[CODE FOLLOWS]

# ben0biJSLoader
Load all your JS files from a single JSON file.

I don't really get how Require.js works. Instead of learning it, I wrote my own JS loader.
You can put all your JS-files (names & path) in a single JSON file and load them into each of your pages with one command.
No PHP and jQuery is needed - I made it work without jQuery so you can load it along with the other files.

It simply loads the filenames and adds some SCRIPT tags to the HEAD tag of your page.

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
