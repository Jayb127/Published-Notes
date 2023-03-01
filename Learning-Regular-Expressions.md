# Learning Regular Expressions
LinkedIn Learning Course 

https://www.linkedin.com/learning/learning-regular-expressions-15586553/write-text-matching-patterns?autoplay=true&u=71391282

> Note: The instructor does make the odd mistake, as you'll see in the comments for the course. Don't be completely thrown off if a solution offered in a video doesn't seem right. In that case, use a website like Regexr to test it out yourself and confirm how it actually works. 

## 1 - Getting Started with Regular Expressions 
A regular expression is a series of symbols that represent a text pattern. They are used for matching, searching, and replacing text, and they are frequently used in programming languages. 

The term "Regular Expressions" refers to the formal language interpreted by a regular expression processor. 

Usage Examples: 
- Test if a credit card number has the corrent number of digits. 
- Test if an email address is in a valid format 
- Search a document for either "color" or "colour" 
Replace all occurrences of "Bob," "Bobby," or "B." with "Robert." 
- Count how many times "training" is preceded by "computer," "video," or "online." 

A regular expression is said to "match" the text if it correctly describes the text. Conversely, text matches a regular expression if it is correctly described by the expression. 

The following programming languages/technologies include RegEx processing engines: 
- C/C++
- Java
- JavaScript
- .NET
- Perl
- PHP
- Python
- Ruby
- Unix
- Apache
- MySQL

Generally speaking, regex will work the same way on all of these engines, but there can be small variations. The most notable example is with Unix. In any case, consult the documentation for the engine to be aware of the nuances. 

RegEx Applications: 
- grep, egrep
- TextMate
- Atom
- Sublime
- Notepad++ 
- RegexBuddy
- RegexMagic
- Various mobile applications

In this course, a JavaScript web application called "regexr" will be used, but there are other options. 
- https://regexr.com
- https://regex101.com
- https://regexpal.com 

### Notation Conventions 
A regular expression is usually defined within two `/` characteers: 
```
/abc/
```
The slashes are used to delimit the expression in the code, but the regex tools used in this course do not require them. 

RegExr's UI supports selection of flags (global, case insensitive, etc). In the expression itself, the flag is added by placing the associated letter after the closing `/`. 

The flags are as follows: 
- Standard: `/abc/` - No flag
- Global: `/abc/g` - A global expression will return all matches, not just the first one
- Case Insensitive: `/abc/i` - A case-insensitive expression will not pay attention to letter case when matching
- Multiline: `/abc/m` - A multiline expression will support matches that span multiple lines rather than the entire match having to be on the same line

## 2 - Characters 

### Literal Characters 
The letter "a" in a regular expression matches the letter "a" in a string. Literal characters are similar to searching in a word processor, and it's the simplest match there is. By default, literal character searches are case-sensitive. 
- `/car/` will match "car" 
- `/car/` will also match the first three letters of "carnival." It won't match the entire word, though. 
- `/car/` will not match "Car." However, flagging the expression as case-insensitive (`/car/i`) would create a match. 
 
### Metacharacters
If something isn't a literal character, it's a metacharacter. Metacharacters are characters with special meaning. They transform literal characters into powerful expressions, but can have more than one meaning and are therefore context-dependent.  The metacharacters are: 
```
\ . * + - {} [] ^ $ | ? () : ! =
```


#### The Wildcard Metacharacter (.)
The wildcard metacharacter (.) matches any character except for a new line. 

Examples: 
- `/h.t/` will match "hat," "hot," and "Hot," but not "heat." 
- `/9.00/` will match "9.00," "9500," and "9-00" because the period is functioning as a wildcard rather than as a decimal to be matched. Fixing this will be addressed in a later section. 

Beginners are prone to being overpermissive with what they're trying to match, often using wildcards excessively. 

#### The Escape Metacharacter (\\)
The escape metacharacter (\\) is used to indicate that the next metacharacter should be interpreted as a literal character, also known as **escaping** that character. 

Examples: 
- `/\./` would match a literal period. 
- `/9\.00/` would now match "9.00" but not "9500" or "9-00" 
- Match a backslash by escaping a backslash: `/\\/`

Remember that escaping is **only** for metacharacters. Literal characters should never be escaped, and doing so may give them unintended meaning. Quotation marks are not metacharacters and do not need to be escaped. 

#### Other Special Characters
Other metacharacters will be reviewed later in the course. This section is about other special characters to be aware of. 

- Spaces are characters and can be matched as literal characters. No special notation is required. 
- Tabs must be notated as `\t`. Note that the backslash escapes the "t". Ordinarily, "t" would be a literal character, but the "\" gives it a special meaning. 
- Line returns must be noted in one of three ways, depending on the processor: 
    - `\r` is a line return 
    - `\n` is a new line. JavaScript appears to favor this option. 
    - `\r\n` is also an option. 

> Note: "Control Characters" are letters that are literal characters by default but are given a special meaning when escaped. 

## 3 - Character Sets 

### The Character Set Metacharacter(s) (`[` and `]`)
The character set metacharacters (`[` and `]`) are used to define a custom character set. A character set will match any one of several characters in the set, but it will *only* match one. The order in which the characters are listed in the set does not matter. This is a tool for evaluating one character at a time. 

Examples: 
- `/aeiou/` would match any one vowel. Note, however, that it would be case-sensitive. 
- `/gr[ea]y/` would match both "grey" and "gray." 
- `/gr[ea]t/` would NOT match "great." 

### The Character Range Metacharacter (`-`)
The character range metacharacter (`-`) is used to define a character range. The dash character is only a metacharacter when it is within a character set. Otherwise, it is a dash literal character. When it appears within a character set, it represents the inclusion of all characters between two characters. Therefore, it is based on an established order in which the characters should appear. This applies to letters and numbers, but also to symbols. 

Examples: 
- `/[0-9/]/` would match any number between 0 and 9 (including 0 and 9)
- `/[A-Za-z]/` would match any letter, either uppercase or lowercase. 
- `/[A-DX-Z]/` would match A, B, C, D, X, Y, Z. 
- `/[50-99]/` would NOT include all numbers between and including 55 and 99. 
    - Remember that a character set only matches one character. There are no two-digit values in character sets, just multiple character sets.  
    - The regex engine will interpret this as a character set including 5, 0-9, and 9, which is just effectively 0-9. 

### The Negative Metacharacter (`^`)
The negative metacharacter (`^`) is used to negate a character set. A negated character set specifies the values that a matching character is *not*. The regex engine will identify any character that is not listed within the negated set as a match. A character set is negated by adding the negative metacharacter (`^`) as the first character inside the set. 

Examples: 
- `/[^aeiou]/` matches any one consonant, any uppercase letter, any number, any special character, or a space. 
- `/see[^mn]/` matches "seek" and "sees" but not "seem" or "seen."
    - It would not match "see". The character set includes all lowercase letters except for m and n, but a black space is not considered a letter. However, it would match "see " with a space after it. 

### Metacharacters Inside Character Sets 
Most metacharacters inside character sets are already escaped and being interpreted as literal characters, so they do not need to be escaped again. The exceptions are:
- `]` because it must be able to tell the regex engine where the end of the character set is
- `-` because it is used to identify a range within a character set. 
- `^` because it is used to negate a character set 
- `\` because it must be available to escape the other metacharacters within the set that need to be escaped. 

Examples: 
- `/h[a.]t/` matches "hat" and "h.t" but not "hot" 
- For the expression `/var[[(][0-9][\])]/`
    - The first character set is `[[(]`, which simply matches either a `[` or a `(`
    - The second character set `[0-9]` matches with any number
    - The final character set `[\])]` matches either `]` or `)`. Note that the `]` must be escaped, which accounts for the `\`. A matching `\` is not present in the first character set because `[` doesn't need to be escaped in a character set. 
    - Examples of matching values: 
        - var[0]
        - var(3)
        - var(7]
- For the expression `/file[0\-\\_]1/`
    - The character set escapes both the `-` and the `\`.
    - Therefore, the range of characters in the set is actually `0`, `-`, `\`, and `_`
    - Examples of matching values: 
        - file01
        - file-1
        - file\1
        - file_1
- For the expression `/2013[-/]10[-/]05/`
    - In some cases, the `-` does not need to be escaped if it's the first character in the character set. Because the `-` metacharacter is meant to appear between the characters that represent the start and end of a range, a `-` appearing at the start of a character set can only be syntactically correct if it's a literal character, not a metacharacter. 
    - Therefore, the range of characters (depending on the engine) may be `-` and `/`, or it may just be `/` 
    - Better safe than sorry; it's best to escape the `-`, even if it's the first character in a character set

### Shorthand Character Sets 
There are several ways to shorten expressions using some established shorthand: 
- `\d` is a **digit,** and the equivalent of any number from 0 to 9. `/[0-9]/`
    - `\D` is the inverse of `\d`, meaning that is any character OTHER than 0 to 9. `/[^0-9]/`
- `\w` is a **word character,** and is the equivalent of any letter uppercase or lowercase, any number, and the underscore character. `/[a-zA-Z0-9_]/`
    - The underscore (`_`) is considered a word character
    - A common practice is to also include the hypen, which can be done by including the shorthand within a character set. `/[\w\-]/`
    - `\W` is the inverse of `\w`. `/[^a-zA-Z0-9_]/` 
- `\s` is a **white space,** and is the equivalent of a space, a tab, a carriage return, or a line break. `/[ \t\r\n]/`
    - `\S` is the inverse of `\s`. `/[^ \t\r\n]/`

### A Note about Using Shorthand
- A negative character set is not always the same as a character set with capital shorthand. 
    - `/^\d\s/` is NOT the same as `[\D\S]`
    - The first one basically means "NOT a digit or space character." The `^` inverses the entire expression, combining all the values included in `\d` and `\s` and then inversing that to find the remaining possible values. 
    - The second one basically means "EITHER NOT digit OR NOT space character." This is different from the first expression, because it's not combining the `\D` and the `\S` and then finding the reverse. Rather, it's evaluating each character one at a time, as is typical for a character set. This means that, even though the number 9 is a digit, (and therefore not a match with `\D`), it is NOT a space, which is a match with `\s`, so it matches. A space would also match for being not a digit. 

> Note: The uppercase shorthand doesn't get used as much, because it can cause confusing problems like the one above. It's much more common to use the lowercase shorthands and inverse them as necessary. 

### Challenge Problems and Solutions 
- Match both "lives" and "lived" 
    - My solution: `/live[sd]/`
- Match "virtue" but not "virtues" 
    - Also, what is the problem with writing this expression based on the information we have right now? Why is it not a perfect solution? 
    - My solution: `/virtue[^s]/`. The problem is that the space is included in the match. 
- Match the numbers and periods on all numbered paragraphs 
    - There are 8 numbers that appear in the text. 4 of them are a date at the top. The second 4 are numbered paragraphs that have a period after them. The solution for this problem should match the 4 paragraph numbers and the periods, but not the date digits. 
    - My solution: `/\d\./`
- Find the 16-character word that starts with "c" 
    - My solution: `/c\w\w\w\w\w\w\w\w\w\w\w\w\w\w/`

## 4 - Repetition 
Repetition is used to make complex expressions easier to write and understand. 

### Repetition Metacharacters 
There are three repetition metacharacters: `*`, `+`, and `?` 
They will all be used after something else in a regular expresison, and that "something else" will be repeated a certain number of times depending on which repetition metacharacter is used. 

#### The `*` Metacharacter 
- Means "preceding item, zero or more times". It doesn't have to appear for a match to occur, and if it does appear, it can appear repeatedly and still be considered a match.  
- `/apples*/` matches "apple", "apples" and "applessssssssss"
- `/\d\d\d\d*/` matches numbers with 3 digits or more

#### The `+` Metacharacter 
- Means "preceding item, one or more times"
- This is the most frequently used repetition metacharacter. 
- `/apples+/` matches "apples" and "applesssssss", but not "apple" 
- `/\d\d\d+/` matches numbers with three digits or more. 
- It's frequently paired with the wildcard metacharacter (`/.+/`), which matches any string of characters except a line return. It's used to signify, in  vague terms, that something is present. 
    - `/Good .+\./` matches "Good morning.", "Good day.", "Good evening.", and "Good night." The `.+\.` segment means that there will be a certain number of characters after the space, and the expression should match all of those until it reaches a period (and include that period). If the text ends (or a line break occurs) without a period to close the expression, it won't match anything. 
- `/\d+/` matches "90210". Note that it doesn't match each number individually. Rather, it matches "90210" as a single match. 
- `/\s[a-z]+ed\s/` matches lowercase words ending in "ed". 

#### The `?` Metacharacter
- Means "preceding item, zero or one time" 
- `/apples?/` matches "apple" and "apples", but not "applesssssss"
- A good use case for `?` is to capture alternative spellings of english words like "color/colour" with `/colou?r/`

### Quantified Repetition
The repetition metacharacters can be very useful, but they are also somewhat vague. **Quantified Repetition** is a more specific method of repetition using the `{` and `}` metacharacters. The `{}` can either contain a minimum and maximum separated by a comma or a single value to indicate a specific number of repetitions. The values should always be positive. The `{}` is placed immediately after the expression segment that it's supposed to repeat. 

There are 3 syntaxes for quantified repetition: 
- `/\d{4,8}/` matches numbers with 4 to 8 digits. 
- `/\d{4}/` matches numbers with exactly 4 digits (minimum and maximum are the same, expressed as a single value)
- `/\d{4,}/` matches numbers with 4 or more digits (the maximum is infinite) 

> Note: Quantified repeition can be used to express things that can also be expressed with the original 3 repeition metacharacters. For example, `/\d{0,}/` is the same as `/\d*/`. Similarly, `/\d{1,}/` is the same as `/\d+/`.

Quantified repeition is commonly used on standardized data where numbers match a specific pattern. For example:
- `/\d{3}-\d{3}-\d{4}/` would match a typical XXX-XXX-XXXX US phone number. 
- `/A{1,2} bonds/` would match "A bonds" and "AA bonds" but not "AAA bonds" 

### Greedy Expressions
Because of the flexibility of regular expressions, it's possible to encounter ambiguous scenarios, where it's not entirely clear how the regex engine should interpret something. 

For example, for the following expression:
```
/".+", ".+"/
```
And given the following text: 
```
"Milton","Waddams", "Initech, Inc." 
```

An argument can be made for any of the following scenarios:
- "Milton" and "Waddams" match the expression
- "Milton" matches the first segment of the expression and "Waddams", "Initech, Inc." matches the second segment. 
- "Milton", "Waddams" matches the first segment of the expression and "Initech, Inc." matches the second. 

Understanding how the regular expression engine works is important to figuring out how the engine will interpret the expression and what it will match. 

Standard repetition quantifiers are **greedy**, meaning that they try to match the longest possible string. In the example above, the wildcard metacharacter (`.`) will try to eat up as much of the available string as possible while still deferring to the ultimate goal of achieving an overall match. Regex engines are eager, meaning that they want to return a match as fast as they can, but they're also greedy, which means that they want to take up as much of the text as they can and give back as little as possible. 

Examples: 
- The expression `/.+\.jpg/` will match "filename.jpg"
    - The + is "greedy," but it "gives back" the ".jpg" to make the match. 
    - Greedy expressions "give back" as little as possible.  
- The expression `/.*[0-9]+/` will match "Page 266"
    - The wildcard (`.`) is going to take up as much as possible, and the `.*` segment of the expression matches "Page 26". The `[0-9]` segment only matches the final "6"
    - The easiest way to think about it is that the wildcard (`.`) tries to match as much as possible before giving control to the next segment of the expression. 
    - As the regex engine moves through the string, it sees that each character technically can be made to match the wildcard (`.`). Eventually, it reaches the end of the string, but it knows that it still has the remainder of the expression to factor in. The engine processes the second segment and realizes that, since it's at the end of the string, there is no match for the second segment. It starts to move backward in the string, checking to see if there's a way to create a match by evaluating each character. Once it finds something that matches the second segment of the expression without unmatching the string with the first segment of the expression, it will have made a full match with the expression. 
- Given the expression `/\d+\w+\d+/` and a value of "01_FY_07_report_99.xls"
    - The first `\d+` will match "01" 
    - The `\w+` will match "_FY_07_report_99" and stop at the literal period cheracter. 
    - Since the literal period character does not match `\d+` either, the engine moves backward once character to the second 9, detects that it matches with the `\d+`, and gives it back, allowing for a match. 
- Given the expression `/".+", ".+"/` and the string `"Milton","Waddams", "Initech, Inc."`
    - The first `".+"` could match the entire string, but it reaches the end and knows that a full match hasn't been made. 
    - If the engine moves back one character from the end, it finds a quotation mark (") to match with the second set of quotation marks in the first segment of the expression, but there's no comma after it. 
    - The expression engine backs all the way up until it finds something that matches the remainder of the expression and then calls it a match. 
    - The entire string matches.
    - The first segment of the expression (`".+",`) matches with `"Milton", "Waddams", `
    - The second segment of the expression (`".+"`) matches with `"Initech, Inc."`

### Lazy Expressions

**Lazy expressions** are the opposite of greedy expressions and change the way the regex engine makes decisions. The "lazy" strategy is to match as little as possible before giving control to the next segment of the expression. Like greedy expressions, lazy expressions still defer to and prioritize an overall match. Lazy expressions are not necessarily faster or slower than greedy expressions; they're just a different way of doing things. To made a quantifier lazy, put a `?` metacharacter before it. For example: 
- `*?`
- `+?`
- `{min, max}?`
- `??`

> Remember, the `?` metacharacter is also a repetition modifier. The context of the character's usage is very important to making sure that an expression achieves the desired result. 

Examples: 
- Given the expression `/.*?[0-9]+/` and the string `Page 266`
    - The `*?` indicates that the use of the wildcard will be "lazy." 
    - The `*` metacharacter means "the preceding value, zero or more times," which means that it doesn't even have to match with the P. At each step, the lazy expression is essentially asking "can I give up yet?" 
    - The `.*?` segment has to match at least `Page `, because the `[0-9+]` can't match anything until it reaches the 2. The second segment, which is *not* lazy, matches `266`, resulting in a full match. 
    - Making the second segment lazy (`[0-9]+?`) would still result in a full match, but only `Page 2` would match. 
- Given the expression `/\d+?\w+?\d+?/` and the string `01_FY_07_report_99.xls`
    - Because the `+` repeition modifier is used, each segment of the expression must appear at least once, but the repeition modifier is lazy for all 3 of them. 
    - The first segment (`\d+?`) will match the first 0 and stop, because it knows that the `\w+?` segment can take care of the next character. 
    - The second segment (`\w+?`) matches `1_FY_` because it knows that the final segment can take care of the rest. 
    - The final segment (`\d+?`) matches the 0 and stops. 
    - The full match is `01_FY_0`. 
- Given the expression `/".+", ".+"/` and the string `"Milton","Waddams", "Initech, Inc." `
    - The first segment (`".+?",`) defers to the first comma it encounters and gives up. 
    - The second segment (`".+?"`) picks up and stops as soon as it encounters a second set of quotation marks. 
    - The full match is `"Milton", "Waddams"`

### Challenge Problems and Solutions 
1. Match: self, himself, herself, itself, myself, yourself, thyself. It can match more than that, but it has to be able to pick up those words. 
    - My solution: `/\w*self/`
2. Match both "virtue" and "virtues"
    - My solution: `/virtues?/`
3. Use quantified repeition to find the word that starts with "T" and has 12 letters. 
    - My solution: `/T\w{11}/`
4. Match all text inside quotation marks, but nothing that is not inside them. 
    - My solution `/".+?"/`
    - This actually doesn't work fully. There's a block of text that contains line breaks in between the two quotes, and the `.` metacharacter doesn't work as a line break. There is no ideal solution for this based on what the course has covered so far, but future concepts will reveal a way to make this easier. 


## 5 - Grouping & Alternation

### Grouping Metacharacters
The open and close parentheses (`(` and `)`) are **grouping** metacharacters. Anything inside a set of parentheses will be considered a "grouped expression." These sorts of expressions can be used with repetition operators and alternation expressions. Grouping also allows segments of the expression to be captured and used in find and replace tools.  

Examples: 
- `/(abc)+/` matches "abc" and "abcabcabc"
- `/(in)?dependent/` matches "independent" and "dependent"
- `/run(s)?/` is the same as `/runs?/`

The "find and replace" aspect of grouping is a bit different from the concepts learned so far. F&R is not about finding matches. Rather, it's a feature for working with the data once it's been matched, which can be done in web applications like Regexr and text editor applications. 

Find and Replace Examples: 
- Given the expression `/\d{3}-\d{3}-\d{4}/` And the value "555-666-7890" 
    - The expression matches the phone number. But what if it was necessary to change the format of the phone number? Using grouping metacharacters, the expression can be split up into chucks that will work with a f&r tool without changing the expression's meaning. In this case, the area code will be the first group, and the rest of the phone number (excluding the hyphen after the area code) will be the second: `/(\d{3})-(\d{3}-\d{4})/`
    - A text editor or web application that supports f&r with regular expressions will automatically store the grous in numbered variables. For example, `$1` will refer to the first group of the expression (`\d{3}`), and `$2` will refer to the second group (`\d{3}-\d{4}`). In the "replace" section of the f&r tool, the variables can be used with literal characters to define a new format: `($1) $2`
    - The result will be the same phone number formatted as "(555) 666-7890". 

> Note: Some regex engines/f&r tools use a backslash (`\`) instead of a dollar sign (`$`) for group references.  

### Alternation Metacharacter 
The alternation metacharacter (`|`) matches the expression either before or after it, making it essentially an "OR" operator within regular expressions. When using alternation, the leftmost expression gets precedence. The other expression is not evaluated at all if the leftmost expression is a match. Multiple choices can be daisy-chained, and groups can be used to keep alternation expressions distinct. 

Examples: 
- `/apple|orange/` will match "apple" and "orange" 
- `/abc|def|ghi|jkl/` will match "abc", "def", "ghi", and "jkl"
- `/apple(juice|sauce)/` is not the same as `/applejuice|sauce/`
- `/w(ei|ie)rd/` matches "weird" and "wierd", so it's a great way to spot common misspellings. 
- `/AA|BB|CC){4}/` matches "AABBAACC" and "CCCCBBBB". The first matched alternation doesn't affect other matches when using repetition together with alternation. 

> **Big Note!**
>
> Remember that the regex engine is eager to return a match. While this is usually a good thing, it can complicate things if expressions are inefficient or don't take into account certain nuances. 
>
> For example, given the expression `/(peanut|peanutbutter)/` and the text "peanutbutter", only the "peanut" portion of the text will match. Even though the expression on the right side of the alternation metacharacter is a better or more complete match, the engine does not evaluate that expression if there has already been a match, which, in this case, there has. 
>
> A better way to write this expression would probably be `/peanut(butter)?/`. Note that, though the `(butter)` is optional, the `?` operator is greedy by default and will match the entire thing. Making the expression lazy (`/peanut(butter)??/`) would result in a match with only "peanut". 
>
> This is one small example of the nuances to consider even for simple expressions and the importance of creating thoughtful and efficient expressions. 

### Challenge Problems and Solutions 
1. Match "myself","yourself","thyself", but not "himself","herself","itself"
    - My solution: `/(my|your|thy)self/`
2. Match "good", "goodness", and "goods" without typing "good" more than once 
    - My solution: `/good(s|ness)?/`
3. Match all occurrences of either "Do" or "does" followed by "no", "not", or "nothing", even when it occurs at the start of a sentence. 
    - My solution: `/(do(es)?) no(thing|t)?/gi` Because of the "eager" nature of the regex engine, it's important to not put the "t" on the left side of the `\`, which will result in "nothing" never being matched. 
    - Alternative solution: `/[Dd]o(es)? no(t(hing)?)?/g` This one avoids using alternation at all, taking advantage of the greedy repetition operator to make sure that the regex engine grabs "hing" if it's there instead of just giving up after the t. 
    - Another option: `/[Dd]o(es)? (nothing|not|no)/`  It's not as fancy, but it's much easier to read, though it still ahs a problem with "eagerness" if the words aren't ordered properly. 

## 6 - Anchors
There are 4 metacharacters (or character combinations) that are used for anchoring: 
- `^` - Start of a string/line 
- `$` - End of a string/line
- `\A` - Start of string, never end of line 
- `\Z` - End of string, never end of line 

Start and end anchors reference a position, not an actual character. They're sometimes referred to as being "zero-width." 

Examples: 
- `/^apple/` will only match the word "apple" if it is at the very beginning of the string. If it's anywhere else, there will not be a match. `/\Aapple/` does essentially the same thing. 
- `/apple$/` or `/apple\Z/` will only match if "apple" appears at the end of the string. 
- `/^apple$/` and `/\Aapple\Z/` are both valid and basically require that "apple" be the entirety of the string. Note that a string that begins and ends with "apple" but has multiple words *would not match.*  
- `^` and `$` are standard and recognized by all regex engines. `\A` and `\Z` are a little newer and not compatible with JavaScript. 

> Note: when using regexr, the default engine is JavaScript, which will cause problems when trying to use the `\A` and `\Z` anchors. To enable them, click the engine dropdown and select "PCRE (Server)", which means Perl Compatible Regular Expression, which is what a lot of programming languages use besides JavaScript. 

Anchors can be especially helpful in validating data. For example: 
- If tasked with writing an expression that would validate an email address, one solution might be: 
```
/\w+@\w+\.[a-z]{3}\g/
```

This would match an email address like "someone@nowhere.com", and it would be correct. However, what if the full string was actually "someone@nowhere.com-junk"? The expression would still match and therefore return a successful validation message. By using anchors to define the entire range of the string (by adding `^` at the beginning and `$` at the end), the string with the "-junk" at the end no longer matches at all, which will correctly return a validation failure. 

### Line Breaks and Multiline Mode
The two sets of anchor metacharacters handle line breaks slightly differently. Specifically, they differ in how they function when in multiline mode. By default, expressions are evaluated in single-line mode. In this mode, none of the 4 anchor metacharacters (`^`, `$`, `\A`, `\Z`) evaluate anything after a line break. 

For example, given the expression `/[a-z ]+/` and the following text: 

```
milk
apple juice
sweet peas
yogurt
sweet corn
```

Each line will be its own, complete match, since all the characters on each line are letters and spaces. Since line breaks are not included, there are 5 total matches. 

Putting an anchor at the beginning of the expression (`/^[a-z ]+/`) will result in a single match, "milk", since the `^` operator does not match at line breaks in single-line mode. 

Multiline mode can be enabled by simply adding an `m` flag after an expression (in most cases). In this mode, the `^` and `$` metacharacters will will match at the start and end of lines. `\A` and `\Z`, however, will continue to behave the same as they do in single-line mode. 

> **Remember:** There are different ways of enabling multiline mode depending on the language: 
>
> ```
> Perl: /^regex$/m
> Ruby: /^regex$/m
> PHP: /^regex$/m
> JavaScript: /^regex$/m
> Java: Pattern.compile("^regex$",Pattern.MULTILINE)
> .NET: Regex.Match("string", "^regex$", RegexOptions.Multiline)
> Python: re.search("^regex$", "string", re.MULTILINE)
> ```
> Make sure to invoke the proper function when using certain language to ensure that multimode is enabled.

With multiline mode enabled, the expression (which includes the `^` anchor) matches the way that it should, with the full text of each line serving as an individual match. Multiline mode enables anchors to work the way they're supposed to on content with linebreaks. 

### Word Boundaries 
A word boundary anchor is used to anchor expressions to word boundaries (i.e. the start or end of a word). There are two word boundary metacharacters: 
- `\b` refers to a word boundary (the start or end of a word) 
- `\B` refers to anything that is NOT a word boundary. 

Like other anchors, word boundaries reference a position, not an actual character. A word boundary exists in multiple locations: 
- Before the first word character in the string
- After the last word character in the string 
- Between a word character and a non-word character

Remember, word characters are all uppercase letters, all numbers, and the underscore character. Simply put, a word boundary exists anywhere between any word character and any non-word character, including at the beginning and and of the first and last word character in the string. 

Examples: 
- `/\b\w+\b/` finds 4 matches in "This is a test." 
    - One match is "This" because there is one `\b` before the "T" and one `\b` after the "s"
    - One match is "is" 
    - One match is "a" 
    - One match is "test", not including the period. 
- The same expression would match all of "abc_123" but only part of "top-notch" because a hyphen is not included in the range for `\w`. 
- The expression `/\bNew\bYork\b/` does not match "New York" because there's no accounting for the space. A space is not a word character, so there would be a boundary between the end of "New" and the space as well as another boundary between the space and "York". The proper match would be `/\bNew\b \bYork\b/`
- `/\B\w+\B/` finds two matches in "This is a test.": "hi" and "es" because there are no word breaks on either side of all the characters in each match. 

Big Example: 

Given the following text: 

```
Shall I compare thee to a summer's day? 
Thou are more lovely and more temperate:
Rough winds do shake the darling buds of May,
And summer's lease hath all too short a date.
```

To find all the words that end in "e", a basic expression might be something like `/e /g`. However, at the end of the second line, "temperate" is followed by a ":". A better expression would be `/e\b/`, which will find any "e" that is followed by a word boundary, which includes any punctuation. 

The expression `/\ba\b/` is a much more effective way of finding all instances of "a" being used as a word than trying to specify spaces or punctuation to account for matches at the beginning or end of a sentence. 

Word boundaries can improve the efficiency of expressions, especially those looking for a specific structure of a word. Specifying a word boundary in an expression can prevent the regex engine from iterating through each letter in a word unnecessarily, saving time and resources. 

### Challenge Problems and Solutions
1. How many paragraphs start with "I", as in "I read". 
    - My solution: 4, `/^I\b/gm`
2. How many paragraphs end with a question mark? 
    - My solution: 1, `/\?$/`
3. Match all words with exactly 15 letters, including hyphenated words. 
    - My solution: 3 (classifications, million-colored, and thousand-cloven), `/\b[\w\-]{15}\b/gim`

## 7 - Capturing Groups and Backreferences
Grouped expressions (the parts of an expression within a group defined by parentheses [`(` and `)`]) are **captured** by default, and the **data** that matches the grouped part of the expression is stored for later use. Once captured, the data can be used in backreferences. 

Example: 
- `/a(ppl)e/` matches "apple" and captures "ppl". It does NOT capture/store the expression `(ppl)`. Rather, it captures/stores the literal text "ppl"
- `/a(ppl/ngl)e/` matches "angle" and captures "ngl". If the expression matched "apple", it would capture "ppl" 

The backreference metacharacter is simply a backslash followed by a number corresponding to the group. For example, `\1` would be a backreference to the first capture in the expression, `\2` would be a backreference to the second capture, and so on. Most regex engines support `\1` through `\9`. Some engines support `\10` through `\99` but it's not recommended to use these, since they're not always supported, and different engines handle double-digit numbers differently. Some engines also use a different backreference syntax: `$1` through `$9` instead of `\1` through `\9`. 

Backreferences can be used inside the same expression or after the match when using a text editor or other find & replace tool. 

Examples: 
- `/(apples) to \1/` matches "apples to apples" 
- `/(ab):(cd):(ef):\3:\2:\1/` matches "ab:cd:ef:ef:cd:ab"
- `/<(i|em)>.+?<\/\1>/` matches `<i>regex</i>` or `<em>regex</em>` which is a great way to dig through HTML code. Since the backreference stores the actual value of the group that's matched, it will be able to look for the appropriate closing tag. 
- Given the following text: 

    ```
    Paris in the 
    the spring.
    ```
    There's a duplicate "the" that is easily missed by human error. However, an expression can be used to find duplicate words, even intermixed with line breaks: 

    ```
    /\b(\w+)\b\s+\1/gm
    ```

    The `/\b(\w+)\b\s+/` finds all the words (flanked by word boundaries) and the spaces (including line breaks) after them. The `\1` ensures that any word captured by the expression will not be repeated. 

### Backreferences to Optional Expressions
When using the optional reptition metacharacter (`?`), a backreference will store a "zero-width match," or an empty string, if the group doesn't match anything. 

Examples: 
- `/(A?)B/` matches "AB" and captures "A"
- `/(A?)B/` matches "B" and captures "" 
- `/(a?)typical/` matches "typical" and captures "" 

A backreference to a zero-width capture is still zero-width. 

Examples: 
- `/(a?)typical & \1political/` matches "atypical & apolitical" 
- `/(a?)typical & \1political/` matches "typical & political" 

### Capturing Optional Groups 
An optional group is only captured if it matches. There's a big difference between putting the optional metacharacter (`?`) on the inside of the group or the outside of the group. An optional group that did not match has no backreference (except in JavaScript, where the regex engine captures optional groups).

Examples: 
- `/(A)?B/` matches "AB" and captures "A" 
- `/(A)?B/` mathces "B" and captures nothing 
- `/(un)?willing/` matches "willing" but captures nothing
    - `/(un)?willing & \1able/` matches "unwilling & unable" but does NOT match "willing & able" (unless in JavaScript, in which case
- When it's important that *something* is captured (in an engine other than JavaScript), a solution is to capture the optional group: 
    - `/((un)?)willing & \1able/` matches both "unwilling & unable" AND "willing & able"
    - `/(un)?/` matches, captured by inner parentheses, assigned to `\1`
    - `/(un)?/` does not match, captured by outer parentheses, assigned to `\1`

> Note: The easy way to think about this is that when the question mark is outside the parentheses, it means that both the group AND the automatic capture that go with that group are optional. 

### Find and Replace (F&R) Using Backreferences 
Some regex engines and code editors allow backreferences to be captured and referenced after, which is handly for find and replace. 

Examples: 
- Given the string "I love hot coffee.", the expression like `/(love) hot/` will store "love" in `\1`. Then, the "replace" tool can be used with the backreference to reformat the string. 
- Given a list of names (including first and last), an expression can be written to recognize the names, store the pieces of the name in backreference, and then reformat them so we can, for example, make the last name first. 
    - `/^(.+) (.+)$/` will split the string into first and last names, stored in `\1` and `\2`, respectively. 
    - In the "replace" box, the string can simply be written as `\2, \1`, which will reorder the first and last names and add a comma between them. 

> Tip: When using groups and backreferences with find & replace, the expression should be written first, making sure that it matches the text that it's supposed to match. Once that's done, the capturing groups should be added, followed by the replacement strings with backreferences. 

Another Example: 
- When nesting groups, the associated backreferences can get complicated. 
- Given the expression: `/((self-)?reliance)/gm` and using PCRE mode instead of JavaScript and the following text: 
    ```
    self-reliance
    reliance
    ```
- "self-reliance" will match. Group #1 will contain "self-reliance" and group #2 will contain "self-" 
- "reliance" will also match. Group #1 will contain "reliance" but there will be no group #2 because the `(self-)?` segment of the expression doesn't match anything and is therefore not captured at all. In JavaScript, the capture would be "undefined". 

### Non-Capturing Group Expressions 
Groups are captured by default, but it's possible to prevent automatic capture. This is handy in situations where grouping is needed to make the expression syntactically correct but the capture definitely won't be used. This frees up storage for other captures and can improve the speed and efficiency of larger expressions. This feature is supported by most engines, but not in Unix. 

A group can be configured to disable capturing by putting a `?:` right at the beginning of the group. 

Example:
- For the string "I like pizza." `/I (love|like) (.+)\./` captures "like" and "pizza". 
    - Changing the first group to `(?:love|like)` will disable capturing for that group, resulting in only "pizza" being captured. 

### Challenge Problems and Solutions 
1. Use captures, backreferences, and find-and-replace to create a new U.S. Presidents list in the format "start-end: full name" 
    - My solution: `^(?:\d{1,2},)(.+),([\d]+),([\d]+)?,(?:\b.+\b)`
    - Breakdown: 
        - `^(?:\d{1,2},)` anchors the expression to the beginning of the line (in multiline mode) and starts the match with any line that starts with 1 or 2 digits and is followed by a comma. This group is not captured because it's not needed. 
        - `(.+),` matches the presidents' names. The `+` is greedy, so it takes as much as it can, but because the dates are defined in the expression, it defers to the overall match and stops short of matching the entire string. 
        - `([\d]+),([\d]+)?,` captures the start and end dates in their own groups/backreferences. Because the current President doesn't have an end date, the second group in this segment is optional. The second date could also be expressed/captured as `(\d{0,4})`
        - `(?:\b.+\b)` captures the remainder of the string but prevents capturing since the data won't be used. 
        - With this structure, the newly-formatted list can be written as `$2-$3, $1`
    - The solution in the course: `/^\d+,(.+),(\d{4}),(\d{0,4}),.+,.+,https:.+$/gm`

## 8 - Lookaround Assertions 
There are two types of lookaround assertions and 2 subtypes for each. The two types are "lookahead" and "lookbehind." The subtypes for each are "positive" and "negative." 

### Positive Lookahead Assertions 
A positive lookahead assertion defines an expression that returns true if a group expression is ahead of the current position. It tells the regex engine to pause and check the content further down the line before it proceeds. It can also be thought of as an additional condition that must be met. If the lookahead assertion fails, the whole match fails. If it succeeds, the regex engine continues. 

Assertions are different from other experssions in that they're not included in the match and they're never captured in groups. They only return "true" and "false", and they're supported by most regex engines, but not Unix tools. 

To define a positive lookahead assertion, put a `?=` ahead of the expression in the group. 

Examples: 
- The expression `/sea/` will match "sea" in "seashore" and "seaside" 
    - The expression `/(?=seashore)sea/` matches "sea" in "seashore" but not "seaside" 
        - Notice that only "sea" would be matched, not "seashore". The purpose of "seashore" is to check if the full term "seashore" exists in the string, NOT to match it. The matching is done by the rest of the expression that is outside the lookaround assertion. 
        - Lookaround assertions do not change the engine's position. 
        - Lookahead assertions examine the same characters as the expression. 
- `/\d{4}/` matches "2025" in "2025-01-01" and "01-01-2025" 
    - `/(?=\d{4}-\d{2}-\d{2})\d{4}/` matches "2025" in "2025-01-01" but does NOT match it in "01-01-2025". 
    - Does not match "01-01-2025", "2025-1-1" or "2025" because the string does not match the format in the positive lookahead assertion. 
    - In this example, the assertion is being used to check the format of the string before it bothers looking for, matching, and possibly capturing actual data. 
    - The assertion can go later in the expression: 
    
        Given the text "2025-01-01", the expression could be `\d{4}(?=-\d{2}-\d{2})-\d{2}-\d{2}/`, which will match the full date. 

        However, if the format of the string is broken (by, for example, taking one of the digits off the month), the string will no longer match the format defined by the positive lookahead assertion, and the entire expression will fail to find any match, even with the matching part of the string that appears before the assertion. 
- What about an expression that finds all words that are followed by some punctuation but DOES NOT INCLUDE the punctuation itself? 
    - Such an expression might be: `/\b[A-Za-z']+\b(?=[,;:.?!])/gm`
        - The segment before the lookahead assertion simply finds any word that includes a combination of capital letters, lowercase letters, and apostraphes, flanked on both sides by word boundaries. 
        - The assertion itself simply looks for any punctuation that immediately follows the word boundary. If it finds one of the puncutation marks after the word, it matches, but the punctuation, which was just part of the assertion logic, is not included in the match. 
- Lookaround assertions can be combined with backreferences. In the expression `/(\b\w+\b)(?=.*\1)/`, the backreference contains any word and then checks to see if it's repeated in the string. If it is, that word becomes a match. If it is NOT repeated, it fails the check in the assertion and no match can occur. 

### Negative Lookahead Assertions 
A negative lookahead assertion evaluates to "true" if a grouped expression is **not** ahead of the current position. It will reject an overall match if the assertion matches. Just like with positive lookahead assertions, the group is not included in the match, nor is it captured. 

To define a negative lookahead assertion, put a `?!` ahead of the expression in the group. 

> Note: These are NOT merely the opposite of positive lookahead assertions. They allow *rejecting* expressions, not matching them. By contrast, the negative metacharacter (`^`) is used in character sets, but they only reject a single character.

Examples: 
- `/(?!seashore)sea/` mathes "sea" in "seaside" but not "seashore". 
- `/\b(?!re)\w+\b/` matches words that do NOT start with "re" 
- `/\b\w+(?!er)\b/` matches words NOT ending in "er". 
- For the text "The green frog chased the green bug in the green grass." a negative lookahead assertion can be used to reject "green" when it's followed by "frog." 
    - The expression: `/\bgreen\b(?! frog)/gm`
    - The other instances of "green" will still be matched, since they aren't followed by "frog." 
    - Using the same string, a backreference can be used to find the last occurrence of the word "green" in the string: `/(\bgreen\b)(?!.*\1)/`
        - Here, the word "green" is captured in a backreference: `\1`
        - The assertion checks to see whether green appears again in the string. If it does, this assertion, which is negative, fails, resulting in no match. 
        - If the assertion finds another instance of green, looks ahead to find another instance, and fails to do so, it matches. 
        - The end result is the final instance of "green" matching because "green" does not occur again in the sentence. 
- A useful example of negative lookahead assertions allows code to be examined for comment characters (`#` or `//` or something else depending on the programming language)
    - The expression might be something like: `/^(?!\s*#).+$/`
    - This expression starts and ends with anchors. 
    - The negative assertion looks for any and all whitespace (expressed by `\s`) that is followed by the comment indicator, which, in this example, is `#`. 
    - If the line starts with the whitespace and comment indicator, the assertion is false, and the line does not match. 

### Lookbehind Assertions 
A lookbehind assertion evaluates to true if the grouped expression is (for positive assertions) or is not (for negative assertions) behind the current position. Like with lookahead assertions, the lookbehind assertion groups are not included in the match, nor are they captured in backreferences. 

> Note: Lookbehind assertions are not as well supported as lookahead assertions. JavaScript support is still being added and may vary by browser. 

Positive lookbehind assertions use the same metacharacters as the lookahead assertionss except that a `<` is inserted after the `?` to indicate that the assertion is looking backward. 
- `?<=` is for a positive lookbehind assertion 
- `?<!` is for a negative lookbehind assertion 

Examples: 
- `/(?<=base)ball/` matches "ball" in "baseball" but not "football" 
- `/(?<!base)ball/` matches "ball" in football" but not "baseball" 
- `/(?<=\bfor\s)\b\w+/` matches the first word after "for" 
- `/\b\w+(?<!er)\b/` matches words not ending in "er" 

> Note: Most regex engines do not allow variable widths for lookbehind assertions
> 
> For example, given the following text: 
> ```
> John Smith
> Mr. Smith
> Ms. Smith
> Mrs. Smith
> Mr. John Smith
> ```
> If the goal is to match any instance of "Smith" that's preceded by "Mr.", "Ms.", or "Mrs.", the expression might be: `/(?<=(Mr|Ms|Mrs)\. )Smith/gm`
> 
> However, this throws an error, because in most regex engines, lookbehind assertions are not compatible with variable-width expressions. In this example, "Mrs" causes the error, since it's a different width (length) than the first two options. 
> 
> If the goal was to match "Mr. John Smith", the expression might be `/(?<=(Mr|Ms)\. [\w.]*)Smith/gm`, but this would also throw an error because `[\w.]*` is not a fixed width. 
> 
> Given these limitations, as a general rule, lookahead assertions can be complex, but lookbehind assertions should be simple. 

### Using Multiple Lookaround Assertions 
Multiple lookaround assertions can be used in a single expression. 

Examples: 
- `/\b(?=\w{6,})sea(?!shore)\w+\b/`
    - This expression checks to see whether a word with a minimum of six characters appears later in the string and matches any word starting with "sea" as long as it's not followed by "shore" (or "shores"). 
- Given the expression: `/^(?=(\b\w+ ){2,})(?!.+\s[a-z]).+$/`
    - Without the assertions, the expression is simply `/^.+$/`, which includes everything on the line. 
    - `^(?=(\b\w+ ){2,})` looks for at least 2 instances of a word of variable length preceded by a word boundary and followed by a space. 
    - `(?!.+\s[a-z])` looks for any instance of a character being followed by a space and then a lowercase letter. Since the assertion is negative, finding a match will cause the assertion to return "false" and fail to find a match.
    - This expression will match "Cool Hand Luke" but not "Forrest Gump" because it's only 2 words or "Chariots of Fire" because "of" starts with a lowercase "o".  
- The expression `/(?<=["']).+(?=["'])/` will match characters appearing inside quotes. 
- The expression `/(?<=[a-z])(?=[A-Z])/` will match the zero-width position before a camel-case letter in "QuickTime" (useful for find-replace)
- Assertions can be useful for validating data like passwords. 
    - Assume that the password must meet the following requirements: 
        - 10+ characters long 
        - Must include: 
            - an uppercase letter
            - a lowercase letter 
            - a number
            - a symbol
    - Example expression: `/\A(?=.*[A-Z])(?=.*[a-z])(?=.*\d)(?=.*[!@#$%^&*]).{10,}\Z/`
        - Remember that the `*` metacharacter means "zero or more times." This means that the `.` wildcard metacharacter can appear any number of times or not at all, meaning that the expression that follows (`[A-Z]`, `[a-z]`, `\d`, or `[!@#$%^&*]`) can be anywhere, including at the beginning. 
- The expression `/^(?=.*\bgive\b)(?=.*\btake\b).+$/` will look for the words "give" and "take" in the string. They can appear in any order. 
- The expression `/(\d{1,3})(?=\d{3})+(?!\d))/` can help appropriately insert commas into large numbers. 
    - `(\d{1,3})` matches 1-3 digits 
    - `(?=\d{3})+(?!\d))` is a double assertion that checks to make sure that there are at least 3 numbers after the initial match (or a multiple of 3). If not, then there's no match. 
    - Using a find and replace tool with backreferences, this expression can be used to convert "1234567.89" to "1,234,567.89". 

Remember that having multiple assertions can impact performance, and it creates multiple layers of regular expressions that the engine has to check. Using anchors, especially at the start of the expression, can reduce searching and improve efficiency. Always put the simplest and fastest assertions first. 

### Challenge Problems and Solutions
1. Match the line for every U.S. President. This will form the basis for the remainder of the challenge's expressions. You should get 46. 
    - My solution: `/^\d{1,2},(\w+) (\w\. )*((?:\w+(?: )?)+),\d{4},\d{0,4},[\w\- \/]+,[\w+ ]+,https:\/\/.+$/gim`
2. Write an expression to match presidents whose home state was NOT Virginia or Massachusettes. You should get 37. 
    - My solution: `/^\d{1,2},(\w+) (\w\. )*((?:\w+(?: )?)+),\d{4},\d{0,4},[\w\- \/]+,(?!Virginia|Massachusetts)[\w+ ]+,https:\/\/.+$/gim`
3. Write an expression to match presidents whose last name is longer than 7 characters. You should get 15. 
    - My solution: `/^\d{1,2},(\w+) (\w\. )*((?:\w+(?: )?)+){8,},\d{4},\d{0,4},[\w\- \/]+,[\w+ ]+,https:\/\/.+$/gim`
4. Write an expression to match presidents whose name does not include a middle initial. You should get 29. 
    - My solution: `/^\d{1,2},(\w+) ((?:\w+(?: )?)+),\d{4},\d{0,4},[\w\- \/]+,[\w+ ]+,https:\/\/.+$/gim`
5. Write an expression to match presidents whose term in office began on or after 1900. You should get 21. 
    - My solution: `/^\d{1,2},(\w+) (\w\. )*((?:\w+(?: )?)+),(?=19|20)\d{2}\d{2},\d{0,4},[\w\- \/]+,[\w+ ]+,https:\/\/.+$/gim`
6. Finally, combine all of these into 1 large expression. There is only 1 president who meets all these requirements. 
    - My solution: `/^\d{1,2},(\w+) ((?:\w+(?: )?)+){8,},(?=19|20)\d{2}\d{2},\d{0,4},[\w\- \/]+,(?!Virginia|Massachusetts)[\w+ ]+,https:\/\/.+$/`
    - The answer is Theodore Roosevelt. 