# Week 5

#### Balanced Brackets
```java
import java.io.*;
import java.math.*;
import java.security.*;
import java.text.*;
import java.util.*;
import java.util.concurrent.*;
import java.util.function.*;
import java.util.regex.*;
import java.util.stream.*;
import static java.util.stream.Collectors.joining;
import static java.util.stream.Collectors.toList;

class Result {

    /*
     * Complete the 'isBalanced' function below.
     *
     * The function is expected to return a STRING.
     * The function accepts STRING s as parameter.
     */

    public static String isBalanced(String s) {
    // Write your code here
        Stack<Character> st = new Stack<>();
        int l = s.length();
        for (int i = 0; i < l; ++i) {
            char c = s.charAt(i);
            if (c == '(' || c == '[' || c == '{') {
                st.push(c);
            } else {
                if (!st.empty()) {
                    char top = st.pop();
                    if ((top == '(' && c == ')')
                            || (top == '[' && c == ']')
                            || (top == '{' && c == '}')) {
                        continue;
                    } else return "NO";
                } else return "NO";
            }
        }
        return (st.empty() ? "YES" : "NO");
    }

}

public class Solution {
    public static void main(String[] args) throws IOException {
        BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bufferedWriter = new BufferedWriter(new FileWriter(System.getenv("OUTPUT_PATH")));

        int t = Integer.parseInt(bufferedReader.readLine().trim());

        IntStream.range(0, t).forEach(tItr -> {
            try {
                String s = bufferedReader.readLine();

                String result = Result.isBalanced(s);

                bufferedWriter.write(result);
                bufferedWriter.newLine();
            } catch (IOException ex) {
                throw new RuntimeException(ex);
            }
        });

        bufferedReader.close();
        bufferedWriter.close();
    }
}
```

#### Queue Using Two Stacks
```java
import java.util.Scanner;
import java.util.Stack;

public class Solution {

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int q = scanner.nextInt();

        Stack<Integer> stack1 = new Stack<>();
        Stack<Integer> stack2 = new Stack<>();

        for (int i = 0; i < q; i++) {
            int queryType = scanner.nextInt();
            switch (queryType) {
                case 1:
                    int x = scanner.nextInt();
                    enqueue(stack1, x);
                    break;
                case 2:
                    dequeue(stack1, stack2);
                    break;
                case 3:
                    System.out.println(peek(stack1, stack2));
                    break;
            }
        }

        scanner.close();
    }

    private static void enqueue(Stack<Integer> stack1, int x) {
        stack1.push(x);
    }

    private static void dequeue(Stack<Integer> stack1, Stack<Integer> stack2) {
        if (stack2.isEmpty()) {
            while (!stack1.isEmpty()) {
                stack2.push(stack1.pop());
            }
        }
        if (!stack2.isEmpty()) {
            stack2.pop();
        }
    }

    private static int peek(Stack<Integer> stack1, Stack<Integer> stack2) {
        if (stack2.isEmpty()) {
            while (!stack1.isEmpty()) {
                stack2.push(stack1.pop());
            }
        }
        return stack2.peek();
    }
}
```

#### Selection Sort
```java
import java.util.Arrays;

public class Main {
    public static void selectionSort(int[] arr) {
        int n = arr.length;
        for (int i = 0; i < n - 1; i++) {
            int minIndex = i;
            for (int j = i + 1; j < n; j++) {
                if (arr[j] < arr[minIndex])
                    minIndex = j;
            }
            int temp = arr[minIndex];
            arr[minIndex] = arr[i];
            arr[i] = temp;
        }
    }

    public static void main(String[] args) {
        int[] arr = {5, 4, 3, 2, 1};
        selectionSort(arr);
        System.out.println(Arrays.toString(arr));
    }
}
```

#### Simple Text Editor
```java
import java.util.Scanner;
import java.util.Stack;

public class Solution {

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int q = scanner.nextInt();
        StringBuilder text = new StringBuilder();
        Stack<StringBuilder> undoStack = new Stack<>();
        for (int i = 0; i < q; i++) {
            int operationType = scanner.nextInt();
            switch (operationType) {
                case 1:
                    String appendString = scanner.next();
                    undoStack.push(new StringBuilder(text));
                    text.append(appendString);
                    break;
                case 2:
                    int k = scanner.nextInt();
                    undoStack.push(new StringBuilder(text));
                    int newLength = text.length() - k;
                    text.setLength(newLength < 0 ? 0 : newLength);
                    break;

                case 3:
                    int printIndex = scanner.nextInt() - 1;
                    if (printIndex >= 0 && printIndex < text.length()) {
                        System.out.println(text.charAt(printIndex));
                    }
                    break;
                case 4:
                    if (!undoStack.isEmpty()) {
                        text = undoStack.pop();
                    }
                    break;
            }
        }
        scanner.close();
    }
}
```

#### Equal Stacks
```java
import java.util.Scanner;
import java.util.Stack;

public class Solution {

    public static void main(String[] args) {
        Scanner scanner = new Scanner(System.in);
        int q = scanner.nextInt();
        StringBuilder text = new StringBuilder();
        Stack<StringBuilder> undoStack = new Stack<>();
        for (int i = 0; i < q; i++) {
            int operationType = scanner.nextInt();
            switch (operationType) {
                case 1:
                    String appendString = scanner.next();
                    undoStack.push(new StringBuilder(text));
                    text.append(appendString);
                    break;
                case 2:
                    int k = scanner.nextInt();
                    undoStack.push(new StringBuilder(text));
                    int newLength = text.length() - k;
                    text.setLength(newLength < 0 ? 0 : newLength);
                    break;

                case 3:
                    int printIndex = scanner.nextInt() - 1;
                    if (printIndex >= 0 && printIndex < text.length()) {
                        System.out.println(text.charAt(printIndex));
                    }
                    break;
                case 4:
                    if (!undoStack.isEmpty()) {
                        text = undoStack.pop();
                    }
                    break;
            }
        }
        scanner.close();
    }
}
```