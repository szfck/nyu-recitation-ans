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
int n, x;
int main() {
    while (cin >> n) {
      int res = 0;
      for (int i = 0; i < n; i++) {
        cin >> x;
        res += abs(x);
      }
      cout << res << endl;
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
        int res = 0;
        for (int i = 0; i < n; i++) {
            res += Math.abs(cin.nextInt());
        }
        System.out.println(res);
    }
}
```
---
## B
```cpp
#include<iostream>
#include<algorithm>
#include<vector>
#include<string>
using namespace std;
int a, b;
int main() {
    while (cin >> a >> b) {
      if (a > b) swap(a, b);
      int res = 0;
      int tired = 0;
      while (a < b) {
        tired++;
        res += tired;
        a++;
        if (a < b) {
          b--;
          res += tired;
        }
      }
      cout << res << endl;
    }
    return 0;
}
```

```java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner cin = new Scanner(System.in);
        int a = cin.nextInt(), b = cin.nextInt();
        if (a > b) {
            int temp = a;
            a = b;
            b = temp;
        }
        int res = 0;
        int tired = 0;
        while (a < b) {
            tired++;
            res += tired;
            a++;
            if (a < b) {
                res += tired;
                b--;
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
#include<iomanip>
#include<algorithm>
#include<vector>
#include<string>
#include<cmath>
using namespace std;
const int N = 5e5 + 10;
int n;
long long prefix[N];
int main() {
    while (cin >> n) {
      int x;
      prefix[0] = 0;
      for (int i = 1; i <= n; i++) {
        cin >> x;
        prefix[i] = prefix[i - 1] + x;
      }
      if (prefix[n] % 3 != 0) {
        cout << 0 << endl;
      } else {
        long long res = 0, sum1 = prefix[n] / 3, sum2 = prefix[n] / 3 * 2;
        long long cnt = 0;
        for (int i = 1; i < n; i++) {
          if (prefix[i] == sum2) {
            res += cnt;
          }
          if (prefix[i] == sum1) {
            cnt++;
          }
        }
        cout << res << endl;
      }
    }
    return 0;
}
```
``` java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner cin = new Scanner(System.in);
        int n = cin.nextInt();
        long[] prefix = new long[n + 1];
        for (int i = 1; i <= n; i++) {
            prefix[i] = prefix[i - 1] + cin.nextInt();
        }
        if (prefix[n] % 3 != 0) {
            System.out.println(0);
        } else {
            long sum1 = prefix[n] / 3, sum2 = prefix[n] / 3 * 2;
            long cnt = 0, res = 0;
            for (int i = 1; i < n; i++) {
                if (prefix[i] == sum2) {
                    res += cnt;
                }
                if (prefix[i] == sum1) {
                    cnt++;
                }
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
#include<algorithm>
#include<vector>
#include<string>
using namespace std;
const int N = 1e5 + 10;
int segTree[N << 2];
int n, q, a[N];
int getSign(int x) {
  if (x > 0) return 1;
  else if (x < 0) return -1;
  else return 0;
}
void pushUp(int root) {
  segTree[root] = segTree[root * 2] * segTree[root * 2 + 1];
}
void buildTree(int root, int left, int right) {
  if (left == right) {
    segTree[root] = a[left];
    return;
  }
  int mid = (left + right) / 2;
  buildTree(root * 2, left, mid);
  buildTree(root * 2 + 1, mid + 1, right);
  pushUp(root);
}
void updateTree(int root, int left, int right, int pos, int value) {
  if (left == right) {
    segTree[root] = value;
    return;
  }
  int mid = (left + right) / 2;
  if (pos <= mid) updateTree(root * 2, left, mid, pos, value);
  else updateTree(root * 2 + 1, mid + 1, right, pos, value);
  pushUp(root);
}
int query(int root, int left, int right, int L, int R) {
  if (L <= left && R >= right) {
    return segTree[root];
  }
  int mid = (left + right) / 2;
  int res = 1;
  if (L <= mid) res *= query(root * 2, left, mid, L, R);
  if (R > mid) res *= query(root * 2 + 1, mid + 1, right, L, R);
  return res;
}
int main() {
  while (cin >> n >> q) {
    for (int i = 1; i <= n; i++) {
      cin >> a[i];
      a[i] = getSign(a[i]);
    }

    buildTree(1, 1, n);
    string op;
    int x, y;
    while (q--) {
      cin >> op >> x >> y;
      if (op[0] == 'C') {
        y = getSign(y);
        updateTree(1, 1, n, x, y);
      } else {
        int res = query(1, 1, n, x, y);
        if (res == 0) cout << 0;
        else if (res > 0) cout << "+";
        else cout << "-";
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
        while (cin.hasNext()) {
            int n = cin.nextInt(), q = cin.nextInt();
            int[] a = new int[n + 1];
            for (int i = 1; i <= n; i++) {
                a[i] = getSign(cin.nextInt());
            }
            int[] segTree = new int[n << 2];
            buildTree(1, 1, n, segTree, a);
            StringBuilder sb = new StringBuilder();
            while (q-- > 0) {
                String op = cin.next();
                int x = cin.nextInt(), y = cin.nextInt();
                if (op.charAt(0) == 'C') {
                    updateTree(1, 1, n, x, getSign(y), segTree);
                } else {
                    int res = query(1, 1, n, x, y, segTree);
                    if (res > 0) sb.append('+');
                    else if (res < 0) sb.append('-');
                    else sb.append('0');
                }
            }
            System.out.println(sb.toString());
        }
    }

    private static int query(int root, int left, int right, int L, int R, int[] segTree) {
        if (L <= left && R >= right) {
            return segTree[root];
        }
        int mid = (left + right) / 2;
        int res = 1;
        if (L <= mid) res *= query(root * 2, left, mid, L, R, segTree);
        if (R > mid) res *= query(root * 2 + 1, mid + 1, right, L, R, segTree);
        return res;
    }

    private static void updateTree(int root, int left, int right, int pos, int value, int[] segTree) {
        if (left == right) {
            segTree[root] = value;
            return;
        }
        int mid = (left + right) / 2;
        if (pos <= mid) updateTree(root * 2, left, mid, pos, value, segTree);
        else updateTree(root * 2 + 1, mid + 1, right, pos, value, segTree);
        pushUp(root, segTree);
    }

    private static void buildTree(int root, int left, int right, int[] segTree, int[] a) {
        if (left == right) {
            segTree[root] = a[left];
            return;
        }
        int mid = (left + right) / 2;
        buildTree(root * 2, left, mid, segTree, a);
        buildTree(root * 2 + 1, mid + 1, right, segTree, a);
        pushUp(root, segTree);
    }

    private static void pushUp(int root, int[] segTree) {
        segTree[root] = segTree[root * 2] * segTree[root * 2 + 1];
    }

    private static int getSign(int x) {
        if (x > 0) return 1;
        else if (x < 0) return -1;
        else return 0;
    }
}
```