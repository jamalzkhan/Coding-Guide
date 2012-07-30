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


