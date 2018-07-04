# Regular Expressions

A regular expression is an expression (character string) that is used to match patterns in text.

You can use a regular expression to do these things:  
1. Extract indexes from the body of a document.  
2. Extract indexes from the filename of a document.  
3. Make sure that node indexes are correct. For example, make sure that an e-mail address or a phone number has the correct structure.  

You can use all the regular expressions [here](http://download.oracle.com/javase/6/docs/api/java/util/regex/Pattern.html). 

Additionally, you can use a named capturing group.

For information about regular expressions, refer to [RegexLib](http://regexlib.com).

## Examples of Regular Expression

## Simple email validation

```javascript
[\w-]+@([\w-]+\.)+[\w-]+
```

Matches: test@example.com  
Matches: test@example.c  
Does not match: test@exa$mple.com  

## Advanced Email Validation 

```javascript
^[A-Za-z0-9._%+-]+@([A-Za-z0-9-_]+\.)+[A-Za-z]{2,6}$
```

Matches: test@example.com (and the e-mail address must be at the start of a line)  
Does not match: test@example.c  
Does not match: test@exa$mple.com  

## Phone number, style 1

```javascript
[0]\d{2}-\d{7}
```

Matches: 011-8804411  
Does not match: 011-880 4411  

## Phone number, style 2

```javascript
^\([0]\d{2}\)\d{7}
```

Matches: (011)8804411 (and the phone number must be at the start of a line)  
Does not match: (011) 880 4411  
Does not match: (0118)804411  

## South African ID

```javascript
(((\d{2}((0[13578]|1[02])(0[1-9]|[12]\d|3[01])|(0[13456789]|1[012])(0[1-9]|[12]\d|30)|02(0[1-9]|1\d|2[0-8])))|([02468][048]|[13579][26])0229))(( |-)(\d{4})( |-)(\d{3})|(\d{7}))
```

Matches: 8001015009087  
Does not match: d001015009087  

Refer [National Identification Number](http://en.wikipedia.org/wiki/National_identification_number#South_Africa).


