
## dfs暴搜

[AcWing 5556. 牛的语言学](https://www.acwing.com/solution/content/199599/)



## dfs枚举

[飞机降落](https://www.dotcpp.com/oj/problem3151.html)



[景区导游 暴力42分](https://www.dotcpp.com/oj/problem3156.html)



## 迭代加深搜索

[P1763 埃及分数](https://www.luogu.com.cn/problem/P1763)



## BFS遍历图

[岛屿个数](https://www.acwing.com/problem/content/4962/)





## BFS板子

~~~cpp
// [蓝桥杯 2019 省 A] D 迷宫 
#include <queue>
#include <cstdio>
#include <cstring>
#include <iostream>

using namespace std;

int m = 30, n = 50;
char map[70][70];
bool vis[70][70];
char dirc[4] = { 'D','L','R','U' };
int dir[4][2] = { {1,0},{0,-1},{0,1},{-1,0} };

struct Node {
	string str;
	int x, y, step;
	Node(int xx, int yy, int ss, string s) {
		x = xx; y = yy; step = ss; str = s;
	}
};

queue<Node> que;

bool check(int x, int y) {
	if (x<0 || x>m - 1 || y<0 || y>n - 1 || vis[x][y] || map[x][y] == '1')
		return false;
	return true;
}

void bfs(int x, int y) {
	que.push(Node(0, 0, 0, ""));
	vis[0][0] = true;

	while (!que.empty()) {
		Node now = que.front();

		if (now.x == m - 1 && now.y == n - 1) {
			cout << now.str << endl;
			cout << now.step << endl;
			break;
		}
		que.pop();
		for (int i = 0; i < 4; i++) {
			int xx = now.x + dir[i][0];
			int yy = now.y + dir[i][1];
			if (check(xx, yy)) {
				que.push(Node(xx, yy, now.step + 1, now.str + dirc[i]));
				vis[xx][yy] = true;
			}
		}
	}
}

int main() {
	for (int i = 0; i < m; i++)
		scanf("%s", map[i]);
	bfs(0, 0);
	return 0;
}

~~~

