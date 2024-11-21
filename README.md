1.Linear
import java.util.*;
public class LinearSearch{
public static int linear_search(int numbers[],int key)
for(int i=0;i<=numbers.length;i++) {
if(numbers[i]==key){
return i;
}
} 
return -1;
}
public static void main(String[] args) {
Scanner sc = new Scanner(System.in);
int numbers[]={2,4,3,7,8,9,10,12,15,20};
System.out.println("Enter a key= ");
int key = sc.nextInt();
int index=linear_search(numbers, key);
if(index==-1){
System.out.println("key not found");
}else{
System.out.println("the key is found at index= "+index);
} sc.close()
}}

/////////////////////////////////////////////////

1.Binary
import java.util.*;

public class BinarySearch {
public static int binary_search(int numbers[], int key) {
int start = 0, end = numbers.length - 1;
while (start <= end) {
int mid = (start + end) / 2;
if (numbers[mid] == key) return mid;
if (numbers[mid] < key) start = mid + 1;
else end = mid - 1;
}
return -1;
}

public static void main(String[] args) {
Scanner sc = new Scanner(System.in);
System.out.print("Enter the number of elements in the sorted array: ");
int n = sc.nextInt();
int[] numbers = new int[n];
System.out.println("Enter the elements of the sorted array:");
for (int i = 0; i < n; i++) numbers[i] = sc.nextInt();
System.out.print("Enter the number to search for: ");
int key = sc.nextInt();
int result = binary_search(numbers, key);
if (result == -1) System.out.println("The number " + key + " is not in the array.");
else System.out.println("The number " + key + " is found at index: " + result);
sc.close();
}
}
/////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
2.Merge
import java.util.Scanner;

class GfG {

static void merge(int arr[], int l, int m, int r) {
int n1 = m - l + 1;
int n2 = r - m;
int L[] = new int[n1];
int R[] = new int[n2];

for (int i = 0; i < n1; ++i) {
L[i] = arr[l + i];
}
for (int j = 0; j < n2; ++j) {
R[j] = arr[m + 1 + j];
}

int i = 0, j = 0, k = l;
while (i < n1 && j < n2) {
if (L[i] <= R[j]) {
arr[k++] = L[i++];
} else {
arr[k++] = R[j++];
}
}

while (i < n1) {
arr[k++] = L[i++];
}
while (j < n2) {
arr[k++] = R[j++];
}
}

static void sort(int arr[], int l, int r) {
if (l < r) {
int m = l + (r - l) / 2;
sort(arr, l, m);
sort(arr, m + 1, r);
merge(arr, l, m, r);
}
}

static void printArray(int arr[]) {
for (int i = 0; i < arr.length; ++i) {
System.out.print(arr[i] + " ");
}
System.out.println();
}

public static void main(String args[]) {
Scanner sc = new Scanner(System.in);
System.out.print("Enter the number of elements: ");
int n = sc.nextInt();
int arr[] = new int[n];
System.out.println("Enter the elements:");
for (int i = 0; i < n; i++) {
arr[i] = sc.nextInt();
}
System.out.println("Given array is:");
printArray(arr);
sort(arr, 0, arr.length - 1);
System.out.println("Sorted array is:");
printArray(arr);
sc.close();
}
}
///////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
3.Heap
import java.util.Scanner;

class GfG {

static void heapify(int arr[], int n, int i) {
int largest = i;
int l = 2 * i + 1;
int r = 2 * i + 2;

if (l < n && arr[l] > arr[largest]) {
largest = l;
}

if (r < n && arr[r] > arr[largest]) {
largest = r;
}

if (largest != i) {
int temp = arr[i];
arr[i] = arr[largest];
arr[largest] = temp;
heapify(arr, n, largest);
}
}

static void heapSort(int arr[]) {
int n = arr.length;

for (int i = n / 2 - 1; i >= 0; i--) {
heapify(arr, n, i);
}

for (int i = n - 1; i > 0; i--) {
int temp = arr[0];
arr[0] = arr[i];
arr[i] = temp;
heapify(arr, i, 0);
}
}

static void printArray(int arr[]) {
for (int i = 0; i < arr.length; i++) {
System.out.print(arr[i] + " ");
}
System.out.println();
}

public static void main(String args[]) {
Scanner sc = new Scanner(System.in);
System.out.print("Enter the number of elements: ");
int n = sc.nextInt();
int arr[] = new int[n];
System.out.println("Enter the elements:");
for (int i = 0; i < n; i++) {
arr[i] = sc.nextInt();
}
heapSort(arr);
System.out.println("Sorted array is:");
printArray(arr);
sc.close();
}
}
////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
4.Prims
import java.util.*;

class Pair {
int v;
int wt;
Pair(int v, int wt) {
this.v = v;
this.wt = wt;
}
}

class GFG {
static int spanningTree(int V, int E, int edges[][]) {
ArrayList<ArrayList<Pair>> adj = new ArrayList<>();
for (int i = 0; i < V; i++) {
adj.add(new ArrayList<Pair>());
}
for (int i = 0; i < edges.length; i++) {
int u = edges[i][0];
int v = edges[i][1];
int wt = edges[i][2];
adj.get(u).add(new Pair(v, wt));
adj.get(v).add(new Pair(u, wt));
}
PriorityQueue<Pair> pq = new PriorityQueue<>(new Comparator<Pair>() {
public int compare(Pair a, Pair b) {
return a.wt - b.wt;
}
});
pq.add(new Pair(0, 0));
int[] vis = new int[V];
int s = 0;
while (!pq.isEmpty()) {
Pair node = pq.poll();
int v = node.v;
int wt = node.wt;
if (vis[v] == 1) continue;
s += wt;
vis[v] = 1;
for (Pair it : adj.get(v)) {
if (vis[it.v] == 0) {
pq.add(new Pair(it.v, it.wt));
}
}
}
return s;
}

public static void main(String[] args) {
int graph[][] = new int[][] {{0, 1, 5}, {1, 2, 3}, {0, 2, 1}};
System.out.println(spanningTree(3, 3, graph));
}
}
/////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
5.Kruskals

package linearSearch;

import java.util.*;

public class KruskalAlgorithm {

static class Edge {
int src, dest, weight;
Edge(int src, int dest, int weight) {
this.src = src;
this.dest = dest;
this.weight = weight;
}
}

static class DisjointSet {
int[] parent, rank;

DisjointSet(int n) {
parent = new int[n];
rank = new int[n];
for (int i = 0; i < n; i++) {
parent[i] = i;
rank[i] = 0;
}
}

int find(int i) {
if (parent[i] != i) {
parent[i] = find(parent[i]); // Path compression
}
return parent[i];
}

void union(int x, int y) {
int rootX = find(x);
int rootY = find(y);

if (rootX != rootY) {
if (rank[rootX] < rank[rootY]) {
parent[rootX] = rootY;
} else if (rank[rootX] > rank[rootY]) {
parent[rootY] = rootX;
} else {
parent[rootY] = rootX;
rank[rootX]++;
}
}
}
}

public static void kruskalAlgorithm(int V, int[][] edges) {
ArrayList<Edge> edgeList = new ArrayList<>();
for (int[] e : edges) {
edgeList.add(new Edge(e[0], e[1], e[2]));
}

// Sort edges by weight
Collections.sort(edgeList, Comparator.comparingInt(e -> e.weight));

DisjointSet ds = new DisjointSet(V);

int mstWeight = 0;
ArrayList<Edge> mst = new ArrayList<>();

for (Edge edge : edgeList) {
int src = edge.src;
int dest = edge.dest;
int weight = edge.weight;

// If including this edge does not form a cycle
if (ds.find(src) != ds.find(dest)) {
mst.add(edge);
mstWeight += weight;
ds.union(src, dest);
}
}

System.out.println("Edges in MST:");
for (Edge e : mst) {
System.out.println(e.src + " - " + e.dest + " : " + e.weight);
}
System.out.println("Total weight of MST: " + mstWeight);
}

public static void main(String[] args) {
int[][] edges = {
{0, 1, 10}, {0, 2, 6}, {0, 3, 5},
{1, 3, 15}, {2, 3, 4}
};
int V = 4; // Number of vertices
kruskalAlgorithm(V, edges);
}
}
/////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
6.Knapsack
public class KnapsackDP {

public static int knapsack(int W, int[] wt, int[] val, int n) {
int[][] dp = new int[n + 1][W + 1];

for (int i = 0; i <= n; i++) {
for (int w = 0; w <= W; w++) {
if (i == 0 || w == 0) {
dp[i][w] = 0;
} else if (wt[i - 1] <= w) {
dp[i][w] = Math.max(val[i - 1] + dp[i - 1][w - wt[i - 1]], dp[i - 1][w]);
} else {
dp[i][w] = dp[i - 1][w];
}
}
}

return dp[n][W];
}

public static void main(String[] args) {
Scanner sc = new Scanner(System.in);

System.out.print("Enter the number of items: ");
int n = sc.nextInt();

int[] val = new int[n];
int[] wt = new int[n];

System.out.println("Enter the values of the items:");
for (int i = 0; i < n; i++) {
val[i] = sc.nextInt();
}

System.out.println("Enter the weights of the items:");
for (int i = 0; i < n; i++) {
wt[i] = sc.nextInt();
}

System.out.print("Enter the capacity of the knapsack: ");
int W = sc.nextInt();

System.out.println("Maximum value in knapsack = " + knapsack(W, wt, val, n));

sc.close();
}
}
///////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
7.Coin Change
public class CoinChange {

public static int minCoins(int[] coins, int amount) {
int[] dp = new int[amount + 1];
Arrays.fill(dp, amount + 1);
dp[0] = 0;

for (int coin : coins) {
for (int i = coin; i <= amount; i++) {
dp[i] = Math.min(dp[i], dp[i - coin] + 1);
}
}

return dp[amount] > amount ? -1 : dp[amount];
}

public static void main(String[] args) {
Scanner sc = new Scanner(System.in);

System.out.print("Enter the number of coin types: ");
int numCoins = sc.nextInt();

int[] coins = new int[numCoins];
System.out.println("Enter the coin denominations:");
for (int i = 0; i < numCoins; i++) {
coins[i] = sc.nextInt();
}

System.out.print("Enter the total amount: ");
int amount = sc.nextInt();

int result = minCoins(coins, amount);

if (result == -1) {
System.out.println("It's not possible to make the amount with the given coins.");
} else {
System.out.println("Minimum number of coins required: " + result);
}

sc.close();
}
}
///////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
8.BFT
class BFT {

static void bfs(List<List<Integer>> adj, int s) {
Queue<Integer> q = new LinkedList<>();
boolean[] visited = new boolean[adj.size()];
visited[s] = true;
q.add(s);

while (!q.isEmpty()) {
int curr = q.poll();
System.out.print(curr + " ");

for (int x : adj.get(curr)) {
if (!visited[x]) {
visited[x] = true;
q.add(x);
}
}
}
}

static void addEdge(List<List<Integer>> adj, int u, int v) {
adj.get(u).add(v);
adj.get(v).add(u);
}

public static void main(String[] args) {
int V = 5;
List<List<Integer>> adj = new ArrayList<>(V);
for (int i = 0; i < V; i++) {
adj.add(new ArrayList<>());
}

addEdge(adj, 0, 1);
addEdge(adj, 0, 2);
addEdge(adj, 1, 3);
addEdge(adj, 1, 4);
addEdge(adj, 2, 4);

System.out.println("BFS starting from 0:");
bfs(adj, 0);
}
}
///////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
9.Bubble
import java.util.Scanner;

class GFG {
    static void bubbleSort(int arr[], int n) {
        int i, j, temp;
        boolean swapped;
        for (i = 0; i < n - 1; i++) {
            swapped = false;
            for (j = 0; j < n - i - 1; j++) {
                if (arr[j] > arr[j + 1]) {
                    temp = arr[j];
                    arr[j] = arr[j + 1];
                    arr[j + 1] = temp;
                    swapped = true;
                }
            }
            if (!swapped)
                break;
        }
    }

    static void printArray(int arr[], int size) {
        for (int i = 0; i < size; i++)
            System.out.print(arr[i] + " ");
        System.out.println();
    }

    public static void main(String args[]) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter the number of elements: ");
        int n = sc.nextInt();
        int arr[] = new int[n];
        System.out.println("Enter the elements of the array:");
        for (int i = 0; i < n; i++) {
            arr[i] = sc.nextInt();
        }
        bubbleSort(arr, n);
        System.out.println("Sorted array: ");
        printArray(arr, n);
        sc.close();
    }
}
//////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
10.Quick
import java.util.Scanner;

class GfG {
    static int partition(int[] arr, int low, int high) {
        int pivot = arr[high]; 
        int i = low - 1; 
        for (int j = low; j <= high - 1; j++) {
            if (arr[j] < pivot) {
                i++;
                swap(arr, i, j);
            }
        }
        swap(arr, i + 1, high);  
        return i + 1;
    }

    static void swap(int[] arr, int i, int j) {
        int temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
    }

    static void quickSort(int[] arr, int low, int high) {
        if (low < high) {
            int pi = partition(arr, low, high);
            quickSort(arr, low, pi - 1);
            quickSort(arr, pi + 1, high);
        }
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);
        System.out.print("Enter the number of elements: ");
        int n = sc.nextInt();
        int[] arr = new int[n];
        System.out.println("Enter the elements of the array:");
        for (int i = 0; i < n; i++) {
            arr[i] = sc.nextInt();
        }
        quickSort(arr, 0, n - 1);
        System.out.println("Sorted array: ");
        for (int val : arr) {
            System.out.print(val + " ");
        }
        sc.close();
    }
}
////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////////
12.Binomial Coeficient
import java.util.Scanner;

public class BinomialCoefficient {

    public static int binomialCoeff(int n, int k) {
        int[][] dp = new int[n + 1][k + 1];

        for (int i = 0; i <= n; i++) {
            for (int j = 0; j <= Math.min(i, k); j++) {
                if (j == 0 || j == i) {
                    dp[i][j] = 1;
                } else {
                    dp[i][j] = dp[i - 1][j - 1] + dp[i - 1][j];
                }
            }
        }

        return dp[n][k];
    }

    public static void main(String[] args) {
        Scanner sc = new Scanner(System.in);

        System.out.print("Enter value of n: ");
        int n = sc.nextInt();

        System.out.print("Enter value of k: ");
        int k = sc.nextInt();

        System.out.println("Binomial Coefficient C(" + n + ", " + k + ") is: " + binomialCoeff(n, k));

        sc.close();
    }
}
