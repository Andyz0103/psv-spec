# PSV - Pipe Separated Values
_CSV without doubts!_

PSV is a text based data format for tabular data. It is similar to [CSV](http://en.wikipedia.org/wiki/Comma-separated_values) in function, but more strictly defined. Although there is [RFC 4180](http://tools.ietf.org/html/rfc4180) for CSV, in practice there are a lot of incompatibilites between CSV implementations. I.e. trying to open a CSV file in a spreadsheet program leads to a plethora of (mostly technical) options. The goal of PSV is to simplify reading and writing tabular data by defining as much technical aspects as possible.

## PSV in a Nutshell
1. PSV files are text files encoded with UTF-8
2. Every line represents a row delimited by LF or CRLF characters
3. The last line has no line ending
4. Every row consists of one or more fields separated by a pipe character
5. There are no leading or trainling pipe characters
6. Some characters are escaped by a leading backslash
    * carriage return: \r
    * line feed: \n
    * backslash: \\\\
    * pipe character: \\|
7. All other characters preceeded by a backslash are treated as is

## PSV in Depth

### 1. PSV files are text files encoded with UTF-8
There are no doubts about the encoding. It's always UTF-8. No BOM!

### 2. Every line represents a row delimited by LF or CRLF characters
Since carriage return and line feed characters are escaped, a parser can assume, that an unescaped LF or CRLF character always represents the end of a row.

A carriage return can therefor simply be ignored, when parsing a PSV stream.

### 3. The last line has no line ending
If the last line in a PSV stream contains a CRLF or LF line ending, the parser will create another row with one empty field.

### 4. Every row consists of one or more fields separated by a pipe character

Every row has at least one field. Multiple fields are separated by the pipe character "|".

### 5. There are no leading or trailing pipe characters

A leading or trailing pipe character in a line represents an additional empty field.

### 6. Some characters are escaped by a leading backslash

The following characters in a fields content are treated special by escaping them with a leading backslash:

* carriage return: \r
* line feed: \n
* backslash: \\\\
* pipe character: \\|

This is one of the core aspects of PSV!

### 7. All other characters preceeded by a backslash are treated as is

A backslash can theoretically occur everywhere in a stream. If the following character is none of the ones listed in Rule 6, it will be ignored.

## Implementations

* [Java](https://github.com/jgis/psv-java)
