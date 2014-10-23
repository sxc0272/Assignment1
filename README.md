Assignment1
===========

import java.io.*;
import java.util.Arrays;
import java.util.StringTokenizer;

public class driver {
	static BufferedReader buf;
	
	static int charClass;
	static char[] lexeme;
	static final int EOF=-1;
	static char nextChar;
	static int lexLen;
	static int token;
	static int nextToken;
	static final int LETTER=0;
	static final int DIGIT=1;
	static final int UNKNOWN=99;
	static final int INT_LIT=10;
	static final int IDENT=11;
	static final int ASSIGN_OP=20;
	static final int ADD_OP=21;
	static final int SUB_OP=22;
	static final int MULT_OP=23;
	static final int DIV_OP=24;
	static final int LEFT_PAREN=25;
	static final int RIGHT_PAREN=26;
	/**
	 * @param args
	 */
	public static void main(String[] args)throws IOException {
		
		
		buf=new BufferedReader( new FileReader("C:/Users/Sowmya-Siri/Desktop/sowmya.txt"));
		// TODO Auto-generated method stub

File filename=new File("C:/Users/Sowmya-Siri/Desktop/sowmya.txt");



if (!filename.exists())
{
	System.out.println("Cant open the file");
	}
else
{
	System.out.println("file present");
	
	 getChar();
	 do{
		 lex();
		 
	 }while(nextToken != EOF);    // error may occur
	}
	
	}


static void getChar() throws IOException
{
	
	nextChar = (char)(buf.read());
	//System.out.println(nextChar);
	if(nextChar!= EOF)
	{
		if(Character.isLetter(nextChar))
		{
			charClass=LETTER;
			//System.out.println(nextChar);
			
		}
		else if (Character.isDigit(nextChar))
		{
			 charClass=DIGIT;
			 //System.out.println(nextChar);		
		}
		else
		{
			 charClass=UNKNOWN;
			// System.out.println(nextChar);
		}
	}
	else
	{
	      System.out.println("done");
	      charClass= EOF;
	}
	}


public static int lex() throws IOException 
{
	lexeme=new char[100];
	 lexLen=0;
	getNonBlank();
	switch (charClass) {
	
	case LETTER:
		addChar();
		getChar();
		while (charClass==LETTER || charClass==DIGIT)
		{
			addChar();
			getChar();
		}
		nextToken= IDENT;
		break;
		
	case DIGIT:
		addChar();
		getChar();
		while (charClass== DIGIT){
			addChar();
			getChar();
		}
		nextToken=INT_LIT;
		break;
		
	case UNKNOWN:
		lookup(nextChar);
		getChar();
		break;
		
	case EOF:
		nextToken= EOF;
		lexeme[0]='E';
		lexeme[1]='O';
		lexeme[2]='F';
		
	}
	
	
	
	System.out.println("Next token is " +nextToken +   "Next lexeme" +String.valueOf(Arrays.copyOf(lexeme, lexLen))); 
  return nextToken;
	}


private static void addChar() {
	// TODO Auto-generated method stub
	if (lexLen <=98)
	{
		lexeme[lexLen++]=nextChar;
		lexeme[lexLen]=0;
		
		
	}
	else
	{
		System.out.println("Error-lexeme is too long \n ");
	}
}
	
public static int lookup(char ch)
{
	switch (ch) {
	case '(':
		addChar();
		nextToken=LEFT_PAREN;		
		break;
		
	case ')':
		addChar();
		nextToken=RIGHT_PAREN;
		break;
		
	case '+':
		addChar();
		nextToken=ADD_OP;
		break;
		
	case'-':
		addChar();
		nextToken=SUB_OP;
		break;
		
	case '*':
		addChar();
		nextToken=MULT_OP;
		break;
		
	case'/':
		addChar();
		nextToken=DIV_OP;
		break;
		
	default:
		addChar();
		nextToken=EOF;
		break;
	}
	
	return nextToken;
	}
	
static void getNonBlank() throws IOException
{
	while(nextChar==' ')
	{
		getChar();
	}
	}
}






