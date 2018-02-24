## A

```cpp
#include <iostream>
using namespace std;
int n;
int main() {
	cin >> n;
	int res = 0;
	for (int i = 1; i < n; i++) {
		if (n % i == 0) res++;
	}
	cout << res << endl;
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
        for (int i = 1; i < n; i++) {
            if (n % i == 0) res++;
        }
        System.out.println(res);
    }
}

```

---

## B

```cpp
#include <iostream>
using namespace std;
int n;
string s;
int cas = 0;
int main() {
	int T;
	cin >> T;
	while (T--) {
		cin >> n >> s;
		int res = 0;
		int pre = -100;
		for (int i = 0; i < n; i++) {
			if (s[i] == '#') continue;
			if (pre + 2 >= i) continue;
			res++;
			pre = i;
		}
		cout << "Case " << ++cas << ": " << res << endl;
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
        int cas = 0;
        while (T-- > 0) {
            int n = cin.nextInt();
            String s = cin.next();
            int res = 0, pre = -100;
            for (int i = 0; i < n; i++) {
                if (s.charAt(i) == '#') continue;
                if (pre + 2 >= i) continue;
                res++;
                pre = i;
            }
            System.out.println("Case " + (++cas) + ": " + res);
        }
    }
}
```

---

## C

```cpp
#include <iostream>
#include <algorithm>
using namespace std;
const int N = 105;
int n, r, d;
int a[N], b[N];
int main() {
	while (cin >> n >> d >> r) {
		if (n == 0 && r == 0 && d == 0) break;
		for (int i = 0; i < n; i++) cin >> a[i];
		for (int i = 0; i < n; i++) cin >> b[i];
		
		int hour = 0;
		sort(a, a + n);
		sort(b, b + n);
		for (int i = 0; i < n; i++) {
			hour += max(a[i] + b[n - 1 - i] - d, 0);
		}
		cout << hour * r << endl;
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
            int n = cin.nextInt(), d = cin.nextInt(), r = cin.nextInt();
            if (n == 0 && r == 0 && d == 0) break;
            ArrayList<Integer> a = new ArrayList<>();
            ArrayList<Integer> b = new ArrayList<>();

            for (int i = 0; i < n; i++) {
                a.add(cin.nextInt());
            }

            for (int i = 0; i < n; i++) {
                b.add(cin.nextInt());
            }

            Collections.sort(a);
            Collections.sort(b, Collections.reverseOrder());
            int hour = 0;
            for (int i = 0; i < n; i++) {
                hour += Math.max(a.get(i) + b.get(i) - d, 0);
            }
            System.out.println(hour * r);
        }
    }
}
```

---

## D

```cpp
#include <iostream>
#include <algorithm>
using namespace std;
unsigned int n, l, u, m;
int main() {
	while (cin >> n >> l >> u) {
		m = 0;
		for (int i = 31; i >= 0; i--) {
			int bitl = (l >> i) & 1, bitu = (u >> i) & 1;
			if (bitl == bitu) {
				m |= bitl * (1u << i);
			} else {
				if ((n >> i) & 1) {
					u = (1u << i) - 1;
				} else {
					m |= (1u << i);
					l = (1u << i);
				} 
			}
		}
		cout << m << endl;
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
            long n = cin.nextLong(), l = cin.nextLong(), u = cin.nextLong();
            long res = 0;
            for (int i = 31; i >= 0; i--) {
                long bitl = (l >> i) & 1, bitu = (u >> i) & 1;
                if (bitl == bitu) {
                    res |= (1l << i) * bitl;
                } else {
                    if ((int)((n >> i) & 1) == 1) {
                        u = (1l << i) - 1;
                    } else {
                        res |= (1l << i);
                        l = 1l << i;
                    }
                }
            }
            System.out.println(res);
        }
    }
}
```



