## String Algorithms

### Computing all substrings of a string

~~~~ {.java}

public static void subStrings(String s){
		
		for (int i = 0; i < s.length(); i++){
			for (int j = i; j < s.length(); j++){
				System.out.println(s.substring(i, j+1));
			}
		}
		
}

~~~~

### Reversing a String

- Code in Java is as follows
- New one

~~~~ {.java}

/*
 * Takes an array together with two numbers and swaps the two characters
 * at the particular place.
 */
private static char [] swap(char [] string, int i, int j){
	
	char c = string[i];
	string[i] = string[j];
	string[j] = c;
	
	return string;
}

/*
 * Takes a particular word without spaces and swaps reverses it
 */
public static char []  reverseWord(char [] string, int start, int end){
	
	for (int i = start; i<=(start+end)/2; i++){
		swap(string, i, end-(i-start));
	}
	return string;
}

/*
 * Given a particular sentence with (with no fullstop) reverses the ordering
 * of the words in it and returns a char array.
 * 
 */

private static char[] reverseSentence(char [] string){
	char [] reversedSentence = reverseWord(string, 0, string.length-1);
	
	System.out.println(reversedSentence);
	
	for (int i = 0; i<reversedSentence.length; i++){
		int j = i;
		
		
		while ((!(reversedSentence[i] == ' ')) && i < reversedSentence.length-1)
			i++;
		
		if ( reversedSentence[i] == ' ')
			reverseWord(reversedSentence, j, i-1);
		else 
			reverseWord(string, j, i);
	}
	
	return reversedSentence;
}




~~~~

### Palindrome

- Two functions are below:
- One is for checking if a string is a palindrome
- The second is for printing all palindromes in a string

~~~~ {.java}

  public static boolean isPalindrome(String s){
		for (int i = 0; i<s.length()/2; i++){
			if (s.charAt(i) != s.charAt(s.length()-(i+1)))
				return false;
		}
		return true;
	}
	
	public static void getPalindrome(String s){
	
	HashMap<String, Integer> p = new HashMap<String, Integer>();
	String d ="";
	
	for (int i = 0; i<s.length(); i++){
		for (int j = i+1; j < s.length(); j++){
			
			d = s.substring(i, j+1);
					
			if (isPalindrome(d)){
				if (p.containsKey(d))
					p.put(d, p.get(d)+1);
				else
					p.put(d, 1);
				
			}
		}
	}
	
	for (String r : p.keySet()){
		System.out.println(r + ", " + p.get(r));
	}

}



~~~~



