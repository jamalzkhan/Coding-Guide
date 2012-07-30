% Jamming the coding interview
% Jamal Khan

## Interesting Links

- [Bit Hacks]:<http://graphics.stanford.edu/~seander/bithacks.html>
- [XOR Linked Lists]:<http://en.wikipedia.org/wiki/XOR_linked_list>

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

## Data Structures

### Linked List

- We use links for the Linked List, so we define a link as follows:

~~~~ {.java}


public class Link<V>{

	private V value;
	private Link<V> next;

	public Link(V value) {
		this.value = value;
	}

	public V getValue() {
		return value;
	}

	public Link<V> getNext() {
		return next;
	}

	public void setNext(Link<V> next) {
		this.next = next;
	}

	public void setValue(V value) {
		this.value = value;
	}

}


~~~~

- The code for an in order linked list is as follows:

~~~~ {.java}

public class LinkedList<V extends Comparable<V>> {
	
	private Link<V> head;
	private int size;
	
	public LinkedList() {
		head = null;
		size = 0;
	}
	
	public void print(){
		Link<V> curr = head;
		while (curr != null){
			System.out.println(curr.getValue());
			curr = curr.getNext();
		}
	}
	
	public void add(V value){
		if (head == null){
			head = new Link<V>(value);
			size++;
		}
		else if (value.compareTo(head.getValue()) < 0) {
			Link<V> curr = new Link<V>(value);
			curr.setNext(head);
			head = curr;
			size++;
		}
		else {
			Link<V> prev = head;
			Link<V> curr = prev.getNext();
			
			while (curr != null && value.compareTo(curr.getValue()) > 0){
				prev = curr;
				curr = curr.getNext();
			}

			prev.setNext(new Link<V>(value));
			if (curr != null)
				prev.getNext().setNext(curr);
			size++;		
		}
		
	}
}

~~~~

### Binary Search Tree

- Once again Binary Tree nodes are used for a Binary Search Tree and the data structure for a node is below:

~~~~ {.java}


public class BTreeEntry<V> {
	
	private V value;
	private BTreeEntry<V> left;
	private BTreeEntry<V> right;
	
	public BTreeEntry(V value) {
		this.value = value;
	}
	public V getValue(){
		return value;
	}
	
	public BTreeEntry<V> getRight(){
		return right;
	}
	
	public BTreeEntry<V> getLeft(){
		return left;
	}
	
	public void setRight(BTreeEntry<V> right){
		this.right = right;
	}
	
	public void setLeft(BTreeEntry<V> left){
		this.left = left;
	}
	

}

~~~~


- The main code for the Binary Search Tree is below
- There are two ways to add, the recursive way (put(), which uses addNode() or the iterative way add())

~~~~ {.java}


public class BTree<V extends Comparable<V>> {


	private BTreeEntry<V> root;
	private int size;

	public void addNode(V value, BTreeEntry<V> node){
		if (node.getValue().compareTo(value) >0){
			if (node.getLeft() == null){
				node.setLeft(new BTreeEntry<V>(value));
				size++;
				return;
			}
			addNode(value, node.getLeft());
		}
		else {
			if (node.getRight() == null){
				node.setRight(new BTreeEntry<V>(value));
				size++;
				return;
			}
			addNode(value, node.getRight());
		}
	}

	public void put(V value){
		if (root == null){
			root = new BTreeEntry<V>(value);
			size++;
		}
		else {
			addNode(value, root);
		}
	}

	public BTree() {
		size = 0;
	}

	public void add(V value){
		if (root == null){
			root = new BTreeEntry<V>(value);
			size++;
		}
		else {
			BTreeEntry<V> node = root;
			while (node != null){
				if (node.getValue().compareTo(value) > 0){
					if (node.getLeft() == null){
						node.setLeft(new BTreeEntry<V>(value));
						size++;
						return;
					}
					node = node.getLeft();
				}
				else {
					if (node.getRight() == null){
						node.setRight(new BTreeEntry<V>(value));
						size++;
						return;
					}
					node = node.getRight();
				}
				
			}
		}
	}



	public void printTree(BTreeEntry<V> node){
		if (node != null){
			printTree(node.getLeft());
			System.out.println(node.getValue());
			printTree(node.getRight());
		}
	}

}
~~~~

### Stack
- We will use the same link structure as in the linked list to define a stack.
- A stack has two main methods pop and push.

~~~~ {.java}

public class Stack<V> {

	
	private Link<V> head;

	private int size;
	
	public Stack() {
		head = null;
	}
	
	public void push(V value){
		Link<V> link = new Link<V>(value);
		link.setNext(head);
		head = link;
		size++;
	}
	
	public Link<V> pop(){
		Link<V> toReturn = head;
		head = head.getNext();
		size--;
		return toReturn;
	}
	
	public void printStack(){
		Link<V> node = head;
		while (node != null){
			System.out.println(node.getValue());
			node = node.getNext();
		}
		
		
	}
}


~~~~

### Hash Tables

- Below is an implemented Hash Table and it's usage.

~~~~ {.java}


public class HashTable<V extends Comparable<V>> {


	private LinkedList<V> [] hashtable;
	private int size;
	private final int LIMIT = 26;
	
	public void add(V value){
		if (hashtable[hash(value)] == null) {
			hashtable[hash(value)] = new LinkedList<V>();
			hashtable[hash(value)].add(value);
		}
		else {
			hashtable[hash(value)].add(value);
		}
		size++;
	}
	
	public HashTable() {
		hashtable = new LinkedList [LIMIT];	
	}
	
	
	private int hash(V value){
		return (value.toString().charAt(0)) % LIMIT;
	}
	
	public void printTable(){
		
		for (int i = 0 ; i<LIMIT;i++){
			System.out.println(i + ":");
			if (hashtable[i] != null){
				hashtable[i].print();
			}
			else {
				
			}
		}
	}
	
	public static void main(String[] args) {
		HashTable<String> table = new HashTable<String>();
		table.add("Jamal");
		table.add("Rafal");
		table.add("Danish");
		table.add("Alessandro");
		table.add("Alex");
		table.printTable();
	}
	
	
}

~~~~


## Graphs

### General Representation in Java

- Below is the representation I will use of a node, a graph and a visited structure.

~~~~ {.java}

/*
 *  Node representation 
 */

class Node<V> implements Comparable<Node>{
		
		String value;
		
		public Node(String value) {
			this.value = value;
		}
		public String getValue(){
			return this.value;
		}
		public void setValue(String value){
			this.value = value;
		}
		public int compareTo(Node node) {
			return this.value.compareTo(node.value);
		}
		
		
}

/*
 * Graph representation
 */

private static HashMap<Node, ArrayList<Node>> graph;
  
/* 
 * Visited structure for recording whether a node is visited or not
 */
  
private static HashMap<Node, Boolean> visited;	

~~~~

### Depth First Search

~~~~ {.java}

public static void DFS(Node n){
		
		visited.put(n, true);
		System.out.println(n.s);

		for (Node node : graph.get(n)){
			if (!visited.get(node)){
				visited.put(node, true);
				DFS(node);
			}
		}

	}

~~~~

### Breath First Search

~~~~ {.java}

public static void BFS(Node n){
		Queue<Node> q = new LinkedList<Node>();
		q.add(n);
		visited.put(n, true);
		System.out.println(n.s);

		while (!q.isEmpty()){
			Node current = q.remove();
			for (Node r : graph.get(current)){
				if (!visited.get(r)){
					visited.put(r, true);
					System.out.println(r.s);
					q.add(r);
				}
			}
		}

}


~~~~


## Sorting & Searching

### Binary Search
- Complexity is O(n)

Solution

~~~~ {.java .highlighting}
int bSearch(int n, int [] array, int start, int end){
  
  if (start < end){
    int middle = (start + end) / 2;
    if (array[middle] == n)
      return middle;
    else if (array[middle] < n)
      bSearch(n, array, middle+1, end);
    else
      bSearch(n, array, start, middle-1);
  }
  return -1
  
}
~~~~

### Merge Sort
- Complexity is 0(n*log(n))

~~~~ {.python}

def mergeSort(array):
  
  if (len(array)) == 1):
    return array
  
  half = len(array)/2
  left = []
  right = []
  
  for i in range(0, half):
    left.append(array[i])
  
  for i in range(half, len(A)):
    right.append(array[i])
  
  return merge(mergeSort(left), mergeSort(right))
  
def merge(left, right):
  
  result = []
  
  while len(left) > 0 || len(right) >0:
    if len(left) > 0 && len(right) > 0:
      if left[0] > right[0]:
        result.append(left[0])
        left = left[1:]
      else:
        result.append(right[0])
        right = right[1:]
    elif len(left) > 0:
      result.append(left[0])
      left = left[1:]
    else
      result.append(right[0])
      right = right[1:]
      
  return result

~~~~

### Insertion Sort

~~~~ {.python}

def insertionSort(a):
  for i in range (1, len(a)):
    value = a[i]
    j = i - 1
    done = False
    while done == False:
      if a[j] > a[j+1]:
        a[j+1] = a[j]
        j = j - 1
        if j < 0:
          done = True
      else:
        done = True
      a[j+1] = value
  return a

~~~~


### Quick Sort


~~~~ {.python}

def quickSort(a, start, end):

  if (start < end):
    pivot = a[end]
    p = start
    for i in range(start, end):
      if a[i] < pivot:
        swap(a, i, p)
        p = p + 1
        swap(a, p, end)
  
      quickSort(a, start, p-1)
      quickSort(a, p+1, end)
  
  return a
  
def swap(a, i, j):
  n = a[i]
  a[i] = a[j]
  a[j] = n

~~~~

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



