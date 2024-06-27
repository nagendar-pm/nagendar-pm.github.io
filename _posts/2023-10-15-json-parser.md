---
layout: post
title: "Json Parser"
date: 2023-10-15
categories: projects
repo : 'https://github.com/nagendar-pm/json-parser/'
filePath : 'blob/main/'
rawParam : '?raw=true'
---

JSON Parser is a perfect place where I wanted to learn about JSON, how different components of a system can be broken to write *maintainable* and *scalable* code. 

<!--more-->

A simple java project written to parse JSON text.<br>

> You can find the project [here]({{ page.repo }})

In this parser we are doing the below:
1. Lexical Analysis
2. Syntactical Analysis
3. Parsing and building the JSON object
4. Formatting and beautifying the JSON

In the first 3 of the above steps, we are throwing exceptions anywhere the rules of JSON standard are not
seems to be conformed by the input text. So the formatter only works on the input which is a valid JSON.

## Diagrams
### Lexer Class Diagram
1. `Lexer` is the only abstraction made available to the main class.
2. In the Lexer, we call the `nextToken()` repeatedly to get the next token at any instant
3. Lexer in turn uses the `TokenizerFactory` to get the `Tokenizer` based on the current character from the input
4. `Tokenizer` has method `getToken(Input input)` to generate the token from the specific index we are at.
5. `Token` is the base interface to represent the type of tokens allowed in the json
![Class diagram for lexer]({{ page.repo }}{{ page.filePath }}UML/Lexer.png{{ page.rawParam }} "Class diagram of Lexer")

### Analyzer Diagrams
#### State diagram
The DFA for the analyzer of JSON is as below: <br>
![State diagram for analyzer]({{ page.repo }}{{ page.filePath }}UML/DFA-json-analyzer.png{{ page.rawParam }} "State diagram of Analyzer")

#### Class diagram
1. `Analyzer` has the method `void analyze(TokenBase tokenBase)` which analyzes the token ordering and lets us know if the standard is followed or not
2. Each analyzer has the next set of characters set up as per the above DFA and on encountering a character which isn't from the allowed list at a lexeme, we throw exception
3. Based on the type of `Token` of the `Lexeme`, we find the next Analyzer from the `AnalyzerFactory` and work on its analyze method
4. This basically follows **Chain of Responsibility pattern**
![Class diagram for analyzer]({{ page.repo }}{{ page.filePath }}UML/Analyzer.png{{ page.rawParam }} "Class diagram of Analyzer")

### Parser Diagrams
1. Parser is the minimal code component in this project
2. `Parser` has the method `Lexeme parse(List<Lexeme> lexemes)` which takes the Lexemes and build the object out of the lexemes
3. If there is any unwanted or unexpected lexemes at any instant, exceptions will be thrown
![Class diagram for Parser]({{ page.repo }}{{ page.filePath }}UML/Parser.png{{ page.rawParam }} "Class diagram of Parser")

### Formatter Diagram
1. `Formatter` has the method `String format(Lexeme lexeme, int depth)` which when given the Lexeme with the value of the json object built by the `Parser`, formats and beautifies it
2. `FormatterFactory` takes the `Token` as the input and gets the Formatter needed to beautify the token and make a string value out of it
![Class diagram for Formatter]({{ page.repo }}{{ page.filePath }}UML/Formatter.png{{ page.rawParam }} "Class diagram of Formatter")


## Test
The output dump when tested looks like below:
```commandline
Working on resources/input.txt
fileContent
{
    "key1" : "value1","key2" : "value2","key3" : {"key31" : "value31"},"key4" : [123, 345.78, 13.45e90, -345.909, +245],
    "key5" : true,"key6" : false,"key7" : [{"key711" : "value711","key712" : "value712"},{"key721" : "value721","key722" : "value722"}]
}

+--------------------+
|  Lexical Analysis  |
+--------------------+
Lexeme{tokenType=LEFT_BRACE, value={, start=0, end=0}
Lexeme{tokenType=STRING, value="key1", start=6, end=11}
Lexeme{tokenType=COLON, value=:, start=13, end=13}
Lexeme{tokenType=STRING, value="value1", start=15, end=22}
Lexeme{tokenType=COMMA, value=,, start=23, end=23}
Lexeme{tokenType=STRING, value="key2", start=24, end=29}
Lexeme{tokenType=COLON, value=:, start=31, end=31}
Lexeme{tokenType=STRING, value="value2", start=33, end=40}
Lexeme{tokenType=COMMA, value=,, start=41, end=41}
Lexeme{tokenType=STRING, value="key3", start=42, end=47}
Lexeme{tokenType=COLON, value=:, start=49, end=49}
Lexeme{tokenType=LEFT_BRACE, value={, start=51, end=51}
Lexeme{tokenType=STRING, value="key31", start=52, end=58}
Lexeme{tokenType=COLON, value=:, start=60, end=60}
Lexeme{tokenType=STRING, value="value31", start=62, end=70}
Lexeme{tokenType=RIGHT_BRACE, value=}, start=71, end=71}
Lexeme{tokenType=COMMA, value=,, start=72, end=72}
Lexeme{tokenType=STRING, value="key4", start=73, end=78}
Lexeme{tokenType=COLON, value=:, start=80, end=80}
Lexeme{tokenType=LEFT_SQUARE_BRACKET, value=[, start=82, end=82}
Lexeme{tokenType=NUMBER, value=123, start=83, end=85}
Lexeme{tokenType=COMMA, value=,, start=86, end=86}
Lexeme{tokenType=NUMBER, value=345.78, start=88, end=93}
Lexeme{tokenType=COMMA, value=,, start=94, end=94}
Lexeme{tokenType=NUMBER, value=13.45e90, start=96, end=103}
Lexeme{tokenType=COMMA, value=,, start=104, end=104}
Lexeme{tokenType=NUMBER, value=-345.909, start=106, end=113}
Lexeme{tokenType=COMMA, value=,, start=114, end=114}
Lexeme{tokenType=NUMBER, value=+245, start=116, end=119}
Lexeme{tokenType=RIGHT_SQUARE_BRACKET, value=], start=120, end=120}
Lexeme{tokenType=COMMA, value=,, start=121, end=121}
Lexeme{tokenType=STRING, value="key5", start=127, end=132}
Lexeme{tokenType=COLON, value=:, start=134, end=134}
Lexeme{tokenType=BOOLEAN, value=true, start=136, end=139}
Lexeme{tokenType=COMMA, value=,, start=140, end=140}
Lexeme{tokenType=STRING, value="key6", start=141, end=146}
Lexeme{tokenType=COLON, value=:, start=148, end=148}
Lexeme{tokenType=BOOLEAN, value=false, start=150, end=154}
Lexeme{tokenType=COMMA, value=,, start=155, end=155}
Lexeme{tokenType=STRING, value="key7", start=156, end=161}
Lexeme{tokenType=COLON, value=:, start=163, end=163}
Lexeme{tokenType=LEFT_SQUARE_BRACKET, value=[, start=165, end=165}
Lexeme{tokenType=LEFT_BRACE, value={, start=166, end=166}
Lexeme{tokenType=STRING, value="key711", start=167, end=174}
Lexeme{tokenType=COLON, value=:, start=176, end=176}
Lexeme{tokenType=STRING, value="value711", start=178, end=187}
Lexeme{tokenType=COMMA, value=,, start=188, end=188}
Lexeme{tokenType=STRING, value="key712", start=189, end=196}
Lexeme{tokenType=COLON, value=:, start=198, end=198}
Lexeme{tokenType=STRING, value="value712", start=200, end=209}
Lexeme{tokenType=RIGHT_BRACE, value=}, start=210, end=210}
Lexeme{tokenType=COMMA, value=,, start=211, end=211}
Lexeme{tokenType=LEFT_BRACE, value={, start=212, end=212}
Lexeme{tokenType=STRING, value="key721", start=213, end=220}
Lexeme{tokenType=COLON, value=:, start=222, end=222}
Lexeme{tokenType=STRING, value="value721", start=224, end=233}
Lexeme{tokenType=COMMA, value=,, start=234, end=234}
Lexeme{tokenType=STRING, value="key722", start=235, end=242}
Lexeme{tokenType=COLON, value=:, start=244, end=244}
Lexeme{tokenType=STRING, value="value722", start=246, end=255}
Lexeme{tokenType=RIGHT_BRACE, value=}, start=256, end=256}
Lexeme{tokenType=RIGHT_SQUARE_BRACKET, value=], start=257, end=257}
Lexeme{tokenType=RIGHT_BRACE, value=}, start=259, end=259}

Analyzing the character pattern...

+------------------------+
|  Syntactical Analysis  |
+------------------------+
parsed Json = {"key1"=Lexeme{tokenType=STRING, value="value1", start=15, end=22}, 
"key2"=Lexeme{tokenType=STRING, value="value2", start=33, end=40}, 
"key3"=Lexeme{tokenType=OBJECT, value={"key31"=Lexeme{tokenType=STRING, value="value31", start=62, end=70}}, start=51, end=71}, 
"key4"=Lexeme{tokenType=ARRAY, value=[Lexeme{tokenType=NUMBER, value=123, start=83, end=85}, 
Lexeme{tokenType=NUMBER, value=345.78, start=88, end=93}, 
Lexeme{tokenType=NUMBER, value=13.45e90, start=96, end=103}, 
Lexeme{tokenType=NUMBER, value=-345.909, start=106, end=113}, 
Lexeme{tokenType=NUMBER, value=+245, start=116, end=119}], start=82, end=120}, 
"key5"=Lexeme{tokenType=BOOLEAN, value=true, start=136, end=139}, 
"key6"=Lexeme{tokenType=BOOLEAN, value=false, start=150, end=154}, 
"key7"=Lexeme{tokenType=ARRAY, value=[Lexeme{tokenType=OBJECT, value={"key711"=Lexeme{tokenType=STRING, value="value711", start=178, end=187}, 
"key712"=Lexeme{tokenType=STRING, value="value712", start=200, end=209}}, start=166, end=210}, 
Lexeme{tokenType=OBJECT, value={"key721"=Lexeme{tokenType=STRING, value="value721", start=224, end=233}, 
"key722"=Lexeme{tokenType=STRING, value="value722", start=246, end=255}}, start=212, end=256}], start=165, end=257}}

+------------------+
|  Formatted Json  |
+------------------+
{
	"key1" : "value1", 
	"key2" : "value2", 
	"key3" : {
		"key31" : "value31"
	}, 
	"key4" : [123, 345.78, 13.45e90, -345.909, +245], 
	"key5" : true, 
	"key6" : false, 
	"key7" : [
		{
			"key711" : "value711", 
			"key712" : "value712"
		}, 
		{
			"key721" : "value721", 
			"key722" : "value722"
		}
	]
}

```

## TODO
1. The string with nested json or string with the inverted quotations needs to be handled <br>
   As per the rules written now, a string is considered till an end quote is encountered.
2. Escape codes needs to be added which fixes the above too.
3. The service can handle files upto 50KB size only. If bigger files are uploaded it breaks with `StackOverflowException` because of tokens building huge number of objects into the memory and multiple stack frames being consumed. This can be fixed by the idea of streaming the files in chunks.

## References
Used the below to write Automata for tokenizing the input into corresponding Token:
[json-reference](https://www.json.org/json-en.html)