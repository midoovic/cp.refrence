# mo's refrence

## 1.Template
```cpp
#include <bits/stdc++.h>
using namespace std;
#define ll long long
#define el "\n"
#define all(v) v.begin(), v.end()
#define allr(v) v.rbegin(), v.rend()
#define F first
#define S second
void ps()
{}
int main()
{
  ios_base::sync_with_stdio(false),
  cin.tie(NULL),
  cout.tie(NULL);

  //freopen("input.txt", "r", stdin);
  //freopen("output.txt", "w", stdout);

  ll t_c = 1;  
  //cin >> t_c;
  while(t_c--) 
  { 
    ps(); 
  }
  return 0;
}
```

---

## 2. Searching & Sorting

### Binary Search (Sorted Array)
```cpp
bool binary_search(ll arr[], int size, int element) 
{
    int start = 0, end = size - 1;
    while (start <= end) 
    {
        int mid = start + (end - start) / 2;
        if (arr[mid] == element) return true;
        if (element > arr[mid]) start = mid + 1;
        else end = mid - 1;
    }
    return false;
}
```

### Custom Comparators
```cpp
// Compare function for pairs
bool compare_pairs(pair<string, int> a, pair<string, int> b)
{
    if (a.second == b.second) 
    {
        return a.first < b.first;
    }
    return a.second > b.second;
}

// Descending sort comparator
bool compare(int a, int b)
{
    return a > b;
}

/* use it as a third parameter in sort function 
  sort(all(v) , compare);
*/
```
---

## 3. Functions

### Frequency Array (Capital & Small Letters)
```cpp
int freq[52] = {0};

void count_freq(string s) 
{
    for (int i = 0; i < s.size(); i++) 
    {
        if (s[i] >= 'A' && s[i] <= 'Z') 
        {
            freq[s[i] - 'A']++;
        } 
        else if (s[i] >= 'a' && s[i] <= 'z') 
        {
            freq[(s[i] - 'a') + 26]++; // Shifted by 26 for lowercase
        }
    }
}
```

### prime:
```cpp
bool prime(ll n)
{
    if(n==1) {return false;}
    
    else if(n==2){return true;}
 
    else 
    {
        for(ll i=2 ;i<=sqrt(n) ; i++)
        {
            if(n%i==0) {return false;}
        }
        return true;
    }
}
```
### to num:
```cpp
int tonum(string s)
{
  int n = 0;
  for(int i = 0; i < s.size(); i++)
  {
    n = (n * 10) + (s[i] - '0');
  }
  return n;
}
```

## 4. math 

### 1. gcd:
```cpp
ll gcd(ll a , ll b)
{
    while(b!=0)
    {
       ll x=a;
       a=b;
       b=x%b;
    }
    return a;
// العوامل المشتركة دايما هتكون من 1 للرقم الاصغر==>(use : gcd of factorial)
}
```
### 2. lcm:
```cpp
ll lcm(ll a, ll b)
{
    ll lcm = (a*b) / gcd(a,b);
    return lcm;
}
```
### 3.fastpower:
```cpp
#define mod 1000000007
ll fastpow(ll num , ll pow)
{
  ll res = 1;
  while(pow > 0)
  {
    if(pow % 2 == 1) 
    {
      res = (res * num) % mod;
    }
    num = (num * num) % mod;
    pow = pow / 2;
  }
  return res;
}
// اعمل مود للناتج فى كود الحل نفسه
```
### 4.K-th Not Divisible by n:
```cpp
{
  ll n , k , block , idx , strt , res;
  cin >> n >> k;
  block = (k % (n-1) == 0 ? (k / (n-1)) : (k / (n-1)) + 1);
  strt = (block - 1) * n;
  idx = k - ((block - 1) * (n-1));
  res = idx + strt;
  cout << res << el;
//! optimize :
  res = k + ( (k-1) / (n-1));
}
```
### 5. factorial
```cpp

__float128 factorial(int a)
{
  __float128 fac = 1;
  for(int i = 2; i <= a; i++)
  {
    fac *= i;
  }
  return fac;
}
// limit n = 20 ... if n > 20 it causes overflow with long long !!
// with datatype "__float128"  your limit changes to n = 1755
// casting result to (long long) or (int64_t) , can't use cout with (__float128)
```
### 6. number of digits of any positive number
```cpp
// mathmatical logic : digits = [log10(x)] + 1  {x : positive number}
// use this code to solve number of digits of factorial n (N!)
ll numOfDigits(int n)
{
  double digits = 0;         // double .. log10() result maybe fraction
  for(int i = 2; i <= n; i++)
  {
    digits += log10(i);
  }
  return floor(digits) + 1;
}
```
### 7.the sum of the numbers in the range between a and b
```cpp
ll mn = min(a , b);
ll mx = max(a , b);
cout << ((mx -  mn+ 1) * (mx + mn)) / 2 << el;
```
### 8. combinations(best formula)
```cpp
ll nCr(ll n , ll r) // optimize 
{
  //Base cases
  if(r > n) return 0;
  if(r == n || r == 0) return 1;

  if(r > (n - r))
  {
    r = n - r;  // nCr(100 , 98) = loop 98 times , but nCr(100 , 2) = loop 2 times
  }
  ll res = 1;
  for(ll i = 1; i <= r ; i++)
  {
    res = (res * (n - i + 1)) / i; 
    // wiithout more brackets because always (res*(n-i+1)) divisible by i but (n-i+1) may gives fraction result 

    /*
    بدل ما نقسم ناتج البسط كله على ناتج المقام كله اللى ممكن يعمل اوفرفلو فى القانون الاساسى بسبب المضروب
    بنقسم كل حد فى البسط على المقابل له فى المقام أول بأول 
    */
  }
  return res;
}
```
### 9. Log2(n) 
```cpp
// log2(n) = how many times can divide n by 2 untill result equal 1
// By recursion:
ll rec(ll n , ll cnt)
{
  if(n == 1)  //Base case
  {
    return cnt;
  }
  cnt++;
  return rec(n/2 , cnt);
}
```
### rules:
```cpp
1. num of enven numbers = n / 2
2. num of odd numbers = tot num - even
3. max num of distinct numbers their sum is <= n --> k = (sqrt(1+(8*n)) - 1) / 2
4. No. of numbers between 1 and b divisible by x --> n = b / x  
  & their sum = x * ((n*(n+1))/2)
5. permutations تباديل nPr = n! / (n - r) --> ترتيب العناصر مهم
6. combinations توافيق nCr = n! / (r! * (n-r)!)
7. valid triangle : sum of two slides > third one
8. area of triangle with 3 slides = sqrt(s * (s-a) * (s-b) * (s-c)) 
   {s : semi perimeter = (a+b+c) / 2} 
9. deleting carry = XOR operation 
   EX : sum of binary 4 + 6 withou carry = 2 ==>  4 XOR 6 = 2 #
```
### modular arithmetic
```cpp
1. (a+b) % c = ((a%c) + (b%c)) % c
2. (a*b) % c = ((a%c) * (b%c)) % c
3. (a-b) % c = ((a%c) - (b%c) + c) % c
4. (a/b) % c = ((a%c) * fastpow(b, c-2)) % c 
```
## 5.L00K:
```cpp
1. max average subarray = max element 

2. * subarray --> ورا بعض
   * subsequence --> مش لازم ورا بعض بس لازم الترتيب
   * subset --> مش لازم ورا بعض ولا نفس الترتيب
 
3. No. of all subseq. of array of size n = 2^n
   each element appears in half times of all subseq. = 2^(n-1)
  max sum of all subseq.:
  {
   ll n , sm = 0;
   cin >> n;
   vector<ll> a(n);
   for(auto &i : a)
   {
     cin >> i;
     sm += i;
     sm = sm % mod;
   }
   sm = (sm * fastpow(2 , n - 1)) % mod ;
   cout << sm << el;
  }

4. to get gcd(num , x) = 1 , then x always prime No.
```

# F refrence

## 1.Extended Euclid (لإيجاد x, y بحيث ax + by = gcd(a,b))
```cpp
ll ext_gcd(ll a, ll b, ll &x, ll &y)
{
    if (b == 0) { x = 1; y = 0; return a; }
    ll x1, y1;
    ll g = ext_gcd(b, a % b, x1, y1);
    x = y1;
    y = x1 - (a / b) * y1;
    return g;
}
```
## 2.
```cpp
2.vector<int> prefix_function(string s)
{
    int n = s.size();
    vector<int> pi(n, 0);
    for (int i = 1; i < n; i++)
    {
        int j = pi[i-1];
        while (j > 0 && s[i] != s[j]) j = pi[j-1];
        if (s[i] == s[j]) j++;
        pi[i] = j;
    }
    return pi;
}
// للبحث عن pattern p في text t:
// كوّن s = p + '#' + t واحسب pi، أي مكان pi[i] == p.size() يبقى وجدت match
```
## 3.
```cpp
// مثال: هل فيه عنصرين مجموعهم = target في array مرتب
bool two_sum_sorted(vector<int> &a, int target)
{
    int l = 0, r = a.size() - 1;
    while (l < r)
    {
        int sum = a[l] + a[r];
        if (sum == target) return true;
        else if (sum < target) l++;
        else r--;
    }
    return false;
}
```
## 4.
```cpp
vector<ll> build_prefix(vector<ll> &a)
{
    int n = a.size();
    vector<ll> pre(n + 1, 0);
    for (int i = 0; i < n; i++) pre[i+1] = pre[i] + a[i];
    return pre;
}
// sum(l, r) 0-indexed inclusive = pre[r+1] - pre[l]
```
## 5.subarray
```cpp
void all_subarrays(vector<int> &a)
{
    int n = a.size();
    for (int i = 0; i < n; i++)
    {
        for (int j = i; j < n; j++)
        {
            // subarray من index i لـ j
            for (int k = i; k <= j; k++) cout << a[k] << " ";
            cout << el;
        }
    }
}
```
## 6.substring
```cpp
void all_substrings(string s)
{
    int n = s.size();
    for (int i = 0; i < n; i++)
        for (int j = i; j < n; j++)
            cout << s.substr(i, j - i + 1) << el;
}
```
## 7.subseq.
```cpp
void all_subsequences(vector<int> &a)
{
    int n = a.size();
    for (int mask = 0; mask < (1 << n); mask++)
    {
        for (int i = 0; i < n; i++)
            if (mask & (1 << i)) cout << a[i] << " ";
        cout << el;
    }
}
```
## 8.
```cpp
1. a ^ a = 0
2. a ^ 0 = a
3. a ^ b = b ^ a                 (commutative)
4. (a ^ b) ^ c = a ^ (b ^ c)     (associative)
5. لو x ^ y = z  -->  x ^ z = y  و  y ^ z = x
6. عدد فردي من التكرارات لعنصر بيفضل موجود في الـ XOR، وعدد زوجي بيلغي نفسه
```
## 9.XOR 1 to n:
```cpp
ll xor_1_to_n(ll n)
{
    if (n % 4 == 0) return n;
    if (n % 4 == 1) return 1;
    if (n % 4 == 2) return n + 1;
    return 0; // n % 4 == 3
}
```
## 10.prime factorization
```cpp
vector<int> primeFactor (int n ){  //vector as a datatype
    vector<int> ans ;
    for (int i = 2 ; i <= n ; i++){
        
        // n %  i  == 0 means n is divisible by i 
        while (n % i == 0 && n > 0 ){
            ans.push_back(i);
            n = n / i ;
        }
    }
    return ans ;
}
```
