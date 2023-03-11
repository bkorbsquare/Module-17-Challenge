# Diving into Regex: Dates

Regular Expressions (or Regex) are sequences of characters that define a search parameter. These sequences are comprised of Literal and Meta Characters, and are wrapped in forward slashes ("/"). Literal Characters are exactly what they sound like - a one to one exact copy of what you're searching for. An example of this would be "L" when searching for the letter L. Meta Characters represent a set of Literal Characters, lack thereof, or position. An examples of this would be "\d" representing any digit. We use Regex to query more complex parameters efficiently. :muscle::muscle::muscle:

## Summary

We're going to break down the components of Regex, taking a specific look at the following example which can find dates in the format DD/MM/YYYY or DD/MM/YY:

/^([1-2][0-9]|3[0-1]|0?[1-9])([-\.\/ ])(1[0-2]|0?[1-9])(\2)([\d]{4}|[\d]{2})$/

## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [OR Operator](#or-operator)
- [Grouping and Capturing](#grouping-and-capturing)
- [Bracket Expressions](#bracket-expressions)
- [Greedy and Lazy Match](#greedy-and-lazy-match)
- [Back-references](#back-references)
- [Assembling the Pieces](#assembling-the-pieces)

## Regex Components

### Anchors

The caret (^) and bling ($) symbols represent the start and end of Regex, and are referred to as Anchors. :anchor:

### Quantifiers

Quantifiers determine how exactly (or loosely) your regex matches the queried string. They usually include a minimum and maximum number of characters that your Regex is looking for. Here are some examples of quantifiers:

? — Matches the pattern zero or one time. <br/>
{ n } — Matches the pattern exactly n number of times.

Note that if you wanted to make the "?" literal (actually searching for "?" and not using "?" as a quantifier), you would need to Escape. Escape allows you to break the default quantifier and instead input literals. We notate Escapes using a backslash (\\).

Can you spot the Quantifiers in our Dates Regex? What do you suppose they're determining specifically? It's okay if you don't know yet, we'll break down the entire sequence later on under "Assembling the Pieces." :blush:

/^([1-2][0-9]|3[0-1]|0?[1-9])([-\.\/ ])(1[0-2]|0?[1-9])(\2)([\d]{4}|[\d]{2})$/

### OR Operator

The OR operator (|) represnts logical "or". We use this to match either what preceeds or follows that pipe symbol (|). Each of these components is called an Alternative. We're using a few OR Operators in our Regex: :balance_scale:

(1[0-2]|0?[1-9])(\2)([\d]{4}|[\d]{2})$/

### Grouping and Capturing

In order to check that different parts of a string meet different requirements, we use Grouping Constructs. The primary way to group a section of Regex is by using parentheses (()). Each section within such a grouping is called a Sub-expression. Here we have the first two Sub-expressions within our Dates Regex: :busts_in_silhouette:

([1-2][0-9]|3[0-1]|0?[1-9])([-\.\/ ]) 

### Bracket Expressions

Meta Characters inside of square brackets ([]) represent the range we're looking to match. These patterns are known as "Bracket Expressions" and contain what we call "Positive Character Groups," which outline the characters we want to include. Hyphens (-) are used between alphanumeric characters to represent a range of possibilities. Try and parse some of the Bracket Expressions in our Dates Regex. :detective:

/^([1-2][0-9]|3[0-1]|0?[1-9])([-\.\/ ])(1[0-2]|0?[1-9])(\2)([\d]{4}|[\d]{2})$/

### Greedy and Lazy Match

Greedy matches find as many occurrences of queried patterns as possible, and by contrast Lazy find as few as possible. You can make a match Lazy by adding "?" after the quantifier. How many Lazy matches does our Regex have? :thinking:

/^([1-2][0-9]|3[0-1]|0?[1-9])([-\.\/ ])(1[0-2]|0?[1-9])(\2)([\d]{4}|[\d]{2})$/

### Back-references

Back-references are items in Regex equivalent to an earlier pattern within the same expression. We notate a Back-reference with a backslash followed by a number representing which Sub-expression we're referencing (\\1). Are we using any Back-references in our Date Regex? :eyes:

/^([1-2][0-9]|3[0-1]|0?[1-9])([-\.\/ ])(1[0-2]|0?[1-9])(\2)([\d]{4}|[\d]{2})$/ 

## Assembling the pieces

We've labeled the minutiae of Regex! Now let's use that knowledge to dissect our Dates example. :nerd_face:

/^([1-2][0-9]|3[0-1]|0?[1-9])([-\.\/ ])(1[0-2]|0?[1-9])(\2)([\d]{4}|[\d]{2})$/

We've wrapped our Regex in the required forward slashes (/), and then we have our Anchor Boundaries (^, $) defining the start and end. Next let's look at each Sub-expression on it's own. 

Sub-expression one: ([1-2][0-9]|3[0-1]|0?[1-9]) <br/>
&nbsp;&nbsp;&nbsp;Here we're validating the day of the month. We've broken the possible inputs into three parts, each separated by an OR Operator (|). First we start with the days 10-29 represented by the digit 1 or 2 ([1-2]) followed by a digit 0-9 ([0-9]). Next we're accounting for days 30 & 31 with the digit 3 (3) followed by a digit 0 or 1 ([0-1]). Lastly we're accounting for days 1-9, with possible zeros in front, represented by a Lazy Operator (?) and a digit 1-9 ([1-9]).

Sub-expression two: ([-\.\/ ]) <br/>
&nbsp;&nbsp;&nbsp;Here we're defining the possible separators between day and month. We want only hyphen, dot, space, or slash (and we Escape the dot and slash). 

Sub-expression three: (1[0-2]|0?[1-9]) <br/>
&nbsp;&nbsp;&nbsp;Here we're validating the month, using many of the same Meta Characters as Sub-expression one. 

Sub-expression four: (\2) <br/>
&nbsp;&nbsp;&nbsp;Here we're Back-referencing Sub-expression two, repeating the possible separators. 
    
Sub-expression five: ([\d]{4}|[\d]{2}) <br/>
&nbsp;&nbsp;&nbsp;Finally we're validating the year. We're asking for any single digit ([\d]) four times ({4}), OR (|) any single digit twice ([\d]{2}). 

And just like that we've parsed an entire 77 character long Regex! Now you can break down and interpret most any Regex that you encounter, and even write your own! :100::100::100:

## Author

Brandon Krussow is a Full Stack Bootcamp student, Retail Manager, and Magic the Gathering enthusiast. https://github.com/bkorbsquare
