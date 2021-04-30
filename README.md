# ITXMGL
#include<bits/stdc++.h>
using namespace std;
int i = 0;
int num = 0;
string s;
void E();
void F();
void T();
void G();
void S();

void E()
{
    if(s[i]=='i'||s[i]=='(')
    {
        cout << num << " E-->TG" << endl;
        num++;
        T();
        G();
    }
    else
    {
        cout << "error" << endl;
        exit(0);
    }
}
void T()
{
    if(s[i]=='i'||s[i]=='(')
    {
        cout << num << " T-->FS" << endl;
        num++;
        F();
        S();
    }
    else
    {
        cout << "error" << endl;
        exit(0);
    }
}
void G()
{
    if(s[i]=='+')
    {
        cout << num << " G-->+TG" << endl;
        num++;
        i++;
        T();
        G();
    }
    else
    {
        cout << num <<" G-->&" << endl;
        num++;
    }
}
void F()
{
    if(s[i]=='(')
    {
        cout << num << " F-->(E)" << endl;
        i++;
        num++;
        E();
        if(s[i]!=')')
        {
            cout << "error" << endl;
            exit(0);
        }
        i++;
    }
    else if(s[i]=='i')
    {
        cout << num << " F-->i" << endl;
        num++;
        i++;
    }
    else
    {
        cout << "error" << endl;
        exit(0);
    }
}
void S()
{
    if(s[i]=='*')
    {
        cout << num << " S-->*FS" << endl;
        i++;
        num++;
        F();
        S();
    }
    else
    {
        cout << num << " S-->&" << endl;
        num++;
    }
}
int main()
{
    cin >> s;
    E();
    if(s[i]!='#')
    {
        cout << "error" << endl;
        exit(0);
    }
    cout << "accept" << endl;
}
