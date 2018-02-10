## A

```cpp
#include<iostream>
using namespace std;
const int N = 1e6 + 10;
int n;
int main() {
    int T; cin >> T;
    while (T--) {
        cin >> n;
        bool ok = false;
        for (int a = 0; a <= n / 3; a++) {
            int b = n - a * 3;
            if (b % 7 == 0) ok = true;
        }
        cout << (ok ? "YES" : "NO") << endl;
    }
    return 0;
}
```

```java
import java.util.ArrayList;
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner cin = new Scanner(System.in);
        int T = cin.nextInt();
        while (T-- > 0) {
            int n = cin.nextInt();
            boolean ok = false;
            for (int i = 0; i <= n / 3; i++) {
                if ((n - i * 3) % 7 == 0) {
                    ok = true;
                }
            }
            System.out.println(ok ? "YES" : "NO");
        }
    }
}

```

---

## B

```cpp
#include<iostream>
using namespace std;
const int N = 1e5 + 10;
int n;
int a[N];
int main() {
    cin >> n;
    int mi = INT_MAX;
    for (int i = 0; i < n; i++) {
      cin >> a[i];
      mi = min(mi, a[i]);
    }
    int pre = -1;
    int res = INT_MAX;
    for (int i = 0; i < n; i++) {
      if (mi == a[i]) {
        if (pre != -1) {
          res = min(res, i - pre);
        }
        pre = i;
      }
    }
    cout << res << endl;
    return 0;
}
```

```java
import java.util.ArrayList;
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner cin = new Scanner(System.in);
        int n = cin.nextInt();
        int[] a = new int[n];
        int mi = Integer.MAX_VALUE;
        for (int i = 0; i < n; i++) {
            a[i] = cin.nextInt();
            mi = Math.min(mi, a[i]);
        }
        int res = Integer.MAX_VALUE;
        int pre = -1;
        for (int i = 0; i < n; i++) {
            if (mi == a[i]) {
                if (pre != -1) {
                    res = Math.min(res, i - pre);
                }
                pre = i;
            }
        }
        System.out.println(res);
    }
}
```

---

## C

```cpp
#include<iostream>
#include<unordered_map>
using namespace std;
const int N = 1e6 + 10;
int n;
int a[N];
int main() {
    int T; scanf("%d", &T);
    while (T--) {
        unordered_map<int, int> mp;
        scanf("%d", &n);
        int x;
        int res = 0;
        int j = 0;
        for (int i = 0; i < n; i++) {
            scanf("%d", a + i);
            mp[a[i]]++;
            while (mp[a[i]] > 1) {
                mp[a[j]]--;
                j++;
            }
            res = max(res, i - j + 1);
        }
        printf("%d\n", res);
    }
    return 0;
}
```

```java
import java.util.ArrayList;
import java.util.HashMap;
import java.util.Map;
import java.util.Scanner;

public class Main {
    public static void main(String[] args) {
        Scanner cin = new Scanner(System.in);
        int T = cin.nextInt();
        while (T-- > 0) {
            int n = cin.nextInt();
            int[] a = new int[n];
            for (int i = 0; i < n; i++) {
                a[i] = cin.nextInt();
            }

            Map<Integer, Integer> map = new HashMap<Integer, Integer>();

            int pre = 0;
            int res = 0;
            for (int i = 0; i < n; i++) {
                while (map.containsKey(a[i])) {
                    map.remove(a[pre]);
                    pre++;
                }
                res = Math.max(res, i - pre + 1);
                map.put(a[i], 1);
            }
            System.out.println(res);

        }
    }
}

```

---

## D

```cpp
#include<iostream>
#include<set>
#include<vector>
#include<queue>
using namespace std;
const int N = 1e3 + 10;
int n, cas;
int a[N];
int main() {
    int T;
    cin >> T;
    while (T--) {
        cin >> cas >> n;
        cout << cas << " " << (n + 1) / 2 << endl;

        priority_queue<int, vector<int>> maxHeap;
        priority_queue<int, vector<int>, greater<int>> minHeap;

        int x;
        int cnt = 0;
        for (int i = 1; i <= n; i++) {
            cin >> x;
            if (i % 2) {
                if (minHeap.size() == 0 || minHeap.top() >= x) {
                    maxHeap.push(x);
                } else {
                    maxHeap.push(minHeap.top());
                    minHeap.pop();
                    minHeap.push(x);
                }
            } else {
                if (x >= maxHeap.top()) {
                    minHeap.push(x);
                } else {
                    minHeap.push(maxHeap.top());
                    maxHeap.pop();
                    maxHeap.push(x);
                }
            }
            if (i % 2) {
                int res = maxHeap.top();
                if (cnt == 10) {
                    cnt = 0;
                    cout << endl;
                }
                if (cnt > 0) cout << " ";
                cout << res;
                cnt++;
            }
        }
        cout << endl;


    }
    return 0;
}

```

```java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner cin = new Scanner(System.in);
        int T = cin.nextInt();
        while (T-- > 0) {
            int cas = cin.nextInt(), n = cin.nextInt();
            int[] a = new int[n];
            PriorityQueue<Integer> minHeap = new PriorityQueue<>();
            PriorityQueue<Integer> maxHeap = new PriorityQueue<>(Collections.reverseOrder());

            System.out.println(cas++ + " " + (n + 1) / 2);
            int cnt = 0;
            for (int i = 1; i <= n; i++) {
                int x = cin.nextInt();
                if (i % 2 == 1) {
                    if (minHeap.isEmpty() || minHeap.peek() >= x) {
                        maxHeap.offer(x);
                    } else {
                        maxHeap.offer(minHeap.peek());
                        minHeap.poll();
                        minHeap.offer(x);
                    }
                } else {
                    if (x >= maxHeap.peek()) {
                       minHeap.offer(x);
                    } else {
                        minHeap.offer(maxHeap.peek());
                        maxHeap.poll();
                        maxHeap.offer(x);
                    }
                }

                if (i % 2 == 1) {
                    int res = maxHeap.peek();
                    if (cnt == 10) {
                        cnt = 0;
                        System.out.println();
                    }
                    if (cnt > 0) System.out.print(" ");
                    System.out.print(res);
                    cnt++;
                }
            }
            System.out.println();

        }

    }
}
```



