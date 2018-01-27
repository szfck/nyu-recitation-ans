## A

```cpp
#include <iostream>
using namespace std;
int a, b;
int main() {
    while (cin >> a >> b) {
        a *= b;
        if (a % 2 == 1) cout << "Odd" << endl;
        else cout << "Even" << endl;
    }
    return 0;
}
```

```java
import java.util.Scanner;

public class Main {

    public static void main(String[] args) {
        Scanner cin = new Scanner(System.in);
        int a = cin.nextInt();
        int b = cin.nextInt();
        a *= b;
        if (a % 2 == 0) System.out.println("Even");
        else System.out.println("Odd");
    }
}
```

---

## B

```cpp
#include <iostream>
using namespace std;
int n, m, a;
int main() {
  while (cin >> n >> m >> a) {
      cout << 1ll * ((n + a - 1) / a) * ((m + a - 1) / a) << endl;
  }
  return 0;
}
```

```java
import java.util.Scanner;

public class Main {

    public static void main(String[] args) {
        Scanner cin = new Scanner(System.in);
        int a = cin.nextInt();
        int b = cin.nextInt();
        int c = cin.nextInt();
        System.out.println((long)((a + c - 1) / c ) * ((b + c - 1) / c));
    }
}
```

---

## C

```cpp
#include <vector>
#include <iostream>
using namespace std;
int n;
int main() {
    while (cin >> n) {
        vector<int> res;
        while (n) {
            res.push_back(n % 2);
            n /= 2;
        }
        for (int i = (int)res.size() - 1; i >= 0; i--) {
            cout << res[i];
        }
        cout << endl;
    }
    return 0;
```

```java
import java.util.ArrayList;
import java.util.Scanner;

public class Main {

    public static void main(String[] args) {
        Scanner cin = new Scanner(System.in);
        while (cin.hasNext()) {
            int n = cin.nextInt();
            ArrayList<Integer> a = new ArrayList<>();
            while (n > 0) {
                a.add(n % 2);
                n /= 2;
            }
            for (int i = a.size() - 1; i >= 0; i--) {
                System.out.print(a.get(i));
            }
            System.out.println();
        }
    }
}
```

---

## D

```cpp
#include <iostream>
using namespace std;
string a[3];
bool win() {
    for (int i = 0; i < 3; i++) {
        bool ok = a[i][0] != '.';
        for (int j = 1; j < 3; j++) {
            if (a[i][j] != a[i][j - 1]) ok = false;
        }
        if (ok) return true;
    }
    for (int j = 0; j < 3; j++) {
        bool ok = a[0][j] != '.';
        for (int i = 1; i < 3; i++) {
            if (a[i][j] != a[i - 1][j]) ok = false;
        }
        if (ok) return true;
    }
    bool ok = a[0][0] != '.';
    for (int i = 1; i < 3; i++) {
        if (a[i][i] != a[i - 1][i - 1]) ok = false;
    }
    if (ok) return true;
    ok = a[0][2] != '.';
    for (int i = 1; i < 3; i++) {
        if (a[i][2 - i] != a[i - 1][3 - i]) ok = false;
    }
    return ok;
}
string solve() {
    int x = 0, o = 0;
    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            if (a[i][j] == 'X') x++;
            else if (a[i][j] == '0') o++;
        }
    }
    char cur = '.';
    if (x == o) {
        cur = '0';
    } else if (x == o + 1){
        cur = 'X';
    } else {
        return "illegal";
    }

    for (int i = 0; i < 3; i++) {
        for (int j = 0; j < 3; j++) {
            if (a[i][j] == cur) {
                bool curWin = win();
                a[i][j] = '.';
                bool preWin = win();
                a[i][j] = cur;
                if (curWin && !preWin) {
                    if (cur == 'X') return "the first player won";
                    else return "the second player won";
                }
            }
        }
    }
    if (win()) return "illegal";
    if (o + x == 9) return "draw";
    return cur == 'X' ? "second" : "first";
}
int main() {
    for (int i = 0; i < 3; i++) {
        cin >> a[i];
    }
    cout << solve() << endl;
    return 0;
}
```

```java
import java.util.ArrayList;
import java.util.Scanner;

public class Main {
    static char[][] a = new char[3][3];
    public static void main(String[] args) {
        Scanner cin = new Scanner(System.in);
        for (int i = 0; i < 3; i++) {
            String s = cin.nextLine();
            for (int j = 0; j < 3; j++) {
                a[i][j] = s.charAt(j);
            }
        }

        System.out.println(solve());
    }

    private static String solve() {
        int x = 0, o = 0;
        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++) {
                if (a[i][j] == 'X') x++;
                else if (a[i][j] == '0') o++;
            }
        }
        char cur;
        if (x == o) cur = '0';
        else if (x == o + 1) cur = 'X';
        else return "illegal";

        for (int i = 0; i < 3; i++) {
            for (int j = 0; j < 3; j++) {
                if (a[i][j] == cur) {
                    boolean curWin = win();
                    a[i][j] = '.';
                    boolean preWin = win();
                    a[i][j] = cur;
                    if (curWin && !preWin) {
                        if (cur == 'X') return "the first player won";
                        else return "the second player won";
                    }
                }
            }
        }

        if (win()) {
            return "illegal";
        }

        if (o + x == 9) {
            return "draw";
        }

        return cur == 'X' ? "second" : "first";
    }

    private static boolean win() {
        return win('X') || win('0');
    }

    private static boolean win(char c) {
        for (int i = 0; i < 3; i++) {
            if (a[i][0] == c && a[i][1] == c && a[i][2] == c) return true;
            if (a[0][i] == c && a[1][i] == c && a[2][i] == c) return true;
        }
        if (a[0][0] == c && a[1][1] == c && a[2][2] == c) return true;
        if (a[0][2] == c && a[1][1] == c && a[2][0] == c) return true;
        return false;
    }
}
```



