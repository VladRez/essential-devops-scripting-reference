# REGEX
Regex is a pattern matching language for processing text. Regex is generally either built in or available as a library in most programming languages. There are minor differences however in the majority of cases regex patterns are interchangeable. 

## Flags
Flags instruct how the pattern matching will treat the entire string. Typically formed with `/pattern/flag`

+ `i` - Case insensitive pattern matching.
    + `/pattern/i`
+ `g` - Global, match all occurrences.
    + `/pattern/ig`
+ `s` - Pattern match string as a single line.
+ `m` - Pattern match string as multiple lines.

## Meta Characters

+ `.` - Match any character in the string.
    + `n..e` Match any character that starts with n and ends with e, name for example.

### Repeating Matches
+ `{}` - Match range of repeating characters.
    + `a{,}` - Match `a` zero or multiple times.
    + `a{,1}` - Match `a` zero or one time.
    + `a{1,}` - Match `a` at least once.
    + `a{1,1}` - Match one `a`.
    + `a{1,2}` - Match `a` once or twice
    + `a{3}` - Match three `a`'s

### Quantifiers

Specify how many times should a match occur.
+ `\+` - Match at least once.
    + Same as `{1,}`
+ `\?` - Match zero or one occurrence.
    + Same as `{,1}`
+ `*` - Match zero or more occurrences.
    + Same as `{,}`
+ `x|y` - Logical `or`, match character `x` or `y`

## Character Class
+ `[]` - match each character within brackets.
    + `[aeiou]` - Match vowels.
    + `s[aeiou]` - Match s followed by a vowel.
    + `s[^aeiou]` - Negation of a character range. Begins with an s followed by any character that's not a vowel.
    + `[a-z]` - All lower case letters
    + `[A-Z]` - All upper case letters
    + `[a-zA-Z]` - All characters. 
    + `[0-9]` - All Numbers
    + `[a-zA-Z0-9]` - All characters and Numbers.  

### Pre-Defined Character Class
+ `\d` - digit 
    + Same as `[0-9]`
+ `\D` - Not digit 
    + Same as `[^0-9]`
+ `\w` - word
    + Same as `[a-z0-9_]`
+ `\W` - word
    + Same as `[^a-z0-9_]`
+ `\s` - White spaces
+ `\S` - Not white spaces
+ `\n` - Newline
+ `\t` - Tab
+ `\r` - Return Character
+ `\f` - Form feed, advance downward to the next "page"

## Anchors
+ `^` - Anchor match at the beginning of the string
    + + `^s[aeiou]` - Start match with `s` followed by a vowel.
+ `$` - Anchor match at the end of the string

## Groups
+ `()` - Group a pattern, used for sub-search
    + `(x|y){2}` - Match two, `xx`, `yy`, `xy`, `yx`
+ `(?:)` - Non-capture group, ignore pattern within the group. 

## Substitution
+ `$1` - Used as a place holder for the first pattern match.
    + `abc abc` match with `\w` replace with `$1,` results in `abc, abc,`
+ `\1` - Repeat of a proceeding pattern, e.g `pattern \1`.
    + `\w \1` Used to suppress repeating words.
