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
int n;
int main() {
    while (cin >> n) {
        int res = 0;
        for (int i = 1; i <= n; i++) {
            int prime = 0;
            int cur = i;
            for (int j = 2; j * j <= cur && prime <= 2; j++) {
                if (cur % j == 0) {
                    prime++;
                    while (cur % j == 0) {
                        cur /= j;
                    }
                }
            }
            if (cur > 1) prime++;
            res += (prime == 2);
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

    public static void main(String[] args) throws Exception { new A().run(); }

}

class A {

    Scanner in;
    PrintWriter out;

    int n, m;

    void solve() {
        n = in.nextInt();
        int res = 0;
        for (int i = 1; i <= n; i++) {
            int prime = 0;
            int cur = i;
            for (int j = 2; j * j <= cur && prime <= 2; j++) {
                if (cur % j == 0) {
                    prime++;
                    while (cur % j == 0) {
                        cur /= j;
                    }
                }
            }
            if (cur > 1) prime++;
            if (prime == 2) res++;
        }
        out.println(res);
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
const int N = 2e7 + 10;
const int INF = 0x3f3f3f3f;
#define pb push_back
#define mp make_pair
#define fi first
#define se second
int n, m;
int vis[N];
vector<int> primes;
vector<int> res;
void init() {
    memset(vis, 0, sizeof vis);
    for (int i = 2; i < N; i++) {
        if (!vis[i]) {
            primes.push_back(i);
            for (int j = 2 * i; j < N; j += i) {
                vis[j] = 1;
            }
        }
    }
    for (int i = 0; i < (int)primes.size() - 1; i++) {
        if (primes[i] + 2 == primes[i + 1]) {
            res.push_back(primes[i]);
        }
    }
}
int main() {
    init();
    while (cin >> n) {
        n--;
        cout << '(' <<  res[n] << ", " << res[n] + 2 << ')' << endl;
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
    final int N = 20000001;
    int n, m;

    void solve() {

        int vis[] = new int[N];
        Arrays.fill(vis, 0);
        ArrayList<Integer> primes = new ArrayList<>();
        ArrayList<Integer> res = new ArrayList<>();

        for (int i = 2; i < N; i++) {
            if (vis[i] == 0) {
                primes.add(i);
                for (int j = 2 * i; j < N; j += i) {
                    vis[j] = 1;
                }
            }
        }
        for (int i = 0; i < primes.size() - 1; i++) {
            if (primes.get(i) + 2 == primes.get(i + 1)) {
                res.add(primes.get(i));
            }
        }

        while (in.hasNext()) {
            n = in.nextInt();
            n--;

            out.printf("(%d, %d)\n", res.get(n), res.get(n) + 2);
            out.flush();
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
int cas = 1;
long long c[55][55];
void init() {
    c[0][0] = 1;
    for (int i = 1; i < 55; i++) {
        for (int j = 0; j <= i; j++) {
            if (j == 0 || j == i) c[i][j] = 1;
            else c[i][j] = c[i - 1][j - 1] + c[i - 1][j];
        }
    }
}
string get(string s, int k) {
    if (k == 1) return s;
    return s + "^" + to_string(k);
}
int main() {
    init();
    int T; 
    cin >> T;
    while (T--) {
        string s;
        cin >> s;
        int n = s.size();
        int pos = s.find('+');
        string foo = s.substr(1, pos - 1);
        int pos2 = s.find(')');
        string bar = s.substr(pos + 1, pos2 - pos - 1);
        int k = stoi(s.substr(pos2 + 2));
        cout << "Case " << cas++ << ": ";

        cout << get(foo, k);
        cout << "+";

        for (int b = 1; b < k; b++) {
            int a = k - b;
            cout << c[k][a] << "*";
            cout << get(foo, a) << "*";
            cout << get(bar, b) << "+";
        }

        cout << get(bar, k);
        cout << endl;
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

    long c[][] = new long[55][55];

    void init() {
        c[0][0] = 1;
        for (int i = 1; i < 55; i++) {
            for (int j = 0; j <= i; j++) {
                if (j == 0 || j == i) c[i][j]= 1;
                else c[i][j] = c[i - 1][j - 1] + c[i - 1][j];
            }
        }
    }
    String get(String s, int k) {
        if (k == 1) return s;
        return s + "^" + k;
    }
    void solve() {
        init();
        int T = in.nextInt();
        int cas = 1;
        while (T-- > 0) {
            String s = in.next();
            int pos = s.indexOf('+');
            int pos2 = s.indexOf(')');
            String foo = s.substring(1, pos);
            String bar = s.substring(pos + 1, pos2);
            int k = Integer.parseInt(s.substring(pos2 + 2));
            out.print("Case " + cas++ + ": ");
            out.print(get(foo, k) + "+");
            for (int b = 1; b < k; b++) {
                int a = k - b;
                out.print(c[k][a] + "*" + get(foo, a) + "*" + get(bar, b) + "+");
            }
            out.println(get(bar, k));
            out.flush();
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
const int N = 1e6 + 10;
const int MOD = 1e9 + 7;
int n, m;
string s;
int hs[N];
int rhs[N];
int fac[N];
void init() {
    fac[0] = 1;
    for (int i = 1; i < N; i++) {
        fac[i] = 1ll * fac[i - 1] * 26 % MOD;
    }
}

// check sub string [a, a + len - 1] with sub string [b - len + 1, b]
// if their hash value is same, return true
int same(int a, int b, int len) {
    int hsA = ((hs[a + len - 1] - hs[a - 1]) % MOD + MOD) % MOD;
    int hsB = ((rhs[b - len + 1] - rhs[b + 1]) % MOD + MOD) % MOD;
    int shiftA = a, shiftB = n + 1 - b;
    if (shiftA > shiftB) {
        swap(shiftA, shiftB);
        swap(hsA, hsB);
    }    
    return (1ll * hsA * fac[shiftB - shiftA] % MOD) == hsB;
}
void solve() {
    n = s.size();
    hs[0] = 0;
    for (int i = 1; i <= n; i++) {
        int cur = s[i - 1] - 'a';
        hs[i] = (hs[i - 1] + 1ll * fac[i] * cur % MOD) % MOD;
    }
    rhs[n + 1] = 0;
    for (int i = n; i >= 1; i--) {
        int cur = s[i - 1] - 'a';
        rhs[i] = (rhs[i + 1] + 1ll * fac[n - i + 1] * cur % MOD) % MOD;
    }
    int l = 1, r = n;
    int start, len;

    // use binary search to find the longest length
    while (l <= r) {
        int m = (l + r) >> 1;
        bool flag = false;
        for (int i = m; i <= n; i++) {
            if (same(1, i, m)) {
                flag = true;
                start = i - m + 1;
                len = m;
                break;
            }
        }

        // if find sub string with length m, go find a longer length
        // ohterwise go find a shorter length
        if (flag) {
            l = m + 1;
        } else {
            r = m - 1;
        }
    }
    cout << s.substr(start - 1, len) << endl;
}
int main() {
    init();
    int T; cin >> T;
    while (T--) {
        cin >> s;
        solve();
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
    final int N = 1000005;
    final int MOD = 1000000007;

    long fac[] = new long[N];

    void init() {
        fac[0] = 1;
        for (int i = 1; i < N; i++) {
            fac[i] = fac[i - 1] * 26 % MOD;
        }
    }

    void solve() {
        init();
        int T = in.nextInt();
        while (T-- > 0) {
            String s = in.next();
            int n = s.length();

            long hs[] = new long[n + 2];
            long rhs[] = new long[n + 2];
            hs[0] = 0;
            for (int i = 1; i <= n; i++) {
                hs[i] = (hs[i - 1] + (s.charAt(i - 1) - 'a') * fac[i]) % MOD;
            }

            rhs[n + 1] = 0;
            for (int i = n; i > 0; i--) {
                rhs[i] = (rhs[i + 1] + (s.charAt(i - 1) - 'a') * fac[n + 1 - i]) % MOD;
            }

            int start = 1, len = 1;

            int l = 1, r = n;
            while (l <= r) {
                int m = (l + r) / 2;
                boolean flag = false;
                for (int i = m; i <= n; i++) {
                    if (same(1, i, m, hs, rhs, n)) {
                        flag = true;
                        start = i - m + 1;
                        len = m;
                        break;
                    }
                }

                if (flag) {
                    l = m + 1;
                } else {
                    r = m - 1;
                }
            }

            out.println(s.substring(start - 1, start - 1 + len));
        }

    }

    private boolean same(int a, int b, int len, long[] hs, long[] rhs, int n) {
        long hsA = ((hs[a + len - 1] - hs[a - 1]) % MOD + MOD) % MOD;
        long hsB = ((rhs[b - len + 1] - rhs[b + 1]) % MOD + MOD) % MOD;
        int shiftA = a, shiftB = n + 1 - b;
        if (shiftA < shiftB) {
            return (hsA * fac[shiftB - shiftA] % MOD) == hsB;
        } else {
            return (hsB * fac[shiftA - shiftB] % MOD) == hsA;
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



