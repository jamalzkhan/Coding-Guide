## Bit Stuff

### Swapping a variable without using a temporary variable

- This is about taking two variables and and swapping their values.
- There are two main ways of doing this, one is using XOR and the other is using addition and multiplication

- The addition method is below:

~~~~ {.java}
public static void swap(){
	
	int r = 12;
	int s = 5;
	
	System.out.println("r, " +  r + " s, " + s);
	
	r = r + s;
	s = r - s;
	r = r - s;
	
	System.out.println("r, " +  r + " s, " + s);
		
}

~~~~

- The XOR method is below:

~~~~ {.java}

public static void swap(){
		
		int r = 12;
		int s = 5;
		
		System.out.println("r, " +  r + " s, " + s);
		
		r = r ^ s;
		s = r ^ s;
		r = r ^ s;
		
		System.out.println("r, " +  r + " s, " + s);
			
	}


~~~~

