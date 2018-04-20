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
int dp[20002];
int n, m, x;
int main() {
    int T; cin >> T;
    while (T--) {
        cin >> m >> n;
        memset(dp, -1, sizeof dp);
        dp[0] = 0;
        for (int i = 0; i < n; i++) {
            cin >> x;
            // since no coin value is larger than 10000, the result should be no larger than 20000
            for (int j = 20001 - x; j >= 0; j--) {
                if (dp[j] > -1) {
                    if (dp[j + x] == -1 || dp[j + x] > dp[j] + 1) {
                        dp[j + x] = dp[j] + 1;
                    }
                }
            }
        }
        for (int i = m; i <= 20001; i++) {
            if (dp[i] > -1) {
                cout << i << " " << dp[i] << endl;
                break;
            }
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

    public static void main(String[] args) throws Exception { new A().run(); }

}

class A {

    Scanner in;
    PrintWriter out;

    int n, m;
    final int INF = 0x3f3f3f3f;

    void solve() {
        int T = in.nextInt();
        while (T-- > 0) {
            m = in.nextInt();
            n = in.nextInt();

            int[] dp = new int[20002];
            Arrays.fill(dp, -1);
            dp[0] = 0;
            for (int i = 0; i < n; i++) {
                int x = in.nextInt();
                for (int j = 20001 - x; j >= 0; j--) {
                    if (dp[j] > -1) {
                        if (dp[j + x] == -1 || dp[j + x] > dp[j] + 1) {
                            dp[j + x] = dp[j] + 1;
                        }
                    }
                }
            }
            for (int i = m; i <= 20001; i++) {
                if (dp[i] > -1) {
                    out.println(i + " " + dp[i]);
                    break;
                }
            }
        }
    }

    void run() throws Exception {
        in = new Scanner(System.in);
        out = new PrintWriter(System.out);

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
const int N = 2e5 + 10;
const int INF = 0x3f3f3f3f;
#define pb push_back
#define mp make_pair
#define fi first
#define se second
int n, m;
int dp[55][55];
int a[55];
int main() {
    while (cin >> m) {
        if (m == 0) break;
        cin >> n;
        for (int i = 1; i <= n; i++) {
            cin >> a[i];
        }
        a[0] = 0, a[n + 1] = m;
        for (int i = 0; i <= n; i++) {
            dp[i][i + 1] = 0;
        }
        for (int len = 2; len <= n + 1; len++) {
            for (int i = 0; i + len <= n + 1; i++) {
                int j = i + len;
                dp[i][j] = INF;
                for (int k = i + 1; k < j; k++) {
                    dp[i][j] = min(dp[i][j], dp[i][k] + dp[k][j]);
                }
                dp[i][j] += a[j] - a[i];
            }
        }
        cout << "The minimum cutting is " << dp[0][n + 1] << "." << endl;
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

    int n, m;
    final int INF = 0x3f3f3f3f;

    void solve() {
        while (true) {
            m = in.nextInt();
            if (m == 0) break;
            n = in.nextInt();
            int[] a = new int[n + 2];
            for (int i = 1; i <= n; i++) {
                a[i] = in.nextInt();
            }
            a[0] = 0;
            a[n + 1] = m;

            int[][] dp = new int[n + 2][n + 2];
            for (int i = 0; i <= n; i++) {
                dp[i][i + 1] = 0;
            }
            for (int len = 2; len <= n + 1; len++) {
                for (int i = 0; i + len <= n + 1; i++) {
                    int j = i + len;
                    dp[i][j] = Integer.MAX_VALUE;
                    for (int k = i + 1; k < j; k++) {
                        dp[i][j] = Math.min(dp[i][j], dp[i][k] + dp[k][j]);
                    }
                    dp[i][j] += a[j] - a[i];
                }
            }
            out.println("The minimum cutting is " + dp[0][n + 1] + ".");

        }
    }

    void run() throws Exception {
        in = new Scanner(System.in);
        out = new PrintWriter(System.out);

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
int weight[1005], load[1005];
// using rolling array
// dp[i][j] : in layer i, largest number of boxes could put with weight j
int dp[2][3005];
int n;
int main() {
    while (cin >> n) {
        if (n == 0) break;
        for (int i = 0; i < n; i++) {
            cin >> weight[i] >> load[i];
        }
        int cur = 0;
        for (int i = 0; i < 3005; i++) {
            dp[cur][i] = -INF;
        }
        dp[cur][0] = 0;

        int res = 0;

        // try to put box from top to bottom
        // cur means current layer, cur ^ 1 means next layer
        for (int i = n - 1; i >= 0; i--) {
            for (int j = 0; j < 3005; j++) {
                dp[cur ^ 1][j] = -INF;
            }
            for (int j = 0; j < 3005; j++) {
                if (dp[cur][j] < 0) continue;

                // not put box i
                dp[cur ^ 1][j] = max(dp[cur ^ 1][j], dp[cur][j]);

                // if load of box could support weight j, then try to add box i to the bottom
                if (load[i] >= j) {
                    res = max(res, 1 + dp[cur][j]);
                    if (j + weight[i] < 3005) {
                        dp[cur ^ 1][j + weight[i]] = max(dp[cur ^ 1][j + weight[i]], dp[cur][j] + 1);
                    }
                }
            }
            cur ^= 1;
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

    public static void main(String[] args) throws Exception { new C().run(); }

}

class C {

    Scanner in;
    PrintWriter out;

    int n, m;
    final int INF = 0x3f3f3f3f;

    void solve() {
        while (true) {
            n = in.nextInt();
            if (n == 0) break;
            int[] weight = new int[n];
            int[] load = new int[n];
            for (int i = 0; i < n; i++) {
                weight[i] = in.nextInt();
                load[i] = in.nextInt();
            }
            int[][] dp = new int[2][3005];
            int cur = 0;
            for (int i = 0; i < 3005; i++) {
                dp[cur][i] = -INF;
            }
            dp[cur][0] = 0;

            int res = 0;

            for (int i = n - 1; i >= 0; i--) {
                for (int j = 0; j < 3005; j++) {
                    dp[cur ^ 1][j] = -INF;
                }
                for (int j = 0; j < 3005; j++) {
                    if (dp[cur][j] < 0) continue;
                    dp[cur ^ 1][j] = Math.max(dp[cur ^ 1][j], dp[cur][j]);

                    if (load[i] >= j) {
                        res = Math.max(res, 1 + dp[cur][j]);
                        if (j + weight[i] < 3005) {
                            dp[cur ^ 1][j + weight[i]] = Math.max(dp[cur ^ 1][j + weight[i]], dp[cur][j] + 1);
                        }
                    }
                }
                cur ^= 1;
            }
            out.println(res);
        }

    }

    void run() throws Exception {
        in = new Scanner(System.in);
        out = new PrintWriter(System.out);

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
int n, m;
int a[55];
// using rolling array
// dp[i][j] means in layer i, the maximum sum get when the difference of two towers is j
int dp[2][500005];
int cas = 1;
int main() {
    int T; cin >> T;
    while (T--) {
        cin >> n;
        for (int i = 0; i < n; i++) {
            cin >> a[i];
        }
        memset(dp, -1, sizeof dp);
        int cur = 0;
        dp[cur][0] = 0;
        int sum = 0;
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < 500005; j++) {
                dp[cur ^ 1][j] = dp[cur][j];
            }
            for (int j = 0; j <= sum; j++) {
                if (dp[cur][j] < 0) continue;

                // add a[i] to the higher tower
                dp[cur ^ 1][j + a[i]] = max(dp[cur ^ 1][j + a[i]], dp[cur][j] + a[i]);

                // add a[i] to the lower tower
                int k = abs(j - a[i]);
                dp[cur ^ 1][k] = max(dp[cur ^ 1][k], dp[cur][j] + a[i]);
            }
            sum += a[i];
            cur ^= 1;
        }
        cout << "Case " << cas++ << ": ";
        if (dp[cur][0] <= 0) {
            cout << "impossible" << endl;
        } else {
            cout << dp[cur][0] / 2 << endl;
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

    int n, m;
    final int INF = 0x3f3f3f3f;

    // put dp variable globally, otherwise may get memory limit exceeded errror
    int[][] dp = new int[2][500005];
    void solve() {
        int T = in.nextInt();
        int cas = 1;

        while (T-- > 0) {
            n = in.nextInt();
            int[] a = new int[n];
            int tot = 0;
            for (int i = 0; i < n; i++) {
                a[i] = in.nextInt();
                tot += a[i];
            }
            Arrays.fill(dp[0], -1);
            Arrays.fill(dp[1], -1);
            dp[0][0] = 0;
            int cur = 0;
            int sum = 0;
            for (int i = 0; i < n; i++) {
                for (int j = 0; j <= tot; j++) {
                    dp[cur ^ 1][j] = dp[cur][j];
                }
                for (int j = 0; j <= sum; j++) {
                    if (dp[cur][j] < 0) continue;

                    dp[cur ^ 1][j + a[i]] = Math.max(dp[cur ^ 1][j + a[i]], dp[cur][j] + a[i]);

                    int k = Math.abs(j - a[i]);
                    dp[cur ^ 1][k] = Math.max(dp[cur ^ 1][k], dp[cur][j] + a[i]);
                }
                cur ^= 1;
                sum += a[i];
            }
            if (dp[cur][0] <= 0) {
                out.println("Case " + cas++ + ": impossible");
            } else {
                out.println("Case " + cas++ + ": " + dp[cur][0] / 2);
            }
        }

    }

    void run() throws Exception {
        in = new Scanner(System.in);
        out = new PrintWriter(System.out);

        solve();

        out.flush();
    }

}
```



