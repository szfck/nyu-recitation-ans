## A

```cpp
#include<iostream>
#include<iomanip>
#include<algorithm>
#include<vector>
#include<string>
#include<cmath>
#include<map>
#include<string.h>
using namespace std;
int x[3], y[3];
long long cross() {
    // AB cross product with BC 
    // > 0 : left
    // < 0: right
    return 1ll * (x[1] - x[0]) * (y[2] - y[1]) - 1ll * (y[1] - y[0]) * (x[2] - x[1]);
}
int main() {
    for (int i = 0; i < 3; i++) {
        cin >> x[i] >> y[i];
    }
    long long res = cross();
    if (res == 0) {
        cout << "TOWARDS" << endl;
    } else if (res > 0) {
        cout << "LEFT" << endl;
    } else {
        cout << "RIGHT" << endl;
    }
    return 0;
}
```

```java
import java.io.*;
import java.lang.reflect.Array;
import java.util.*;

public class Main {

    public static void main(String[] args) throws Exception { new A().run(); }

}

class A {

    Scanner in;
    PrintWriter out;


    void solve() {
        long[] x = new long[3], y = new long[3];
        for (int i = 0; i < 3; i++) {
            x[i] = in.nextLong();
            y[i] = in.nextLong();
        }
        long res = cross(x, y);
        if (res == 0) {
            out.println("TOWARDS");
        } else if (res > 0) {
            out.println("LEFT");
        } else if (res < 0) {
            out.println("RIGHT");
        }
    }

    private long cross(long[] x, long[] y) {
        return (x[1] - x[0]) * (y[2] - y[1]) - (y[1] - y[0]) * (x[2] - x[1]);
    }

    void run() throws Exception {
        in = new Scanner(System.in);
        out = new PrintWriter(  System.out);

        solve();

        out.flush();
    }

}
```

---

## B

```cpp
#include<iostream>
#include<algorithm>
#include<queue>
#include<vector>
#include<string>
#include<string.h>
using namespace std;
const int N = 2e7 + 10;
const int INF = 0x3f3f3f3f;
#define pb push_back
#define mp make_pair
#define fi first
#define se second
int n, m;
int nxt[1000005];
string s;
// using properties of array next KMP, n - next[n] is the minimum cycle, then n / circular section is the answer
void kmp() {
    nxt[0] = nxt[1] = 0;
    int j = 0;
    for (int i = 2; i <= n; i++) {
        while (j && s[j] != s[i - 1]) j = nxt[j];
        if (s[j] == s[i - 1]) j++;
        nxt[i] = j;
    }
}
int main() {
    while (cin >> s) {
        if (s == ".") break;
        n = s.size();
        kmp();
        cout << n / (n - nxt[n]) << endl;
    }
    return 0;
}
```

```java
import java.io.*;
import java.lang.reflect.Array;
import java.util.*;

public class Main {

    public static void main(String[] args) throws Exception { new B().run(); }

}

class B {

    Scanner in;
    PrintWriter out;

    void solve() {
        while (in.hasNext()) {
            String s = in.next();
            if (s.equals(".")) break;
            int n = s.length();
            int[] nxt = new int[n + 1];
            kmp(s, n, nxt);
            out.println(n / (n - nxt[n]));
            out.flush();
        }

    }

    private void kmp(String s, int n, int[] nxt) {
        nxt[0] = nxt[1] = 0;
        int j = 0;
        for (int i = 2; i <= n; i++) {
            while (j > 0 && s.charAt(j) != s.charAt(i - 1)) j = nxt[j];
            if (s.charAt(j) == s.charAt(i - 1)) j++;
            nxt[i] = j;
        }
    }

    void run() throws Exception {
        in = new Scanner(System.in);
        out = new PrintWriter(  System.out);

        solve();

        out.flush();
    }

}
```

---

## C

```cpp
#include<iostream>
#include<queue>
#include<set>
#include<iomanip>
#include<algorithm>
#include<vector>
#include<string>
#include<cmath>
using namespace std;
const int INF = 0x3f3f3f3f;
int n, m;
int a[1000005];
int dp[2][1005];
int main() {
    while (cin >> n >> m) {
        for (int i = 0; i < n; i++) {
            cin >> a[i];
        }
        // if n > m, the answer is YES.
        // consider the prefix sum, according to the pigeonhole principle, there are sum equals sum modulo m
        if (n > m) {
            cout << "YES" << endl;
            continue;
        }

        for (int i = 0; i < 2; i++) {
            for (int j = 0; j < m; j++) {
                dp[i][j] = 0;
            }
        }
        int cur = 0;
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                dp[cur ^ 1][j] = dp[cur][j];
            }
            int add = a[i] % m;
            for (int j = 0; j < m; j++) {
                if (dp[cur][j]) {
                    dp[cur ^ 1][(j + add) % m] = 1;
                }
            }
            dp[cur ^ 1][add] = 1;
            cur ^= 1;
        }
        cout << (dp[cur][0] ? "YES" : "NO") << endl;
    }
    return 0;
}
```

```java
import java.io.*;
import java.lang.reflect.Array;
import java.util.*;

public class Main {

    public static void main(String[] args) throws Exception { new C().run(); }

}

class C {

    Scanner in;
    PrintWriter out;

    void solve() {
        int n = in.nextInt();
        int m = in.nextInt();
        int[] a = new int[n];
        for (int i = 0; i < n; i++) a[i] = in.nextInt();
        if (n > m) {
            out.println("YES");
            return;
        }
        
        boolean[][] dp = new boolean[2][m];
        int cur = 0;
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < m; j++) {
                dp[cur ^ 1][j] = dp[cur][j];
            }
            int add = a[i] % m;
            for (int j = 0; j < m; j++) {
                if (dp[cur][j]) {
                    dp[cur ^ 1][(j + add) % m] = true;
                }
            }
            dp[cur ^ 1][add] = true;
            cur ^= 1;
        }
        out.println((dp[cur][0] ? "YES" : "NO"));

    }

    void run() throws Exception {
        in = new Scanner(System.in);
        out = new PrintWriter(  System.out);

        solve();

        out.flush();
    }

}
```

---

## D

```cpp
#include<iostream>
#include<stack>
#include<algorithm>
#include<vector>
#include<string>
#include<string.h>
using namespace std;
const int INF = 0x3f3f3f3f;
const int N = 1e6 + 10;
const int MOD = 1e9 + 7;
int n, q;
long long a[200005];
int main() {
    while (cin >> n >> q) {
        a[0] = 0;
        // calculate prefix strength sum
        for (int i = 1; i <= n; i++) {
            cin >> a[i];
            a[i] += a[i - 1];
        }
        // current attack sum
        long long attack = 0;
        long long x;
        while (q--) {
            cin >> x;
            attack += x;
            int res;
            int l = 0, r = n;
            // binary search for the biggest index whose prefix sum <= attack
            while (l <= r) {
                int m = (l + r) / 2;
                if (a[m] <= attack) {
                    res = m;
                    l = m + 1;
                } else {
                    r = m - 1;
                }
            }
            if (res == n) {
                res = 0;
                attack = 0;
            }
            cout << n - res << endl;
        }
    }
    return 0;
}
```

```java
import java.io.*;
import java.lang.reflect.Array;
import java.util.*;

public class Main {

    public static void main(String[] args) throws Exception { new D().run(); }

}

class D {

    Scanner in;
    PrintWriter out;

    void solve() {
        int n = in.nextInt();
        int q = in.nextInt();
        long[] a = new long[n + 1];
        for (int i = 1; i <= n; i++) {
            a[i] = in.nextLong();
            a[i] += a[i - 1];
        }
        long attack = 0;
        while (q-- > 0) {
            long x = in.nextLong();
            attack += x;
            int res = -1;
            int l = 0, r = n;
            while (l <= r) {
                int m = (l + r) / 2;
                if (a[m] <= attack) {
                    res = m;
                    l = m + 1;
                } else {
                    r = m - 1;
                }
            }
            if (res == n) {
                res = 0;
                attack = 0;
            }
            out.println(n - res);
        }

    }

    void run() throws Exception {
        in = new Scanner(System.in);
        out = new PrintWriter(  System.out);

        solve();

        out.flush();
    }

}
```

---

## E

```cpp
#include<iostream>
#include<stack>
#include<algorithm>
#include<vector>
#include<string>
#include<string.h>
using namespace std;
const int INF = 0x3f3f3f3f;
const int N = 1e6 + 10;
const int MOD = 1e9 + 7;
int n, m, k;
vector<int> G[105];
int vis[205];
int f[205];
bool find(int x) {
    for (auto v : G[x]) {
        if (!vis[v]) {
            vis[v] = 1;
            if (!f[v] || find(f[v])) {
                f[v] = x;
                return true;
            }
        }
    }
    return false;
}
int main() {
    while (cin >> n) {
        if (n == 0) break;
        cin >> m >> k;
        for (int i = 0; i < n; i++) G[i].clear();
        // A: [0, n)  B: [n, n + m)
    
        int id, a, b;
        // construct a bipartite graph from A to B
        for (int i = 0; i < k; i++) {
            cin >> id >> a >> b;
            b += n;
            if (a == 0 || b == 0) continue;
            G[a].push_back(b);
        }

        for (int i = n; i < n + m; i++) f[i] = 0;

        int res = 0;
        // use konig theorem: maximum matching = minimum vertex cover
        for (int i = 0; i < n; i++) {
            for (int j = n; j < n + m; j++) vis[j] = 0;
            if (find(i)) res++;
        }
        cout << res << endl;

    }
    return 0;
}
```

```java
import java.io.*;
import java.lang.reflect.Array;
import java.util.*;

public class Main {

    public static void main(String[] args) throws Exception { new D().run(); }

}

class D {

    Scanner in;
    PrintWriter out;

    void solve() {
        while (in.hasNext()) {
            int n = in.nextInt();
            if (n == 0) break;
            int m = in.nextInt();
            int k = in.nextInt();

            ArrayList<Integer>[] G = new ArrayList[n];
            for (int i = 0; i < n; i++) {
                G[i] = new ArrayList<>();
            }

            boolean[] vis = new boolean[n + m];
            int[] f = new int[n + m];

            for (int i = 0; i < k; i++) {
                int id = in.nextInt();
                int a = in.nextInt();
                int b = in.nextInt();
                b += n;
                if (a == 0 || b == 0) continue;
                G[a].add(b);
            }

            for (int i = n; i < n + m; i++) {
                f[i] = 0;
            }

            int res = 0;
            for (int i = 0; i < n; i++) {
                for (int j = n; j < n + m; j++) vis[j] = false;
                if (find(i, vis, f, G)) res++;
            }
            out.println(res);
            out.flush();
        }

    }

    private boolean find(int x, boolean[] vis, int[] f, ArrayList<Integer>[] G) {
        for (int v : G[x]) {
            if (!vis[v]) {
                vis[v] = true;
                if (f[v] == 0 || find(f[v], vis, f, G)) {
                    f[v] = x;
                    return true;
                }
            }
        }
        return false;
    }

    void run() throws Exception {
        in = new Scanner(System.in);
        out = new PrintWriter(  System.out);

        solve();

        out.flush();
    }

}
```



