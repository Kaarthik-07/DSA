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

