# Week 7

#### Java String Reverse
```java
import java.io.*;
import java.util.*;

class Solution {

    public static void main(String[] args) throws IOException {
        BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(System.in));
        String s = bufferedReader.readLine().trim();

        String result = isPalindrome(s) ? "Yes" : "No";
        System.out.println(result);
    }

    public static boolean isPalindrome(String s) {
        int left = 0;
        int right = s.length() - 1;

        while (left < right) {
            if (s.charAt(left) != s.charAt(right)) {
                return false;
            }
            left++;
            right--;
        }

        return true;
    }
}
```

#### Jesse and Cookies
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
     * Complete the 'cookies' function below.
     *
     * The function is expected to return an INTEGER.
     * The function accepts following parameters:
     *  1. INTEGER k
     *  2. INTEGER_ARRAY A
     */

    public static int cookies(int k, List<Integer> A) {
        // Write your code here
        PriorityQueue<Integer> priorityQueue = new PriorityQueue<>(A);
        int operations = 0;

        while (priorityQueue.size() > 1 && priorityQueue.peek() < k) {
            int leastSweet = priorityQueue.poll();
            int secondLeastSweet = priorityQueue.poll();

            int newCookie = leastSweet + 2 * secondLeastSweet;
            priorityQueue.offer(newCookie);
            operations++;
        }

        return priorityQueue.peek() >= k ? operations : -1;
    }

}

public class Solution {
    public static void main(String[] args) throws IOException {
        BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bufferedWriter = new BufferedWriter(new FileWriter(System.getenv("OUTPUT_PATH")));

        String[] firstMultipleInput = bufferedReader.readLine().replaceAll("\\s+$", "").split(" ");

        int n = Integer.parseInt(firstMultipleInput[0]);

        int k = Integer.parseInt(firstMultipleInput[1]);

        List<Integer> A = Stream.of(bufferedReader.readLine().replaceAll("\\s+$", "").split(" "))
            .map(Integer::parseInt)
            .collect(toList());

        int result = Result.cookies(k, A);

        bufferedWriter.write(String.valueOf(result));
        bufferedWriter.newLine();

        bufferedReader.close();
        bufferedWriter.close();
    }
}
```

#### Java Priority Queue
```java
import java.util.ArrayList;
import java.util.List;
import java.util.PriorityQueue;

class Student implements Comparable<Student> {
    private int id;
    private String name;
    private double cgpa;

    public Student(int id, String name, double cgpa) {
        this.id = id;
        this.name = name;
        this.cgpa = cgpa;
    }

    public int getID() {
        return id;
    }

    public String getName() {
        return name;
    }

    public double getCGPA() {
        return cgpa;
    }

    @Override
    public int compareTo(Student other) {
        if (this.cgpa != other.cgpa) {
            return Double.compare(other.cgpa, this.cgpa);
        } else if (!this.name.equals(other.name)) {
            return this.name.compareTo(other.name);
        } else {
            return Integer.compare(this.id, other.id);
        }
    }
}

class Priorities {
    public List<Student> getStudents(List<String> events) {
        PriorityQueue<Student> priorityQueue = new PriorityQueue<>();

        for (String event : events) {
            String[] parts = event.split(" ");
            if (parts[0].equals("ENTER")) {
                int id = Integer.parseInt(parts[3]);
                String name = parts[1];
                double cgpa = Double.parseDouble(parts[2]);
                priorityQueue.add(new Student(id, name, cgpa));
            } else if (parts[0].equals("SERVED")) {
                priorityQueue.poll();
            }
        }

        List<Student> result = new ArrayList<>(priorityQueue);
        result.sort(null);
        return result;
    }
}
```

#### Find the Running Median
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
public static List<Double> runningMedian(List<Integer> a) {
        List<Double> medians = new ArrayList<>();
        PriorityQueue<Integer> maxHeap = new PriorityQueue<>(Collections.reverseOrder()); // Lower half
        PriorityQueue<Integer> minHeap = new PriorityQueue<>(); // Upper half

        for (int num : a) {
            addToHeaps(maxHeap, minHeap, num);
            balanceHeaps(maxHeap, minHeap);
            medians.add(getMedian(maxHeap, minHeap));
        }

        return medians;
    }

    private static void addToHeaps(PriorityQueue<Integer> maxHeap, PriorityQueue<Integer> minHeap, int num) {
        if (maxHeap.isEmpty() || num <= maxHeap.peek()) {
            maxHeap.add(num);
        } else {
            minHeap.add(num);
        }
    }

    private static void balanceHeaps(PriorityQueue<Integer> maxHeap, PriorityQueue<Integer> minHeap) {
        while (Math.abs(maxHeap.size() - minHeap.size()) > 1) {
            if (maxHeap.size() > minHeap.size()) {
                minHeap.add(maxHeap.poll());
            } else {
                maxHeap.add(minHeap.poll());
            }
        }
    }

    private static double getMedian(PriorityQueue<Integer> maxHeap, PriorityQueue<Integer> minHeap) {
        if (maxHeap.size() == minHeap.size()) {
            return (maxHeap.peek() + minHeap.peek()) / 2.0;
        } else {
            return maxHeap.size() > minHeap.size() ? maxHeap.peek() : minHeap.peek();
        }
    }
}

public class Solution {
    public static void main(String[] args) throws IOException {
        BufferedReader bufferedReader = new BufferedReader(new InputStreamReader(System.in));
        BufferedWriter bufferedWriter = new BufferedWriter(new FileWriter(System.getenv("OUTPUT_PATH")));

        int aCount = Integer.parseInt(bufferedReader.readLine().trim());

        List<Integer> a = IntStream.range(0, aCount).mapToObj(i -> {
            try {
                return bufferedReader.readLine().replaceAll("\\s+$", "");
            } catch (IOException ex) {
                throw new RuntimeException(ex);
            }
        })
            .map(String::trim)
            .map(Integer::parseInt)
            .collect(toList());

        List<Double> result = Result.runningMedian(a);

        bufferedWriter.write(
            result.stream()
                .map(Object::toString)
                .collect(joining("\n"))
            + "\n"
        );

        bufferedReader.close();
        bufferedWriter.close();
    }
}
```