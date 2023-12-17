# Week 10

#### Tree: Height of a Binary Tree
```java
public static int height(Node root) {
        if (root == null) {
            return -1;
        }
        int leftHeight = height(root.left);
        int rightHeight = height(root.right);
        return Math.max(leftHeight, rightHeight) + 1;
    }
```

#### Binary Search Tree : Insertion
```java
    public static Node insert(Node root,int data) {
        if (root == null) {
            root = new Node(data);
            return root;
        }
        else if (data < root.data) {
            root.left = insert(root.left, data);
        } else if (data > root.data) {
            root.right = insert(root.right, data);
        }
        return root;
    }
```

#### Binary Search Tree : Lowest Common Ancestor
```java
    public static Node lca(Node root, int v1, int v2) {
        if (root == null || root.data == v1 || root.data == v2) return root;
        Node left = lca(root.left, v1, v2);
        Node right = lca(root.right, v1, v2);
        if (left != null && right != null) return root;
        if (left == null) return right;
        return left;     
    }
```

#### Is This a Binary Search Tree?
```java
    private static boolean isBSTUtil(Node root, int minValue, int maxValue) {
        if (root == null) {
            return true;
        }

        if (root.data <= minValue || root.data >= maxValue) {
            return false;
        }

        return isBSTUtil(root.left, minValue, root.data) && isBSTUtil(root.right, root.data, maxValue);
    }

    public static boolean checkBST(Node root) {
        return isBSTUtil(root, Integer.MIN_VALUE, Integer.MAX_VALUE);
    }
```
