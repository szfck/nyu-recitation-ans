## A
```cpp
#include<iostream>
#include<iomanip>
#include<algorithm>
#include<vector>
#include<string>
#include<cmath>
#include<map>
using namespace std;
#define rep(i, a, b) for (int i = (a); i < (b); i++)
int n;
int main() {
    while (cin >> n) {
        map<int, int> mp;
        int x;
        rep(i, 0, n) {
            cin >> x;
            if (x > 0) mp[x]++;
        }
        cout << mp.size() << endl;
    }
    return 0;
}

```
```java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner cin = new Scanner(System.in);
        int n = cin.nextInt();
        int x;
        HashMap<Integer, Integer> map = new HashMap<>();
        for (int i = 0; i < n; i++) {
            x = cin.nextInt();
            if (x > 0) {
                if (map.containsKey(x)) {
                    map.put(x, map.get(x) + 1);
                } else {
                    map.put(x, 1);
                }
            }
        }
        System.out.println(map.size());
    }
}
```
---

## B

```cpp
#include<iostream>
#include<iomanip>
#include<algorithm>
#include<vector>
#include<string>
#include<cmath>
using namespace std;
const int N = 1e5 + 10;
#define rep(i, a, b) for (int i = (a); i < (b); i++)
int n;
double p, q, r, s, t, u;
double func(double x) {
    return p * exp(-x) + q * sin(x) + r * cos(x) + s * tan(x) + t * x * x + u;
}
int main() {
    while (cin >> p >> q >> r >> s >> t >> u) {
        double l = 0, r = 1;
        if (func(l) * func(r) > 0) {
            cout << "No solution" << endl;
        } else {
            while (l + 1e-7 < r) {
                double m = (l + r) / 2.0;
                if (func(m) > 0) l = m;
                else r = m;
            }
            cout << setprecision(4) << fixed << (l + r) / 2.0 << endl;
        }
    }
    return 0;
}
```
```java
import java.util.*;

public class Main {
    static double p, q, r, s, t, u;
    static double func(double x) {
        return p * Math.exp(-x) + q * Math.sin(x) + r * Math.cos(x) + s * Math.tan(x) + t * x * x + u;
    }
    public static void main(String[] args) {
        Scanner cin = new Scanner(System.in);
        while (cin.hasNext()) {
            p = cin.nextDouble();
            q = cin.nextDouble();
            r = cin.nextDouble();
            s = cin.nextDouble();
            t = cin.nextDouble();
            u = cin.nextDouble();

            double l = 0, r = 1;
            if (func(l) * func(r) > 0) {
                System.out.println("No solution");
            } else {
                while (l + 1e-7 < r) {
                    double m = (l + r) / 2.0;
                    if (func(m) > 0) l = m;
                    else r = m;
                }
                System.out.printf("%.4f\n", (l + r) / 2.0);
            }
        }
    }
}
```
---

## C

```cpp
#include<iostream>
#include<algorithm>
#include<vector>
#include<string>
using namespace std;
const int N = 1e5 + 10;
#define rep(i, a, b) for (int i = (a); i < (b); i++)
int n;
int a[N];
int main() {
    int T; cin >> T;
    int cas = 1;
    while (T--) {
        cin >> n;
        int l = 1, r = 0;
        a[0] = 0;
        rep(i, 1, n + 1) cin >> a[i], r = max(r, a[i]);
        int res;
        while (l <= r) {
            int m = (l + r) / 2;
            int k = m;
            rep(i, 0, n) {
                int step = a[i + 1] - a[i];
                if (step > k) {
                    k = -1;
                    break;
                } else if (step == k) {
                    k--;
                }
            }
            if (k >= 0) {
                res = m;
                r = m - 1;
            } else {
                l = m + 1;
            }
        }
        cout <<"Case " << cas++ << ": " << res << endl;
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
        int cas = 1;
        while (T-- > 0) {
            int n = cin.nextInt();
            int l = 1, r = 0;
            int[] a = new int[n + 1];
            for (int i = 1; i <= n; i++) {
                a[i] = cin.nextInt();
                r = Math.max(a[i], r);
            }
            int res = 0;
            while (l <= r) {
                int m = (l + r) / 2;
                int k = m;
                for (int i = 0; i < n; i++) {
                    int step = a[i + 1] - a[i];
                    if (step > k) {
                        k = -1;
                        break;
                    } else if (step == k) {
                        k--;
                    }
                }
                if (k >= 0) {
                    res = m;
                    r = m - 1;
                } else {
                    l = m + 1;
                }
            }
            System.out.printf("Case %d: %d\n", cas++, res);
        }
    }
}
```
---

## D

```cpp
#include<iostream>
#include<algorithm>
#include<vector>
#include<string>
using namespace std;
const int N = 1e6 + 10;
#define rep(i, a, b) for (int i = (a); i < (b); i++)
int n;
int nxt[N][52];
int getId(char ch) {
    if (ch >= 'a' && ch <= 'z') return ch - 'a';
    else return ch - 'A' + 26;
}
string s;
void init() {
    int pos[52];
    rep(i, 0, 52) pos[i] = n;
    for (int i = n - 1; i >= 0; i--) {
        rep(j, 0, 52) {
            nxt[i][j] = pos[j];
        }
        pos[getId(s[i])] = i;
    }
}
int main() {
    while (cin >> s) {
        n = s.size();
        init();
        int q;
        cin >> q;
        string str;
        while (q--) {
            cin >> str;
            int m = str.size();
            int st = str[0] == s[0] ? 0 : nxt[0][getId(str[0])];
            int p = st;
            rep(j, 1, m) {
                if (p >= n) break;
                p = nxt[p][getId(str[j])];
            }
            if (p >= n) {
                cout << "Not matched" << endl;
            } else {
                cout << "Matched " << st << " " << p  << endl;
            }
        }
    }
    return 0;
}
```
```java
import java.util.*;

public class Main {
    static int getId(char ch) {
        if (ch >= 'a' && ch <= 'z') return ch - 'a';
        else return ch - 'A' + 26;
    }
    public static void main(String[] args) {
        Scanner cin = new Scanner(System.in);
        String s = cin.next();
        int n = s.length();
        int nxt[][] = new int[n][52];
        int lastPos[] = new int[52];
        for (int i = 0; i < 52; i++) lastPos[i] = n;
        for (int i = n - 1; i >= 0; i--) {
            for (int j = 0; j < 52; j++) {
                nxt[i][j] = lastPos[j];
            }
            lastPos[getId(s.charAt(i))] = i;
        }
        int q = cin.nextInt();
        while (q-- > 0) {
            String str = cin.next();
            int m = str.length();
            int st = str.charAt(0) == s.charAt(0) ? 0 : nxt[0][getId(str.charAt(0))];
            int p = st;
            for (int i = 1; i < m; i++) {
                if (p >= n) break;
                p = nxt[p][getId(str.charAt(i))];
            }
            if (p >= n) {
                System.out.println("Not matched");
            } else {
                System.out.printf("Matched %d %d\n", st, p);
            }
        }

    }
}
```