# Regular Expressions and the world of transcribing strings and text like a Cyborg

Hello and good day to you Gangsta. I would like to begin this gist by expressing my gratitude towards you for reading this. It is my honor to introduce to you the wonderful world of regular expressions and how these simple patterns can be used to parse through a string with ease to hunt for anything you may want. Regular Expressions do not have to be used solely for client side purposes or server side. Regular Expressions can be used by a developer even for something as simple as debugging, where a regular expression can parse through thousands of line of code to find a the parentheses that is missing its second half. The possibilities are truly endless with regular expressions and i do hoep you enjoy this reading material.


## Summary

A regular expression is a pattern or sequence of characters that can be used to identify patterns in a string of characters to capture, manipulate, or identify these patterns among the text.
The regular expression of focus will be the pattern used to find and capture into multiple subgroups an HTML Tag: `/^<([a-z]+)([^<]+)*(?:>(.*)<\/\1>|\s+\/>)$/`. This regular expression is useful for parsing through any form of file where html tags may be included, whether this is a react component, a N.O.D.E file, or a standard doctype html file. As mentioned, when the tag is found it is partiotioned into multiple sub groups, so as a developer, the text can be used to replace parts of the HTML tag with an alternate version of the same tag or simply for locating potential areas in need of improvement, adaptation, or identification. The HTML regular Tag regular expression is used to identify HTML tags in a source document, saves portons of these tags n subgroups, and allows developers to make changes to these tags through out the entire document with ease. 


## Table of Contents

- [Anchors](#anchors)
- [Quantifiers](#quantifiers)
- [Grouping Constructs](#grouping-constructs)
- [Bracket Expressions](#bracket-expressions)
- [Character Classes](#character-classes)
- [The OR Operator](#the-or-operator)
- [Flags](#flags)
- [Character Escapes](#character-escapes)
- [The Whole Enchilada](#the-whole-enchilada)
- [Author](#author)


## Regex Components

There is a multitude of regular expression components which range from simple literal characters like a or b to complex structures like our HTML Tag regular expression `/^<([a-z]+)([^<]+)*(?:>(.*)<\/\1>|\s+\/>)$/`.
Here is a list of some of the many regular expression components in relation to how a regular expression can be used in javascript.
Regex components 
-	Literals: Direct matches of characters.
-	Character Classes: Match any character from a set.
-	Predefined Character Classes: Shorthand for common sets (e.g., \d for digits).
-	Negated Character Classes: Match any character not in a set.
-	Dot (.): Matches any character except newline (unless the s flag is used).
-	Anchors: Match positions rather than characters (^, $, \b, \B).
-	Quantifiers: Specify how many instances of a preceding element are allowed (*, +, ?, {n}, {n,}, {n,m}).
-	Grouping and Capturing: Group parts of the pattern ((), (?:), (?<name>)).
-	Alternation (OR Operator): Matches one pattern or another (|).
-	Lookahead and Lookbehind Assertions: Assert conditions for preceding or following sequences without including them in the match ((?=), (?!), (?<=), (?<!)).
-	Escape Characters: Denote special characters or signal special sequences (\).
-	Flags: Modify how the entire expression is interpreted (g, i, m, s, u, y).
-	Conditional Expressions: Matching different patterns depending on the presence of a previous capture.
-	Backreferences: Referencing previous capture groups within the same expression.
-	Unicode Property Escapes: Matching characters based on Unicode properties (\p{} and \P{} in engines that support Unicode property escapes).
-	Recursive Patterns: For some engines, patterns that can match patterns within themselves.
-	Atomic Grouping and Possessive Quantifiers: Advanced constructs for controlling backtracking and efficiency.


### Anchors

Anchors are special characters used to match position within a string. They are essential for ensuring that a regex (regular expression) pattern matches only at specific places in the text such as the beginning or end of a string or around word boundaties 

Here are some of the types of anchors 
  ^ (^) - carrot – start of string anchor – Used to match the beginning of a string class and has a different meaning where it can also be used as negation when used inside of Bracket Expressions.
    ^ /^Hello/.test("Hello, world!"); // true - the string starts with "Hello"
    ^ /^world/.test("Hello, world!"); // false - "world" is not at the start of the string
  $ - dollar sign – End of string anchor – matches the end of a string
    $/world!$/.test("Hello, world!"); // true - the string ends with "world!"
    $/Hello$/.test("Hello, world!"); // false - "Hello" is not at the end of the string
  \b Word boundary (\b) – used to match positions where one side is a word character (\w) – alphanumeric and underscore – and the other side is not a word character (\s, \(, \], etc…) 
    \b /\bworld\b/.test("Hello, world!"); // true - "world" is a whole word
    \b /\bwor\b/.test("Hello, world!"); // false - "wor" is not a whole word
  \B Non-Word-Boundary \B – matches at positions where both sides are word characters or both sides are not word characters
    \B /\Bwor\B/.test("Hello, world!"); // false - "wor" is at the boundary of a word
    \B /\Bello\B/.test("Hello, world!"); // true - "ello" is not at the beginning or end of a word or string of characters 
   
In our regular expression of Focus `/^<([a-z]+)([^<]+)*(?:>(.*)<\/\1>|\s+\/>)$/` it is easy to identify a couple anchors. 
  ^ - The first character within our regular expression and its onoly use. This carrot looks for a pattern of characters that begins a string instance. In this case, the regular expression is looking for a pattern of characters that begins with the less than symbol (<). This will reduce the number of patterns where the < symbol is used at any position other than the beginning of a string.


### Quantifiers

Quantifiers are characters that modify the prviosu character in a regular expression or coonstructs that specify how many instances of a character, group, or character class must be present in the target query for a match to occur. Quantifiers are of the most important characters for defining a specific quantity of characters the regular expression will look for. 

Here are some of the many tyoes of Quantifiers:
  * - The asterisk looks for 0 or ore instances of the preceding character 
    * - /Mo*/ - This will look for a range of different words with the only changing variable being the amount of o's following the M like M, Mo, Moo, Moooooooooooooooo are all acceptable patterns.
  + - The plus looks for one or more instances of the preceding character
    + - /Mo+/ - This will return all instances where M and o are found where there must be at least one o, so M will not be returned but Mo, Moo, Moooooooooooo will be returned 
  ? - The Question mark, also known as an or Operator, looks for one or none of the characters that precede the symbol.
    ? - /Mo?/ - This regular expression will either return M or Mo and nothing else.
  {n} - Braces have a variety of uses for quantifying
    {n} - Where n can be any integer, this will return look for a pattern where the specific character appears n amount of times 
      {n} - /Mo{2}/ - This will return Moo only 
    {n,} - For any number n or more 
      {n,} - /Mo{3,}/ this will look for any instances where M is followed by three or more o's
    {n,m} - Where n is the minimum range and m is the maximum range of the character to be queried by the regexp
      {n,m} - /Mo{2,4} - This regex will return any instances where M is followed by 2 or 4 o's, like Moo or Moooo
  Greedy Quantifiers - Much like the cookie monster, greedy quantifiers will match with anything wihtout restriction as long as they fit the pattern 
    * /<.*?/ - This will look for anything between the first possibel < and the last possible >
  Lazy Quantifiers - When a greedy quantifier becomes restricted, it also becomes lazy.
    ? /.*?> - This will look for everything between the first < and the first > 
    
  In our Regular Expression of focus: `/^<([a-z]+)([^<]+)*(?:>(.*)<\/\1>|\s+\/>)$/` 
    Multiple Quantifiers can be identified. There is the one or more quantifier and the 0 or more quantifier. These quantifiers are used to find one or more instances of a lower case letter in the first subgroup, one or more instances of the Bracket Expression in the second subgroup, 0 or more entire second index subgroups, 0 or more characters in the third subgroups sub sub group, and finally one or more instances of white space towards the rear end of the third subgroup.


### Grouping Constructs

Grouping constructs allow the combination of a sequence of tokens into a single unit for various purposes such as applying quantifiers to a group of characters, capturing substrings for later use, or specifying alternatives. 
  - Grouping is achieved with the use of parentheses ().
  
 There are many types of grouping constructs.
  -	Capturing groups – stores the part of the string that matches the regex query inside of the parnetheses where captured groups are organized from left to right
    o	Example:  
      	const regex = /(\w+) (\w+)/;
      	const str = "Moo Cow";
      	const match = str.match(regex);
      	console.log(match[1]); // "Moo" - The first captured group
      	console.log(match[2]); // "Cow" - The second captured group
  -	Non-capturing-groups – a non capturing group can use the ? (one or zero quantifier) to ensure the group is not captured.
    o	Example;
      	const regex = /(?:\w+) (\w+)/; // Only the second word will be captured
      	const str = "Moo Cow";
      	const match = str.match(regex);
      	console.log(match[1]); // "Doe" - The first (and only) captured group
  -	Named capture groups allow the dev to assign a name to the group instead of using a numerical index. This makes the code more readable and easier to maintain.
    o	Named groups are denoted by (?<name>…)
      	Example:
        •	const regex = /(?<firstName>\w+) (?<lastName>\w+)/;
        •	const str = "Moo Cow";
        •	const match = str.match(regex);
        •	console.log(match.groups.firstName); // "Moo"
        •	console.log(match.groups.lastName); // "Cow"
  -	Lookahead and Lookbehind assertions are a form of non-capturing groups that allow devs to match a group of characters only if they are followed or preceded by another group of characters.
    o	Assertiosn do not consume characters in the string but only assert whether a  match is possible 
    o	Lookahead assertion X(?=Y) matches X only If X is followed by Y 
      	const regex = /\d(?=\w)/; - Match a digit only if it's followed by a word character
      	console.log("1a 2b 3c".match(regex)); - "1"
    o	Negative lookahead assertion: X(?!Y) matches X only if X is not followed by Y 
      	const regex = /\d(?! \w+)/; - Match a digit only if it's not followed by a word character
      	console.log("1 a 2b 3c".match(regex)); - "2", "3"
    o	Lookbehind assertion: (?<=Y)X matches X only if X is preced by Y
      	const regex = /(?<=\d) \w/; - Match a word character preceded by a digit and a space
      	console.log("1 a 2 b".match(regex)); - " a"
    o	Negative lookbehind assertion: (?!Y)X matches X only if X is not preceded by Y 
      	const regex = /(?<!\d) \w/; - Match a word character not preceded by a digit and a space
      	console.log("1a b".match(regex)); - " b"
  -	Characters to manipulate or utilize capture groups 
    o	$n – where n is any positive integer is used to replace the second subgroup of a captured group 
    o	\n where n is any positive integer is used to refer to the sub group of a captured group 

      
In our regular Expression of focus: `/^<([a-z]+)([^<]+)*(?:>(.*)<\/\1>|\s+\/>)$/`,
While there are no Lookbehind or Lookahead or even named capture groups, there are stull multiple capture groups and non-capture groups. following the opening < symbol there is a capture group that looks for a lowercase word, followed by another capture group with a quantifier that will look for 0 or more of the same characters identified by the bracket expression, and an optional non-captured group.


### Bracket Expressions

Bracket Expression are used to specify a set of characters that can match a single character in the string being searched.
  -	Bracket expressions ar enclosed in brackets [] and are a useful way to find a character is a string that matches one or more of the characters within the brackets if used with quanitfiers 
  -	Matching one character from a set 
    o	/[abc]/ will match with either a or b or c from a string 
    o	“apples”.mach(/[abc]/) returns an a
  -	Ranges – the hyphen is used to identify a range of characters 
    o	[0-9] – looks for all numbers from 0 to 9
    o	[a-z] – looks for all letters that are lowercase 
    o	[A-Za-z0-9] – will match any single alphanumeric character 
  -	Negation – using the carrot on a bracket expression will return everything except for whatever values are included in the bracket.
    o	“abc”.match(/[^abc]/) will return null since the only characters in the bracket match all of the characters in the string.
  -	Special characters inside brackets 
    o	\ backslash still acts as an escape character unless escaped \\.
    o	Carrot ^ negates the character class if it is the first character in use.
    o	The hyphen - specifies a range unless it is the first character in the bracket expression.
    o	Closing bracket needs to be escaped \] to be included in the bracket unless it is the first character.

In our RegEx of focues: `/^<([a-z]+)([^<]+)*(?:>(.*)<\/\1>|\s+\/>)$/`,
Almost the entire regular expression is composed of bracket expressions. The first looks for any instance of a lower case letter. The second looks for anything BUT a < symbol. My original statement was incorrect. This regular expression is hardly made of bracket expressions.


### Character Classes

Character classes are predefined shorthand sets that match specific types of characters, such as digits, word characters, or whitespace 
  -	\d – matches any digit character – equivalent to [0-9].
  -	\D – Looks for non-numeric characters.
  -	\w – Looks for alphanumerics.
  -	\W - Looks for anything but alphanumeric characters.
  -	\s - Looks for white space.
  -	\S - Looks for anything that is not white space.
  
In our regular expression of focus: `/^<([a-z]+)([^<]+)*(?:>(.*)<\/\1>|\s+\/>)$/`,
We can see a variety of character classes. There is the \n character class, where n can be any positive integer and the \n refers to a subgroup from the captured groups enclosed in parentheses. In this csae it is \1 and when used for the escaped forward slash (\/) it is telling the regular expression to look for a second HTML tag with the same alphanumeric characters inside of it as the first subgroup. Similarly for the \s with the one or more quantifier, the amount of backspace included is limited only on the left side by 1 space but can include as much white space as theortetically possible. 


### The OR Operator

OR operator – OR operator represented by the vertical line | character. Allows for the matching of either one pattern or another within the same regular expression, functioning essentiall as a logical OR that selects between alternatives 
  -	Syntax for using the OR operator 
    o	/pattern1|pattern2/
      	Will match if either patten1 or pattern2 (or both) are found in the string being tested 
  -	Usage 
    o	Matching different words 
      	/cat|dog/
    o	Using OR with group constructs 
      	Using the or operator within groups (parentheses) to specify that part of the pattern should match one of several alternatives.
        •	/file\.(jpg|png)/
    o	This will match with the string file followed by a dot (.) followed by either jpeg or png.
      o	File.jpeg
      o	File.png
    o	Combining with other elements 
        	When used alongide the carrot anchor ^ and the dollar sign anchor $ the or operator can look for a specific pattern or another.
        	/^Hello (world|mars)$/
          •	This will look for a patten where Hello is at the beginning of a string where that same string will end with either world or mars.

In our regular expression of focus: `/^<([a-z]+)([^<]+)*(?:>(.*)<\/\1>|\s+\/>)$/`,
There is a singular or statement made to differentiate between either ">string of letters </>" OR "  />". This is useful for HTML Tags that may end immediately without a closing tag like an <input/> tag or alternatively a <div> </div> tag that has both an operning and closing tag.


### Flags

Flags are special settings that change how the query is interpreted and are used to for various functionalities or behaviors in the regex engine.
  -	Global – (‘g’): caueses the regex engine to find all matches in the string, instead of stopping after the first match 
  -	Ignore Case (i): Makes the search case-insensitive, allowing the pattern to match letters of any case.
  -	Multi-line (m): Treats the beginning (^) and end ($) anchor characters as working across multiple lines. That means ^ matches the start of any line within the string and $ matches the end of any line.
  -	DotAll (s): Allows the dot (.) character to match newline characters as well. By default, the dot matches any character except newline characters.
  -	Unicode (u): Treats the pattern as a sequence of Unicode code points. This flag enables correct handling of surrogate pairs.
  -	Sticky (y): Ensures the match starts from the current position in the string. The regex engine does not search further ahead for a match if the next character does not fit the pattern. This is useful for matching from a specific index.
  -	Unicode Property Escapes (u): When combined with the u flag, it enables the use of Unicode Property Escapes syntax in the regex, allowing for the matching of characters based on their Unicode properties, such as \p{Script=Greek} to match characters in the Greek script.
  -	Has Indices (d): Available in more recent versions of JavaScript, this flag makes the resulting match object include indices of captured groups. This is useful for knowing where in the input string each group was matched.
  -	Usage of flags used by appending them to the end of the regex pattern. This modifies the behavior of the search according to what each flag is designed to do.
    o	Two main ways to use a regexp in JS- literal notation and using regex constructor.
      	Literal notation – enclose the pattern between slashes and plave the flags right after the closing slash.
        •	Let regex = /pattern/ig;
        •	This regular expression will match any instance of the word pattern in the global document regardless of its case.
      	Regex constructor – when using the regex constructor the pattern is placed as the first parameter and the flags as the second parameter.
        •	Let pattern = “pattern”
        •	Let flags – “ig”
        •	Let regex = new RegExp(pattern, flags)

In our regular expression of focus: `/^<([a-z]+)([^<]+)*(?:>(.*)<\/\1>|\s+\/>)$/`,
There are no flags but a simple application of a flag could be used so the regular expression could capture any HTML Tag in the global object like so: 
        `/^<([a-z]+)([^<]+)*(?:>(.*)<\/\1>|\s+\/>)$/g'
        
        
### Character Escapes

Last but not least comes a concept that is used nearly more than anythoer regular expression component, the character escape. 
Character Escapes utiize the backslash to escape an otherwise special character. 
Some examples of Character Escapes include:
-	\\ means a literal backslash 
-	\. Means a literal period 
-	\^ means a literal carrot
-	In addition to escaping special characters, escape sequences are used to represent special types of characters:
  o	Whitespace characters: Such as \n for a newline, \t for a tab, \r for a carriage return, and \f for a form feed.
  o	Word boundary (\b): Matches a position where one side is a word character (like letters or digits) and the other side is not.
  o	Digit (\d): Matches any digit character. Equivalent to [0-9].
  o	Non-Digit (\D): Matches any non-digit character. Equivalent to [^0-9].
  o	Word Character (\w): Matches any alphanumeric character including the underscore. Equivalent to [A-Za-z0-9_].
  o	Non-Word Character (\W): Matches any character that is not a word character. Equivalent to [^A-Za-z0-9_].
  

## The Whole Enchilada 

Finally, we have everything we need to dissect our Regular Expression of Focus in its entirety. Let's begin. 

`/^<([a-z]+)([^<]+)*(?:>(.*)<\/\1>|\s+\/>)$/`

  - The regular expression is created between the first and last forward slash. - /.../
  - The regular expression must begin at a new line ^ and must end as the last element of a line $
  - The first character searched for is a literal < with any number of one or more lower case characters contained in a subgroup.
  - The second subgroup looks for none or more of any characters except for an opening < tag. There can be 0 or more of this subgroup, meaning this will look for anything between the opening tag and the next subgroup.
  - The third subgroup is a non-captured group or one as identified by the ?: (one or none quantifier) at the beginning of the subgroup and accounts for anything within this subgroup. 
  - Optionally the third subgroup could either be composed of "> '0 or more characters without limit to the type of character' </(whatever was typed into subgroup 1 that could be a div, article, p, etc...)>" OR "(white space of one or more characters)/>". In other words the third subgroup could include a paragraph or what have you with a closing tag the same as the inititial opening tag or the end of the initial tag.


## Author
Hello, my name is Grant. If you have any questions, comments, or concerns you cannot reach me throguh this Gist. Alternatively you can hunt me down via my Github Profile. 
Github: https://github.com/Grantlw100

Happy Hunting! :)