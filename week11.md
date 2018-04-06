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
const int N = 15;
char G[N][N];
int n, m, c;
int step[N][N];
int dir[8] = {
    0, 1, 0, -1, 1, 0, -1, 0
};
void dfs(int x, int y) {
    int dx = x, dy = y;
    if (G[x][y] == 'N') {
        dx -= 1;
    } else if (G[x][y] == 'S') {
        dx += 1;
    } else if (G[x][y] == 'W') {
        dy -= 1;
    } else if (G[x][y] == 'E') {
        dy += 1;
    }
    if (dx < 1 || dx > n || dy < 1 || dy > m) {
        printf("%d step(s) to exit\n", step[x][y] + 1);
        return;
    }

    if (step[dx][dy] != -1) {
        printf("%d step(s) before a loop of %d step(s)\n", step[dx][dy], step[x][y] - step[dx][dy] + 1);
        return;
    }
    step[dx][dy] = step[x][y] + 1;
    dfs(dx, dy);
}
int main() {
    while (cin >> n >> m >> c) {
        if (n == 0 && m == 0 && c == 0) break;
        for (int i = 1; i <= n; i++) {
            cin >> (G[i] + 1);
        }
        for (int i = 1; i <= n; i++) {
            for (int j = 1; j <= m; j++) {
                step[i][j] = -1;
            }
        }
        step[1][c] = 0;
        dfs(1, c);
    }
    return 0;
}
```

```java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner cin = new Scanner(System.in);

        while (true) {
            int n = cin.nextInt(), m = cin.nextInt(), c = cin.nextInt();
            if (n == 0 && m == 0 && c == 0) break;
            char G[][] = new char[n + 1][m + 1];
            int step[][] = new int[n + 1][m + 1];
            for (int i = 1; i <= n; i++) {
                for (int j = 1;j <= m; j++) {
                    step[i][j] = -1;
                }
            }
            for (int i = 1; i <= n; i++) {
                String str = cin.next();
                for (int j = 1; j <= m; j++) {
                    G[i][j] = str.charAt(j - 1);
                }
            }
            step[1][c] = 0;
            dfs(1, c, G, step, n, m);
        }
    }

    private static void dfs(int r, int c, char[][] G, int[][] step, int n, int m) {
        int dx = r, dy = c;
        if (G[r][c] == 'N') {
            dx -= 1;
        } else if (G[r][c] == 'S') {
            dx += 1;
        } else if (G[r][c] == 'W') {
            dy -= 1;
        } else if (G[r][c] == 'E') {
            dy += 1;
        }

        if (dx < 1 || dx > n || dy < 1 || dy > m) {
            System.out.printf("%d step(s) to exit\n", step[r][c] + 1);
            return;
        }

        if (step[dx][dy] != -1) {
            System.out.printf("%d step(s) before a loop of %d step(s)\n", step[dx][dy], step[r][c] - step[dx][dy] + 1);
            return;
        }

        step[dx][dy] = step[r][c] + 1;
        dfs(dx, dy, G, step, n, m);

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
using namespace std;
const int N = 2e5 + 10;
const int INF = 0x3f3f3f3f;
#define pb push_back
#define mp make_pair
#define fi first
#define se second
int n, m;
vector<int> G[N];
int in[N];
void topoSort() {
    queue<int> que;
    for (int i = 1; i <= n; i++) {
        if (in[i] == 0) {
            que.push(i);
        }
    }
    vector<int> res;
    while (que.size()) {
        int cur = que.front();
        que.pop();
        res.pb(cur);
        for (auto v : G[cur]) {
            in[v]--;
            if (in[v] == 0) {
                que.push(v);
            }
        }
    }
    if (res.size() != n) {
        cout << "IMPOSSIBLE" << endl;
    } else {
        for (auto v : res) {
            cout << v << endl;
        }
    }
}
int main() {
    while (cin >> n >> m) {
        if (n == 0 && m == 0) break;
        for (int i = 1; i <= n; i++) {
            in[i] = 0;
            G[i].clear();
        }
        for (int i = 0; i < m; i++) {
            int u, v;
            cin >> u >> v;
            G[u].pb(v);
            in[v]++;
        }
        topoSort();
    }
    return 0;
}
```

```java
import java.util.*;

public class Main {
    public static void main(String[] args) {
        Scanner cin = new Scanner(System.in);

        int n, m;
        while (cin.hasNext()) {
            n = cin.nextInt();
            m = cin.nextInt();
            if (n == 0 && m == 0) break;
            ArrayList<Integer> G[] = new ArrayList[n + 1];

            int in[] = new int[n + 1];

            for (int i = 1; i <= n; i++) {
                G[i] = new ArrayList<>();
            }

            for (int i = 0; i < m; i++) {
                int u = cin.nextInt(), v = cin.nextInt();
                G[u].add(v);
                in[v]++;
            }

            ArrayList<Integer> res = new ArrayList<>();

            Queue<Integer> que = new LinkedList<>();

            for (int i = 1; i <= n; i++) {
                if (in[i] == 0) {
                    que.offer(i);
                }
            }

            while (!que.isEmpty()) {
                int cur = que.poll();
                res.add(cur);
                for (int v : G[cur]) {
                    in[v]--;
                    if (in[v] == 0) {
                        que.offer(v);
                    }
                }
            }

            if (res.size() != n) {
                System.out.println("IMPOSSIBLE");
            } else {
                for (int v : res) {
                    System.out.println(v);
                }
            }

        }
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
const int N = 5e5 + 10;
int L, U, R;
int vis[10000];
int add[10];
int cas = 1;
int main() {
    while (cin >> L >> U >> R) {
        if (L == 0 && U == 0 && R == 0) break;
        for (int i = 0; i < R; i++) {
            cin >> add[i];
        }
        queue<pair<int, int>> que;
        for (int i = 0; i < 10000; i++) vis[i] = 0;
        que.push(make_pair(L, 0));
        vis[L] = 1;
        int res = -1;
        while (que.size()) {
            auto cur = que.front();
            que.pop();
            int num = cur.first, step = cur.second;
            if (num == U) {
                res = step;
                break;
            }
            for (int i = 0; i < R; i++) {
                int nxt = (num + add[i]) % 10000;
                if (!vis[nxt]) {
                    vis[nxt] = 1;
                    que.push(make_pair(nxt, step + 1));
                }
            }
        }
        if (res == -1) {
            printf("Case %d: Permanently Locked\n", cas++);
        } else {
            printf("Case %d: %d\n", cas++, res);
        }
    }
    return 0;
}

```

```java
import java.util.*;

public class Main {
    static class Node {
        int val, step;
        Node(int val, int step) {
            this.val = val;
            this.step = step;
        }
    }
    public static void main(String[] args) {
        Scanner cin = new Scanner(System.in);
        int cas = 1;
        while (true) {
            int L = cin.nextInt();
            int U = cin.nextInt();
            int R = cin.nextInt();

            if (L == 0 && U == 0 && R == 0) break;

            boolean vis[] = new boolean[10000];
            int add[] = new int[10];

            for (int i = 0; i < R; i++) {
                add[i] = cin.nextInt();
            }

            Queue<Node> que = new LinkedList<>();

            vis[L] = true;
            que.offer(new Node(L, 0));

            int res = -1;
            while (!que.isEmpty()) {
                Node cur = que.poll();
                int val = cur.val, step = cur.step;
                if (val == U) {
                    res = step;
                    break;
                }
                for (int i = 0; i < R; i++) {
                    int nval = (val + add[i]) % 10000;
                    if (vis[nval]) continue;
                    vis[nval] = true;
                    que.offer(new Node(nval, step + 1));
                }
            }

            if (res == -1) {
                System.out.printf("Case %d: Permanently Locked\n", cas++);
            } else {
                System.out.printf("Case %d: %d\n", cas++, res);
            }


        }
    }


}
```

---

## D

```cpp
// cin cout will time limit exceed for this question
// use scanf printf instead
#include<iostream>
#include<stack>
#include<algorithm>
#include<vector>
#include<string>
using namespace std;
const int N = 1e5 + 10;
const int INF = 0x3f3f3f3f;
int n, m;
vector<int> G[N];
int scc[N];
int cnt;
int low[N], num[N], vis[N];
int tim;
stack<int> stk;
void dfs(int x) {
    low[x] = num[x] = tim++;
    vis[x] = 1;
    stk.push(x);
    for (auto v : G[x]) {
        if (scc[v] != -1) continue;
        if (!vis[v]) dfs(v);
        low[x] = min(low[x], low[v]);
    }
    if (low[x] == num[x]) {
        cnt++;
        int cur;
        do {
            cur = stk.top();
            stk.pop();
            scc[cur] = cnt;
        } while (cur != x);
    }
}
int in[N];
int tarjan() {
    cnt = 0;
    for (int i = 1; i <= n; i++) {
        if (scc[i] == -1) {
            tim = 0;
            dfs(i);
        }
    }
    for (int i = 1; i <= cnt; i++) {
        in[i] = 0;
    }
    for (int i = 1; i <= n; i++) {
        for (auto j : G[i]) {
            int u = scc[i], v = scc[j];
            if (u != v) {
                in[v]++;
            }
        }
    }
    int res = 0;
    for (int i = 1; i <= cnt; i++) {
        if (in[i] == 0) res++;
    }
    return res;
}
int main() {
    int T; scanf("%d", &T);
    while (T--) {
        scanf("%d%d", &n, &m);
        for (int i = 1; i <= n; i++) {
            G[i].clear();
            scc[i] = -1;
            vis[i] = 0;
        }
        for (int i = 0; i < m; i++) {
            int u, v;
            scanf("%d%d", &u, &v);
            G[u].push_back(v);
        }
        printf("%d\n", tarjan());
    }
    return 0;
}
```

```java
import java.io.*;
import java.util.*;

public class Main {
    static int cnt;
    static int tim;
    static int scc[];
    static int low[];
    static int num[];
    static boolean vis[];
    static ArrayList<Integer> G[];
    static Stack<Integer> stk;

    public static void main(String[] args) throws IOException {
        Scanner cin = new Scanner(System.in);
        OutputWriter out = new OutputWriter(System.out);
        int T = cin.nextInt();
        while (T-- > 0) {
            int n = cin.nextInt();
            int m = cin.nextInt();
            G = new ArrayList[n + 1];
            for (int i = 1; i <= n; i++) {
                G[i] = new ArrayList<>();
            }

            for (int i = 0; i < m; i++) {
                int u = cin.nextInt();
                int v = cin.nextInt();
                G[u].add(v);
            }

            tarjan(n, out);

        }
        out.close();
    }

    private static void tarjan(int n, OutputWriter out) throws IOException {
        cnt = 0;
        scc = new int[n + 1];
        low = new int[n + 1];
        num = new int[n + 1];
        vis = new boolean[n + 1];

        for (int i = 1; i <= n; i++) {
            scc[i] = -1;
        }
        stk = new Stack<>();
        for (int i = 1; i <= n; i++) {
            if (scc[i] != -1) continue;
            tim = 0;
            dfs(i, n);
        }

        int in[] = new int[cnt + 1];
        for (int i = 1; i <= n; i++) {
            for (int j : G[i]) {
                int u = scc[i], v = scc[j];
                if (u != v) {
                    in[v]++;
                }
            }
        }
        int res = 0;
        for (int i = 1; i <= cnt; i++) {
            if (in[i] == 0) res++;
        }

        out.print(res + "\n");

    }


    private static void dfs(int x, int n) {
        low[x] = num[x] = tim++;
        vis[x] = true;
        stk.push(x);
        for (int v : G[x]) {
            if (scc[v] != -1) continue;
            if (!vis[v]) dfs(v, n);
            low[x] = Math.min(low[x], low[v]);
        }

        vis[x] = false;
        if (low[x] == num[x]) {
            int cur;
            cnt++;
            do {
                cur = stk.peek();
                stk.pop();
                scc[cur] = cnt;
            } while (cur != x);
        }
    }
    static class Scanner{
        public BufferedReader reader;
        public StringTokenizer st;

        public Scanner(InputStream stream){
            reader = new BufferedReader(new InputStreamReader(stream));
            st = null;
        }

        public String next(){
            while(st == null || !st.hasMoreTokens()){
                try{
                    String line  = reader.readLine();
                    if(line == null) return null;
                    st =  new StringTokenizer(line);
                }catch (Exception e){
                    throw (new RuntimeException());
                }
            }
            return st.nextToken();
        }

        public int nextInt(){
            return Integer.parseInt(next());
        }
        public long nextLong(){
            return Long.parseLong(next());
        }
        public double nextDouble(){
            return Double.parseDouble(next());
        }
    }
    static class OutputWriter{
        BufferedWriter writer;

        public OutputWriter(OutputStream stream){
            writer = new BufferedWriter(new OutputStreamWriter(stream));
        }

        public void print(int i) throws IOException {
            writer.write(i);
        }

        public void print(String s) throws IOException {
            writer.write(s);
        }

        public void print(char []c) throws IOException {
            writer.write(c);
        }
        public  void close() throws IOException {
            writer.close();
        }
    }
}
```



