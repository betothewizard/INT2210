# Week 2

#### UFClient1
```java
import edu.princeton.cs.algs4.*;

public class UFClient { 
   public static void main(String[] args) { 
      int N = StdIn.readInt(); 
      UF uf = new UF(N); 
      while (!StdIn.isEmpty()) { 
         int p = StdIn.readInt(); 
         int q = StdIn.readInt(); 
         if (!uf.connected(p, q)) { 
            uf.union(p, q); StdOut.println(p + " " + q); 
         } 
      } 
   }
}
```

#### UFClient2
```java
import edu.princeton.cs.algs4.*;

public class UFClient2 {
    public static void main(String[] args) {
        int N = StdIn.readInt();
        int cnt = 0;
        UF uf = new UF(N);
        while (!StdIn.isEmpty()) {
            int p = StdIn.readInt();
            int q = StdIn.readInt();
            uf.union(p, q);
            ++cnt;
            if (uf.count() == 1) {
                StdOut.println(cnt);
                return;
            }
        }
        StdOut.println("FAILED");
    }
}

```

#### TwoSum
```java
import java.util.*;

public class TwoSum {
    public static int binarySearch(List<Integer> a, int l, int r, int val) {
        while (l <= r) {
            int mid = l + (r - l) / 2;
            if (val < a.get(mid)) r = mid - 1;
            else if (val > a.get(mid)) l = mid + 1;
            else return mid;
        }
        return -1;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        List<Integer> a = new ArrayList<>();
        while (sc.hasNextInt()) {
            a.add(sc.nextInt());
        }
        int n = a.size();
        Collections.sort(a);
        for (int i = 0; i < n - 1; ++i) {
            int key = binarySearch(a, i + 1, n - 1, -a.get(i));
            if (key != -1) System.out.println(a.get(i) + " " + a.get(key));
        }
    }
}
```

#### ThreeSum
```java
import java.util.*;

public class ThreeSum {
    public static int binarySearch(List<Integer> a, int l, int r, int val) {
        while (l <= r) {
            int mid = l + (r - l) / 2;
            if (val < a.get(mid)) r = mid - 1;
            else if (val > a.get(mid)) l = mid + 1;
            else return mid;
        }
        return -1;
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        List<Integer> a = new ArrayList<>();
        while (sc.hasNextInt()) {
            a.add(sc.nextInt());
        }
        int n = a.size();
        Collections.sort(a);
        for (int i = 0; i < n - 2; ++i) {
            for (int j = i + 1; j < n - 1; ++j) {
                int key = binarySearch(a, j + 1, n - 1, -a.get(i) - a.get(j));
                if (key != -1) System.out.println(a.get(i) + " " + a.get(j) + " " + a.get(key));
            }
        }
    }
}

```