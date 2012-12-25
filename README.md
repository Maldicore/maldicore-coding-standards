# IDE

We shall use Sublime Text 2 (ST2) licensed version for all our coding, including customization specified in this document and elsewhere in the Maldicore knowledge-base.

# Indenting and Line Length

Use an indent of one tab (no spaces! ST2 convert a tab to pseudo 4 spaces, check the setting in ST2 file at Preferences->Setting - Default->"tab_size" = 4).

It is recommended that you break lines at approximately 80 characters. For a visual guide for this in ST preferences file set "rulers":[80]. However there is no particular standard rule for the best way to break a line; use your judgement. This applies to all file types: PHP, HTML, CSS, Javascript, etc.

Indentation rules should be applied in the source file that will be edited by others. The visual appeal of HTML output should not be taken into consideration when writing code that generates HTML.

# HTML Standards

- As of September 2012, we will be using HTML5 in all our HTML coding standard, for quick reference use the attached HTML5 cheat sheets. 

- When multiple browser compatibility is necessity use http://caniuse.com/.

- To enable HTML5 on older versions of IE use the following code.

```html
<!--[if lt IE 9]>
<script src="http://html5shim.googlecode.com/svn/trunk/html5.js"></script>
<![endif]-->
```

Alternatively, can use http://modernizr.com/

- The DocType on our HTML documents will be HTML5 based <!DOCTYPE html>.This standard should be followed unless we have to comply with other standards for specific purposed, eg: HTML 4.

- All markup should be delivered as UTF-8, as its the most internationalization friendly.

```html
<meta charset="utf-8">
```

- Always add a lang attribute on html element, e.g.: <html lang=”en”>

- Write all HTML5 tags in lowercase.

- Use double quotes for attribute value eg: charset="utf-8".

- Start with a base HTML5 template code generated use http://switchtohtml5.com/ or http://shikiryu.com/html5/. Alternatively for quick start use http://html5boilerplate.com/

* A basic, but semantically correct HTML5 document should look like the following:

```html
<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8">
  <title></title>
</head>
<body>
  <header>
  ...
  </header>

  <div role="main">
	...
  </div>

  <footer>
	...
  </footer>
</body>
</html>
```

- Place an html comment on some closing div tags to indicate what element you're closing. It will help when there is lots of nesting and indentation.

- Use microformats[[http://en.wikipedia.org/wiki/Microformat]] and/or Microdata where appropriate, specifically hCard and adr.

- Make use of THEAD, TBODY, and TH tags in tables (and Scope attribute) when appropriate.

# Styling/CSS Standards

- Place all the styling on a separate stylesheet, never use inline styling unless necessary,

- Only give elements an ID attribute if they are unique. They should be applied to that element only and nothing else. Classes can be applied to multiple elements that share the same style properties. Things that should look and work in the same way can have the same class name.

- Always use spirit for background images, use http://spriteme.org/ (though this requires the codes to be online)

- As the CSS grow give special attention to CSS Specifity: [[http://www.stuffandnonsense.co.uk/archives/css_specificity_wars.html]]

To calculated Specificity count the CSS components and expressing them in a form (a,b,c,d).

  + Element, Pseudo Element: d = 1 – (0,0,0,1)

  + Class, Pseudo class, Attribute: c = 1 – (0,0,1,0)

  + Id: b = 1 – (0,1,0,0)

  + Inline Style: a = 1 – (1,0,0,0)

- Always use CSS shorthand, note the TRBL acronym, element are defined, in a clock-wise manner: Top, Right, Bottom, Left. If bottom is undefined, it inherits its value from top, if left is undefined, it inherits its value from right. If only the top value is defined, all sides inherit from that one declaration.

For more info on CSS shorthand usage visit the following links

 + http://qrayg.com/journal/news/css-background-shorthand
 + http://sonspring.com/journal/css-redundancy
 + http://dustindiaz.com/css-shorthand

- Use the _px_ unit of measurement to define font size, instead of _em_ because it offers absolute control over text.

- Avoid using !important if possible (as it mess up CSS specificity) and only use it as a last resort.

- When CSS minification is in need use https://github.com/barryvan/CSSMin/

- For mission critical app/site test performance using:

 + http://developer.yahoo.com/yslow/
 + http://code.google.com/speed/page-speed/
 + http://stevesouders.com/hammerhead/
 + http://msfast.myspace.com/
 + http://www.webpagetest.org/

# Javascript Syntax

See PHP Syntax Below. The languages are similar enough that the same rules apply in most cases.

# Request Vars

Although our php setup have register_globals enabled, PHP6 will remove this option. Therefore, in new code, we should always use the super globals $_GET, $_POST, and $_COOKIE. $_REQUEST should be used only when it is known for sure that a variable could be supplied using multiple methods.

# PHP Syntax

## PHP & HTML

Do not echo HTML using PHP but rather echo the variable/data where it will display.

Example PHP/HTML Mix

```php
<ul>
    <label>Publications</label>
    <?php foreach($publications as $pub) { ?>
        <li><?php echo $pub["name"]?></li>
    <?php } ?>
</ul>

```

## Control Structures

These include if, for, while, switch, etc.

Example if statement

```php
if (condition1 || condition2) {
    action1;
} else if (condition3 && (condition4 || condition5)) {
    action2;
} else {
    defaultaction;
}
```

Control statements should have one space between the control keyword and opening parenthesis, to distinguish them from function calls.

It is strongly encouraged to always use curly braces even in situations where they are technically optional. Having them increases readability and decreases the likelihood of logic errors being introduced when new lines are added.

Example switch statement

```
switch (condition) {
    case 1:
        action1;
        break;
    case 2:
        action2;
        break;
    
    default:
        defaultaction;
        break;
}

```

## Function Calls

Functions should be called with no spaces between the function name, the opening parenthesis, and the first parameter; spaces between commas and each parameter, and no space between the last parameter, the closing parenthesis, and the semicolon.

Example function call

```php
$var = foo($bar, $baz, $quux);
```

As displayed above, there should be one space on either side of an equals sign used to assign the return value of a function to a variable. In the case of a block of related assignments, more space may be inserted to promote readability:

```php
$short         = foo($bar);
$long_variable = foo($baz);
```

## Function Definitions

Function declarations are similar to function calls with the beginning brace on the same line as the function declaration.

Example function definition

```php
function foo_func($arg1, $arg2 = '') {
    if (condition) {
        statement;
    }
    return $val;
}
```

Arguments with default values go at the end of the argument list. Always attempt to return a meaningful value from a function if one is appropriate.

Longer function example

```php
function connect(&$dsn, $persistent = false) {
    if (is_array($dsn)) {
        $dsninfo = &$dsn;
    } else {
        $dsninfo = DB::parseDSN($dsn);
    }

    if (!$dsninfo || !$dsninfo['phptype']) {
        return $this->raiseError();
    }

    return true;
}
```

## Comments

Complete inline documentation comment blocks (docblocks) must be provided. Please use the header standards in the knowledgebase. These will be used for automatic documentation so for more information visit phpDocumentor [[http://www.phpdoc.org/]].

Non-documentation comments are strongly encouraged. A general rule of thumb is that if you look at a section of code and think "Wow, I don't want to try and describe that", you need to comment it before you forget how it works.
C style comments (/* */) and standard C++ comments (//) are both fine. The use of Perl / shell style comments (#) is strongly discouraged.

## PHP Code Tags

Always use <?php ?> to delimit PHP code, not the <? ?> shorthand. This is the most portable way to include PHP code on different operating systems and server setups.

## Header Comment Blocks

All source code files shall contain a "page-level" docblock at the top of each file and a "class-level" docblock immediately above each class or function.

Example docblocks

```php
<?php
/**
 * Short description for file
 *
 * Long description for file (if any)...
 *
 * @category   CategoryName
 * @package    PackageName
 * @author     Original Author <author@example.com>
 * @author     Another Author <another@example.com>
 * @copyright  1997-2005 The PHP Group
 * @license    http://www.php.net/license/3_0.txt  PHP License 3.0
 * @version    CVS: $Id:$
 * @link       http://pear.php.net/package/PackageName
 * @see        NetOther, Net_Sample::Net_Sample()
 * @since      File available since Release 1.2.0
 * @deprecated File deprecated in Release 2.0.0
 */

/*
 * Place includes, constant defines and $_GLOBAL settings here.
 * Make sure they have appropriate docblocks to avoid phpDocumentor
 * construing they are documented by the page-level docblock.
 */

/**
 * Short description for class
 *
 * Long description for class (if any)...
 *
 * @category   CategoryName
 * @package    PackageName
 * @author     Original Author <author@example.com>
 * @author     Another Author <another@example.com>
 * @copyright  1997-2005 The PHP Group
 * @license    http://www.php.net/license/3_0.txt  PHP License 3.0
 * @version    Release: @package_version@
 * @link       http://pear.php.net/package/PackageName
 * @see        NetOther, Net_Sample::Net_Sample()
 * @since      Class available since Release 1.2.0
 * @deprecated Class deprecated in Release 2.0.0
 */
class Foo
{
}

?>
```

## Required Tags That Have Variable Content

### Short Descriptions

Short descriptions must be provided for all docblocks. They should be a quick sentence, not the name of the item. Please read the Coding Standard's Sample File about how to write good descriptions.

### @author

There's no hard rule to determine when a new code contributor should be added to the list of authors for a given source file. In general, their changes should fall into the "substantial" category (meaning somewhere around 10% to 20% of code changes). Exceptions could be made for rewriting functions or contributing new logic.
Simple code reorganization or bug fixes would not justify the addition of a new individual to the list of authors.

### @since

This tag is required when a file or class is added after the package's initial release. Do not use it in an initial release.

### @deprecated

This tag is required when a file or class is no longer used but has been left in place for backwards compatibility.

## Order and Spacing

To ease long term readability of the source code, the text and tags must conform to the order and spacing provided in the example above. This standard is adopted from the JavaDoc standard.

## Example URLs

Use example.com, example.org and example.net for all example URLs and email addresses, per RFC 2606.

## Naming Conventions

### Classes

Classes should be given descriptive names. Avoid using abbreviations where possible. Class names should always begin with an uppercase letter and use mixed case to separate words.

Examples of good class names are:

```php
Log
NetFinger
HTMLUploadError
```

## Functions, Methods and Variable Names

Functions, methods and variable names should be named using CamelCase style. If applicable, functions should have the package or library name as a prefix to avoid name collisions. Names should all start with lowercase with each new "word" starting with an upperCase. Some Examples:

```php
connect() 
getData()
buildSomeWidget()

$i
$count
$tempArray
```

Private class members (meaning class members that are intended to be used only from within the same class in which they are declared are preceded by a single underscore. For example:

```php
_sort()
_initTree()
$this->_status
```

## Constants and Global Variables

Constants and global variables should always be all-uppercase, with underscores to separate words. Prefix constant names with the uppercased name of the class/package they are used in. For example, the constants used by a package named DB begin with DB_.

Note: The true, false and null constants are excepted from the all-uppercase rule, and must always be lowercase.

## File Formats

All scripts must:

* Be stored as ASCII text
* Use ISO-8859-1 character encoding
* Be Unix formatted, which means:
** Lines must end only with a line feed (LF). Line feeds are represented as ordinal 10, octal 012 and hex 0A. Do not use carriage returns (CR) like Macintosh computers do or the carriage return/line feed combination (CRLF) like Windows computers do.
** It is recommended that the last character in the file is a line feed. This means that when the cursor is at the very end of the file, it should be one line below the last line of text. Some utilities, such as diff, will complain if the last character in the file is not a line feed.

## Sample File

Each docblock in the example contains many details about writing Docblock Comments. Following those instructions is important for two reasons. First, when docblocks are easy to read, users and developers can quickly ascertain what your code does.

Please take note of the vertical and horizontal spacing. They are part of the standard.

```php
<?php
/**
 * Short description for file
 *
 * Long description for file (if any)...
 *
 * @category   CategoryName
 * @package    PackageName
 * @author     Original Author <author@example.com>
 * @author     Another Author <another@example.com>
 * @copyright  1997-2005 The PHP Group
 * @license    http://www.php.net/license/3_0.txt  PHP License 3.0
 * @version    CVS: $Id:$
 * @link       http://pear.php.net/package/PackageName
 * @see        NetOther, Net_Sample::Net_Sample()
 * @since      File available since Release 1.2.0
 * @deprecated File deprecated in Release 2.0.0
 */

/**
 * This is a "Docblock Comment," also known as a "docblock."  The class'
 * docblock, below, contains a complete description of how to write these.
 */
require_once 'PEAR.php';

/**
 * Methods return this if they succeed
 */
define('NET_SAMPLE_OK', 1);

/**
 * The number of objects created
 * @global int $GLOBALS['NET_SAMPLE_COUNT']
 */
$GLOBALS['NET_SAMPLE_COUNT'] = 0;

/**
 * An example of how to write code to PEAR's standards
 *
 * Docblock comments start with "/**" at the top.  Notice how the "/"
 * lines up with the normal indenting and the asterisks on subsequent rows
 * are in line with the first asterisk.  The last line of comment text
 * should be immediately followed on the next line by the closing asterisk
 * and slash and then the item you are commenting on should be on the next
 * line below that.  Don't add extra lines.  Please put a blank line
 * between paragraphs as well as between the end of the description and
 * the start of the @tags.  Wrap comments before 80 columns in order to
 * ease readability for a wide variety of users.
 *
 * Docblocks can only be used for programming constructs which allow them
 * (classes, properties, methods, defines, includes, globals).  See the
 * phpDocumentor documentation for more information.
 * http://phpdoc.org/docs/HTMLSmartyConverter/default/phpDocumentor/tutorial_phpDocumentor.howto.pkg.html
 *
 * The Javadoc Style Guide is an excellent resource for figuring out
 * how to say what needs to be said in docblock comments.  Much of what is
 * written here is a summary of what is found there, though there are some
 * cases where what's said here overrides what is said there.
 * http://java.sun.com/j2se/javadoc/writingdoccomments/index.html#styleguide
 *
 * The first line of any docblock is the summary.  Make them one short
 * sentence, without a period at the end.  Summaries for classes, properties
 * and constants should omit the subject and simply state the object,
 * because they are describing things rather than actions or behaviors.
 *
 * Below are the tags commonly used for classes. @category through @access
 * are required.  The remainder should only be used when necessary.
 * Please use them in the order they appear here.  phpDocumentor has
 * several other tags available, feel free to use them.
 *
 * @category   CategoryName
 * @package    PackageName
 * @author     Original Author <author@example.com>
 * @author     Another Author <another@example.com>
 * @copyright  1997-2005 The PHP Group
 * @license    http://www.php.net/license/3_0.txt  PHP License 3.0
 * @version    Release: @package_version@
 * @link       http://pear.php.net/package/PackageName
 * @see        NetOther, Net_Sample::Net_Sample()
 * @since      Class available since Release 1.2.0
 * @deprecated Class deprecated in Release 2.0.0
 */
class NetSample
{
    /**
     * The status of foo's universe
     *
     * Potential values are 'good', 'fair', 'poor' and 'unknown'.
     *
     * @var string
     */
    var $foo = 'unknown';

    /**
     * The status of life
     *
     * Note that names of private properties or methods must be
     * preceeded by an underscore.
     *
     * @var bool
     * @access private
     */
    var $_good = true;

    /**
     * Registers the status of foo's universe
     *
     * Summaries for methods should use 3rd person declarative rather
     * than 2nd person imperative, begining with a verb phrase.
     *
     * Summaries should add description beyond the method's name. The
     * best method names are "self-documenting", meaning they tell you
     * basically what the method does.  If the summary merely repeats
     * the method name in sentence form, it is not providing more
     * information.
     *
     * Summary Examples:
     *   + Sets the label              (preferred)
     *   + Set the label               (avoid)
     *   + This method sets the label  (avoid)
     *
     * Below are the tags commonly used for methods.  A @param tag is
     * required for each parameter the method has.  The @return and
     * @access tags are mandatory.  The @throws tag is required if the
     * method uses exceptions.  @static is required if the method can
     * be called statically.  The remainder should only be used when
     * necessary.  Please use them in the order they appear here.
     * phpDocumentor has several other tags available, feel free to use
     * them.
     *
     * The @param tag contains the data type, then the parameter's
     * name, followed by a description.  By convention, the first noun in
     * the description is the data type of the parameter.  Articles like
     * "a", "an", and  "the" can precede the noun.  The descriptions
     * should start with a phrase.  If further description is necessary,
     * follow with sentences.  Having two spaces between the name and the
     * description aids readability.
     *
     * When writing a phrase, do not capitalize and do not end with a
     * period:
     *   + the string to be tested
     *
     * When writing a phrase followed by a sentence, do not capitalize the
     * phrase, but end it with a period to distinguish it from the start
     * of the next sentence:
     *   + the string to be tested. Must use UTF-8 encoding.
     *
     * Return tags should contain the data type then a description of
     * the data returned.  The data type can be any of PHP's data types
     * (int, float, bool, string, array, object, resource, mixed)
     * and should contain the type primarily returned.  For example, if
     * a method returns an object when things work correctly but false
     * when an error happens, say 'object' rather than 'mixed.'  Use
     * 'void' if nothing is returned.
     *
     * Here's an example of how to format examples:
     * <sample>
     * require_once 'Net/Sample.php';
     *
     * $s = new NetSample();
     * if (PEAR::isError($s)) {
     *     echo $s->getMessage() . "\n";
     * }
     * </sample>
     *
     * @param string $arg1  the string to quote
     * @param int    $arg2  an integer of how many problems happened.
     *                       Indent to the description's starting point
     *                       for long ones.
     *
     * @return int  the integer of the set mode used. FALSE if foo
     *               foo could not be set.
     * @throws exceptionclass  [description]
     *
     * @access public
     * @static
     * @see NetSample::$foo, NetOther::someMethod()
     * @since Method available since Release 1.2.0
     * @deprecated Method deprecated in Release 2.0.0
     */
    function set_foo($arg1, $arg2 = 0) {
        /*
         * This is a "Block Comment."  The format is the same as
         * Docblock Comments except there is only one asterisk at the
         * top.  phpDocumentor doesn't parse these.
         */
        if ($arg1 == 'good' || $arg1 == 'fair') {
            $this->foo = $arg1;
            return 1;
        } else if ($arg1 == 'poor' && $arg2 > 1) {
            $this->foo = 'poor';
            return 2;
        } else {
            return false;
        }
    }

}

?>
```
