[Previous](vector.md) [Next](vector_distance.md) JavaScript must be
enabled to correctly display this content

  1. [SQL Language Reference ](index.md)
  2. [Functions](Functions.md)
  3. VECTOR_CHUNKS

## VECTOR_CHUNKS

Syntax

  

![Description of vector_chunks.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/vector_chunks.gif)  
[Description of the illustration
vector_chunks.eps](img_text/vector_chunks.md)

  

chunks_table_arguments::=

  

![Description of chunks_table_arguments.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/chunks_table_arguments.gif)  
[Description of the illustration
chunks_table_arguments.eps](img_text/chunks_table_arguments.md)

  

chunking_spec::=

  

![Description of chunking_spec.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/chunking_spec.gif)  
[Description of the illustration
chunking_spec.eps](img_text/chunking_spec.md)

  

split_characters_list::=

  

![Description of split_characters_list.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/split_characters_list.gif)  
[Description of the illustration
split_characters_list.eps](img_text/split_characters_list.md)

  

custom_split_characters_list

  

![Description of custom_split_characters_list.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/custom_split_characters_list.gif)  
[Description of the illustration
custom_split_characters_list.eps](img_text/custom_split_characters_list.md)

  

normalization_spec

  

![Description of normalization_spec.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/normalization_spec.gif)  
[Description of the illustration
normalization_spec.eps](img_text/normalization_spec.md)

  

custom_normalization_spec

  

![Description of custom_normalization_spec.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/custom_normalization_spec.gif)  
[Description of the illustration
custom_normalization_spec.eps](img_text/custom_normalization_spec.md)

  

normalization_mode

  

![Description of normalization_mode.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/normalization_mode.gif)  
[Description of the illustration
normalization_mode.eps](img_text/normalization_mode.md)

  

chunking_mode::=

  

![Description of chunking_mode.eps
follows](https://docs.oracle.com/en/database/oracle/oracle-database/23/sqlrf/img/chunking_mode.gif)  
[Description of the illustration
chunking_mode.eps](img_text/chunking_mode.md)

  

Purpose

`VECTOR_CHUNKS` is a one-to-many table function that takes a row of textual
input and returns the output as one or more chunks with metadata.

The chunking output includes:

  * `chunk_offset`: Position of each chunk (`NUMBER`) in the source document, relative to the start of document which has a position of `1`

  * `chunk_length`: Character length (`NUMBER`) of each chunk 

  * `chunk_text`: Text pieces from each chunk 

`VECTOR_CHUNKS` takes as input one of the following data types: `VARCHAR2`,
`CHAR`, `CLOB`, `NVARCHAR2`, `NCLOB`, `NCHAR`. It is aware of the database
character set and the national language character set.

It returns as output a text chunk as `VARCHAR2` or `NVARCAHR2`.

Table 7-13 Input and Output Data Type Details

Input Data Type | Database NLS Parameter | Input Encoding | Output Data Type | Output Offset  
---|---|---|---|---  
`VARCHAR2` |  `NLS_CHARACTERSET` |  Any |  `VARCHAR2` |  `byte`  
`CHAR` |  `NLS_CHARACTERSET` |  Any |  `VARCHAR2` | `byte`  
`CLOB` |  `NLS_CHARACTERSET` Note:`CLOB` is a special case, as it stores the data in `UTF-16` (when this character set is multi-byte) but provides access in this NLS character set. The chunking table function uses the `NLS_CHARACTER_SET` so it can output in a `VARCHAR2`. However, the returned offset and length are in terms of characters.)  |  Any |  `VARCHAR2` |  `character`  
`NVARCHAR2` |  `NLS_NCHAR_CHARACTERSET` |  `AL16UTF16` (also `AL32UTF8`)  |  `NVARCHAR2` |  `byte`  
`NCLOB` |  `NLS_NCHAR_CHARACTERSET` |  `AL16UTF16` (also `AL32UTF8`)  |  `NVARCHAR2` |  `character`  
`NCHAR` |  `NLS_NCHAR_CHARACTERSET` |  `AL16UTF16` (also `AL32UTF8`)  |  `NVARCHAR2` |  `byte`  
  
Note:

  * The SQL `NCHAR`, `NVARCHAR2`, and `NCLOB` data types support Unicode data only. You can use either `UTF8` or `AL16UTF16` character set. The default is `AL16UTF16`. 

  * The `VARCHAR2` input data type is limited to `4000` bytes unless the `MAX_STRING_SIZE` parameter is set to `EXTENDED`, which increases the limit to `32767`. 

Parameters

All chunking parameters are optional, and the default chunking specifications
are automatically applied to your chunk data.

When specifying chunking parameters for this API, ensure that you provide
these parameters only in the listed order.

Table 7-14 Parameters Table

Parameter | Description and Acceptable Values  
---|---  
`BY` |  Specifies the mode for splitting your data, that is, to split by counting the number of characters, words, or vocabulary tokens. Valid values: 

  * `BY CHARACTERS` (or `BY CHARS`):  Splits by counting the number of characters.
  * `BY WORDS`:  Splits by counting the number of words. Words are defined as sequences of alphabetic characters, sequences of digits, individual punctuation marks, or symbols. For segmented languages without whitespace word boundaries (such as Chinese, Japanese, or Thai), each native character is considered a word (that is, unigram).
  * `BY VOCABULARY`:  Splits by counting the number of vocabulary tokens. Vocabulary tokens are words or word pieces, recognized by the vocabulary of the tokenizer that your embedding model uses. You can load your vocabulary file using the `VECTOR_CHUNKS` helper API `DBMS_VECTOR_CHAIN.CREATE_VOCABULARY`.  Note: For accurate results, ensure that the chosen model matches the vocabulary file used for chunking. If you are not using a vocabulary file, then ensure that the input length is defined within the token limits of your model. 

Default value: `BY WORDS`  
`MAX` |  Specifies a limit on the maximum size of each chunk. This setting splits the input text at a fixed point where the maximum limit occurs in the larger text. The units of `MAX` correspond to the `BY` mode, that is, to split data when it reaches the maximum size limit of a certain number of characters, words, numbers, punctuation marks, or vocabulary tokens.  Valid values: 

  * `BY CHARACTERS`: `50` to `4000` characters 
  * `BY WORDS`: `10` to `1000` words 
  * `BY VOCABULARY`: `10` to `1000` tokens 

Default value: `MAX 100`  
`SPLIT [BY]` |  Specifies where to split the input text when it reaches the maximum size limit. This helps to keep related data together by defining appropriate boundaries for chunks.  Valid values: 

  * `NONE`:  Splits at the `MAX` limit of characters, words, or vocabulary tokens. 
  * `NEWLINE`, `BLANKLINE`, and `SPACE`:  These are single-split character conditions that split at the last split character before the `MAX` value.  Use `NEWLINE` to split at the end of a line of text. Use `BLANKLINE` to split at the end of a blank line (sequence of characters, such as two newlines). Use `SPACE` to split at the end of a blank space. 
  * `RECURSIVELY`:  This is a multiple-split character condition that breaks the input text using an ordered list of characters (or sequences).  `RECURSIVELY` is predefined as `BLANKLINE`, `NEWLINE`, `SPACE`, `NONE` in this order:  1\. If the input text is more than the `MAX` value, then split by the first split character.  2\. If that fails, then split by the second split character.  3\. And so on.  4\. If no split characters exist, then split by `MAX` wherever it appears in the text. 
  * `SENTENCE`:  This is an end-of-sentence split condition that breaks the input text at a sentence boundary. This condition automatically determines sentence boundaries by using knowledge of the input language's sentence punctuation and contextual rules. This language-specific condition relies mostly on end-of-sentence (EOS) punctuations and common abbreviations.  Contextual rules are based on word information, so this condition is only valid when splitting the text by words or vocabulary (not by characters).  Note: This condition obeys the `BY WORD` and `MAX` settings, and thus may not determine accurate sentence boundaries in some cases. For example, when a sentence is larger than the `MAX` value, it splits the sentence at `MAX`. Similarly, it includes multiple sentences in the text only when they fit within the `MAX` limit. 
  * `CUSTOM`:  Splits based on custom split characters list. You can provide custom sequences up to a limit of `16` split character strings, with a maximum length of `10` each.  Provide valid text literals as follows:
    
        VECTOR_CHUNKS(c. doc, BY character SPLIT CUSTOM ('<html>' , '</html>')) vc

You can omit sequences only for tab (`\t`), newline (`\n`), and linefeed
(`\r`).

Default value: `RECURSIVELY`  
`OVERLAP` |  Specifies the amount (as a positive integer literal or zero) of the preceding text that the chunk should contain, if any. This helps in logically splitting up related text (such as a sentence) by including some amount of the preceding chunk text.  The amount of overlap depends on how the maximum size of the chunk is measured (in characters, words, or vocabulary tokens). The overlap begins at the specified `SPLIT` condition (for example, at `NEWLINE`).  Valid value: `5%` to `20%` of `MAX` Default value: `0`  
`LANGUAGE` |  Specifies the language of your input data. This clause is important, especially when your text contains certain characters (for example, punctuations or abbreviations) that may be interpreted differently in another language. Valid value: Any NLS-supported language name or language abbreviation, as listed in [Oracle Database Globalization Support Guide](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=NLSPG-GUID-D2FCFD55-EDC3-473F-9832-AAB564457830).  You must use double quotation marks (`"`) for any language name with spaces. For example:  `LANGUAGE "simplified chinese"` For one-word language names, quotation marks are not needed. For example:  `LANGUAGE american` Note: You can use the `DBMS_VECTOR_CHAIN.CREATE_LANG_DATA` chunker helper API to load language-specific data (abbreviation tokens) into the database, for your specified language.  Default value: `NLS_LANGUAGE` from session   
`NORMALIZE` |  Automatically pre-processes or post-processes issues (such as multiple consecutive spaces and smart quotes) that may arise when documents are converted into text. Oracle recommends you to use this mode to extract good-quality chunks. Valid values: 

  * `NONE`:  Specifies no normalization.
  * `ALL`:  Normalizes common multi-byte (unicode) punctuation to standard single-byte.
  * `PUNCTUATION`:  Includes the smart quotes, smart hyphens, and other multi-byte equivalents to simple single-byte punctuation. For example: 
    * `2018u 'map to 0027'`
    * `2019u 'map to 0027'`
    * `201Bu 'map to 0027'`
  * `WHITESPACE`:  Minimizes whitespace by eliminating unnecessary characters.  For example, retain blanklines, but remove any extra newlines and interspersed spaces or tabs: `" \n \n " => "\n\n"`
  * `WIDECHAR`:  Normalizes wide, multi-byte digits and (a-z) letters to single-byte. These are multi-byte equivalents for `0-9` and `a-z A-Z`, which can show up in `ZH/JA` formatted text. 

Note: You must specify a comma-separated list of `WHITESPACE`, `PUNCTUATION`,
and `WIDECHAR` in parentheses.  Default value: None  
`EXTENDED` |  Increases the output limit of a `VARCHAR2` string to `32767` bytes, without requiring you to set the `MAX_STRING_SIZE` parameter to `EXTENDED`.  Default value: `4000` or `32767` (when `MAX_STRING_SIZE=EXTENDED`)   
  
Example

    
    
    CREATE TABLE documentation_tab (
      id   NUMBER,
      text VARCHAR2(2000));
    
    INSERT INTO documentation_tab 
       VALUES(1, 'sample');
    
    COMMIT;
    
    SET LINESIZE 100;
    SET PAGESIZE 20;
    COLUMN pos FORMAT 999;
    COLUMN siz FORMAT 999;
    COLUMN txt FORMAT a60;
    
    PROMPT SQL VECTOR_CHUNKS
    SELECT D.id id, C.chunk_offset pos, C.chunk_length siz, C.chunk_text txt
    FROM documentation_tab D, VECTOR_CHUNKS(D.text BY words
                                      MAX 200
                                      OVERLAP 10
                                      SPLIT BY recursively
                                      LANGUAGE american
                                      NORMALIZE all) C;

See Also:

  * For a complete set of examples on each of the chunking parameters listed in the preceding table, see [Explore Chunking Techniques and Examples](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=VECSE-GUID-BFDE8B0A-6302-472C-AD8B-1BEB9AA2CB87) in the Oracle AI Vector Search User's Guide. 

  * To run an end-to-end example scenario using this function, see [Convert Text to Chunks With Custom Chunking Specifications](/pls/topic/lookup?ctx=en/database/oracle/oracle-database/23/sqlrf&id=VECSE-GUID-E6771B78-5FB4-4EBA-92F5-BE9FF2DF6AFA) in the Oracle AI Vector Search User's Guide. 

  * [Vector Functions](Single-Row-Functions.md#GUID-C0C477F1-8210-4CA9-A5FA-0A340C409892)


[← Previous](vector.md)

[Next →](vector_distance.md)
