Some Gustav core options require a specific format or content to be converted into another datatype than a string or to be processed in another way. Besides processing their values, these options can also be validated.  
Below are shown the options whose values are processed or validated.

         array _templ
         _____ ______
           |        |
    datatype of    name of the option
    processed
    value

For information on the options' values expected datatypes see *Gustav core options*.



##`array _templ`

If an empty string is specified, the processed value will be an empty array.  
If not an empty string, the string is expected to be similar to the one below.

    html5.site_2015.blog

The templates are separated using `.`s. Whitespaces before and after a template's name are removed and empty template names or those consisting of whitespaces only are removed from the list.  
After removing the empty items at least one item has to be remained.  
All template names that are still in the list must have a corresponding template file.



##`array _conv`

The string is expected to be similar to the one below.

    markdown.html

The converters are separated using `.`s. Whitespaces before and after a converters's name are removed and empty converter names or those consisting of whitespaces only are removed from the list. Converter names that don't have a corresponsing converter are removed, too.  
If the last converter in the list returns a valid converter name, that converter name is appended to the list of converters. If the appended converter returns a converter name, that is appended to the list, too, and so on.  
Finally the list of coverters must include at least one item.



##`array _tags`

The string is expected to be similar to the one below.

    tag1,tag2,TAg3,tag3

The tags are separated using `,`s. Whitespaces before and after a tag are removed and empty tags or those consisting of whitespaces only are removed from the list.  
Any kind of whitespaces in the remaining tags are replaced by a simple space.  
Finally the tags in the list are made unique (case-insensitively). The first instance of two *equal* strings is kept while the latter ones are removed. For example, the list above would result in the following array.

    array( "tag1", "tag2", "TAg3" )



##`string _dest`

If the `replace_directory_separator` configuration option is set to a non-empty string, the character specified by that option is replaced with the OS's directory separator.  
The path of the destination directory followed by the dirname of the used source file's path, relative to the source directory, is prepended to the string if it doesn't start with a directory separator.  
If the path doesn't end with a directory separator, the file-extension of its filename is replaced with the appropiate file-extension of the destination file, `php` if the `_dyn` option is set, otherwise `html`.  
If a value of an empty string is used, the path described above is prepended and its last path segment is used as filename. The resulting path won't have a trailing directory separator.  
A value of `./`, `/` being the OS's directory separator, or `index` can be used to create a `index.*` file in the directory the path described above is pointing on. Using `{{$dest_dir}}` as value will create a `index.*` file in the destination directory's root. See *$dest\_dir* under *Available variables* in *GvBlock option templating* for more information.  
The final string always starts with a directory separator and should describe a path pointing on a location beneath the document root.



##`string _ext`

If the `replace_directory_separator` configuration option is set to a non-empty string, the character specified by that option is replaced with the OS's directory separator.  
The string must not be empty.  
The specified path is treated relatively to the source directory. Therefore that directory's path is prepended to the path.  
Finally the path must point on a file.  
The final string always starts with a directory separator. Although it's not recommended, the source directory can be left using `..` path segments.



##`string _ext_content`

If no value has been specified for this option - for boolean options a value `true` is used - its value is set to an empty string.  
A specified string value isn't treated literally, rather it's handled like a double-quoted string in PHP. That means that some character escape sequences like `\n` for a newline or `\t` for a tab are available. The only difference between a double-quotes PHP string and this option is that variables in the string aren't resolved. For exmaple `$foo` would remain `$foo`, even if `$foo` would have been defined. Moreover, whitespaces in the beginning and in the end of the string are not removed.



##`int _pub`

The value must be parseable by PHP's `strtotime()` function. That function's return value is used as this option's final value.



##`string _title`

As for the `_tags` option, any kind of whitespaces in the string are replaced by a simple space.



##`string _desc`

The value of this option isn't processed in any way. It's just validated to be a string.