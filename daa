Fractional Knapsack


#include <bits/stdc++.h>
using namespace std;
struct Item{
 int value, weight;
 Item(int value, int weight){
 this->value=value;
 this->weight=weight; }
};
bool cmp(Item a, Item b){
 double r1=(double)a.value/(double)a.weight;
 double r2=(double)b.value/(double)b.weight;
 return r1>r2;
}
double fractional_KnapSack(int W, Item arr[], int n)
{
sort(arr,arr+n,cmp);
int curr_wt=0;
double final_value=0;
for(int i=0;i<n;i++){
 if(curr_wt+arr[i].weight<=W){
 curr_wt+=arr[i].weight;
 final_value+=arr[i].value;
 }else{
 int remain_wt=W-curr_wt;
 final_value+=(double)remain_wt*(arr[i].value/arr[i].weight);
 break;
 }
}
return final_value;
}
int main()
{
int W = 50;
Item arr[] = { { 60, 10 }, { 100, 20 }, { 120, 30 } };
int N = sizeof(arr) / sizeof(arr[0]);
cout << fractional_KnapSack(W, arr, N);
return 0;
}








0/1 Knapsack using DP
#include <bits/stdc++.h>
using namespace std;
int knapSack(int capacity, int wt[], int val[], int n)
{
 vector<vector<int>> DP(n + 1, vector<int>(capacity + 1));
 for(int i = 0; i <= n; i++)
 {
 for(int w = 0; w <= capacity; w++)
 {
 if (i == 0 || w == 0)
 DP[i][w] = 0;
 else if (wt[i - 1] <= w)
 DP[i][w] = max(DP[i - 1][w],
 val[i - 1] +DP[i - 1][w - wt[i - 1]],);
 else
 DP[i][w] = DP[i - 1][w];
 }
 }
 return DP[n][capacity];
}
int main()
{
 int val[] = { 60, 100, 120 };
 int wt[] = { 10, 20, 30 };
 int capacity = 50;
 int n = sizeof(val) / sizeof(val[0]);
 cout << knapSack(capacity, wt, val, n);
 return 0;
}





Huffman Encoding
#include <bits/stdc++.h>
using namespace std;
struct MinHeapNode {
char data; unsigned freq;
MinHeapNode *left, *right;
MinHeapNode(char data, unsigned freq)
{
left = right = NULL;
this->data = data;
this->freq = freq;
}
};
struct compare {
bool operator()(MinHeapNode* l, MinHeapNode* r){
 return (l->freq > r->freq);}
};
void printCodes(struct MinHeapNode* root, string str)
{
if (!root)
return;
if (root->data != '$')
cout << root->data << ": " << str << "\n";
printCodes(root->left, str + "0");
printCodes(root->right, str + "1");
}
void HuffmanCodes(char data[], int freq[], int size)
{
struct MinHeapNode *left, *right, *top;
priority_queue<MinHeapNode*, vector<MinHeapNode*>, compare> minHeap;
for (int i = 0; i < size; ++i)
minHeap.push(new MinHeapNode(data[i], freq[i]));
while (minHeap.size() != 1) {
left = minHeap.top(); minHeap.pop();
right = minHeap.top(); minHeap.pop();
top = new MinHeapNode('$', left->freq + right->freq);
top->left = left; top->right = right;
minHeap.push(top);
}
printCodes(minHeap.top(), "");
}
int main()
{
char arr[] = { 'a', 'b', 'c', 'd', 'e', 'f' };
int freq[] = { 5, 9, 12, 13, 16, 45 };
int size = sizeof(arr) / sizeof(arr[0]);
HuffmanCodes(arr, freq, size);
return 0;
}







N-Queen
#include <iostream>
using namespace std;
#define N 8
void printBoard(int board[N][N])
{
for (int i = 0; i < N; i++)
{
for (int j = 0; j < N; j++)
{
cout << board[i][j] << " ";
}
cout << endl;
}
}
bool isValid(int board[N][N], int row, int col)
{
for (int i = 0; i < col; i++)
{
if (board[row][i])
{
return false;
}
}
for (int i = row, j = col; i >= 0 && j >= 0; i--, j--)
{
if (board[i][j])
{
return false;
}
}
for (int i = row, j = col; j >= 0 && i < N; i++, j--)
{
if (board[i][j])
{
return false;
}
}
return true;
}
bool solveNQueen(int board[N][N], int col)
{
if (col >= N)
{
return true;
}
for (int i = 0; i < N; i++)
{
if (isValid(board, i, col))
{
board[i][col] = 1;
if (solveNQueen(board, col + 1))
{
return true;
}
board[i][col] = 0;
}
}
return false;
}
bool checkSolution()
{
int board[N][N]={0};
if (solveNQueen(board, 0) == false)
{
cout << "Solution does not exist";
return false;
}
printBoard(board);
return true;
}






0/1 Knapsack using Branch and Bound
struct Item
{ float weight;int value; };
struct Node
{ int level, profit, bound; float weight; };
bool cmp(Item a, Item b)
{
 double r1 = (double)a.value / a.weight;
 double r2 = (double)b.value / b.weight;
 return r1 > r2;
}
int bound(Node u, int n, int W, Item arr[])
{
 if (u.weight >= W){
 return 0;}
 int profit_bound = u.profit;
 int j = u.level + 1;
 int totweight = u.weight;
 while ((j < n) && (totweight + arr[j].weight <= W))
 {
 totweight += arr[j].weight;
 profit_bound += arr[j].value;
 j++;
 }
 if (j < n)
 profit_bound += (W - totweight) * arr[j].value /
 arr[j].weight;
 return profit_bound;
}
int knapsack(int W, Item arr[], int n)
{
 sort(arr, arr + n, cmp);
 queue<Node> Q;
 Node u, v;
 u.level = -1;
 u.profit = u.weight = 0;
 Q.push(u);
 int maxProfit = 0;
 while (!Q.empty())
 {
 u = Q.front();
 Q.pop();
 if (u.level == -1){
 v.level = 0;}
 if (u.level == n-1){
 continue;}
 v.level = u.level + 1;
 v.weight = u.weight + arr[v.level].weight;
 v.profit = u.profit + arr[v.level].value;
 if (v.weight <= W && v.profit > maxProfit){
 maxProfit = v.profit; }
 v.bound = bound(v, n, W, arr);
 if (v.bound > maxProfit){
 Q.push(v);}
 v.weight = u.weight;
 v.profit = u.profit;
 v.bound = bound(v, n, W, arr);
 if (v.bound > maxProfit){
 Q.push(v); }
 }
 return maxProfit;
}







Quick Sort
#include<iostream>
#include<cstdlib>
#include<ctime>
#define MAX 100
using namespace std;
void random_shuffle(int arr[]) {
 srand(time(NULL));
 for (int i = MAX - 1; i > 0; i--) {
 int j = rand()%(i + 1);
 int temp = arr[i];
 arr[i] = arr[j];
 arr[j] = temp;
 }
}
int Partition(int a[], int low, int high) {
 int pivot, index, i;
 index = low;
 pivot = high;
 for(i=low; i < high; i++) {
 if(a[i] < a[pivot]) {
 swap(a[i], a[index]);
 index++;
 }
 }
 swap(a[pivot], a[index]);
 return index;
}
int RandomPivotPartition(int a[], int low, int high){
 int pvt, n, temp;
 n = rand();
 pvt = low + n%(high-low+1);
 swap(a[high], a[pvt]);
 return Partition(a, low, high);
}
void quick_sort(int arr[], int p, int q) {
 int pindex;
 if(p < q){
 pindex = RandomPivotPartition(arr, p, q);
 quick_sort(arr, p, pindex-1);
 quick_sort(arr, pindex+1, q);
 }
}
int main() {
 int i;
 int arr[MAX];
 for (i = 0;i < MAX; i++)
 arr[i] = i + 1;
 random_shuffle(arr);
 quick_sort(arr, 0, MAX - 1);
 for (i = 0; i < MAX; i++)
 cout << arr[i] << " ";
 cout << endl;
 return 0;
}







Job Sequencing Problem
#include<iostream>
#include<algorithm>
using namespace std;
struct Job {
 char id;
 int dead;
 int profit;
};
bool compare(Job a, Job b) {
return (a.profit > b.profit);
}
void jobschedule (Job arr[], int n) {
sort(arr, arr+n, compare);
int result[n];
bool slot[n];
for (int i=0; i<n; i++)
 slot[i] = false;
for (int i=0; i<n; i++) {
 for (int j=min(n, arr[i].dead)-1; j>=0; j--) {
 if (slot[j]==false) {
 result[j] = i;
 slot[j] = true;
 break;
 }
 }
}
for (int i=0; i<n; i++)
if (slot[i])
cout << arr[result[i]].id << " ";
}
int main() {
Job arr[] = { {'a', 2, 20}, {'b', 2, 15}, {'c', 1, 10},{'d', 3, 5}, {'e', 3, 1}};
int n = 5;
cout << "Maximum Profit Sequence of jobs is --> ";
jobschedule(arr, n);
}







Fibonacci Series
int fib1(int n){
 int a=0;
 int b=1;
 int c;
 if(n==0){
 return a;
 }
 for(int i=2;i<=n;i++){
 c=a+b;
 a=b;
 b=c;
 }
 return b;
}
int fib(int n)
{
 if (n <= 1)
 return n;
 return fib(n - 1) + fib(n - 2);
}
int main() {
 int n = 9;
 cout<<"Recursive Method :"<<endl;
 cout << fib(n);
 cout<<"Iterative method : "<<endl;
 for (int i = 1; i <= n; i++)
 {
 cout<<fib1(i)<<" ";
 }
 return 0;
}
