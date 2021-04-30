# ITXMGL
#include <bits/stdc++.h>
 
using namespace std;
int cnt,n; 
char s[10]; 
char ans[101][101];
bool flas[101];
 
struct st{
    char id; 
    int left = -1; 
    int right = -1;
    vector<char>var;
}node[101];
bool find_var(int i, char c)
{
    int len = node[i].var.size();
    for(int k = 0; k < len; k ++)
    {
        if(node[i].var[k] == c)
        {
            return true;
        }
    }
    return false;
}
int add_node(char c)
{
    // 遍历当前已经建立的结点
    for(int i = cnt - 1; i >= 0; i --)
    {
        if(node[i].id == c || find_var(i,c))
        {
            return i;
        }
    }
    node[cnt].id = c;
    return cnt ++;
}
void add_operator(char c, char op, int l, int r)
{
    for(int i = cnt - 1; i >= 0; i --)
    {
        if(op == node[i].id && node[i].left == l && node[i].right == r)
        {
            node[i].var.push_back(c);
            return ;
        }
    }
    node[cnt].id = op;
    node[cnt].left = l;
    node[cnt].right = r;
    node[cnt].var.push_back(c);
    cnt ++;
}
void dfs(int i){
    if(node[i].left != -1)
    {
        flas[i] = 1;
        dfs(node[i].left);
        dfs(node[i].right);
    }
}
char ok(int i)
{
    int len = node[i].var.size();
    for(int k = 0; k < len; k++)
    {
        if(node[i].var[k] == 'A' || node[i].var[k] == 'B')
        {
            return node[i].var[k];
        }
    }
    return node[i].var[0];
}
int main()
{
    cnt = 0;
    cin >> n;
    for(int i = 0; i < n; i ++)
    {
        cin >> s;
        int l = add_node(s[2]);
        int r = add_node(s[4]);
        add_operator(s[0],s[3],l,r);
    }
    for(int i = 0; i < cnt; i ++)
    {
        if(node[i].left != -1){
            ans[i][0] = ok(i);
            ans[i][1] = '=';
            st ll = node[node[i].left];
            st rr = node[node[i].right];
            ans[i][2] = ll.left != -1 ? ok(node[i].left) : ll.id;
            ans[i][3] = node[i].id;
            ans[i][4] = rr.left != -1 ? ok(node[i].right) : rr.id;
            ans[i][5] = '\0';
        }
    }
    for(int i = cnt - 1; i >= 0; i --)
    {
        if(ans[i][0] == 'A')
        {
            dfs(i);
            break;
        }
    }
     for(int i = cnt - 1; i >= 0; i --)
    {
        if(ans[i][0] == 'B')
        {
            dfs(i);
            break;
        }
    }
    for(int i = 0; i < cnt; i ++)
    {
        if(flas[i])
        {
            puts(ans[i]);
        }
    }
    return 0;
}
 
