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


