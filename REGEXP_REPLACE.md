[Previous](REGEXP_INSTR.md) [Next](REGEXP_SUBSTR.md) JavaScript must be
enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. REGEXP_REPLACE 

## REGEXP_REPLACE

Syntax

![Description of regexp_replace.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/regexp_replace.gif)  
[Description of the illustration
regexp_replace.eps](img_text/regexp_replace.md)

Purpose

`REGEXP_REPLACE` extends the functionality of the `REPLACE` function by
letting you search a string for a regular expression pattern. By default, the
function returns `source_char` with every occurrence of the regular expression
pattern replaced with `replace_string`. The string returned is in the same
character set as `source_char`. The function returns `VARCHAR2` if the first
argument is not a LOB and returns `CLOB` if the first argument is a LOB.

This function complies with the POSIX regular expression standard and the
Unicode Regular Expression Guidelines. For more information, refer to [Oracle
Regular Expression Support](Oracle-Regular-Expression-
Support.md#GUID-969230D6-FC1A-4C75-BF2A-6B1BE909DED6).

  * `source_char` is a character expression that serves as the search value. It is commonly a character column and can be of any of the data types `CHAR`, `VARCHAR2`, `NCHAR`, `NVARCHAR2`, `CLOB` or `NCLOB`. 

  * `pattern` is the regular expression. It is usually a text literal and can be of any of the data types `CHAR`, `VARCHAR2`, `NCHAR`, or `NVARCHAR2`. It can contain up to 512 bytes. If the data type of `pattern` is different from the data type of `source_char`, then Oracle Database converts `pattern` to the data type of `source_char`. For a listing of the operators you can specify in `pattern`, refer to [Oracle Regular Expression Support](Oracle-Regular-Expression-Support.md#GUID-969230D6-FC1A-4C75-BF2A-6B1BE909DED6). 

  * `replace_string` can be of any of the data types `CHAR`, `VARCHAR2`, `NCHAR`, `NVARCHAR2`, `CLOB`, or `NCLOB`. If `replace_string` is a `CLOB` or `NCLOB`, then Oracle truncates `replace_string` to 32K. The `replace_string` can contain up to 500 backreferences to subexpressions in the form `\n`, where `n` is a number from 1 to 9. If you want to include a backslash (`\`) in `replace_string`, then you must precede it with the escape character, which is also a backslash. For example, to replace `\2` you would enter `\\2`. For more information on backreference expressions, refer to the notes to "[Oracle Regular Expression Support](Oracle-Regular-Expression-Support.md#GUID-969230D6-FC1A-4C75-BF2A-6B1BE909DED6)", [Table D-1](Multilingual-Regular-Expression-Syntax.md#GUID-B03DEEAC-3F9E-4BFD-89D5-F481EA391D7C__BABJDBHB "Column 1 contains regular expression operators and column 2 describes Oracle Database support of each symbol."). 

  * `position` is a positive integer indicating the character of `source_char` where Oracle should begin the search. The default is 1, meaning that Oracle begins the search at the first character of `source_char`. 

  * `occurrence` is a nonnegative integer indicating the occurrence of the replace operation: 

    * If you specify 0, then Oracle replaces all occurrences of the match.

    * If you specify a positive integer `n`, then Oracle replaces the `n`th occurrence. 

If `occurrence` is greater than 1, then the database searches for the second
occurrence beginning with the first character following the first occurrence
of `pattern`, and so forth. This behavior is different from the `INSTR`
function, which begins its search for the second occurrence at the second
character of the first occurrence.

  * `match_param` is a character expression of the data type `VARCHAR2` or `CHAR` that lets you change the default matching behavior of the function. The behavior of this parameter is the same for this function as for `REGEXP_COUNT`. Refer to [REGEXP_COUNT](REGEXP_COUNT.md#GUID-5148AF2E-9CED-497D-A78D-3A7847A45276) for detailed information. 

See Also:

  * [REPLACE](REPLACE.md#GUID-1A79BDDF-2D3B-4AD4-98E7-985B2E59DA6B)

  * [REGEXP_INSTR](REGEXP_INSTR.md#GUID-D21B53A1-83E2-4722-9BBB-638470715DD6), [REGEXP_SUBSTR](REGEXP_SUBSTR.md#GUID-2903904D-455F-4839-A8B2-1731EF4BD099), and [REGEXP_LIKE Condition](Pattern-matching-Conditions.md#GUID-D2124F3A-C6E4-4CCA-A40E-2FFCABFD8E19)

  * Appendix C in [Oracle Database Globalization Support Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=NLSPG-GUID-AFCE41ED-775B-4A00-AF38-C436776AE0C5) for the collation determination rules, which define the collation `REGEXP_REPLACE` uses to compare characters from `source_char` with characters from `pattern`, and for the collation derivation rules, which define the collation assigned to the character return value of this function 

Examples

The following example examines `phone_number`, looking for the pattern
`xxx`.`xxx`.`xxxx`. Oracle reformats this pattern with (`xxx`) `xxx`-`xxxx`.

    
    
    SELECT
      REGEXP_REPLACE(phone_number,
                     '([[:digit:]]{3})\.([[:digit:]]{3})\.([[:digit:]]{4})',
                     '(\1) \2-\3') "REGEXP_REPLACE"
      FROM employees
      ORDER BY "REGEXP_REPLACE";
    
    REGEXP_REPLACE
    --------------------------------------------------------------------------------
    (515) 123-4444
    (515) 123-4567
    (515) 123-4568
    (515) 123-4569
    (515) 123-5555
    . . .
    

The following example examines `country_name`. Oracle puts a space after each
non-null character in the string.

    
    
    SELECT
      REGEXP_REPLACE(country_name, '(.)', '\1 ') "REGEXP_REPLACE"
      FROM countries;
    
    REGEXP_REPLACE
    --------------------------------------------------------------------------------
    A r g e n t i n a
    A u s t r a l i a
    B e l g i u m
    B r a z i l
    C a n a d a
    . . .
    

The following example examines the string, looking for two or more spaces.
Oracle replaces each occurrence of two or more spaces with a single space.

    
    
    SELECT
      REGEXP_REPLACE('500   Oracle     Parkway,    Redwood  Shores, CA',
                     '( ){2,}', ' ') "REGEXP_REPLACE"
      FROM DUAL;
    
    REGEXP_REPLACE
    --------------------------------------
    500 Oracle Parkway, Redwood Shores, CA

REGEXP_REPLACE pattern matching: Examples

The following statements create a table regexp_temp and insert values into it:

    
    
    CREATE TABLE regexp_temp(empName varchar2(20), emailID varchar2(20));
    
    INSERT INTO regexp_temp (empName, emailID) VALUES ('John Doe', 'johndoe@example.com');
    INSERT INTO regexp_temp (empName, emailID) VALUES ('Jane Doe', 'janedoe@example.com');

The following statement replaces the string âJaneâ with âJohnâ:

    
    
    SELECT empName, REGEXP_REPLACE (empName, 'Jane', 'John') "STRING_REPLACE" FROM regexp_temp;
    
    EMPNAME		STRING_REPLACE
    --------	--------------
    John Doe	John Doe
    Jane Doe	John Doe

The following statement replaces the string âJohnâ with âJaneâ:

    
    
    SELECT empName, REGEXP_REPLACE (empName, 'Jane', 'John') "STRING_REPLACE" FROM regexp_temp;
    
    EMPNAME		STRING_REPLACE
    --------	--------------
    John Doe	Jane Doe
    Jane Doe	Jane Doe

Live SQL:

View and run a related example on Oracle Live SQL at [REGEXP_REPLACE - Pattern
Matching](https://livesql.oracle.com/apex/livesql/docs/sqlrf/regexp_replace/match-
replace1.md)

REGEXP_REPLACE: Examples

The following statement replaces all the numbers in a string:

    
    
    WITH strings AS (   
      SELECT 'abc123' s FROM dual union all   
      SELECT '123abc' s FROM dual union all   
      SELECT 'a1b2c3' s FROM dual   
    )   
      SELECT s "STRING", regexp_replace(s, '[0-9]', '') "MODIFIED_STRING"  
      FROM strings;
    
      STRING               MODIFIED_STRING
    -------------------- --------------------
    abc123               abc
    123abc               abc
    a1b2c3               abc

The following statement replaces the first numeric occurrence in a string:

    
    
    WITH strings AS (   
      SELECT 'abc123' s from DUAL union all   
      SELECT '123abc' s from DUAL union all   
      SELECT 'a1b2c3' s from DUAL   
    )   
      SELECT s "STRING", REGEXP_REPLACE(s, '[0-9]', '', 1, 1) "MODIFIED_STRING"  
      FROM   strings;
    
     STRING               MODIFIED_STRING
    -------------------- --------------------
    abc123               abc23
    123abc               23abc
    a1b2c3               ab2c3

The following statement replaces the second numeric occurrence in a string:

    
    
    WITH strings AS (   
      SELECT 'abc123' s from DUAL union all   
      SELECT '123abc' s from DUAL union all   
      SELECT 'a1b2c3' s from DUAL   
    )   
      SELECT s "STRING", REGEXP_REPLACE(s, '[0-9]', '', 1, 2) "MODIFIED_STRING"  
      FROM   strings;
    
    STRING               MODIFIED_STRING
    -------------------- --------------------
    abc123               abc13
    123abc               13abc
    a1b2c3               a1bc3

The following statement replaces multiple spaces in a string with a single
space:

    
    
    WITH strings AS (   
      SELECT 'Hello  World' s FROM dual union all   
      SELECT 'Hello        World' s FROM dual union all   
      SELECT 'Hello,   World  !' s FROM dual   
    )   
      SELECT s "STRING", regexp_replace(s, ' {2,}', ' ') "MODIFIED_STRING"  
      FROM   strings;
    
     STRING               MODIFIED_STRING
    -------------------- --------------------
    Hello  World         Hello World
    Hello        World   Hello World
    Hello,   World  !    Hello, World !

The following statement converts camel case strings to a string containing
lower case words separated by an underscore:

    
    
    WITH strings as (   
      SELECT 'AddressLine1' s FROM dual union all   
      SELECT 'ZipCode' s FROM dual union all   
      SELECT 'Country' s FROM dual   
    )   
      SELECT s "STRING",  
             lower(regexp_replace(s, '([A-Z0-9])', '_\1', 2)) "MODIFIED_STRING"  
      FROM strings;
    
      STRING               MODIFIED_STRING
    -------------------- --------------------
    AddressLine1         address_line_1
    ZipCode              zip_code
    Country              country

The following statement converts the format of a date:

    
    
    WITH date_strings AS (   
      SELECT  '2015-01-01' d from dual union all   
      SELECT '2000-12-31' d from dual union all   
      SELECT '900-01-01' d from dual   
    )   
      SELECT d "STRING",   
             regexp_replace(d, '([[:digit:]]+)-([[:digit:]]{2})-([[:digit:]]{2})', '\3.\2.\1') "MODIFIED_STRING"  
      FROM date_strings;
    
      STRING               MODIFIED_STRING
    -------------------- --------------------
    2015-01-01           01.01.2015
    2000-12-31           31.12.2000
    900-01-01            01.01.900

The following statement replaces all the letters in a string with â1â:

    
    
    WITH strings as (   
      SELECT 'NEW YORK' s FROM dual union all   
      SELECT 'New York' s FROM dual union all   
      SELECT 'new york' s FROM dual   
    )   
      SELECT s "STRING",  
            regexp_replace(s, '[a-z]', '1', 1, 0, 'i') "CASE_INSENSITIVE",  
            regexp_replace(s, '[a-z]', '1', 1, 0, 'c') "CASE_SENSITIVE",  
            regexp_replace(s, '[a-zA-Z]', '1', 1, 0, 'c') "CASE_SENSITIVE_MATCHING"  
      FROM  strings;
    
      STRING     CASE_INSEN CASE_SENSI CASE_SENSI
    ---------- ---------- ---------- ----------
    NEW YORK   111 1111   NEW YORK   111 1111
    New York   111 1111   N11 Y111   111 1111
    new york   111 1111   111 1111   111 1111

Live SQL:

View and run a related example on Oracle Live SQL at
[REGEXP_REPLACE](https://livesql.oracle.com/apex/livesql/docs/sqlrf/regexp_replace/regexp-
replace1.md)


[← Previous](REGEXP_INSTR.md)

[Next →](REGEXP_SUBSTR.md)
