# Diving into Regex: Dates

Regular Expressions (or Regex) are sequences of characters that define a search parameter. These sequences are comprised of Literal and Meta Characters, and are wrapped in forward slashes ("/"). Literal Characters are exactly what they sound like - a one to one exact copy of what you're searching for. An example of this would be "L" when searching for the letter L. Meta Characters represent a set of Literal Characters, lack thereof, or position. An examples of this would be "\s\s" representing two white spaces. We use Regex to query more complex parameters efficiently. :muscle::muscle::muscle:

## Summary

Here we'll break down the components of Regex, taking a specific look at an example focusing on dates. The following Regex can find dates in the format DD/MM/YYYY or DD/MM/YY.

/^([1-2][0-9]|3[0-1]|0?[1-9])([-\.\/ ])(1[0-2]|0?[1-9])(\2)([\d]{4}|[\d]{2})$/

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

## Regex Components

### Anchors

The caret (^) and bling ($) symbols represent the start and end of Regex, and are referred to as Anchors. :anchor:

### Quantifiers

Quantifiers determine how exactly (or loosely) your regex matches the queried string. They usually include a minimum and maximum number of characters that your Regex is looking for. Here are some examples of quantifiers:

*—Matches the pattern zero or more times
+—Matches the pattern one or more times
?—Matches the pattern zero or one time
{ n }—Matches the pattern exactly n number of times
{ n, }—Matches the pattern at least n number of times
{ n, x }—Matches the pattern from a minimum of n number of times to a maximum of x number of times

Note that if you wanted to make the "?" literal (actually searching for "?" and not using "?" as a quantifier), you would need to Escape. Escape allows you to break the default quantifier and instead input literals. We notate Escapes using the backslash ("\"). 

Can you spot the Quantifiers in our Dates Regex? What do you suppose they're determining specifically? It's okay if you don't know yet, we'll break down the entire sequence under "Assembling the Pieces" once we round out the other Regex Components. :blush:

/^([1-2][0-9]|3[0-1]|0?[1-9])([-\.\/ ])(1[0-2]|0?[1-9])(\2)([\d]{4}|[\d]{2})$/

### OR Operator

The OR operator (|) specifies at least one match from a series. Here we have the first instance(s) of the OR Operator in our Dates Regex:

([1-2][0-9]|3[0-1]|0?[1-9])

### Character Classes

A Character Class defines a set of characters. To reference on of our examples in the introduction, "\s" is a common Character Class that matches whitespace. One interesting note is that capitalizing many Character Classes changes them to perform the opposite match. In our example "\S" matches non-white space. 

### Flags

Flags are located at the end of a Regex (outside of the /), and define additional functionality or limits for the Regex. Here are three common flags:

g—Global search: the regex should be tested against all possible matches in a string.
i—Case-insensitive search: case should be ignored while attempting a match in a string
m—Multi-line search: a multi-line input string should be treated as multiple lines

### Grouping and Capturing

In order to check that different parts of a string meet different requirements, we use Grouping Constructs. The primary way to group a section of Regex is by using parentheses (()). Each section within such a grouping is called a Sub-expression. Here we have the first two Sub-expressions within our Dates Regex:

([1-2][0-9]|3[0-1]|0?[1-9])([-\.\/ ]) 

### Bracket Expressions

Meta Characters inside of square brackets ([]) represent the range we're looking to match. These patterns are known as "Bracket Expressions" and contain what we call "Positive Character Groups," which outline the characters we want to include. Hyphens (-) are used between alphanumeric characters to represent a range of possibilities. Try and parse some of the Bracket Expressions in our Dates Regex. :detective:

/^([1-2][0-9]|3[0-1]|0?[1-9])([-\.\/ ])(1[0-2]|0?[1-9])(\2)([\d]{4}|[\d]{2})$/

### Greedy and Lazy Match

Greedy matches find as many occurrences of queried patterns as possible, and by contrast Lazy find as few as possible. You can make a match Lazy by adding "?" after the quantifier. 

### Boundaries

Boundary Markers define what comes before or after. One type of Boundary Marker is the Word Boundary ("\b"). This Boundary matches positions where the specified side is:
    Before the first character in a string if the first character is a word character.
    After the last character in a string if the last character is a word character.
    Between two characters in a string if one is a word character and the other is not.
For example "/\bJS\b/" would match the "JS" in "Hello JS!", but not in "Hello JSscript." 

Note that Anchors are a type of Boundary. 

### Back-references

Back-references are items in Regex equivalent to text matched by an earlier pattern within the same expression. We notate a Back-reference with a backslash ("\") followed by a number representing which Sub-expression we're referencing. Are we using any Back-references in our Date Regex? :eyes:

/^([1-2][0-9]|3[0-1]|0?[1-9])([-\.\/ ])(1[0-2]|0?[1-9])(\2)([\d]{4}|[\d]{2})$/

### Look-ahead and Look-behind

Collectively called Look-around, Look-ahead and Look-behind are zero-length assertions that return only "match" or "no match". For example "(?=foo)" is a Look-ahead that asserts what immediately follows the current position in the string is "foo". The Look-behind (therefore asserting what immediately precedes the current position) for the same example would look like this "(?<=foo)". 

## Assembling the pieces

We've labeled the minutiae of Regex! Now let's use that knowledge to dissect our Dates example. :dart:

/^([1-2][0-9]|3[0-1]|0?[1-9])([-\.\/ ])(1[0-2]|0?[1-9])(\2)([\d]{4}|[\d]{2})$/

We've wrapped our Regex in the required forward slashes ("/"), and then we have our Anchor Boundaries ("^", "$") defining the start and end. 
Let's start with our first Sub-expression:
    ([1-2][0-9]|3[0-1]|0?[1-9])
    Here we're validating the day of the month. We have a numeric digit 1 or two ("[1-2]") followed by a numeric digit 0-9 ("[0-9]"). Following the OR Operator ("|") we have the literal digit 3 followed by a numeric digit 0 or 1 ("[0-1]"). OR the literal digit 0 with a Lazy Operator ("?") signifying we want to see that "0" zero or one time, followed by a numeric digit 1-9 ("[1-9]"). That wraps up our first Capturing Group which should account for and find the possible combinations of numbers making up the day of the month!

Sub-expression two:
    ([-\.\/ ])
    Here we're defining the possible separators between day and month. We want only hyphen, dot, space, or slash (and we escape the dot and slash). 

Sub-expression three:
    (1[0-2]|0?[1-9])
    Here we're validating the month, using many of the same Meta Characters as Sub-expression one. 

Sub-expression four:
    (\2)
    Here we're Back-referencing Sub-expression two, repeating the possible separators. 
    
Sub-expression five:
    ([\d]{4}|[\d]{2})
    Finally we're validating our year input. We're asking for any single numeric digit ("[\d]") four times ("{4}"), OR any single numeric digit twice ("|[\d]{2}"). 

And just like that we've parsed an entire 77 character long Regex! I hope now you can break down and interpret most any Regex that you encounter, and even try writing your own! :100::100::100:

## Author

Brandon Krussow is a Full Stack Bootcamp student, Retail Manager, and Magic the Gathering enthusiast. https://github.com/bkorbsquare