![image-20230223173033167](C:\Users\86136\AppData\Roaming\Typora\typora-user-images\image-20230223173033167.png)

```cpp
1.1用binary_search进行二分查找（用法一）

在从小到大排好序的基本类型数组上进行二分查找

　　binary_search(数组名+n1, 数组名+n2,值);

　　
1.2用binary_search进行二分查找（用法二）

在用自定义排序规则排好序的、元素为任意的T类型的数组中进行二分查找。

　　binary_search(数组名+n1, 数组名+n2, 值, 排序规则结构名());

2.1用lower_bound二分查找下界（用法一）

在对元素类型为T的从小到大排好序的基本类型的数组中进行查找

　　T * lower_bound(数组名+n1, 数组名+n2, 值);

　　返回一个指针 T * p;

*p 是查找区间里下标最小的，大于等于值的元素。如果找不到，p指向下标为n2的元素。（反正n2不在查找区间内，要是要写判断可以用这个作为依据）

2.2用lower_bound二分查找下界（用法二）

在元素为任意的T类型、按照自定义排序规则排好序的数组中进行查找

　　T * lower_bound(数组名+n1, 数组名+n2, 值, 排序规则名());

　　返回一个指针 T * p;

*p是查找区间里下标最小的，按自定义排序规则，可以排在“值”后面的元素。如果找不到，p指向下标为n2的元素。

3.1用upper_bound二分查找上界（用法一）

在对元素类型为T的从小到大排好序的基本类型的数组中进行查找

　　T * upper_bound(数组名+n1, 数组名+n2, 值);

　　返回一个指针 T * p;

*p 是查找区间里下标最小的，大于值的元素。如果找不到，p指向下标为n2的元素。（这里是大于，不要和前面弄混了）

3.2用upper_bound二分查找上界（用法二）

在元素为任意的T类型、按照自定义排序规则排好序的数组中进行查找

　　T * upper_bound(数组名+n1, 数组名+n2, 值, 排序规则名());

　　返回一个指针 T * p;

*p是查找区间里下标最小的，按自定义排序规则，必须排在“值”后面的元素。如果找不到，p指向下标为n2的元素。
```



```cpp
///////vector 示例 
#include <iostream>
#include <cstring>
#include <algorithm>
#include <vector>
using namespace std;

vector<int> v;

int main(){
  int n,x;
  cin>>n;
  for(int i=0;i<n;i++){
    cin>>x;
    v.push_back(x);
  }
  
  for(int i=0;i<v.size();i++)cout<<v[i]<<' ';
  puts("");
  sort(v.begin(),v.end()); 
  for(int e:v)cout<<e<<' ';
  puts("");
  reverse(v.begin(),v.end());
  for(int e:v)cout<<e<<' ';
}

///////vector 示例
#include <iostream>
#include <cstring>
#include <algorithm>
#include <vector>
using namespace std;

struct edge{
  int u,v,w;
  bool operator<(const edge &t)const
  {return w < t.w;}  
};
vector<edge> es;//边集 

int main(){
  int m,a,b,c;
  cin>>m;
  for(int i=1;i<=m;i++){ 
    cin>>a>>b>>c,
    es.push_back({a,b,c});
  }
  sort(es.begin(),es.end());
  for(int i=0;i<es.size();i++)
    printf("%d %d %d\n",es[i].u,es[i].v,es[i].w);
  // for(auto e : es)
  //   printf("%d %d %d\n",e.u,e.v,e.w);
}

///////stack 示例
#include <iostream>
#include <stack>
using namespace std;
stack<int> s;

int main(){
  int n,x;
  cin>>n;
  for(int i=1;i<=n;i++){
    cin>>x;
    s.push(x);
  }
  while(s.size()){
    cout<<s.top()<<'\n';
    s.pop();
  }
}
///////手写栈 示例
#include <iostream>
using namespace std;
int s[10000],top;

int main(){
  int n,x;
  cin>>n;
  for(int i=1;i<=n;i++){
    cin>>x;
    s[++top]=x;
  }
  while(top){
    cout<<s[top]<<'\n';
    top--;
  }
}

///////queue 示例
#include <iostream>
#include <queue>
using namespace std;
const int N=100010;
vector<int> e[N];
int vis[N];
queue<int> q;

void bfs(){
  vis[1]=1;q.push(1);
  while(q.size()){
    int x=q.front();q.pop();
    cout<<x<<endl;
    for(auto y : e[x]){
      if(vis[y])continue;
      vis[y]=1; //标记
      q.push(y);
    }
  }
}
int main(){
  int n, m, a, b;
  cin>>n>>m;
  for(int i=0;i<m;i++){
    cin>>a>>b;
    e[a].push_back(b);
    e[b].push_back(a);//加边
  }
  bfs();
}

///////priority_queue 示例
priority_queue<int> q1; // 默认大根堆, 即每次取出的元素是队列中的最大值
priority_queue<int, vector<int>, less<int> > q2; 
// 大根堆, 每次取出的元素是队列中的最大值，同第一行

priority_queue<int, vector<int>, greater<int> > q3; 
// 小根堆, 每次取出的元素是队列中的最小值


#include <iostream>
#include <queue>
using namespace std;

const int N=100010;
int n,m,s,a,b,c;
struct edge{int v,w;};
vector<edge> e[N];
int d[N], vis[N];
priority_queue<pair<int,int>> q;
        
void dijkstra(){
  for(int i=0;i<=n;i++) d[i]=1e9;
  d[1]=0; q.push({0,1});
  while(q.size()){
    auto t=q.top(); q.pop();
    int u=t.second;
    if(vis[u])continue;
    vis[u]=1; //标记
    for(auto ed : e[u]){
      int v=ed.v, w=ed.w;
      if(d[v]>d[u]+w){
        d[v]=d[u]+w;
        q.push({-d[v],v});
      }
    }
  }
}
int main(){
  cin>>n>>m;
  for(int i=0; i<m; i++){
    cin>>a>>b>>c;
    e[a].push_back({b,c});
  }
  dijkstra();
}

///////unordered_set 示例
#include <iostream>
#include <unordered_set>
using namespace std;

unordered_set<int> s;

int main(){
  int n,c,x; 
  cin>>n;
  while(n--){
    cin>>c>>x;
    if(c==1)s.insert(x);
    else
      s.count(x)?puts("Yes"):puts("No");
  }
}

///////unordered_map 示例
#include <iostream>
#include <unordered_map>
using namespace std;

unordered_map<string,int> h;

int main(){
  int n,c; string str; 
  cin>>n;
  while(n--){
    cin>>c>>str;
    if(c==1)h[str]++;
    else{
      if(h.count(str))
        printf("%d\n",h[str]);
      else
        puts("No");
    }
  }
}
```

