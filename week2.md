## A

```cpp
#include <vector>
#include <stdio.h>
using namespace std;
const int N = 1005;
int n;
int vis[N];
int f[100];
int main() {
    for (int i = 0; i < N; i++) vis[i] = 0;
    f[1] = f[2] = 1;
    vis[1] = 1;
    for (int i = 3; ;i++) {
        f[i] = f[i - 1] + f[i - 2];
        if (f[i] >= N) break;
        vis[f[i]] = 1;
    }
    while (scanf("%d", &n) == 1) {
        for (int i = 1; i <= n; i++) {
            printf("%c", vis[i] ? 'O' : 'o');
        }
        puts("");
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
        int n = cin.nextInt();
        int[] f = new int[1005];
        boolean[] vis = new boolean[1005];
        f[1] = f[2] = 1;
        vis[1] = true;
        for (int i = 3; ; i++) {
            f[i] = f[i - 1] + f[i - 2];
            if (f[i] >= 1000) break;
            vis[f[i]] = true;
        }
        StringBuilder sb = new StringBuilder();
        for (int i = 1; i <= n; i++) {
            sb.append(vis[i] ? 'O' : 'o');
        }
        System.out.println(sb.toString());
    }
}

```

---

## B

```cpp
#include <vector>
#include <stdio.h>
using namespace std;
int n, m;
int main() {
    while (scanf("%d%d", &n, &m) == 2) {
        if (n >= 30) n = 30;
        printf("%d\n", m % (1 << n));
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
        int n = cin.nextInt();
        int m = cin.nextInt();
        if (n >= 30) n = 30;
        System.out.println(m % (1 << n));
    }
}
```

---

## C

```cpp
#include <vector>
#include <stdio.h>
#include <stack>
#include <string.h>
#include <iostream>
#include <string>
using namespace std;
string s;
bool match(char a, char b) {
    return (a == '(' && b == ')') || (a == '[' && b == ']');
}
bool solve() {
    stack<char> stk;
    int n = s.size();
    for (int i = 0; i < n; i++) {
        if (s[i] == '(' || s[i] == '[') {
            stk.push(s[i]);
        } else {
            if (stk.size() == 0) return false;
            if (!match(stk.top(), s[i])) return false;
            stk.pop();
        }
    }
    return stk.size() == 0;
}
int main() {
    int T;
    cin >> T;
    getchar();
    while (T--) {
        getline(cin, s);
        if (s == "") {
            puts("Yes");
            continue;
        }
        puts(solve() ? "Yes" : "No");
    }

    return 0;
}
```

```java
import java.util.ArrayList;
import java.util.Scanner;
import java.util.Stack;

public class Main {
    public static void main(String[] args) {
        Scanner cin = new Scanner(System.in);
        int T = cin.nextInt();
        cin.nextLine();
        while (T-- > 0) {
            String str = cin.nextLine();
            System.out.println(solve(str) ? "Yes" : "No");
        }
    }

    private static boolean solve(String str) {
        if (str == "") return true;
        Stack<Character> stk = new Stack();
        for (int i = 0; i < str.length(); i++) {
            char cur = str.charAt(i);
            if (cur == '(' || cur == '[') {
                stk.push(cur);
            } else {
                if (stk.empty() || !match(stk.peek(), cur)) return false;
                stk.pop();
            }
        }
        return stk.empty();
    }

    private static boolean match(char a, char b) {
        return a == '(' && b == ')' || a == '[' && b == ']';
    }
}

```

---

## D

```cpp
#include <vector>
#include <stdio.h>
#include <stack>
#include <string.h>
using namespace std;
const int N = 1e5 + 10;
int h[N];
int n;
long long solve() {
    stack<pair<int, int>> stk;
    long long res = 0;
    h[n + 1] = 0;
    for (int i = 1; i <= n + 1; i++) {
        int idx = i;
        while (stk.size() && h[i] <= stk.top().first) {
            pair<int, int> cur = stk.top();
            stk.pop();
            int height = cur.first;
            int index = cur.second;
            res = max(res, 1ll * (height) * (i - index));
            idx = min(idx, index);
        }
        stk.push(make_pair(h[i], idx));
    }
    return res;
}
int main() {
    while (scanf("%d", &n) == 1) {
        if (n == 0) break;
        for (int i = 1; i <= n; i++) scanf("%d", &h[i]);
        printf("%lld\n", solve());
    }
    return 0;
}


```

```java
import java.util.ArrayList;
import java.util.Scanner;
import java.util.Stack;

public class Main {
    public static void main(String[] args) {
        Scanner cin = new Scanner(System.in);
        while (true) {
            int n = cin.nextInt();
            if (n == 0) break;
            int[] heights = new int[n + 2];
            for (int i = 1 ; i <= n; i++) {
                heights[i] = cin.nextInt();
            }
            heights[n + 1] = 0;
            Stack<Node> stk = new Stack<>();
            long res = 0;
            for (int i = 1; i <= n + 1; i++) {
                int idx = i;
                while (!stk.empty() && stk.peek().height >= heights[i]) {
                    Node cur = stk.peek();
                    stk.pop();
                    res = Math.max(res, (long)cur.height * (i - cur.index));
                    idx = Math.min(idx, cur.index);
                }
                stk.push(new Node(heights[i], idx));
            }
            System.out.println(res);
        }
    }

    private static class Node {
        int height, index;
        Node(int height, int index) {
            this.height = height;
            this.index = index;
        }
    }
}


```



