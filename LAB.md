### PROGRAM 1 : Quicksort 
```python
def q_sort (a,low,high):
    if low < high :
        pivotpos = partition(a,low,high) 
        q_sort (a,low,pivotpos-1) 
        q_sort (a,pivotpos+1,high) 
 
def partition (a, low, high):
    pivotvalue = a[low] 
    up = low + 1 
    down = high 
    done = False
    while not done:
        while up<=down and a[up] <= pivotvalue:
            up += 1 
        while down>=up and a[down] >= pivotvalue:
            down -= 1 
        if down<up:
            done = True 
        else:
            temp = a[up] 
            a[up] = a[down] 
            a[down] = temp 
        temp = a[low] 
        a[low] = a[down] 
        a[down] = temp 
    return down 
    
print ("Enter elements into list") 
a =[int (x) for x in input().split()]	    
high = len (a) 
q_sort (a, 0, high - 1) 
print (a)
```
### PROGRAM 2 : Mergesort
```python
def m_sort(a):
    if len(a)>1:
        mid = len(a)//2
        l_half=a[:mid]
        r_half=a[mid:]
        m_sort(l_half)
        m_sort(r_half)
        i=j=k=0
        while i<len(l_half) and j<len(r_half):
            x=l_half[i]
            y=r_half[j]
            if x<y:
                a[k]=l_half[i]
                i+=1
            else:
                a[k]=r_half[j]
                j+=1
            k+=1
        while i<len(l_half):
                a[k]=l_half[i]
                i+=1
                k+=1
        while j<len(r_half):
                a[k]=r_half[j]
                j+=1
                k+=1
                
def printList(array):
    for m in range(len(array)):
        print(array[m])
    
    
print("Enter elements into list : ")
a=[int(x) for x in input().split()]
m_sort(a)
printList(a)
```
### PROGRAM 3 : Warshall's Algorithm
```python
n=int(input("Enter the number of nodes:")) 
cost=[[0 for i in range(n)] for j in range(n)] 
print("Enter the adjacency matrix in integers:")
for i in range(n):
  for j in range(n):
    temp=int(input()) 
    cost[i][j]=temp
print("The adjacency matrix in integers:") 
for i in range(n):
   for j in range(n):
    if cost[i][j]==999:
     print("INF",end="\t")
    else:
         print(cost[i][j],end="\t") 
print("\n")
for k in range(n): 
    for i in range(n):
       for j in range(n): 
           cost[i][j]=min(cost[i][j],cost[i][k]+cost[k][j])
print("**FLOYD WARSHALL***") 
for i in range(n):
   for j in range(n):
       if cost[i][j]==999: 
               print("INF",end="\t")
else:
              print(cost[i][j],end="\t") 
              print("\n")
```
### PROGRAM 5 : Knapsack
```python
def show(W,n,wt,V): 
    i=n
    w=W
    print("The items entered into the knapsack are:") 
    while i>0 and w>0:
        if V[i][w]!=V[i-1][w]:
            print(i,"item with weight",wt[i]) 
            w=w-wt[i]
            i=i-1 
        else:
            i=i-1
    print("Weight taken into the sack is",W-w,"with having maximum value",V[n][W]) 
def knapsack(W,n,val,wt):
    V=[[0 for j in range(W+2)]  for i in range(n+2)]
    for i in range(n+1):
        for w in range(W+1): 
            if wt[i]<=w:
                V[i][w]=max(V[i-1][w],(val[i]+V[i-1][w-wt[i]])) 
            else:
                V[i][w]=V[i-1][w]
            print(V[i][w],end="\t")
        print("\n")
    show(W,n,wt,V)
    
n=int(input("Enter the items:"))
val=[0 for i in range(0,n+1,1)]
wt=[0 for i in range(0,n+1,1)]
print("Enter the values of products:")
for i in range(1,n+1,1):
    temp=int(input())
    val[i]=temp
print("Enter the weights of products:") 
for i in range(1,n+1,1):
    temp=int(input()) 
    wt[i]=temp
W=int(input("Enter the maximum capacity of knapsack:")) 
knapsack(W,n,val,wt)

```
### PROGRAM 6 : Dijkstra
```python
def dij(n,v,cost,dist):
    flag=[0 for x in range(1,n+2,1)] 
    for i in range(1,n+1,1):
        flag[i]=0 
        dist[i]=cost[v][i]
        count=2
        while count<=n: 
            mini=99
            for w in range(1,n+1,1):
                if (dist[w] < mini and not(flag[w])): 
                    mini=dist[w]
                u=w 
                flag[u]=1 
                count=count+1
                for w in range(1,n+1,1):
                    if ((dist[u]+cost[u][w]<dist[w]) and not(flag[w])): 
                        dist[w]=dist[u]+cost[u][w]

n=int(input("Enter number of nodes:"))
cost=[[0 for j in range(1,n+2,1)] for i in range(1,n+2,1)] 
print("Enter the adjacency matrix:")
for i in range(1,n+1,1): 
    for j in range(1,n+1,1):
        temp=int(input()) 
        cost[i][j]=temp
        if cost[i][j]==0: 
            cost[i][j]=999
v=int(input("Enter the source node:")) 
dist=[0 for i in range(1,n+2,1)] 
dij(n,v,cost,dist)
print("****Shortest path****") 
for i in range(1,n+1,1):
    if(i!=v):
        print(v,"->",i,"cost=",dist[i])

```
### PROGRAM 6 : Kruskal's (minimum cost spanning tree)
```python
maxi=9999999
n=int(input("Enter the number of nodes:"))
parent=[0 for i in range(n)]
def find(i):
    while parent[i]!=i:
        i=parent[i]
    return i
def uni(i,j):
    x=find(i)
    y=find(j)
    parent[x]=y
def main(n,cost):
    mincost=0
    for i in range(n):
        parent[i]=i
    e_ctr=0
    while e_ctr<n-1:
        mini=maxi
        a=0
        b=0
        for i in range(n):
            for j in range(n):
                if(cost[i][j]<=mini and find(i)!=find(j)):
                    mini=cost[i][j]
                    a=i
                    b=j
        uni(a,b)
        print("Edge",e_ctr+1,":(",a+1,",",b+1,")cost:",mini)
        e_ctr+=1
        mincost=mincost+mini
        print("Minimum cost=",mincost)
cost=[[0 for i in range(n)]for j in range(n)]
for i in range(n):
    for j in range(n):
        temp=int(input())
        cost[i][j]=temp
if cost[i][j]==0:
    cost[i][j]=maxi
main(n,cost)

```
### PROGRAM 9 : Sum of Subsets
```python
b=[]
def solution(a,n,subset,s): 
    global ctr
    ctr=0
    if s==0:
        b.append(subset)
        return
    if n==0:
        return
    if a[n-1]<=s:
        solution(a,n-1,subset,s)
        solution(a,n-1,subset+str(a[n-1])+" ",s-a[n-1]) 
    else:
        solution(a,n-1,subset,s) 
print("Enter the list of integers",end=":")
a=[int(x) for x in input().split()] 
s=int(input("Enter the sum value:")) 
subset=""
solution(a,len(a),subset,s)
ctr=1
for i in b:
    print("Solution",ctr,">",i)
    ctr=ctr+1
print("The total number of solution for sum of subsets is",len(b))

```
### PROGRAM 10 :  TSP
```python
n=int(input("Enter number of nodes:"))
cost=0
def main():
 global a,visit
 a=[[0 for i in range(n)] for j in range(n)]
 visit=[0 for i in range(n)]
 for i in range(n):
     for j in range(n):
         temp=int(input())
         a[i][j]=temp
 for i in range(n):
     for j in range(n):
         print(a[i][j],end="\t")
     print("\n")
 print("Path is")
 mincost(0)
def mincost(c):
 global cost
 visit[c]=1
 print(c+1,end="-->")
 x=least(c)
 if x==999:
     x=0
     print(x+1)
     cost=cost+a[c][x]
     return
 mincost(x)
def least(u):
 global cost
 mini=v=999
 for i in range(n):
     if a[u][i]!=0 and visit[i]==0:
         if a[u][i]+a[i][u]<mini:
             mini=a[i][u]+a[u][i]
             kmin=a[u][i]
             v=i
 if mini!=999:
     cost=cost+kmin
 return v
main()
print("Minimum Cost is : ",cost)

```
### PROGRAM 12 : Warshall transtitive
```python
n = int(input("Enter the number of nodes : "))
graph = [[0 for i in range(n)]for j in range(n)]
print("Enter the adjacency matrix in boolean values : ")
for i in range(n):
    for j in range(n):
        temp = int(input())
        graph[i][j] = temp
print("The adjacency matrix in boolean values : ")
for i in range(n):
    for j in range(n):
        print(graph[i][j],end="\t")
    print("\n")
for k in range(n):
    for i in range(n):
        for j in range(n):
            if(graph[i][k]==1 and graph[k][j]==1):
                graph[i][j] = 1
print("***WARSHALL'S TRANSITIVE CLOSURE***")
for i in range(n):
    for j in range(n):
        print(graph[i][j],end="\t")
    print("\n")

```
### PROGRAM 13 : NQueens Problem 
```python
board = [0 for i in range(20)]
ctr = 0
def printx(n):
    global ctr
    ctr = ctr+1
    print("Solution ",ctr)
    for i in range(1,n+1,1):
        for j in range(1,n+1,1):
            if(board[i]==j):
                print("Q",end=" ")
            else:
                print("-",end=" ")
        print("\n")
    print("__________")
def place(r,c):
    for i in range(1,r,1):
        if(board[i]==c):
            return 0
        else:
            if(abs(board[i]-c)==abs(i-r)):
                return 0
    return 1
def queen(r,n):
    for c in range(1,n+1,1):
        if(place(r,c)):
            board[r] = c
            if(r==n):
                printx(n)
            else:
                queen(r+1,n)
print("***NQueens Problem Using Backtracking****")
n = int(input("\n Enter number of Queens : "))
queen(1,n)
print("The number of solutions for ",n," Queens problem ",ctr)
```