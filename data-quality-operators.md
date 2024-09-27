[Previous](User-Defined-Operators.md) [Next](graph_table-operator.md)
JavaScript must be enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [ Operators](Operators.md)
  3. Data Quality Operators

## Data Quality Operators

You can expand data quality capabilities within Oracle Database with string
matching operators `PHONIC_ENCODE` and `FUZZY_MATCH`.

These operators can help you find near duplicate rows by matching strings that
sounds alike or have small differences in spelling, for example:

  * "Chris" and "Kris", in strings that sound alike

  * "kitten" and "sitten", in strings that have small differences in spelling

### FUZZY_MATCH

`FUZZY_MATCH` takes the algorithm to be used as the first argument, the
strings to be processed as the second and third arguments, and some optional
arguments that control the quality of the desired output.

  

![Description of fuzzy_match.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/fuzzy_match.gif)  
[Description of the illustration fuzzy_match.eps](img_text/fuzzy_match.md)

  

The `UTL_MATCH` package evaluates byte by byte, while `FUZZY_MATCH` evaluates
character by character. Therefore `UTL_MATCH` only works for comparison
between single-byte strings while `FUZZY_MATCH` handles multi-byte
charactersets.

When the `UNSCALED` option is specified, `FUZZY_MATCH` returns a measure in
characters for the following algorithms: `LEVENSHTEIN` , `DAMERAU_LEVENSHTEIN`
, `BIGRAM` , `TRIGRAM` , `LONGEST_COMMON_SUBSTRING` .

Arguments

The supported algorithms are:

  * `LEVENSHTEIN` corresponds to `UTL_MATCH.EDIT_DISTANCE` or `UTL_MATCH.EDIT_SIMILARITY` and gives a measure of character edit distance or similarity. 

  * `DAMERAU_LEVENSHTEIN` distance differs from the classical `LEVENSHTEIN` distance by including transpositions among its allowable operations in addition to the three classical single-character edit operations (insertions, deletions and substitutions). 

  * `JARO_WINKLER` corresponds to `UTL_MATCH.JARO_WINKLER` (a percentage between 0-1) or `UTL_MATCH.JARO_WINKLER_SIMILARITY` (the same but scaled from 0-100). 

  * `BIGRAM` and `TRIGRAM` are instances of the N-gram matching technique, which counts the number of common contiguous sub-strings (grams) between the two strings. 

  * `WHOLE_WORD_MATCH` corresponds to Word Match Percentage or Count comparison in Oracle Enterprise Data Quality. It calculates the `LEVENSHTEIN` or edit distance of two phrases with words (instead of letters) as matching units. 

  * `LONGEST_COMMON_SUBSTRING` finds the longest common substring between the two strings. 

Both `str` arguments can be any of the datatypes `CHAR`, `VARCHAR2`, `NCHAR`,
`NVARCHAR2`.

UNSCALED

The keyword `UNSCALED` is optional. If you specify `UNSCALED` the return is
one of :

  * `LEVENSHTEIN` or edit distance 

  * `JARO_WINKLER` value in percentage 

  * N-grams, the number of common substrings

  * LCS, the length of the longest common substring 

RELATE_TO_SHORTER

The keyword `RELATE_TO_SHORTER` is optional. If you specify
`RELATE_TO_SHORTER`, then the similarity measure is scaled by the length of
the shorter input string. If you do not specify `RELATE_TO_SHORTER`, then the
default behavior is that the longer string length is used as the denominator.

EDIT_TOLERANCE

The keyword `EDIT_TOLERANCE` is optional. You can only specify
`EDIT_TOLERANCE` with the `WHOLE_WORD_MATCH` algorithm. If you specify
`EDIT_TOLERANCE`, the character error tolerance is the maximum percentage of
the number of characters in a word that you allow to be different, while still
considering each word as the same.

Returns

The operator returns `NUMBER`. By default, it is a similarity score normalized
to be a percentage between 0-100.

Examples

    
    
    SQL> select fuzzy_match(LEVENSHTEIN, 'Mohamed Tarik', 'Mo Tariq') from dual;
    
    FUZZY_MATCH(LEVENSHTEIN,'MOHAMEDTARIK','MOTARIQ')
    -------------------------------------------------
                                                   54
    
    1 row selected.
    
    
    SQL> select fuzzy_match(LEVENSHTEIN, 'Mohamed Tarik', 'Mo Tariq', unscaled) from dual;
    
    FUZZY_MATCH(LEVENSHTEIN,'MOHAMEDTARIK','MOTARIQ',UNSCALED)
    ----------------------------------------------------------
                                                             6
    
    1 row selected.
    
    
    
    
    SQL> select fuzzy_match(DAMERAU_LEVENSHTEIN, 'Mohamed Tarik', 'Mo Tariq', relate_to_shorter) from dual;
    
    FUZZY_MATCH(DAMERAU_LEVENSHTEIN,'MOHAMEDTARIK','MOTARIQ',RELATE_TO_SHORTER)
    ---------------------------------------------------------------------------
                                                                             25
    
    1 row selected.
    
    
    SQL> select fuzzy_match(BIGRAM, 'Mohamed Tarik', 'Mo Tariq', unscaled) from dual;
    
    FUZZY_MATCH(BIGRAM,'MOHAMEDTARIK','MOTARIQ',UNSCALED)
    -----------------------------------------------------
                                                        5
    
    1 row selected.
    
    
    SQL> select fuzzy_match(LONGEST_COMMON_SUBSTRING, 'Mohamed Tarik', 'Mo Tariq', unscaled) from dual;
    
    FUZZY_MATCH(LONGEST_COMMON_SUBSTRING,'MOHAMEDTARIK','MOTARIQ',UNSCALED)
    -----------------------------------------------------------------------
                                                                          5
    
    1 row selected.
    
    
    SQL> select fuzzy_match(WHOLE_WORD_MATCH,  'Mohamed Tarik', 'Mo Tariq') from dual;
    
    FUZZY_MATCH(WHOLE_WORD_MATCH,'MOHAMEDTARIK','MOTARIQ')
    ------------------------------------------------------
                                                         0
    
    1 row selected
    
    
    SQL> select fuzzy_match(WHOLE_WORD_MATCH, 'Pawan Kumar Goel', 'Pavan Kumar G', EDIT_TOLERANCE 60) from dual;
    
    FUZZY_MATCH(WHOLE_WORD_MATCH,'PAWANKUMARGOEL','PAVANKUMARG',EDIT_TOLERANCE60)
    -----------------------------------------------------------------------------
                                                                               67
    
    1 row selected.

### PHONIC_ENCODE

`PHONIC_ENCODE` takes the algorithm to be used as the first argument, the
string to be processed as the second argument, and an optional `max_code_len`
argument that controls the length of the desired output. `max_code_len` must
be an integer between 1 and 12.

  

![Description of phonic_encode.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/phonic_encode.gif)  
[Description of the illustration
phonic_encode.eps](img_text/phonic_encode.md)

  

Arguments

`DOUBLE_METAPHONE` returns the primary code. `DOUBLE_METAPHONE_ALT` returns
the alternative code if present. If the alternative code is not present, it
returns the primary code.

`str` can be any of the datatypes `CHAR`, `VARCHAR2`, `NCHAR`, `NVARCHAR2`.

The optional argument `max_code_len` must be an integer. It allows codes
longer than the default 4 characters to be returned for the original Metaphone
algorithm.

Returns

The operator returns `VARCHAR2`.

Examples

    
    
    SQL> select phonic_encode(DOUBLE_METAPHONE,     'smith') c1,
      2         phonic_encode(DOUBLE_METAPHONE_ALT, 'smith') c2 from dual;
    
    C1            C2
    ------------- -------------
    SM0           XMT
    
    1 row selected.
    
    
    SQL> select phonic_encode(DOUBLE_METAPHONE,     'Schmidt') c1,
      2         phonic_encode(DOUBLE_METAPHONE_ALT, 'Schmidt') c2 from dual;
    
    C1            C2
    ------------- -------------
    XMT           SMT
    
    1 row selected.
    
    
    SQL> select phonic_encode(DOUBLE_METAPHONE,     'phone') c1,
      2         phonic_encode(DOUBLE_METAPHONE_ALT, 'phone') c2 from dual;
    
    C1            C2
    ------------- -------------
    FN            FN
    
    1 row selected.
    
    
    SQL> select phonic_encode(DOUBLE_METAPHONE,     'George') c1,
      2         phonic_encode(DOUBLE_METAPHONE_ALT, 'George') c2 from dual;
    
    C1            C2
    ------------- -------------
    JRJ           KRK
    
    1 row selected.
    
    
    SQL> -- PNNT / PKNNT
    SQL> select phonic_encode(DOUBLE_METAPHONE,     'poignant') c1,
      2         phonic_encode(DOUBLE_METAPHONE_ALT, 'poignant') c2,
      3         phonic_encode(DOUBLE_METAPHONE_ALT, 'poignant', 10) c3 from dual;
    
    C1            C2            C3
    ------------- ------------- -------------
    PNNT          PKNN          PKNNT


[← Previous](data-quality-operators.md)

[Next →](graph_table-operator.md)
