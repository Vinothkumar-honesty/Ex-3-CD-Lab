# Ex-3-RECOGNITION-OF-A-VALID-ARITHMETIC-EXPRESSION-THAT-USES-OPERATOR-AND-USING-YACC
# Date:20.11.2026

# AIM
To write a yacc program to recognize a valid arithmetic expression that uses operator +,- ,* and /.
# ALGORITHM
1.	Start the program.
2.	Write a program in the vi editor and save it with .l extension.
3.	In the lex program, write the translation rules for the operators =,+,-,*,/ and for the identifier.
4.	Write a program in the vi editor and save it with .y extension.
5.	Compile the lex program with lex compiler to produce output file as lex.yy.c. eg $ lex filename.l
6.	Compile the yacc program with yacc compiler to produce output file as y.tab.c. eg $ yacc –d arith_id.y
7.	Compile these with the C compiler as gcc lex.yy.c y.tab.c
8.	Enter an arithmetic expression as input and the tokens are identified as output.
# PROGRAM
### .l
```

%{
#include "y.tab.h"
#include <stdio.h>
%}

%%
"="     { printf("\nOperator is EQUAL"); return '='; }
"+"     { printf("\nOperator is PLUS"); return PLUS; }
"-"     { printf("\nOperator is MINUS"); return MINUS; }
"/"     { printf("\nOperator is DIVISION"); return DIVISION; }
"*"     { printf("\nOperator is MULTIPLICATION"); return MULTIPLICATION; }

[a-zA-Z][a-zA-Z0-9]* {
    printf("\nIdentifier is %s", yytext);
    return ID;
}

[0-9]+  {
    printf("\nNumber is %s", yytext);
    return ID;
}

[ \t]+  ;
\n      { return 0; }
.       { return yytext[0]; }

%%

int yywrap()
{
    return 1;
}

```
### .y:

```

%{
#include <stdio.h>
#include <stdlib.h>
%}

%token ID PLUS MINUS MULTIPLICATION DIVISION

%%

statement : ID '=' E
{
    printf("\nValid arithmetic expression");
}
;

E : E PLUS ID
  | E MINUS ID
  | E MULTIPLICATION ID
  | E DIVISION ID
  | ID
;

%%

int main()
{
    printf("Enter an arithmetic expression:\n");
    yyparse();
    return 0;
}

int yyerror(char *s)
{
    printf("\nInvalid arithmetic expression");
    return 0;
}


```
# OUTPUT

<img width="1920" height="1200" alt="image" src="https://github.com/user-attachments/assets/9b80da6b-c799-4fc3-8ab2-524295de0e62" />


# RESULT
A YACC program to recognize a valid arithmetic expression that uses operator +,-,* and / is executed successfully and the output is verified.
