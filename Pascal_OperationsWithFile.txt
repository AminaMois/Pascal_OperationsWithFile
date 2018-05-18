{
This program reads text file and then prints on the screen words
with no repeating from each row.
}
program ReadFromFile;
uses crt;

{
Array of string WordArray is used to store words got from
the input string.
}

type WordArray = array[1 .. 5000] of string;

{
Procedure GetWords writes content between 'space' into the array
WordArray. Procedure GetWords returns number of words in the array.
}

//i - counter variable, used to check each character in the 
//	  string, to check for 'space'
//FirstLetterPosition - local variable, used to get content
//						from the string, if it is not 'space'
//WordCount - global variable, used to count words in the input string

procedure GetWords(s:string; var words:WordArray; var WordCount:integer);
var i, FirstLetterPosition:integer;
begin
	i := 1; //first character in the string
	WordCount := 0; //no words found yet
	while (i<=length(s)) do begin //while not the end of the string 
		if s[i]=' ' then begin //looking for word to start
			inc(i);			
		end else begin //word found
			FirstLetterPosition := i; //character is the first letter of word
			while s[i]<>' ' do begin //while word is not ended
				inc(i);				//check characters till the end of the word
			end;      //when no more characters
			inc(WordCount); //end of the word
			words[WordCount] := copy(s, FirstLetterPosition, i - FirstLetterPosition);
		end;		//stores words in the array WordArray
	end;
end;	

{
Procedure EqualWordCounter counts number of words, that appear in the
string more than 1 time.
}

//words - global variable, used to get access to words in the array
//WordCount - global variable, used to get number of words in the
//			string array. Procedure EqualWordCounter goes through
//			this number to find equal elements
//i, j, a,times, count, RepeatedWordCounter - local counters, used
//			to go through the elements in the array of words

procedure EqualWordCounter(words:WordArray; WordCount:integer);
type NonUniqueWords= array[1 .. 500] of string;
var i, j, a,times, count, RepeatedWordCounter:integer;
RepeatedWord:NonUniqueWords;
NoRepeating:boolean;
begin
	i:=1; //first element in the array of words
	count:=WordCount;
	RepeatedWordCounter:=0;
	while i<=(Count) do begin
		NoRepeating:=true;
		j:=i+1;
		times:=1;
		for a:=0 to RepeatedWordCounter do begin
			if words[i]=RepeatedWord[a] then begin
				NoRepeating:=false;			//checking for duplicate elements
			end;
		end;
		if NoRepeating=true then begin
			while j<=Count do begin
				if words[i]=words[j] then begin
					inc(times);//counts how many times word repeated
				end;
				inc(j);
			end;
		end;
		if times>1 then begin //store repeating word in the array
			inc(RepeatedWordCounter); 
			RepeatedWord[RepeatedWordCounter]:=words[i];
			writeln('WORD:   ', words[i],'   ', times,' times');
		end;
		inc(i);
	end;
end;

//f - file variable
//s - string variable, used to get string input
//words - elements of the string array WordArray

var f:text;
	s:string;
	words:WordArray;
	WordCount:integer;

begin
	writeln('This program displays words from the text file TextWordList.txt .');
	writeln('Words, that repeat more than 1 time.');
	assign(f, 'TextWordList.txt');
	reset(f);
	WordCount := 0; 
	while not eof(f) do begin
		readln(f, s);
		GetWords(s, words, WordCount);//finds content in the string
		EqualWordCounter(words, WordCount);{displays number of each word in the array}
	end;
	close(f);
end.