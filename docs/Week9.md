# Week 9

#### Java Map
```java
import java.util.HashMap;
import java.util.Map;
import java.util.Scanner;

public class Solution {
    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        Map map = new HashMap();
        int N = Integer.parseInt(sc.nextLine());
        for (int i = 0; i < N; ++i) {
            map.put(sc.nextLine(), Integer.parseInt(sc.nextLine()));
        }
        while (sc.hasNext()) {
            String line = sc.nextLine();
            if (map.containsKey(line)) {
                System.out.println(line + "=" + map.get(line));
            } else {
                System.out.println("Not found");
            }
        }
    }
}

```

#### Java HashSet
```java
import java.io.*;
import java.util.*;

public class Solution {

    public static void main(String[] args) {
        /* Enter your code here. Read input from STDIN. Print output to STDOUT. Your class should be named Solution. */
        Scanner sc = new Scanner(System.in);
        Set set = new HashSet();
        sc.nextLine();
        while (sc.hasNext()) {
            set.add(sc.nextLine());
            System.out.println(set.size());
        }
    }
}
```

#### Tree: Inorder Traversal
```java
    public static void inOrder(Node root) {
        if (root != null) {
            inOrder(root.left);
            System.out.print(root.data + " ");
            inOrder(root.right);
        }
    }
```
#### Tree: Preorder Traversal
```java
    public static void preOrder(Node root) {
        if (root != null) {
            System.out.print(root.data + " ");
            preOrder(root.left);
            preOrder(root.right);
        }
    }
```

#### Tree: Level Order Traversal
```java
    public static void levelOrder(Node root) {
        if (root == null) {
            return;
        }

        Queue<Node> queue = new LinkedList<>();
        queue.add(root);

        while (!queue.isEmpty()) {
            Node current = queue.poll();
            System.out.print(current.data + " ");

            if (current.left != null) {
                queue.add(current.left);
            }

            if (current.right != null) {
                queue.add(current.right);
            }
        }
    }
```

#### Closest Numbers (Merge Sort)
```java
import java.io.*;
import java.util.*;
import java.util.stream.*;

class Result {

    public static List<Integer> closestNumbers(List<Integer> arr) {
        List<Integer> sortedArr = mergeSort(arr);

        int minDifference = Integer.MAX_VALUE;
        for (int i = 0; i < sortedArr.size() - 1; i++) {
            int diff = sortedArr.get(i + 1) - sortedArr.get(i);
            minDifference = Math.min(minDifference, diff);
        }

        List<Integer> result = new ArrayList<>();
        for (int i = 0; i < sortedArr.size() - 1; i++) {
            int diff = sortedArr.get(i + 1) - sortedArr.get(i);
            if (diff == minDifference) {
                result.add(sortedArr.get(i));
                result.add(sortedArr.get(i + 1));
            }
        }

        return result;
    }

    private static List<Integer> mergeSort(List<Integer> arr) {
        if (arr.size() <= 1) {
            return arr;
        }

        int mid = arr.size() / 2;
        List<Integer> left = arr.subList(0, mid);
        List<Integer> right = arr.subList(mid, arr.size());

        left = mergeSort(new ArrayList<>(left));
        right = mergeSort(new ArrayList<>(right));

        return merge(left, right);
    }

    private static List<Integer> merge(List<Integer> left, List<Integer> right) {
        List<Integer> merged = new ArrayList<>();
        int i = 0, j = 0;

        while (i < left.size() && j < right.size()) {
            if (left.get(i) <= right.get(j)) {
                merged.add(left.get(i));
                i++;
            } else {
                merged.add(right.get(j));
                j++;
            }
        }

        while (i < left.size()) {
            merged.add(left.get(i));
            i++;
        }

        while (j < right.size()) {
            merged.add(right.get(j));
            j++;
        }

        return merged;
    }
}

public class Solution {
    public static void main(String[] args) throws IOException {
        BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bufferedWriter = new BufferedWriter(new FileWriter(System.getenv("OUTPUT_PATH")));

        int n = Integer.parseInt(bufferedReader.readLine().trim());

        List<Integer> arr = Stream.of(bufferedReader.readLine().replaceAll("\\s+$", "").split(" "))
            .map(Integer::parseInt)
            .collect(Collectors.toList());

        List<Integer> result = Result.closestNumbers(arr);

        bufferedWriter.write(
            result.stream()
                .map(Object::toString)
                .collect(Collectors.joining(" "))
            + "\n"
        );

        bufferedReader.close();
        bufferedWriter.close();
    }
}
```