# RegEx Tutorial

RegEx (Regular Expressions) is a series of characters that define a search pattern, usually used to search through a string. They can be used to find patterns of characters within a string, or to replaces characters or sequences of characters within a string, etc.

## Summary

This document will first lay out the "methods" available in regulaer expressions; then, an example of a regular expression will be provided: /^#?([a-f0-9]{6}|[a-f0-9]{3})$/
This expression is used to match a hex value of a character. The expression will be deconstructed and explained, elaborating on what each part of the expression is doing.

## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [OR Operator](#or-operator)
- [Character Classes](#character-classes)
- [Flags](#flags)
- [Grouping and Capturing](#grouping-and-capturing)
- [Bracket Expressions](#bracket-expressions)
- [Greedy and Lazy Match](#greedy-and-lazy-match)
- [Boundaries](#boundaries)
- [Back-references](#back-references)
- [Look-ahead and Look-behind](#look-ahead-and-look-behind)
- [Example and Explanation](#example-and-explanation)

## Regex Components

### Anchors

In regular expressions, anchors are special characters that allow you to match a pattern only at specific positions in a string. There are two main types of anchors:

Start of line anchor: The caret (^) character matches the beginning of a line. For example, the regular expression "^Hello" would match the word "Hello" only if it appears at the beginning of a line.

End of line anchor: The dollar sign ($) character matches the end of a line. For example, the regular expression "world$" would match the word "world" only if it appears at the end of a line.

These anchors can be used in combination with other regular expression patterns to create more specific matches. For example, the regular expression "^Hello.\*world$" would match any line that starts with the word "Hello" and ends with the word "world", with any characters in between.

In addition to these line anchors, there are also word anchors that match the beginning and end of a word, respectively:

Start of word anchor: The "\b" character (backslash followed by the letter b) matches the beginning of a word. For example, the regular expression "\bHello" would match the word "Hello" only if it appears at the beginning of a word.

End of word anchor: The "\b" character (backslash followed by the letter b) matches the end of a word. For example, the regular expression "world\b" would match the word "world" only if it appears at the end of a word.

These anchors can also be used in combination with other regular expression patterns to create more specific matches. For example, the regular expression "\bHello.\*world\b" would match any word that starts with the word "Hello" and ends with the word "world", with any characters in between.

### Quantifiers

In regular expressions, quantifiers are special characters that allow you to specify how many times a character or group of characters should be matched. There are several types of quantifiers:

The asterisk () quantifier matches zero or more occurrences of the preceding character or group. For example, the regular expression "abc" would match "ac", "abc", "abbc", "abbbc", and so on.

The plus sign (+) quantifier matches one or more occurrences of the preceding character or group. For example, the regular expression "ab+c" would match "abc", "abbc", "abbbc", and so on, but not "ac".

The question mark (?) quantifier matches zero or one occurrence of the preceding character or group. For example, the regular expression "ab?c" would match "ac" and "abc", but not "abbc" or "abbbc".

Curly braces ({}) can be used to specify a specific number of occurrences of the preceding character or group. For example, the regular expression "a{3}" would match "aaa", but not "aa" or "aaaa".

Curly braces ({}) can also be used to specify a range of occurrences of the preceding character or group. For example, the regular expression "a{2,4}" would match "aa", "aaa", and "aaaa", but not "a" or "aaaaa".

The question mark followed by a curly brace ({}) (?,{}) is used for lazy quantification, which tries to match the minimum number of occurrences possible. For example, the regular expression "a+?" would match only "a", whereas "a+" would match all "a" characters in the string.

Quantifiers can be used in combination with other regular expression patterns to create more specific matches. For example, the regular expression "a{2,4}[bc]+" would match any string that contains "a" repeated 2-4 times followed by one or more occurrences of "b" or "c".

### OR Operator

In regular expressions, the OR operator allows you to match either one pattern or another pattern. The OR operator is represented by the pipe character (|).

For example, the regular expression "cat|dog" would match either "cat" or "dog". So if the input string is "I love my cat and my dog", the regular expression would match "cat" and "dog".

You can use parentheses to group patterns together when using the OR operator. For example, the regular expression "apple(s|es)?" would match "apple", "apples", or "apples" (the ? quantifier makes the "s" optional).

You can also use the OR operator with other regular expression constructs, such as character classes and quantifiers. For example, the regular expression "(red|blue|green) car(s)?" would match "red car", "blue cars", "green car", or "green cars".

Note that when using the OR operator, the regular expression engine will attempt to match the leftmost pattern first. So if the input string is "catdog", the regular expression "cat|dog" would match "cat", not "dog", because "cat" is the leftmost pattern that matches.

### Character Classes

In regular expressions, character classes allow you to match a set of characters in a single position in the input string. There are several predefined character classes, as well as the ability to create custom character classes.

Predefined character classes:
\d: Matches any digit character (equivalent to [0-9]).
\D: Matches any non-digit character (equivalent to [^0-9]).
\w: Matches any word character (equivalent to [a-zA-Z0-9_]).
\W: Matches any non-word character (equivalent to [^a-za-z0-9_]).
\s: Matches any whitespace character (equivalent to [\t\n\f\r ]).
\S: Matches any non-whitespace character (equivalent to [^\t\n\f\r ]).
Custom character classes:
[abc]: Matches any of the characters "a", "b", or "c".
[a-z]: Matches any lowercase letter between "a" and "z".
[A-Z]: Matches any uppercase letter between "A" and "Z".
[0-9]: Matches any digit between "0" and "9".
[a-zA-Z]: Matches any letter between "a" and "z" or between "A" and "Z".
[a-fA-F0-9]: Matches any hexadecimal digit between "0" and "9" or between "a" and "f" or between "A" and "F".
You can also use quantifiers with character classes to match a specific number of characters. For example, the regular expression "\d{3}" would match any three-digit number.

Character classes can be combined with other regular expression constructs, such as anchors and the OR operator, to create more specific matches. For example, the regular expression "^[\w.-]+@[a-zA-Z]+.[a-zA-Z]{2,3}$" would match any email address that starts with one or more word characters, followed by an "@" symbol, followed by a domain name that consists of one or more letters, followed by a period and two or three letters.

### Flags

In regular expressions, flags modify the behavior of the pattern matching. The most common flags are:

Case-insensitive flag (i): This flag makes the regular expression match characters regardless of their case. For example, the regular expression "/hello/i" would match "hello", "HELLO", "HeLlO", and so on.

Global flag (g): This flag causes the regular expression to match all occurrences in the input string, not just the first one. For example, the regular expression "/\d+/g" would match all digits in the input string.

Multi-line flag (m): This flag changes the behavior of the "^" and "$" anchors so that they match the beginning and end of each line in a multi-line input string, not just the beginning and end of the entire string.

Unicode flag (u): This flag enables support for Unicode characters and properties in the regular expression.

Sticky flag (y): This flag causes the regular expression to match only at the current position in the input string, and to fail if the position is moved.

Flags are usually appended to the end of the regular expression, after the closing delimiter (e.g. "/pattern/flags"). You can also combine multiple flags by placing them together (e.g. "/pattern/igm").

Note that not all regular expression engines support all flags. You should consult the documentation for your specific programming language or tool to see which flags are available.

### Grouping and Capturing

In regular expressions, grouping and capturing allows you to group parts of a pattern together and extract the matched substrings for later use. This is done using parentheses "(" and ")".

Grouping:
Parentheses are used to group parts of a regular expression together. This is useful when you want to apply a quantifier to a group of characters or match a specific sequence of characters. For example, the regular expression "(apple)+\d+" matches one or more occurrences of "apple" followed by one or more digits.

Capturing:
Capturing allows you to extract the matched substrings and use them for further processing. This is done by defining a capture group using parentheses. When the regular expression matches, the contents of the capture group are stored in a numbered variable. The first capture group is numbered 1, the second is numbered 2, and so on. For example, the regular expression "(\d+)-(\w+)" would capture a string like "123-abc" as two groups: "123" and "abc".

Some regular expression engines also support named capture groups, where you can give a specific name to a capture group instead of using a number. For example, the regular expression "(?<year>\d{4})-(?<month>\d{2})-(?<day>\d{2})" would capture a date in the format "YYYY-MM-DD" as three named groups: "year", "month", and "day".

Capturing groups can be referenced in the regular expression itself or in the replacement string when doing a search-and-replace operation. For example, the regular expression "(\w+) (\w+)" can be used to capture the first and last names in a string, and the replacement string "$2, $1" would swap the order of the names and separate them with a comma.

It's important to note that capturing groups can impact the performance of the regular expression, especially if there are many nested groups. In some cases, it may be more efficient to use non-capturing groups (denoted by "(?: )") instead.

### Bracket Expressions

In regular expressions, bracket expressions allow you to specify a set of characters to match a single character. They are defined using square brackets "[" and "]" and can contain any combination of characters, character classes, or ranges.

Here are some examples of bracket expressions:

[abc]: Matches any single character that is either "a", "b", or "c".
[a-z]: Matches any single lowercase letter from "a" to "z".
[A-Z0-9]: Matches any single uppercase letter or digit.
The "^" character at the beginning of a bracket expression negates the set of characters, matching anything that is not in the set. For example, the bracket expression "[^a-z]" matches any single character that is not a lowercase letter.

Ranges can be specified using a hyphen "-" between two characters. For example, the bracket expression "[a-z]" matches any single lowercase letter from "a" to "z". It's important to note that the range includes both endpoints, so "[0-9]" matches any single digit from 0 to 9.

Character classes can also be used inside bracket expressions to match certain groups of characters, such as digits, whitespace, or word characters. For example, the bracket expression "\d" matches any single digit, and the bracket expression "\s" matches any whitespace character.

Bracket expressions can be combined with other regular expression features, such as quantifiers and alternation, to create more complex patterns. For example, the regular expression "(cat|dog)[0-9]{3}" matches strings like "cat123" and "dog456".

### Greedy and Lazy Match

In regular expressions, greedy and lazy matching refer to the way in which a quantifier matches text.

Greedy matching is the default behavior of most regular expression engines, and it means that the quantifier matches as much text as possible while still allowing the overall pattern to match. For example, the regular expression "a.\*b" applied to the string "abcdbefb" would match the entire string "abcdbefb", not just "abcdb".

Lazy matching, on the other hand, matches as little text as possible while still allowing the overall pattern to match. This is done by appending a "?" to the quantifier. For example, the regular expression "a.\*?b" applied to the string "abcdbefb" would match only "abcdb" because the "?" tells the regular expression engine to match as little text as possible between "a" and "b".

Here are some examples of greedy and lazy matching with different quantifiers:

"\*" (zero or more): The regular expression "a.b" matches as much text as possible between "a" and "b", while "a.?b" matches as little as possible.
"+" (one or more): The regular expression "a.+b" matches as much text as possible between "a" and "b", while "a.+?b" matches as little as possible.
"?" (zero or one): The regular expression "a.?b" matches either "ab" or "a" followed by "b", but "a.??b" matches only "ab".
It's important to note that greedy and lazy matching can have a significant impact on the performance of the regular expression, especially with large input strings or complex patterns. In some cases, it may be more efficient to use a more specific pattern that avoids the use of greedy or lazy matching altogether.

### Boundaries

In regular expressions, boundaries are special characters that match specific positions in the input string, rather than matching actual characters. These positions include the start and end of the string, as well as the boundaries between words and other types of characters.

Here are some common boundary characters used in regular expressions:

"^": Matches the beginning of the string. For example, the regular expression "^hello" matches any string that starts with "hello".
"$": Matches the end of the string. For example, the regular expression "world$" matches any string that ends with "world".
"\b": Matches a word boundary. This can be used to match the beginning or end of a word. For example, the regular expression "\bhello\b" matches the word "hello" but not "hellos" or "helloworld".
"\B": Matches a non-word boundary. This can be used to match positions within a word. For example, the regular expression "l\B" matches the "l" in "hello" but not the "l" in "hell".
"(?<=...)": Positive lookbehind assertion. Matches the position immediately following a specific sequence of characters. For example, the regular expression "(?<=abc)def" matches "def" only if it's preceded by "abc".
"(?<!...)": Negative lookbehind assertion. Matches the position not immediately following a specific sequence of characters. For example, the regular expression "(?<!abc)def" matches "def" only if it's not preceded by "abc".
"(?=...)": Positive lookahead assertion. Matches the position immediately before a specific sequence of characters. For example, the regular expression "abc(?=def)" matches "abc" only if it's followed by "def".
"(?!...)": Negative lookahead assertion. Matches the position not immediately before a specific sequence of characters. For example, the regular expression "abc(?!def)" matches "abc" only if it's not followed by "def".
Boundaries are useful for creating more specific regular expressions that match only certain positions or patterns in the input string. By using boundaries, you can avoid accidentally matching characters that are part of a larger word or sequence.

### Back-references

In regular expressions, back-references allow you to reuse a previously matched group within the same regular expression pattern. This can be useful when you need to match repeated patterns, such as multiple occurrences of the same word or character.

Back-references are created by using parentheses to group a portion of the regular expression pattern, and then referring to that group by its number in the pattern. For example, the regular expression pattern "(cat)\s+\1" matches the word "cat" followed by one or more spaces, followed by the same word "cat" again.

Here's how back-references work in more detail:

Use parentheses to create a capturing group. In the regular expression pattern, enclose the portion of the pattern you want to reuse in parentheses.
For example, to match repeated words separated by a comma, you might use the regular expression pattern "(\w+),\s\*\1".

Refer to the capturing group in the pattern. To reuse the captured text, refer to it in the pattern using a backslash followed by the group number. Group numbers start at 1 and increase with each additional group in the pattern.
For example, in the pattern "(\w+),\s\*\1", the back-reference to the first group is "\1".

Test the regular expression pattern. Use the regular expression with a matching function or tool to test whether it matches the input text. If the pattern matches, the back-reference will match the same text as the original capturing group.
Back-references can be very powerful when used correctly, but they can also be complex and difficult to debug. Be careful when using back-references in your regular expressions and always test your patterns thoroughly.

### Look-ahead and Look-behind

Look-ahead and look-behind are special types of regular expression constructs that allow you to match patterns based on what comes before or after a particular point in the input string, without actually including that text in the match.

Look-ahead and look-behind are called "zero-width assertions" because they don't actually match any characters themselves, but rather they check for the existence or non-existence of certain characters or patterns around the current position in the input string.

Here are the basic syntaxes for look-ahead and look-behind:

Positive look-ahead: (?=pattern)
This matches the current position in the string only if it is followed by a match for the pattern. For example, the pattern "foo(?=bar)" would match "foo" only if it is followed by "bar".

Negative look-ahead: (?!pattern)
This matches the current position in the string only if it is not followed by a match for the pattern. For example, the pattern "foo(?!bar)" would match "foo" only if it is not followed by "bar".

Positive look-behind: (?<=pattern)
This matches the current position in the string only if it is preceded by a match for the pattern. For example, the pattern "(?<=foo)bar" would match "bar" only if it is preceded by "foo".

Negative look-behind: (?<!pattern)
This matches the current position in the string only if it is not preceded by a match for the pattern. For example, the pattern "(?<!foo)bar" would match "bar" only if it is not preceded by "foo".

Here are a few examples of how you can use look-ahead and look-behind:

Matching email addresses: (?<=\s|^)[\w.-]+@[a-z0-9.-]+.[a-z]{2,}(?=\s|$)
This pattern matches any valid email address in the input string by using look-ahead and look-behind to ensure that the email address is not part of a larger word or sequence.

Matching numbers in parentheses:
(
?
=
\d

- )
  \d
- (?=\d+)\d+
  This pattern matches any number enclosed in parentheses by using a positive look-ahead assertion to check for the presence of at least one digit after the opening parenthesis, and then matching the digits inside the parentheses.

Look-ahead and look-behind are very powerful tools for creating complex regular expression patterns that match specific patterns in the input string. However, they can also be quite complex to use and debug, so it's important to test your patterns carefully and make sure that they are matching the correct parts of the input string.

### Example and Explanation

Example expression: /^#?([a-f0-9]{6}|[a-f0-9]{3})$/

This regular expression is used to match hexadecimal color codes in CSS, HTML, or other programming languages. Here's what each part of the expression does:

^ matches the start of the string.
#? matches an optional "#" character at the beginning of the string. This allows for both #FF0000 and FF0000 to be matched.
([a-f0-9]{6}|[a-f0-9]{3}) matches either a group of 6 hexadecimal digits or a group of 3 hexadecimal digits. The [a-f0-9] character class matches any hexadecimal digit (0-9 or A-F). The {6} and {3} quantifiers specify the exact length of the match.
$ matches the end of the string.
So, to summarize, this regular expression matches a string that starts with an optional "#" character, followed by either 6 or 3 hexadecimal digits, and nothing else. This ensures that only valid hexadecimal color codes are matched and nothing else.

## Author

Alan Hornbaker is a junior programmer and developer wanting to sharpen skills in general, specifically in regards to security and validation, etc. You can find his github profile at https://github.com/alanhornbaker.
