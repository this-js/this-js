# Model Filters

The following is a full list of available filters:

- ## camelToHyphen ( )

    Changes camel case string to hyphen case
- ## camelToSnake ( )

    Changes camel case string to snake case
- ## capitalize ( )

    Capitalizes a string
- ## date ( format )

    Parses a date string or timestamp with the given **format**.

    **Format Parts**:

    *Day*

    - *D*       -   Day of the week, no leading zero
    - *DD*      -   Day of the week with a leading zero
    - *DDD*     -   Day, 3 letter string
    - *Ddd*     -   Day, capitalized 3 letter string
    - *ddd*     -   Day, lower case 3 letter string
    - *DDDD*    -   Day, full string
    - *Dddd*    -   Day, capitalized full string
    - *dddd*    -   Day, lower case full string

    *Date*

    - *d*       -   Date, no leading zero
    - *dd*      -   Date with a leading zero

    *Month*

    - *M*       -   Month, no leading zero
    - *MM*      -   Month with leading zero
    - *MMM*     -   Month, 3 letter string
    - *Mmm*     -   Month, capitalized 3 letter string
    - *mmm*     -   Month, lower case 3 letter string
    - *MMMM*    -   Month, full string
    - *Mmmm*    -   Month, capitalized full string
    - *mmmm*    -   Month, lower case full string

    *Year*

    - *YY*      -   2 digit year
    - *yy*      -   2 digit year
    - *YYYY*    -   4 digit year
    - *yyyy*    -   4 digit year

    *Hour*

    - *H*       -   24 hour, no leading zero
    - *h*       -   12 hour, no leading zero
    - *HH*      -   24 hour with leading zero
    - *hh*      -   12 hour with leading zero
    - *MER*     -   Meridian status, upper case (AM/PM)
    - *mer*     -   Meridian status, lower case (am/pm)

    *Minute*

    - *m*       -   Minute, no leading zero
    - *mm*      -   Minute with leading zero

    *Second*

    - *s*       -   Second, no leading zero
    - *ss*      -   Second with leading zero

    - *ms*      -   Milliseconds

    *Timezone*

    - *TZ*      -   Timezone, upper case
    - *tz*      -   Timezone, lower case

    - *t*       -   Timestamp of date, in milliseconds.

    *Position [ st, nd, rd, th ]*

    - *P*         - The upper case position of the number to which attached.
                    e.g. dP = date POSITION
    - *p*         - The lower case position of the number to which attached.
                    e.g. mp = minute POSITION

        Note: Position can be used with any character that outputs an integer.

- ## filter ( funcName )

    Filters items out of an object or array with the function whose name is provided.

    The function would receive two parameters: the value and the index, in that order.

    If the function returns true, then the value is retained otherwise it's removed.
- ## join ( glue )

    A shortcut to `Array.join()`
- ## lcase ( )

    A shortcut to filter `lowercase`
- ## lcfirst ( )

    Shortcut to filter `smallize`
- ## length ( )

    Gets the length of the value if value is object, array or string. Returns 0 otherwise.
- ## lowercase ( )

    Shortcut to `String.toLowerCase()`
- ## nl2br ( )

    Converts new lines into HTML break tags
- ## or ( def )

    Uses the provided parameter as the value if model property holds no value
- ## replace ( options )

    Performs a search and replace on the value of the property. The format of 
    the parameter is `search:replacement,flags;search2:replacement2,flags;...`
- ## smallize ( )

    Changes the first letter to lower case
- ## snakeToCamel

    Changes snake case to camel case
- ## split ( separator )

    Shortcut to `String.split()`
- ## trim ( )

    Shortcut to `String.trim()`
- ## ucase ( )

    Shortcut to filter `uppercase`
- ## ucwords ( )

    Capitalizes the first letter of each word
- ## uppercase ( )

    Shortcut to `String.toUpperCase()`

## Usage

Filters are applied to variables by separating the variable name and the filter
name by a pipe (`|`):

    {{ variable | filter }}

Multiple filters can be applied to a variable by separating each filter by
a pipe (`|`):

    {{ varable | filter1 | filter2 | filter3 | ... }}

### Filter options

Some filters take options while other don't. For those that do, the options
should be separated from the filter name by the equal sign (`=`):

    {{ variable | split=. }}

For string options, do not enclose in quotes, whether single or double. Just
write it out as is.

    {{ variable | or=No Value }}

In some cases, a filter may take multiple options. Separate these with semi-colons (`;`):

    {{ variable | replace=start:no start;change:no change }}

## Custom Filters

Custom filters can be created by extending the `Filters` object with `ThisApp.Filters()`
which returns the [`Extender` object](../extender.md).

When extending, you should specifiy a `name` for the filter and a `function`
to be called whenever a filtering is being done.

The function would be called with 2 parameers:

    (value, options)

`value` is the value to be filtered while `options` is the `string` options 
passed to the filter.

### Returned Value

The function should return the value after the filter has been performed on it.
This is then passed on to the next filter or simply rendered if not other filter
is specified.