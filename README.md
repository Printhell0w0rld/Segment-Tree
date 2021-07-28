# Segment-Tree
```cpp
#include <bits/stdc++.h>
using namespace std;
#define ll long long
#define fast  ios::sync_with_stdio(0);cin.tie(0);
#define eb emplace_back
#define pb push_back
#define ff first
#define ss second
#define gcd __gcd
const int mod=1e9+7;

const int Max=1e5;
ll arr[Max],tree[4*Max];
 
void build(int idx,int l,int r){
    if(l==r){
        tree[idx]=arr[l];
    }
    else{
       int m=(l+r)/2;
       build(idx*2,l,m);
       build(idx*2+1,m+1,r); 
       tree[idx] =tree[idx*2]+tree[idx*2+1]; 
    }
}
 
ll query(int ql, int qr, int idx, int l, int r){
    if(l>=ql and r<=qr){
        return tree[idx];
    }
    int m = (l+r)/2;
    if(ql > m){
        return query(ql, qr, idx*2+1, m+1, r);
    }
    if(qr <= m){
        return query(ql, qr, idx*2, l, m);
    }
    return query(ql, qr, idx*2, l, m)+query(ql, qr, idx*2+1, m+1, r);
}
 
void update(int pos, int val, int idx, int l, int r){
    if(l==r){
        tree[idx] = val;
        return;
    }
    int m = (l+r)/2;
    if(pos <= m) update(pos, val, idx*2, l, m);
    else update(pos, val, idx*2+1, m+1, r);
    tree[idx] = tree[idx*2]+tree[idx*2+1]; 
}
 
int main(){
    fast;
    int n,m;cin>>n>>m;
    for(int i=0;i<n;i++){
        cin>>arr[i];
    }
    build(1, 0, n-1);
    for(int i=0;i<m;i++){
        int a,b,c;cin>>a>>b>>c;
        if(a==1){
            update(b, c, 1, 0, n-1);
        }
        else{
            cout<<query(b, c-1, 1, 0, n-1) << "\n";
        }   
    }
}
```
