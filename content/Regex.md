## What is Regular Expression?

Regular Expression (commonly referred to as "regex") is a string of characters that define a search pattern.  This can be as simple as looking or an exact match of a word like "cat", or something more complex, such as a regular expression to find any email address: 

[0-9a-zA-Z.+_]+@[0-9a-zA-Z.+_]+\.[a-zA-Z]{2,4}

This allows users to create their own custom search to find the exact violation or criteria they specify.

**Please note BetterCloud uses the RE2 Golang flavor of Regular Expression**

## Basics of Regular Expression

Regular expression utilizes character classes, special characters, and quantifiers to create more complex and expansive searches. This allows the user to expand their search, as opposed to searching for an exact match using literal pieces of text. Please note that regular expressions are by default case sensitive.

### Character Classes:

Character classes tell the regex engine to match only a certain set of characters, such as digits, whitespace, or words.

Examples of character classes:

- \s Match any character which is considered whitespace (space, tab etc)
- \d Match any character which is a digit ( 0 - 9 ).
- \w Match any character which is a word character ( A-Z, a-z, 0-9 and _ )

Character classes also have their negated version, which tells the regex engine to match only a certain set of characters.

Examples of negated character classes:

- \S Match any character which is not whitespace
- \D Match any character which is not a digit
- \W Match any character which is not a word character

### Special Characters:

Special characters are characters that are reserved for special use. These characters expand the use of regex.

- **dot or period .** Match any single character.

- Example: **b.g** will find words like big, bug, beg, or bag

- **vertical bar or pipe |** functions as a boolean "or"

- Example: **a|b** will return a or b

- **brackets[ ]** Match a range of characters contained within the square brackets

- Example: **[abc]** will match a single character of either a, b, or c

- **parentheses ()** capture everything enclosed within the parentheses

- Example: **(abc)** will match the exact string of abc

- **curly brackets {}** acts as a quantifier 

- Example: **{4}** will search for a number of matches exactly equal to 4 of the item preceding it
- Example: **{3,6}** will search for a number of matches between 3 and 6 of the item preceding it

- **Caret ^** can have a few meanings. ^ by itself means the start of a string

- Example:**^bag** will match any string that starts with the characters "bag"
    - An example of a sentence that will trigger this regex: bag the groceries.
- Another meaning for the caret character ^ is when it is used in conjunction with brackets []. It will tell the regex engine NOT to match any of the characters contained within the brackets

- Example: **[^abc]** will match a single character that is NOT a, b, or c

- **dollar sign $** end of a string or line

- Example: **$bag** will search any string that ends with the characters "bag"
    - an example sentence: Put the groceries in the bag

- **backslash \** Escapes, or remove the special meaning of the next character. Useful for when you are searching for these special characters 

- Example: **\$** will negate the special meaning of the $ character and do a literal search for the $ symbol

### Quantifiers:

Quantifiers tell the regex engine how many or how few characters to search for. Here are some examples of quantifiers:

- ***** Match zero or more of the preceding item
- **+** Match one or more of the preceding item
- **?** Match zero or one of the preceding item
- **{n}** Match exactly n of the preceding item
- **{n,m}** Match between n and m of the preceding item
- **{n,}** Match n or more of the preceding item

### **Breaking down a basic regular expression:**

Below is an example of a basic regular expression that can be used searching for United States passport identification numbers:

\d{9}

- **\d** means the regex searching for a digit (equal to [0-9])
- {9} **is a** **type of quantifier** where the regex searches for the exact number of matches specified inside of the brackets, in this case, 9 matches.

Putting that together:

\d{9} is searching for a string that has nine consecutive digits without any breaks or whitespace.

Examples of content that will match the above regular expression:

- 123456789
- 571651982
- 128585861

Examples of content that will not match the above regular expression

- 123 456 789
- 123-456-789

### **Breaking down more complex regular expressions:**

The below regular expression searches for credit card numbers:

\d{4}[-, ]?\d{4}[-, ]?\d{4}[-, ]\d{4}

 Breaking down each separate part of the above regular expression:

- **\d** means the regex searching for a digit (equal to [0-9])
- **{4} is a** **type of quantifier** where the regex searches for the exact number of matches specified inside of the brackets, in this case, 4 matches
- **[-, ]** when characters are surrounded by brackets, that means that the regular expression is searching for any single character that is specified inside the bracket. In this instance, it is a search for a hyphen, a comma, or an empty space. 
- **? is a type of quantifier** means that the regular expression is looking for zero or one of the preceding item in the regular expression 

Putting that together:

- **\d{4}**

-  means the regex is searching for 4 digits followed by

- **[-, ]?**

- a hyphen, comma, or space, zero or one time followed by

- **\d{4}**

- 4 digits followed by

- **[-, ]?** 

- a hyphen, comma, or space, zero or one time followed by

- **\d{4}**

- 4 digits followed by

- **[-, ]?** 

- a hyphen, comma, or space, zero or one time followed by

- **\d{4}** 4 digits

Examples of content that would be found by the above regular expression:

- 1234 1455 1212 2451
- 4582-1231-5152-9586
- 1723,4234,1234,6456

Here is a second example of a regular expression. This regex searches for any email address:

[0-9a-zA-Z.+_]+@[0-9a-zA-Z.+_]+\.[a-zA-Z]{2,4}

Let's break down each part of the above regex:

- **Brackets []** means that is searching for any single character that is inside the brackets 
- **0-9** the regular expression is searching for any single character in the range of 0-9
- **a-z** searching for any single character in between a lowercase a and lowercase z
- **A-Z** searching for any single character in between an uppercase A and an uppercase Z 
- **.** the regular expression is looking for an exact match to a period **.**
- **+** the regular expression is looking for an exact match to a plus sign **+**
- _ the regular expression is looking for an exact match to an underscore **_**
- + when the plus sign is outside of brackets or does not have a backslash preceding it, it is a metacharacter with a special definition. The **+** acts as a quantifier similar to curly brackets **{}** and question marks **?** The plus sign **+** means that the regular expression is looking between one or more of the preceding item.
- **@** means that the regular expression is looking for a literal exact match to the @ symbol
- **\.** means that the regular expressions is looking for a literal exact match to the dot or period symbol. This is because we are "escaping" or "negating" the dot's\period's special character meaning with the use of a backslash \
- **{2,4}** means that the regular expression will try to match the preceding item between 2 and 4 times. In this example it is searching domain extensions, such as ca, com, org, edu, etc.

Putting that together:

- [0-9a-zA-Z.+_]+

- means the regex is searching for any single character that is either a digit between 0-9, or a lower case letter between a and z, or an upper case letter between A and Z, or a period, or a plus sign, or an underscore. With a quantity of one to an unlimited amount.

- **@**

- means that the regular expression is looking for a literal exact match to the @ symbol

With the above, the regular expression will find anything up to and including the @ symbol in an email address. Continuing on we have the same regex string to find anything before the domain extension:

- [0-9a-zA-Z.+_]+

- means the regex is searching for any single character that is either a digit between 0-9, or a lower case letter between a and z, or an upper case letter between A and Z, or a period, or a plus sign, or an underscore. With a quantity of one to an unlimited amount.

- \.

- means the regex is escaping\negating the special meaning of the dot/period symbol, and is telling the regex engine to search for an exact match to a dot/period.

- [a-zA-Z]{2,4}

- means the regex is searching for any single character that is a lower case letter between a and z, or an upper case letter between A and Z. The regex engine is searching for that match between two and four times.

Examples of content that will be found by this regular expression:

- john.doe@email.blog
- Jane_Doe@email.org
- John.Doe1191@email.ca

Examples of content that will not be found by this regular expression:

- @email.com
- john.doe@email.education