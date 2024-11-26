**BST** is for oraganizing and storing data in sorted manner 

 A Binary Search Tree is,
	-->  Every Node's *Left Child is lesser than  the node*
	--> Whereas the *Right child is greater than it*


> [!TIP]
> **BST** never contains duplicates elements

### Why we have to use BST Tree over a BST Array

#### --> Downside of using a sorted array
   - If we need to _add/delete_ any elements in the array to maintain the *_Sorted Property_ it Takes a **O(n) Time**.
#### --> In case of BST:
-  The Same _add/delete_ operation takes a time of _O(log n)_* which is efficient compared to an Array

### **1. Implementation of BST**  

1. **Node creation**
```java
class Node {
    int value;
    Node left, right;

    Node(int value) {
        this.value = value;
        left = right = null; // Initially, no child nodes
    }
}

public class bst{
    public static void main(String[] args) {
        Node root = new Node(50);

        root.left = new Node(30);
        root.right = new Node(70);

        root.left.left = new Node(45);
        root.right.right = new Node(90);

        System.out.println("Root value: " + root.value);
        System.out.println("Left value: " + root.left.value);
        System.out.println("Right value: " + root.right.value);
        System.out.println(" root left value: " + root.left.left.value);
        System.out.println("root Right value: " + root.right.right.value);
    }
}

```


2. **Insertion in BST**:
```java
class Node {
    int value;
    Node left, right;

    Node(int value) {
        this.value = value;
        left = right = null; 
    }
}

class bst{
    static Node insert(Node root, int value) {
        if (root == null) {
            return new Node(value); 
        }

        if (value < root.value) {
            root.left = insert(root.left, value);
        }
        else if (value > root.value) {
            root.right = insert(root.right, value);
        }
        return root;
    }

    static void inorder(Node root) {
        if (root != null) {
            inorder(root.left); 
            System.out.print(root.value + " "); 
            inorder(root.right); 
        }
    }

    public static void main(String[] args) {
        Node root = null;

        root = insert(root, 50);
        root = insert(root, 30);
        root = insert(root, 20);
        root = insert(root, 40);
        root = insert(root, 23);
        root = insert(root, 70);
        root = insert(root, 60);
        root = insert(root, 80);

        System.out.print("Inorder Traversal of the BST: ");
        inorder(root); // Output: 20 23 30 40 50 60 70 80
        System.out.print("Inorder Traversal of the BST: "+ root.value);
    }
}

```


2. Validate a BST , TOP , LEFT , RIGHT, BOTTOM view
```java
import java.util.*;

class Node {
    int value;
    Node left, right;

    Node(int value) {
        this.value = value;
        left = right = null;
    }
}

class bst {

    static Node insert(Node root, int value) {
        if (root == null) {
            return new Node(value);
        }
        if (value < root.value) {
            root.left = insert(root.left, value);
        } else {
            root.right = insert(root.right, value);
        }
        return root;
    }

    static boolean isBST(Node root, int min, int max) {
        if (root == null) return true;
        if (root.value < min || root.value > max) return false;
        return isBST(root.left, min, root.value - 1) && isBST(root.right, root.value + 1, max);
    }

    static void topView(Node root) {
        if (root == null) return;
        
        Map<Integer, Integer> map = new TreeMap<>();
        Queue<Pair> queue = new LinkedList<>();
        queue.add(new Pair(root, 0));
        
        while (!queue.isEmpty()) {
            Pair temp = queue.poll();
            Node currentNode = temp.node;
            int hd = temp.hd;

            if (!map.containsKey(hd)) {
                map.put(hd, currentNode.value);
            }

            if (currentNode.left != null) {
                queue.add(new Pair(currentNode.left, hd - 1));
            }
            if (currentNode.right != null) {
                queue.add(new Pair(currentNode.right, hd + 1));
            }
        }
        
        for (int value : map.values()) {
            System.out.print(value + " ");
        }
        System.out.println();
    }

    static void bottomView(Node root) {
        if (root == null) return;

        Map<Integer, Integer> map = new TreeMap<>();
        Queue<Pair> queue = new LinkedList<>();
        queue.add(new Pair(root, 0));

        while (!queue.isEmpty()) {
            Pair temp = queue.poll();
            Node currentNode = temp.node;
            int hd = temp.hd;

            map.put(hd, currentNode.value);

            if (currentNode.left != null) {
                queue.add(new Pair(currentNode.left, hd - 1));
            }
            if (currentNode.right != null) {
                queue.add(new Pair(currentNode.right, hd + 1));
            }
        }

        for (int value : map.values()) {
            System.out.print(value + " ");
        }
        System.out.println();
    }

    static void leftView(Node root) {
        if (root == null) return;

        Queue<Node> queue = new LinkedList<>();
        queue.add(root);
        while (!queue.isEmpty()) {
            int n = queue.size();
            for (int i = 0; i < n; i++) {
                Node currentNode = queue.poll();
                if (i == 0) {
                    System.out.print(currentNode.value + " ");
                }
                if (currentNode.left != null) {
                    queue.add(currentNode.left);
                }
                if (currentNode.right != null) {
                    queue.add(currentNode.right);
                }
            }
        }
        System.out.println();
    }

    static void rightView(Node root) {
        if (root == null) return;

        Queue<Node> queue = new LinkedList<>();
        queue.add(root);
        while (!queue.isEmpty()) {
            int n = queue.size();
            for (int i = 0; i < n; i++) {
                Node currentNode = queue.poll();
                if (i == n - 1) {
                    System.out.print(currentNode.value + " ");
                }
                if (currentNode.left != null) {
                    queue.add(currentNode.left);
                }
                if (currentNode.right != null) {
                    queue.add(currentNode.right);
                }
            }
        }
        System.out.println();
    }

    static class Pair {
        Node node;
        int hd;
        Pair(Node node, int hd) {
            this.node = node;
            this.hd = hd;
        }
    }

    public static void main(String[] args) {
        Node root = null;

        root = insert(root, 50);
        root = insert(root, 30);
        root = insert(root, 20);
        root = insert(root, 40);
        root = insert(root, 70);
        root = insert(root, 60);
        root = insert(root, 80);

        System.out.print("Top View of the BST: ");
        topView(root);

        System.out.print("Bottom View of the BST: ");
        bottomView(root);

        System.out.print("Left View of the BST: ");
        leftView(root);

        System.out.print("Right View of the BST: ");
        rightView(root);

        boolean isValid = isBST(root, Integer.MIN_VALUE, Integer.MAX_VALUE);
        System.out.println("Is this a valid BST? " + (isValid ? "Yes" : "No"));
    }
}
```


**OUTPUT:**

![Screenshot from 2024-11-25 13-39-58](https://github.com/user-attachments/assets/3ac813a0-e2b8-4d18-9822-d30780a2a1f6)



