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
int n;
int main() {
    while (cin >> n) {
        cout << n / 3 << endl;
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
            int n = cin.nextInt();
            System.out.println(n / 3);
        }
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
const int N = 2e4 + 10;
const int INF = 0x3f3f3f3f;
vector<pair<int, int>> G[N];
int n, m, s, t;
#define pb push_back
#define mp make_pair
#define fi first
#define se second

int dis[N];
void dijkstra(int c, int s, int t) {
    for (int i = 0; i < n; i++) dis[i] = INF;
    priority_queue<pair<int, int> > pq;
    dis[s] = 0;
    pq.push(mp(-dis[s], s));
    while (pq.size()) {
        auto cur = pq.top();
        pq.pop();
        int u = cur.se;
        if (-cur.fi > dis[u]) continue;
        for (auto p : G[u]) {
            int v = p.fi, w = p.se;
            if (dis[u] + w < dis[v]) {
                dis[v] = dis[u] + w;
                pq.push(mp(-dis[v], v));
            }
        }
    }
    cout << "Case #" << c << ": ";
    if (dis[t] == INF) {
        cout << "unreachable" << endl;
    } else {
        cout << dis[t] << endl;
    }
}
int main() {
    int cas; cin >> cas;
    for (int c = 1; c <= cas; c++) {
        cin >> n >> m >> s >> t;
        for (int i = 0; i < n; i++) G[i].clear();
        int u, v, w;
        for (int i = 0; i < m; i++) {
            cin >> u >> v >> w;
            G[u].pb(mp(v, w));
            G[v].pb(mp(u, w));
        }
        dijkstra(c, s, t);
    }
    return 0;
}
```

```java
import java.util.*;

public class Main {
    static final int INF = 0x3f3f3f3f;
    static class Pair {
        int to, dis;
        Pair(int to, int dis) {
            this.to = to;
            this.dis = dis;
        }
    }

    public static void main(String[] args) {
        Scanner cin = new Scanner(System.in);
        int cas = cin.nextInt();
        for (int c = 1; c <= cas; c++) {
            int n = cin.nextInt();
            int m = cin.nextInt();
            int s = cin.nextInt();
            int t = cin.nextInt();
            ArrayList<Pair> G[] = new ArrayList[n];
            for (int i = 0; i < n; i++) {
                G[i] = new ArrayList<>();
            }
            int u, v, w;
            for (int i = 0; i < m; i++) {
                u = cin.nextInt();
                v = cin.nextInt();
                w = cin.nextInt();
                addEdge(G, u, v, w);
            }
            dijkstra(c, G, n, s, t);
        }
    }

    private static void dijkstra(int c, ArrayList<Pair>[] G, int n, int s, int t) {
        PriorityQueue<Pair> pq = new PriorityQueue<>(new Comparator<Pair>() {
            @Override
            public int compare(Pair o1, Pair o2) {
                return o1.dis - o2.dis;
            }
        });
        int dist[] = new int[n];
        for (int i = 0 ; i < n; i++) dist[i] = INF;
        dist[s] = 0;
        pq.offer(new Pair(s, dist[s]));
        while (!pq.isEmpty()) {
            Pair cur = pq.peek();
            pq.poll();
            int u = cur.to, w = cur.dis;
            if (w > dist[u]) continue;
            for (Pair pair : G[u]) {
                if (dist[u] + pair.dis < dist[pair.to]) {
                    dist[pair.to] = dist[u] + pair.dis;
                    pq.offer(new Pair(pair.to, dist[pair.to]));
                }
            }
        }

        if (dist[t] == INF) {
            System.out.printf("Case #%d: unreachable\n", c);
        } else {
            System.out.printf("Case #%d: %d\n", c, dist[t]);
        }
    }

    private static void addEdge(ArrayList<Pair>[] G, int u, int v, int w) {
        G[u].add(new Pair(v, w));
        G[v].add(new Pair(u, w));
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
int n;
string get() {
    string s;
    getline(cin, s);
    return s;
}

int bfs(vector<string>& dic, string s, string t) {
    if (s == t) return 0;
    set<string> words(dic.begin(), dic.end());
    set<string> vis;
    int res = 0;
    queue<pair<int, string>> que;
    que.push(make_pair(0, s));
    while (que.size()) {
        auto cur = que.front();
        que.pop();
        int d = cur.first;
        string str = cur.second;
        for (int i = 0; i < str.size(); i++) {
            for (int j = 0; j < 26; j++) {
                string tmp = str;
                tmp[i] = 'a' + j;
                if (words.find(tmp) != words.end() && vis.find(tmp) == vis.end()) {
                    if (tmp == t) return d + 1;
                    vis.insert(tmp);
                    que.push(make_pair(d + 1, tmp));
                }
            }
        }
    }
}

void solve() {
    string word;
    vector<string> dic;
    while((word = get()) != "*") {
        dic.push_back(word);
    }

    while((word = get()) != "") {
        int pos = word.find(" ");
        string s = word.substr(0, pos);
        string t = word.substr(pos + 1);
        cout << s << " " << t << " " <<  bfs(dic, s, t) << endl;
    }
}
int main() {
    int T; cin >> T;
    get();
    while (T--) {
        solve();
        if (T) cout << endl;
    }
    return 0;
}


```

```java
import java.util.*;

public class Main {
    static class Pair {
        int d;
        String s;

        public Pair(int d, String s) {
            this.d = d;
            this.s = s;
        }
    }
    public static void main(String[] args) {
        Scanner cin = new Scanner(System.in);
        int cas = Integer.parseInt(cin.nextLine());
        cin.nextLine();
        for (int c = 1; c <= cas; c++) {
            solve(cin);
            if (c < cas) {
                System.out.println();
            }
        }

    }

    private static void solve(Scanner cin) {
        String word;
        HashSet<String> dic = new HashSet<>();
        while (!(word = cin.nextLine()).equals("*")) {
            dic.add(word);
        }

        while (cin.hasNext() && !(word = cin.nextLine()).equals("")) {
            String words[] = word.split(" ");
            System.out.println(words[0] + " " + words[1] + " " + bfs(dic, words[0], words[1]));
        }

    }

    private static int bfs(HashSet<String> dic, String s, String t) {
        if (s.equals(t)) return 0;
        HashSet<String> vis = new HashSet<>();
        Queue<Pair> queue = new LinkedList<>();
        queue.add(new Pair(0, s));
        vis.add(s);
        while (!queue.isEmpty()) {
            Pair pair = queue.poll();

            int d = pair.d;
            String str = pair.s;
            for (int i = 0; i < str.length(); i++) {
                for (int j = 0; j < 26; j++) {
                    StringBuilder sb = new StringBuilder(str);
                    sb.setCharAt(i, (char)(j + 'a'));
                    String tmp = sb.toString();

                    if (dic.contains(tmp) && !vis.contains(tmp)) {

                        if (t.equals(tmp)) {
                            return d + 1;
                        }
                        queue.add(new Pair(d + 1, tmp));
                        vis.add(tmp);
                    }
                }
            }


        }
        return 0;
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
const int N = 105;
const int INF = 0x3f3f3f3f;
int G[N][N];
int n, m;
int main() {
    int cas; cin >> cas;
    for (int c = 1; c <= cas; c++) {
        cin >> n >> m;
        for (int i = 0; i < n; i++) {
            for (int j = 0; j < n; j++) {
                if (i == j) G[i][j] = 0;
                else G[i][j] = INF;
            }
        }
        for (int i = 0; i < m; i++) {
            int u, v;
            cin >> u >> v;
            G[u][v] = 1;
            G[v][u] = 1;
        }
        for (int k = 0; k < n; k++) {
            for (int i = 0; i < n; i++) {
                for (int j = 0; j < n; j++) {
                    G[i][j] = min(G[i][k] + G[k][j], G[i][j]);
                }
            }
        }
        int res = 0;
        int s, t;
        cin >> s >> t;
        for (int i = 0; i < n; i++) {
            res = max(res, G[s][i] + G[i][t]);
        }
        printf("Case %d: %d\n", c, res);
    }
    return 0;
}

```

```java
import java.util.*;

public class Main {
    static final int INF = 0x3f3f3f3f;

    public static void main(String[] args) {
        Scanner cin = new Scanner(System.in);
        int cas = cin.nextInt();
        for (int c = 1; c <= cas; c++) {
            int n = cin.nextInt(), m = cin.nextInt();
            int G[][] = new int[n][n];
            for (int i = 0; i < n; i++) {
                for (int j = 0; j < n; j++) {
                    if (i == j) G[i][j] = 0;
                    else G[i][j] = INF;
                }
            }
            for (int i = 0; i < m; i++) {
                int u = cin.nextInt(), v = cin.nextInt();
                G[u][v] = G[v][u] = 1;
            }
            for (int k = 0; k < n; k++) {
                for (int i = 0; i < n; i++) {
                    for (int j = 0; j < n; j++) {
                        G[i][j] = Math.min(G[i][j], G[i][k] + G[k][j]);
                    }
                }
            }
            int res = 0;
            int s = cin.nextInt(), t = cin.nextInt();
            for (int i = 0; i < n; i++) {
                res = Math.max(res, G[s][i] + G[i][t]);
            }
            System.out.printf("Case %d: %d\n", c, res);
        }
    }

}
```



