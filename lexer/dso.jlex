package lexer;
import java_cup.*;

%%

%line
%column

%cup
%unicode
%standalone

%class DsoLexer

/* Identificadores: um identificador começa com uma letra ou underline e é seguido por qualquer quantidade de letras, underline e dígitos.
Apenas letras entre A/a e Z/z são permitidos, há diferença entre maiúscula e minúscula.
Palavras-chave não são identificadores; */

/* Literais Inteiros: uma sequência de dígitos iniciada com qualquer um dos dígitos entre 1 e 9 e seguida por qualquer número de dígitos entre 0 e 9.
O dígito 0 também é um inteiro. */

letters = [A-Za-z]
underline = [_]
digit = [0-9]
integer = {digit}*
first = {letters} | {underline}
alphanumerics = {letters}|{digit}|{underline}
identifiers = {first}({alphanumerics})*
whitespace = {linebreak}|[ \t\f]
linebreak = \r|\n|\r\n

/* Comentários: os dois tipos de comentário são possíveis, comentários de linha, iniciando com // e indo até o final da linha, e comentários de múltiplas linhas, que consistem de qualquer texto entre /* e */, sem considerar aninhamento */

comment = {multilinecomment} | {onelinecomment}
multilinecomment = "/*" ~"*/"
onelinecomment = "//" ~{linebreak}

%%
/* Operadores: &&, <, ==, !=, +, -, *, !; 
(não há operador de divisão, por enquanto) */

"&&" |
"<"	 |
"==" |
"!=" |
"+"	 |
"-"	 |
"*"	 |
"!"	 |

/* Delimitadores e pontuação: ; . , = ( ) { } [ ] */

";"	 |
"."	 |
","	 |
"="	 |
"("	 |
")"	 |
"{"	 |
"}"	 |
"["	 |
"]"	 { System.out.println("Token " + yytext()); }

/* Palavras reservadas: boolean, class, public, extends, static, void, main, String, int, while,
if, else, return, length, true, false, this, new, System.out.println; */

boolean	|
class	|
public	|
extends	|
static	|
void	|
main	|
String	|
int 	|
while	|
if		|
else	|
return	|
length	|
true	|
false	|
this	|
new		|
System.out.println	{ System.out.println("Palavra reservada: " + yytext()); }

{integer}		{ System.out.println("Inteiro: " + yytext()); }
{identifiers}	{ System.out.println("Identificador: " + yytext()); }

/* Comentários e whitespace não tem significado algum, exceto para separar os tokens. */
{comment} 	 { /* ignora */ }
{whitespace} { /* ignora */ } 
. 			 { throw new RuntimeException("Caractere ilegal! '" + yytext() + "' na linha: " + yyline + ", coluna: " + yycolumn); }