# Về bờ :(

#### Về bờ 1
```java
import java.util.*;

public class Solution1 {
    public static PriorityQueue<Integer> left = new PriorityQueue<>();
    public static PriorityQueue<Integer> right = new PriorityQueue<>(Collections.reverseOrder());

    public static void add(int val) {
        if (!left.isEmpty() && val > left.peek()) {
            left.add(val);
        } else {
            right.add(val);
        }
        if (right.size() - left.size() == 2) {
            left.add(right.remove());
        } else if (left.size() - right.size() == 2) {
            right.add(left.remove());
        }
    }

    public static void remove() {
        if (right.size() >= left.size()) right.remove();
        else left.remove();
    }

    public static int med() {
        if (right.size() >= left.size()) {
            return right.peek();
        }
        return left.peek();
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int N = sc.nextInt();
        int M = sc.nextInt();
        for (int i = 0; i < N; ++i) {
            add(sc.nextInt());
        }
        for (int i = 0; i < M; ++i) {
            int q = sc.nextInt();
            switch (q) {
                case 1:
                    add(sc.nextInt());
                    break;
                case 2:
                    if (left.size() +  right.size() > 0) remove();
                    break;
                case 3:
                    if (left.size() + right.size() > 0) System.out.println(med());
                    else System.out.println(0);
                    break;
            }
        }
    }
}
```
#### Về bờ 2
```java
import java.util.PriorityQueue;
import java.util.Scanner;

public class Solution {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int N = sc.nextInt();
        int K = sc.nextInt();
        long[] a = new long[N];
        long curr = 0;
        for (int i = 0; i < N; ++i) {
            a[i] = sc.nextLong();
        }
        PriorityQueue<Long> pq = new PriorityQueue<>(K);
        for (int i = 0; i < K; ++i) {
            curr += a[i];
            pq.add(a[i]);
            System.out.print(curr + " ");
        }
        for (int i = K; i < N; ++i) {
            if (a[i] > pq.peek()) {
                curr += (a[i] - pq.peek());
                pq.poll();
                pq.add(a[i]);
            }
            System.out.print(curr + " ");
        }
    }
}
```
#### Về bờ 4
```java
import java.util.*;

public class Solution {
    public static int[] tree;

    public static void buildTree(int[] arr, int node, int b, int e) {
        if (b == e) {
            tree[node] = arr[b];
            return;
        }
        int mid = (b + e) / 2;
        buildTree(arr, 2 * node, b, mid);
        buildTree(arr, 2 * node + 1, mid + 1, e);
        tree[node] = Math.max(tree[2 * node], tree[2 * node + 1]);
    }

    public static int query(int node, int b, int e, int l, int r) {
        if (r < b || e < l)
            return Integer.MIN_VALUE;
        if (l <= b && e <= r)
            return tree[node];
        int mid = (b + e) / 2;
        int left = query(2 * node, b, mid, l, r);
        int right = query(2 * node + 1, mid + 1, e, l, r);
        return Math.max(left, right);
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int[] arr = new int[n];
        for (int i = 0; i < n; ++i) {
            arr[i] = sc.nextInt();
        }
        int q = sc.nextInt();
        tree = new int[4 * n];
        buildTree(arr, 1, 0, n - 1);
        for (int i = 0; i < q; ++i) {
            System.out.println(query(1, 0, n - 1, sc.nextInt()-1, sc.nextInt()-1));
        }
    }
}
```

#### Về bờ 5
```java
import java.io.*;
import java.util.*;

public class Solution {
    public static int[] tree;
    
    public static void buildTree(int[] arr, int node, int b, int e) {
        if (b == e) {
            tree[node] = arr[b];
            return;
        }
        int mid = (b + e) / 2;
        buildTree(arr, 2 * node, b, mid);
        buildTree(arr, 2 * node + 1, mid + 1, e);
        tree[node] = Math.min(tree[2 * node], tree[2 * node + 1]);
    }
    
    public static int query(int node, int b, int e, int l, int r){
        if (r < b || e < l) 
            return Integer.MAX_VALUE;
        if (b >= l && e <= r)
            return tree[node];
        int mid = (b + e) / 2;
        int left = query(2 * node, b, mid, l, r); 
        int right = query(2 * node + 1, mid + 1, e, l, r);
        return Math.min(left, right);
    }
    
    public static void update(int node, int b, int e, int id, int value) {
        if (id < b || id > e) 
            return;
        if (b == e) {
            tree[node] = value;
            return;
        }
        int mid = (b + e) / 2;
        update(2 * node, b, mid, id, value); 
        update(2 * node + 1, mid + 1, e, id, value);  
        tree[node] = Math.min(tree[2 * node], tree[2 * node + 1]);
    }
    
    
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        int n = sc.nextInt();
        int[] arr = new int[n];
        for (int i = 0; i < n; ++i) {
             arr[i] = sc.nextInt();
        }
        int q = sc.nextInt();
        tree = new int [4 * n];
        buildTree(arr, 1, 0, n-1);
        for (int i = 0; i < q; ++i) {
            switch (sc.nextInt()) {
                case 1:
                    System.out.println(query(1, 0, n - 1, sc.nextInt() - 1, sc.nextInt() - 1));
                    break;
                case 2:
                    update(1, 0, n - 1, sc.nextInt() - 1, sc.nextInt());
            }
        }
    }
}
```