# task__9


1. Nearest Greater to left

#include<bits/stdc++.h>

//#include <ext/pb_ds/assoc_container.hpp>
//#include <ext/pb_ds/tree_policy.hpp>
//using namespace __gnu_pbds;

using namespace std;

//=============================================CONSTANTS=============================================

const long long SZ = 1e5 + 7;
const long long inf = 1e18;
const long long mod = 1e9 + 7;
const long long MOD = 998244353;
const long long PI = 3.1415926535897932384;

//=============================================MACROS=============================================

#define FastIO 					ios_base::sync_with_stdio(0); cin.tie(0); cout.tie(0)
#define kitnalega           	long long ___tc=1; cin >> ___tc; while (___tc--	)

#define rep(i,x,y)				for(int i=x;i<y;i++)
#define rep_Eq(i,x,y)			for(int i=x;i<=y;i++)
#define rep_Rev(i,x,y)			for(int i=x-1;i>=y;i--)
#define ll						long long
#define lli						long long int

#define ci(X)               	ll X; 			cin >> X
#define cii(X, Y)           	ll X, Y; 		cin >> X >> Y
#define ciii(X, Y, Z)       	ll X, Y, Z;		cin >> X >> Y >> Z
#define ciiii(A,X,Y,Z)			ll A,X,Y,Z;		cin >> A >> X >> Y >> Z
#define cs(s)					string s; 		cin>>s;



#define pb 						push_back
#define pf 						push_front
#define eb 						emplace_back
#define endl					"\n"
#define	newl					cout<<endl;
#define sep						cout<<"-----------------"<<endl;

#define mp 						make_pair
#define pq 						priority_queue

#define ff 						first
#define ss 						second

#define Max(a,b)            	((a > b) ? a : b)
#define Min(a,b)            	((a < b) ? a : b)

#define lb 						lower_bound
#define ub 						upper_bound
#define mx 						*max_element
#define mn 						*min_element



typedef vector<int> 			vi;
typedef vector<vi> 				vvi;
typedef vector<ll> 				vll;
typedef pair<int, int>			pii;
typedef pair<ll, ll>			pll;
typedef vector<pii>				vpii;
typedef vector<pll>				vpll;
typedef pair<lli, lli>			pll;



//=============================================FUNCTIONS=============================================

#define srt(a)			sort(a,a+n);
#define srt2(a)			sort(a.begin(),a.end());
#define rev(a)			reverse(a.begin(),a.end());

//=============================================Templates=============================================

template <typename ForwardIterator, class T>
ForwardIterator search(ForwardIterator start, ForwardIterator end, T key) {
	while (start != end) {
		if (*start == key) {
			return start;
		}
		start++;
	}
	return end;
}

//=============================================Input/Output=============================================

void start_func()
{	FastIO;
#ifndef ONLINE_JUDGE
	freopen("input.txt", "r", stdin);
	freopen("output.txt", "w", stdout);
#endif
}

//=============================================Sieve=============================================

vll prime;
bool isPrime(int n)
{
	if (n == 1) {
		return false;
	}
	if (n == 2 || n == 3) {
		return true;
	}
	if (n % 2 == 0 || n % 3 == 0) {
		return false;
	}
	for (int i = 5; i * i <= n; i = i + 6) {
		if (n % i == 0 || n % (i + 2) == 0) {
			return false;
		}
		return true;
	}
}
void sieve(int n)
{
	vector <bool> isPrime(n + 1, true);
	rep(i, 2, n + 1) {
		if (isPrime[i]) {
			prime.push_back(i);
			for (ll j = i * i; j <= n; j++) {
				isPrime[j] = false;
			}
		}
	}
}
void segSieve(int l, int h)
{
	ll sq = sqrt(h);
	sieve(sq);
	vector<bool>isPrime(h - l + 1, true);
	for (ll p : prime) {
		ll sm = (l / p) * p;
		if (sm < l)
			sm += p;
		for (ll m = sm; m <= h; m += p)
			isPrime[m - l] = false;
	}
	int cc = 0;
	int ans = 0;
	rep(i, l, h + 1) {
		if (isPrime[i - l] == true) {
			cout << i << " ";
			//cc++;
		}
		else {
			//cout << i << " ";
		}
	}
	//cout << cc << endl;
	newl
}
//=============================================GCD=============================================

int gcd(int a, int b) {
	return b == 0 ? 0 : gcd(b, a & b);
}
int gcd2(int a, int b) {
	while (b != 0) {
		a %= b;
		swap(a, b);
	}
	return a;
}
//lcm finder
int lcm(int a, int b) {
	return (a * b) / gcd(a, b);
}
//extended Euclidian Algorithm  	to find linear Diophatine solution 		(ax+by=g) ==> g=gcd(a,b)
int gcdExt(int a, int b, int &x, int &y) {
	if (b == 0) {
		x = 1, y = 0;
		return a;
	}
	int x1, y1;
	int g = gcdExt(b, a % b, x1, y1);
	x = y1, y = x1 - (a / b) * y1;
	return g;
}


int smallestPrime(int n)
{
	cout << 1 << " ";
	vi v(n + 1, 0);
	for (int i = 2; i <= n; i++)
	{
		if (v[i] == 0)
		{
			cout << i << " ";
			for (int j = i * i; j <= n; j = j + i)
			{
				if (v[j] == 0)
				{
					v[j] = i;
				}
			}
		}
		else {
			cout << v[i] << " ";
		}
	}
}
void num_to_bin(int n) {
	if (n == 0) {return; }
	num_to_bin(n / 2);
	cout << n % 2;
}
bool str_palli(string s, int start, int end) {
	if (start >= end) {
		return true;
	}
	return (s[start] == s[end]) && str_palli(s, start + 1, end - 1);
}
//=============================================Sample Codes=============================================

void print_per(string s, int i = 0)
{
	if (i == s.length() - 1) {
		cout << s << "\n";
	}
	for (int j = i; j < s.length(); j++)
	{
		swap(s[i], s[j]);
		print_per(s, i + 1);
		swap(s[i], s[j]);
	}
}

void subset(string s, string curr = "", int index = 0)
{
	if (index == s.length())
	{
		cout << curr << " ";
		return;
	}
	subset(s, curr, index + 1);
	subset(s, curr + s[index], index + 1);
}

//=============================================MAIN CODE=============================================

void chalochale() {
	ci(n);
	int arr[n];
	rep(i, 0, n)	cin >> arr[i];
	stack<int>s;
	vi v;
	//for (int i = n - 1; i >= 0; i--)
	rep(i, 0, n)
	{
		if (s.size() == 0) {
			v.pb(-1);
		}
		else if (s.size() > 0 && s.top() > arr[i])
		{
			v.pb(s.top());
		}
		else if (s.size() > 0 && s.top() <= arr[i])
		{
			while (s.size() > 0 && s.top() <= arr[i])
			{
				s.pop();
			}
			if (s.size() == 0)
			{
				v.pb(-1);
			}
			else
			{
				v.pb(s.top());
			}
		}
		s.push(arr[i]);
	}
	//reverse(v.begin(), v.end());
	rep(i, 0, v.size())	{
		cout << v[i] << " ";
	}
}

int32_t main()
{
	start_func();
	//kitnalega
	{
		chalochale();
		//newl
	}
	return 0;
}


2. Nearest smaller to left

#include<bits/stdc++.h>

//#include <ext/pb_ds/assoc_container.hpp>
//#include <ext/pb_ds/tree_policy.hpp>
//using namespace __gnu_pbds;

using namespace std;

//=============================================CONSTANTS=============================================

const long long SZ = 1e5 + 7;
const long long inf = 1e18;
const long long mod = 1e9 + 7;
const long long MOD = 998244353;
const long long PI = 3.1415926535897932384;

//=============================================MACROS=============================================

#define FastIO 					ios_base::sync_with_stdio(0); cin.tie(0); cout.tie(0)
#define kitnalega           	long long ___tc=1; cin >> ___tc; while (___tc--	)

#define rep(i,x,y)				for(int i=x;i<y;i++)
#define rep_Eq(i,x,y)			for(int i=x;i<=y;i++)
#define rep_Rev(i,x,y)			for(int i=x-1;i>=y;i--)
#define ll						long long
#define lli						long long int

#define ci(X)               	ll X; 			cin >> X
#define cii(X, Y)           	ll X, Y; 		cin >> X >> Y
#define ciii(X, Y, Z)       	ll X, Y, Z;		cin >> X >> Y >> Z
#define ciiii(A,X,Y,Z)			ll A,X,Y,Z;		cin >> A >> X >> Y >> Z
#define cs(s)					string s; 		cin>>s;



#define pb 						push_back
#define pf 						push_front
#define eb 						emplace_back
#define endl					"\n"
#define	newl					cout<<endl;
#define sep						cout<<"-----------------"<<endl;

#define mp 						make_pair
#define pq 						priority_queue

#define ff 						first
#define ss 						second

#define Max(a,b)            	((a > b) ? a : b)
#define Min(a,b)            	((a < b) ? a : b)

#define lb 						lower_bound
#define ub 						upper_bound
#define mx 						*max_element
#define mn 						*min_element



typedef vector<int> 			vi;
typedef vector<vi> 				vvi;
typedef vector<ll> 				vll;
typedef pair<int, int>			pii;
typedef pair<ll, ll>			pll;
typedef vector<pii>				vpii;
typedef vector<pll>				vpll;
typedef pair<lli, lli>			pll;



//=============================================FUNCTIONS=============================================

#define srt(a)			sort(a,a+n);
#define srt2(a)			sort(a.begin(),a.end());
#define rev(a)			reverse(a.begin(),a.end());

//=============================================Templates=============================================

template <typename ForwardIterator, class T>
ForwardIterator search(ForwardIterator start, ForwardIterator end, T key) {
	while (start != end) {
		if (*start == key) {
			return start;
		}
		start++;
	}
	return end;
}

//=============================================Input/Output=============================================

void start_func()
{	FastIO;
#ifndef ONLINE_JUDGE
	freopen("input.txt", "r", stdin);
	freopen("output.txt", "w", stdout);
#endif
}

//=============================================Sieve=============================================

vll prime;
bool isPrime(int n)
{
	if (n == 1) {
		return false;
	}
	if (n == 2 || n == 3) {
		return true;
	}
	if (n % 2 == 0 || n % 3 == 0) {
		return false;
	}
	for (int i = 5; i * i <= n; i = i + 6) {
		if (n % i == 0 || n % (i + 2) == 0) {
			return false;
		}
		return true;
	}
}
void sieve(int n)
{
	vector <bool> isPrime(n + 1, true);
	rep(i, 2, n + 1) {
		if (isPrime[i]) {
			prime.push_back(i);
			for (ll j = i * i; j <= n; j++) {
				isPrime[j] = false;
			}
		}
	}
}
void segSieve(int l, int h)
{
	ll sq = sqrt(h);
	sieve(sq);
	vector<bool>isPrime(h - l + 1, true);
	for (ll p : prime) {
		ll sm = (l / p) * p;
		if (sm < l)
			sm += p;
		for (ll m = sm; m <= h; m += p)
			isPrime[m - l] = false;
	}
	int cc = 0;
	int ans = 0;
	rep(i, l, h + 1) {
		if (isPrime[i - l] == true) {
			cout << i << " ";
			//cc++;
		}
		else {
			//cout << i << " ";
		}
	}
	//cout << cc << endl;
	newl
}
//=============================================GCD=============================================

int gcd(int a, int b) {
	return b == 0 ? 0 : gcd(b, a & b);
}
int gcd2(int a, int b) {
	while (b != 0) {
		a %= b;
		swap(a, b);
	}
	return a;
}
//lcm finder
int lcm(int a, int b) {
	return (a * b) / gcd(a, b);
}
//extended Euclidian Algorithm  	to find linear Diophatine solution 		(ax+by=g) ==> g=gcd(a,b)
int gcdExt(int a, int b, int &x, int &y) {
	if (b == 0) {
		x = 1, y = 0;
		return a;
	}
	int x1, y1;
	int g = gcdExt(b, a % b, x1, y1);
	x = y1, y = x1 - (a / b) * y1;
	return g;
}


int smallestPrime(int n)
{
	cout << 1 << " ";
	vi v(n + 1, 0);
	for (int i = 2; i <= n; i++)
	{
		if (v[i] == 0)
		{
			cout << i << " ";
			for (int j = i * i; j <= n; j = j + i)
			{
				if (v[j] == 0)
				{
					v[j] = i;
				}
			}
		}
		else {
			cout << v[i] << " ";
		}
	}
}
void num_to_bin(int n) {
	if (n == 0) {return; }
	num_to_bin(n / 2);
	cout << n % 2;
}
bool str_palli(string s, int start, int end) {
	if (start >= end) {
		return true;
	}
	return (s[start] == s[end]) && str_palli(s, start + 1, end - 1);
}
//=============================================Sample Codes=============================================

void print_per(string s, int i = 0)
{
	if (i == s.length() - 1) {
		cout << s << "\n";
	}
	for (int j = i; j < s.length(); j++)
	{
		swap(s[i], s[j]);
		print_per(s, i + 1);
		swap(s[i], s[j]);
	}
}

void subset(string s, string curr = "", int index = 0)
{
	if (index == s.length())
	{
		cout << curr << " ";
		return;
	}
	subset(s, curr, index + 1);
	subset(s, curr + s[index], index + 1);
}

//=============================================MAIN CODE=============================================

void chalochale() {
	ci(n);
	int arr[n];
	rep(i, 0, n)	cin >> arr[i];
	stack<int>s;
	vi v;
	//for (int i = n - 1; i >= 0; i--)
	rep(i, 0, n)
	{
		if (s.size() == 0) {
			v.pb(-1);
		}
		else if (s.size() > 0 && s.top() < arr[i])
		{
			v.pb(s.top());
		}
		else if (s.size() > 0 && s.top() >= arr[i])
		{
			while (s.size() > 0 && s.top() >= arr[i])
			{
				s.pop();
			}
			if (s.size() == 0)
			{
				v.pb(-1);
			}
			else
			{
				v.pb(s.top());
			}
		}
		s.push(arr[i]);
	}
	//reverse(v.begin(), v.end());
	rep(i, 0, v.size())	{
		cout << v[i] << " ";
	}
}

int32_t main()
{
	start_func();
	//kitnalega
	{
		chalochale();
		//newl
	}
	return 0;
}




#include<bits/stdc++.h>

//#include <ext/pb_ds/assoc_container.hpp>
//#include <ext/pb_ds/tree_policy.hpp>
//using namespace __gnu_pbds;

using namespace std;

//=============================================CONSTANTS=============================================

const long long SZ = 1e5 + 7;
const long long inf = 1e18;
const long long mod = 1e9 + 7;
const long long MOD = 998244353;
const long long PI = 3.1415926535897932384;

//=============================================MACROS=============================================

#define FastIO 					ios_base::sync_with_stdio(0); cin.tie(0); cout.tie(0)
#define kitnalega           	long long ___tc=1; cin >> ___tc; while (___tc--	)

#define rep(i,x,y)				for(int i=x;i<y;i++)
#define rep_Eq(i,x,y)			for(int i=x;i<=y;i++)
#define rep_Rev(i,x,y)			for(int i=x-1;i>=y;i--)
#define ll						long long
#define lli						long long int

#define ci(X)               	ll X; 			cin >> X
#define cii(X, Y)           	ll X, Y; 		cin >> X >> Y
#define ciii(X, Y, Z)       	ll X, Y, Z;		cin >> X >> Y >> Z
#define ciiii(A,X,Y,Z)			ll A,X,Y,Z;		cin >> A >> X >> Y >> Z
#define cs(s)					string s; 		cin>>s;



#define pb 						push_back
#define pf 						push_front
#define eb 						emplace_back
#define endl					"\n"
#define	newl					cout<<endl;
#define sep						cout<<"-----------------"<<endl;

#define mp 						make_pair
#define pq 						priority_queue

#define ff 						first
#define ss 						second

#define Max(a,b)            	((a > b) ? a : b)
#define Min(a,b)            	((a < b) ? a : b)

#define lb 						lower_bound
#define ub 						upper_bound
#define mx 						*max_element
#define mn 						*min_element



typedef vector<int> 			vi;
typedef vector<vi> 				vvi;
typedef vector<ll> 				vll;
typedef pair<int, int>			pii;
typedef pair<ll, ll>			pll;
typedef vector<pii>				vpii;
typedef vector<pll>				vpll;
typedef pair<lli, lli>			pll;



//=============================================FUNCTIONS=============================================

#define srt(a)			sort(a,a+n);
#define srt2(a)			sort(a.begin(),a.end());
#define rev(a)			reverse(a.begin(),a.end());

//=============================================Templates=============================================

template <typename ForwardIterator, class T>
ForwardIterator search(ForwardIterator start, ForwardIterator end, T key) {
	while (start != end) {
		if (*start == key) {
			return start;
		}
		start++;
	}
	return end;
}

//=============================================Input/Output=============================================

void start_func()
{	FastIO;
#ifndef ONLINE_JUDGE
	freopen("input.txt", "r", stdin);
	freopen("output.txt", "w", stdout);
#endif
}

//=============================================Sieve=============================================

vll prime;
bool isPrime(int n)
{
	if (n == 1) {
		return false;
	}
	if (n == 2 || n == 3) {
		return true;
	}
	if (n % 2 == 0 || n % 3 == 0) {
		return false;
	}
	for (int i = 5; i * i <= n; i = i + 6) {
		if (n % i == 0 || n % (i + 2) == 0) {
			return false;
		}
		return true;
	}
}
void sieve(int n)
{
	vector <bool> isPrime(n + 1, true);
	rep(i, 2, n + 1) {
		if (isPrime[i]) {
			prime.push_back(i);
			for (ll j = i * i; j <= n; j++) {
				isPrime[j] = false;
			}
		}
	}
}
void segSieve(int l, int h)
{
	ll sq = sqrt(h);
	sieve(sq);
	vector<bool>isPrime(h - l + 1, true);
	for (ll p : prime) {
		ll sm = (l / p) * p;
		if (sm < l)
			sm += p;
		for (ll m = sm; m <= h; m += p)
			isPrime[m - l] = false;
	}
	int cc = 0;
	int ans = 0;
	rep(i, l, h + 1) {
		if (isPrime[i - l] == true) {
			cout << i << " ";
			//cc++;
		}
		else {
			//cout << i << " ";
		}
	}
	//cout << cc << endl;
	newl
}
//=============================================GCD=============================================

int gcd(int a, int b) {
	return b == 0 ? 0 : gcd(b, a & b);
}
int gcd2(int a, int b) {
	while (b != 0) {
		a %= b;
		swap(a, b);
	}
	return a;
}
//lcm finder
int lcm(int a, int b) {
	return (a * b) / gcd(a, b);
}
//extended Euclidian Algorithm  	to find linear Diophatine solution 		(ax+by=g) ==> g=gcd(a,b)
int gcdExt(int a, int b, int &x, int &y) {
	if (b == 0) {
		x = 1, y = 0;
		return a;
	}
	int x1, y1;
	int g = gcdExt(b, a % b, x1, y1);
	x = y1, y = x1 - (a / b) * y1;
	return g;
}


int smallestPrime(int n)
{
	cout << 1 << " ";
	vi v(n + 1, 0);
	for (int i = 2; i <= n; i++)
	{
		if (v[i] == 0)
		{
			cout << i << " ";
			for (int j = i * i; j <= n; j = j + i)
			{
				if (v[j] == 0)
				{
					v[j] = i;
				}
			}
		}
		else {
			cout << v[i] << " ";
		}
	}
}
void num_to_bin(int n) {
	if (n == 0) {return; }
	num_to_bin(n / 2);
	cout << n % 2;
}
bool str_palli(string s, int start, int end) {
	if (start >= end) {
		return true;
	}
	return (s[start] == s[end]) && str_palli(s, start + 1, end - 1);
}
//=============================================Sample Codes=============================================

void print_per(string s, int i = 0)
{
	if (i == s.length() - 1) {
		cout << s << "\n";
	}
	for (int j = i; j < s.length(); j++)
	{
		swap(s[i], s[j]);
		print_per(s, i + 1);
		swap(s[i], s[j]);
	}
}

void subset(string s, string curr = "", int index = 0)
{
	if (index == s.length())
	{
		cout << curr << " ";
		return;
	}
	subset(s, curr, index + 1);
	subset(s, curr + s[index], index + 1);
}

//=============================================MAIN CODE=============================================

void chalochale() {
	ci(n);
	int arr[n];
	rep(i, 0, n)	cin >> arr[i];
	stack<int>s;
	vi v;
	for (int i = n - 1; i >= 0; i--)
	//rep(i, 0, n)
	{
		if (s.size() == 0) {
			v.pb(-1);
		}
		else if (s.size() > 0 && s.top() < arr[i])
		{
			v.pb(s.top());
		}
		else if (s.size() > 0 && s.top() >= arr[i])
		{
			while (s.size() > 0 && s.top() >= arr[i])
			{
				s.pop();
			}
			if (s.size() == 0)
			{
				v.pb(-1);
			}
			else
			{
				v.pb(s.top());
			}
		}
		s.push(arr[i]);
	}
	reverse(v.begin(), v.end());
	rep(i, 0, v.size())	{
		cout << v[i] << " ";
	}
}

int32_t main()
{
	start_func();
	//kitnalega
	{
		chalochale();
		//newl
	}
	return 0;
}


3. Nearest smaller to right

#include<bits/stdc++.h>

//#include <ext/pb_ds/assoc_container.hpp>
//#include <ext/pb_ds/tree_policy.hpp>
//using namespace __gnu_pbds;

using namespace std;

//=============================================CONSTANTS=============================================

const long long SZ = 1e5 + 7;
const long long inf = 1e18;
const long long mod = 1e9 + 7;
const long long MOD = 998244353;
const long long PI = 3.1415926535897932384;

//=============================================MACROS=============================================

#define FastIO 					ios_base::sync_with_stdio(0); cin.tie(0); cout.tie(0)
#define kitnalega           	long long ___tc=1; cin >> ___tc; while (___tc--	)

#define rep(i,x,y)				for(int i=x;i<y;i++)
#define rep_Eq(i,x,y)			for(int i=x;i<=y;i++)
#define rep_Rev(i,x,y)			for(int i=x-1;i>=y;i--)
#define ll						long long
#define lli						long long int

#define ci(X)               	ll X; 			cin >> X
#define cii(X, Y)           	ll X, Y; 		cin >> X >> Y
#define ciii(X, Y, Z)       	ll X, Y, Z;		cin >> X >> Y >> Z
#define ciiii(A,X,Y,Z)			ll A,X,Y,Z;		cin >> A >> X >> Y >> Z
#define cs(s)					string s; 		cin>>s;



#define pb 						push_back
#define pf 						push_front
#define eb 						emplace_back
#define endl					"\n"
#define	newl					cout<<endl;
#define sep						cout<<"-----------------"<<endl;

#define mp 						make_pair
#define pq 						priority_queue

#define ff 						first
#define ss 						second

#define Max(a,b)            	((a > b) ? a : b)
#define Min(a,b)            	((a < b) ? a : b)

#define lb 						lower_bound
#define ub 						upper_bound
#define mx 						*max_element
#define mn 						*min_element



typedef vector<int> 			vi;
typedef vector<vi> 				vvi;
typedef vector<ll> 				vll;
typedef pair<int, int>			pii;
typedef pair<ll, ll>			pll;
typedef vector<pii>				vpii;
typedef vector<pll>				vpll;
typedef pair<lli, lli>			pll;



//=============================================FUNCTIONS=============================================

#define srt(a)			sort(a,a+n);
#define srt2(a)			sort(a.begin(),a.end());
#define rev(a)			reverse(a.begin(),a.end());

//=============================================Templates=============================================

template <typename ForwardIterator, class T>
ForwardIterator search(ForwardIterator start, ForwardIterator end, T key) {
	while (start != end) {
		if (*start == key) {
			return start;
		}
		start++;
	}
	return end;
}

//=============================================Input/Output=============================================

void start_func()
{	FastIO;
#ifndef ONLINE_JUDGE
	freopen("input.txt", "r", stdin);
	freopen("output.txt", "w", stdout);
#endif
}

//=============================================Sieve=============================================

vll prime;
bool isPrime(int n)
{
	if (n == 1) {
		return false;
	}
	if (n == 2 || n == 3) {
		return true;
	}
	if (n % 2 == 0 || n % 3 == 0) {
		return false;
	}
	for (int i = 5; i * i <= n; i = i + 6) {
		if (n % i == 0 || n % (i + 2) == 0) {
			return false;
		}
		return true;
	}
}
void sieve(int n)
{
	vector <bool> isPrime(n + 1, true);
	rep(i, 2, n + 1) {
		if (isPrime[i]) {
			prime.push_back(i);
			for (ll j = i * i; j <= n; j++) {
				isPrime[j] = false;
			}
		}
	}
}
void segSieve(int l, int h)
{
	ll sq = sqrt(h);
	sieve(sq);
	vector<bool>isPrime(h - l + 1, true);
	for (ll p : prime) {
		ll sm = (l / p) * p;
		if (sm < l)
			sm += p;
		for (ll m = sm; m <= h; m += p)
			isPrime[m - l] = false;
	}
	int cc = 0;
	int ans = 0;
	rep(i, l, h + 1) {
		if (isPrime[i - l] == true) {
			cout << i << " ";
			//cc++;
		}
		else {
			//cout << i << " ";
		}
	}
	//cout << cc << endl;
	newl
}
//=============================================GCD=============================================

int gcd(int a, int b) {
	return b == 0 ? 0 : gcd(b, a & b);
}
int gcd2(int a, int b) {
	while (b != 0) {
		a %= b;
		swap(a, b);
	}
	return a;
}
//lcm finder
int lcm(int a, int b) {
	return (a * b) / gcd(a, b);
}
//extended Euclidian Algorithm  	to find linear Diophatine solution 		(ax+by=g) ==> g=gcd(a,b)
int gcdExt(int a, int b, int &x, int &y) {
	if (b == 0) {
		x = 1, y = 0;
		return a;
	}
	int x1, y1;
	int g = gcdExt(b, a % b, x1, y1);
	x = y1, y = x1 - (a / b) * y1;
	return g;
}


int smallestPrime(int n)
{
	cout << 1 << " ";
	vi v(n + 1, 0);
	for (int i = 2; i <= n; i++)
	{
		if (v[i] == 0)
		{
			cout << i << " ";
			for (int j = i * i; j <= n; j = j + i)
			{
				if (v[j] == 0)
				{
					v[j] = i;
				}
			}
		}
		else {
			cout << v[i] << " ";
		}
	}
}
void num_to_bin(int n) {
	if (n == 0) {return; }
	num_to_bin(n / 2);
	cout << n % 2;
}
bool str_palli(string s, int start, int end) {
	if (start >= end) {
		return true;
	}
	return (s[start] == s[end]) && str_palli(s, start + 1, end - 1);
}
//=============================================Sample Codes=============================================

void print_per(string s, int i = 0)
{
	if (i == s.length() - 1) {
		cout << s << "\n";
	}
	for (int j = i; j < s.length(); j++)
	{
		swap(s[i], s[j]);
		print_per(s, i + 1);
		swap(s[i], s[j]);
	}
}

void subset(string s, string curr = "", int index = 0)
{
	if (index == s.length())
	{
		cout << curr << " ";
		return;
	}
	subset(s, curr, index + 1);
	subset(s, curr + s[index], index + 1);
}

//=============================================MAIN CODE=============================================

void calculateSpan(int arr[], int n, int S[])
{
	stack<int> st;
	st.push(0);
	S[0] = 1;
	for (int i = 1; i < n; i++)
	{
		while (!st.empty() && arr[st.top()] <= arr[i])
		{
			st.pop();
		}
		S[i] = (st.empty()) ? (i + 1) : (i - st.top());
		st.push(i);
	}
}
void printArray(int arr[], int n)
{
	for (int i = 0; i < n; i++)
		cout << arr[i] << " ";
}
void chalochale() {
	ci(n);
	int arr[n];
	int S[n];
	rep(i, 0, n)
	{
		cin >> arr[i];
	}
	calculateSpan(arr, n, S);
	printArray(S, n);

}

int32_t main()
{
	start_func();
	//kitnalega
	{
		chalochale();
		//newl
	}
	return 0;
}

Stock span problem. //(Amazon Interview Question)

#include<bits/stdc++.h>

//#include <ext/pb_ds/assoc_container.hpp>
//#include <ext/pb_ds/tree_policy.hpp>
//using namespace __gnu_pbds;

using namespace std;

//=============================================CONSTANTS=============================================

const long long SZ = 1e5 + 7;
const long long inf = 1e18;
const long long mod = 1e9 + 7;
const long long MOD = 998244353;
const long long PI = 3.1415926535897932384;

//=============================================MACROS=============================================

#define FastIO 					ios_base::sync_with_stdio(0); cin.tie(0); cout.tie(0)
#define kitnalega           	long long ___tc=1; cin >> ___tc; while (___tc--	)

#define rep(i,x,y)				for(int i=x;i<y;i++)
#define rep_Eq(i,x,y)			for(int i=x;i<=y;i++)
#define rep_Rev(i,x,y)			for(int i=x-1;i>=y;i--)
#define ll						long long
#define lli						long long int

#define ci(X)               	ll X; 			cin >> X
#define cii(X, Y)           	ll X, Y; 		cin >> X >> Y
#define ciii(X, Y, Z)       	ll X, Y, Z;		cin >> X >> Y >> Z
#define ciiii(A,X,Y,Z)			ll A,X,Y,Z;		cin >> A >> X >> Y >> Z
#define cs(s)					string s; 		cin>>s;



#define pb 						push_back
#define pf 						push_front
#define eb 						emplace_back
#define endl					"\n"
#define	newl					cout<<endl;
#define sep						cout<<"-----------------"<<endl;

#define mp 						make_pair
#define pq 						priority_queue

#define ff 						first
#define ss 						second

#define Max(a,b)            	((a > b) ? a : b)
#define Min(a,b)            	((a < b) ? a : b)

#define lb 						lower_bound
#define ub 						upper_bound
#define mx 						*max_element
#define mn 						*min_element



typedef vector<int> 			vi;
typedef vector<vi> 				vvi;
typedef vector<ll> 				vll;
typedef pair<int, int>			pii;
typedef pair<ll, ll>			pll;
typedef vector<pii>				vpii;
typedef vector<pll>				vpll;
typedef pair<lli, lli>			pll;



//=============================================FUNCTIONS=============================================

#define srt(a)			sort(a,a+n);
#define srt2(a)			sort(a.begin(),a.end());
#define rev(a)			reverse(a.begin(),a.end());

//=============================================Templates=============================================

template <typename ForwardIterator, class T>
ForwardIterator search(ForwardIterator start, ForwardIterator end, T key) {
	while (start != end) {
		if (*start == key) {
			return start;
		}
		start++;
	}
	return end;
}

//=============================================Input/Output=============================================

void start_func()
{	FastIO;
#ifndef ONLINE_JUDGE
	freopen("input.txt", "r", stdin);
	freopen("output.txt", "w", stdout);
#endif
}

//=============================================Sieve=============================================

vll prime;
bool isPrime(int n)
{
	if (n == 1) {
		return false;
	}
	if (n == 2 || n == 3) {
		return true;
	}
	if (n % 2 == 0 || n % 3 == 0) {
		return false;
	}
	for (int i = 5; i * i <= n; i = i + 6) {
		if (n % i == 0 || n % (i + 2) == 0) {
			return false;
		}
		return true;
	}
}
void sieve(int n)
{
	vector <bool> isPrime(n + 1, true);
	rep(i, 2, n + 1) {
		if (isPrime[i]) {
			prime.push_back(i);
			for (ll j = i * i; j <= n; j++) {
				isPrime[j] = false;
			}
		}
	}
}
void segSieve(int l, int h)
{
	ll sq = sqrt(h);
	sieve(sq);
	vector<bool>isPrime(h - l + 1, true);
	for (ll p : prime) {
		ll sm = (l / p) * p;
		if (sm < l)
			sm += p;
		for (ll m = sm; m <= h; m += p)
			isPrime[m - l] = false;
	}
	int cc = 0;
	int ans = 0;
	rep(i, l, h + 1) {
		if (isPrime[i - l] == true) {
			cout << i << " ";
			//cc++;
		}
		else {
			//cout << i << " ";
		}
	}
	//cout << cc << endl;
	newl
}
//=============================================GCD=============================================

int gcd(int a, int b) {
	return b == 0 ? 0 : gcd(b, a & b);
}
int gcd2(int a, int b) {
	while (b != 0) {
		a %= b;
		swap(a, b);
	}
	return a;
}
//lcm finder
int lcm(int a, int b) {
	return (a * b) / gcd(a, b);
}
//extended Euclidian Algorithm  	to find linear Diophatine solution 		(ax+by=g) ==> g=gcd(a,b)
int gcdExt(int a, int b, int &x, int &y) {
	if (b == 0) {
		x = 1, y = 0;
		return a;
	}
	int x1, y1;
	int g = gcdExt(b, a % b, x1, y1);
	x = y1, y = x1 - (a / b) * y1;
	return g;
}


int smallestPrime(int n)
{
	cout << 1 << " ";
	vi v(n + 1, 0);
	for (int i = 2; i <= n; i++)
	{
		if (v[i] == 0)
		{
			cout << i << " ";
			for (int j = i * i; j <= n; j = j + i)
			{
				if (v[j] == 0)
				{
					v[j] = i;
				}
			}
		}
		else {
			cout << v[i] << " ";
		}
	}
}
void num_to_bin(int n) {
	if (n == 0) {return; }
	num_to_bin(n / 2);
	cout << n % 2;
}
bool str_palli(string s, int start, int end) {
	if (start >= end) {
		return true;
	}
	return (s[start] == s[end]) && str_palli(s, start + 1, end - 1);
}
//=============================================Sample Codes=============================================

void print_per(string s, int i = 0)
{
	if (i == s.length() - 1) {
		cout << s << "\n";
	}
	for (int j = i; j < s.length(); j++)
	{
		swap(s[i], s[j]);
		print_per(s, i + 1);
		swap(s[i], s[j]);
	}
}

void subset(string s, string curr = "", int index = 0)
{
	if (index == s.length())
	{
		cout << curr << " ";
		return;
	}
	subset(s, curr, index + 1);
	subset(s, curr + s[index], index + 1);
}

//=============================================MAIN CODE=============================================
int largestRectangleArea(vector<int>& heights)
{
	int n;
	n = heights.size();
	stack<pair<int, int>>str;
	vector<int>vl;
	int pseudo_index = -1;
	for (int i = 0; i < n; i++)
	{
		if (str.empty())
		{
			vl.push_back(pseudo_index);
		}
		else if (!str.empty() && heights[i] > str.top().first)
		{
			vl.push_back(str.top().second);
		}
		else if (!str.empty() && heights[i] <= str.top().first)
		{
			while (!str.empty() && heights[i] <= str.top().first)
			{
				str.pop();
			}
			if (str.empty())
			{
				vl.push_back(pseudo_index);
			}
			else
			{
				vl.push_back(str.top().second);
			}
		}
		str.push({heights[i], i});
	}
	//nsr
	while (!str.empty())
	{
		str.pop();
	}
	pseudo_index = n;
	vector<int>vr;
	for (int i = n - 1; i >= 0; i--)
	{
		if (str.empty())
		{
			vr.push_back(pseudo_index);
		}
		else if (!str.empty() && heights[i] > str.top().first)
		{
			vr.push_back(str.top().second);
		}
		else if (!str.empty() && heights[i] <= str.top().first)
		{
			while (!str.empty() && heights[i] <= str.top().first)
			{
				str.pop();
			}
			if (str.empty())
			{
				vr.push_back(pseudo_index);
			}
			else
			{
				vr.push_back(str.top().second);
			}
		}
		str.push({heights[i], i});
	}
	reverse(vr.begin(), vr.end());
	int width[n];
	for (int i = 0; i < n; i++)
	{
		width[i] = vr[i] - vl[i] - 1;
	}
	int area[n];
	for (int i = 0; i < n; i++)
	{
		area[i] = width[i] * heights[i];
	}
	int max = area[0];
	for (int i = 1; i < n; i++)
	{
		if (area[i] > max)
		{
			max = area[i];
		}
	}
	return max;
}


void chalochale() {
	ci(n);
	vi heights;
	rep(i, 0, n)
	{
		ci(x);
		heights.pb(x);
	}
	cout << largestRectangleArea(heights);
}

int32_t main()
{
	start_func();
	//kitnalega
	{
		chalochale();
		//newl
	}
	return 0;
}



#include<bits/stdc++.h>

//#include <ext/pb_ds/assoc_container.hpp>
//#include <ext/pb_ds/tree_policy.hpp>
//using namespace __gnu_pbds;

using namespace std;

//=============================================CONSTANTS=============================================

const long long SZ = 1e5 + 7;
const long long inf = 1e18;
const long long mod = 1e9 + 7;
const long long MOD = 998244353;
const long long PI = 3.1415926535897932384;

//=============================================MACROS=============================================

#define FastIO 					ios_base::sync_with_stdio(0); cin.tie(0); cout.tie(0)
#define kitnalega           	long long ___tc=1; cin >> ___tc; while (___tc--	)

#define rep(i,x,y)				for(int i=x;i<y;i++)
#define rep_Eq(i,x,y)			for(int i=x;i<=y;i++)
#define rep_Rev(i,x,y)			for(int i=x-1;i>=y;i--)
#define ll						long long
#define lli						long long int

#define ci(X)               	ll X; 			cin >> X
#define cii(X, Y)           	ll X, Y; 		cin >> X >> Y
#define ciii(X, Y, Z)       	ll X, Y, Z;		cin >> X >> Y >> Z
#define ciiii(A,X,Y,Z)			ll A,X,Y,Z;		cin >> A >> X >> Y >> Z
#define cs(s)					string s; 		cin>>s;



#define pb 						push_back
#define pf 						push_front
#define eb 						emplace_back
#define endl					"\n"
#define	newl					cout<<endl;
#define sep						cout<<"-----------------"<<endl;

#define mp 						make_pair
#define pq 						priority_queue

#define ff 						first
#define ss 						second

#define Max(a,b)            	((a > b) ? a : b)
#define Min(a,b)            	((a < b) ? a : b)

#define lb 						lower_bound
#define ub 						upper_bound
#define mx 						*max_element
#define mn 						*min_element



typedef vector<int> 			vi;
typedef vector<vi> 				vvi;
typedef vector<ll> 				vll;
typedef pair<int, int>			pii;
typedef pair<ll, ll>			pll;
typedef vector<pii>				vpii;
typedef vector<pll>				vpll;
typedef pair<lli, lli>			pll;



//=============================================FUNCTIONS=============================================

#define srt(a)			sort(a,a+n);
#define srt2(a)			sort(a.begin(),a.end());
#define rev(a)			reverse(a.begin(),a.end());

//=============================================Templates=============================================

template <typename ForwardIterator, class T>
ForwardIterator search(ForwardIterator start, ForwardIterator end, T key) {
	while (start != end) {
		if (*start == key) {
			return start;
		}
		start++;
	}
	return end;
}

//=============================================Input/Output=============================================

void start_func()
{	FastIO;
#ifndef ONLINE_JUDGE
	freopen("input.txt", "r", stdin);
	freopen("output.txt", "w", stdout);
#endif
}

//=============================================Sieve=============================================

vll prime;
bool isPrime(int n)
{
	if (n == 1) {
		return false;
	}
	if (n == 2 || n == 3) {
		return true;
	}
	if (n % 2 == 0 || n % 3 == 0) {
		return false;
	}
	for (int i = 5; i * i <= n; i = i + 6) {
		if (n % i == 0 || n % (i + 2) == 0) {
			return false;
		}
		return true;
	}
}
void sieve(int n)
{
	vector <bool> isPrime(n + 1, true);
	rep(i, 2, n + 1) {
		if (isPrime[i]) {
			prime.push_back(i);
			for (ll j = i * i; j <= n; j++) {
				isPrime[j] = false;
			}
		}
	}
}
void segSieve(int l, int h)
{
	ll sq = sqrt(h);
	sieve(sq);
	vector<bool>isPrime(h - l + 1, true);
	for (ll p : prime) {
		ll sm = (l / p) * p;
		if (sm < l)
			sm += p;
		for (ll m = sm; m <= h; m += p)
			isPrime[m - l] = false;
	}
	int cc = 0;
	int ans = 0;
	rep(i, l, h + 1) {
		if (isPrime[i - l] == true) {
			cout << i << " ";
			//cc++;
		}
		else {
			//cout << i << " ";
		}
	}
	//cout << cc << endl;
	newl
}
//=============================================GCD=============================================

int gcd(int a, int b) {
	return b == 0 ? 0 : gcd(b, a & b);
}
int gcd2(int a, int b) {
	while (b != 0) {
		a %= b;
		swap(a, b);
	}
	return a;
}
//lcm finder
int lcm(int a, int b) {
	return (a * b) / gcd(a, b);
}
//extended Euclidian Algorithm  	to find linear Diophatine solution 		(ax+by=g) ==> g=gcd(a,b)
int gcdExt(int a, int b, int &x, int &y) {
	if (b == 0) {
		x = 1, y = 0;
		return a;
	}
	int x1, y1;
	int g = gcdExt(b, a % b, x1, y1);
	x = y1, y = x1 - (a / b) * y1;
	return g;
}


int smallestPrime(int n)
{
	cout << 1 << " ";
	vi v(n + 1, 0);
	for (int i = 2; i <= n; i++)
	{
		if (v[i] == 0)
		{
			cout << i << " ";
			for (int j = i * i; j <= n; j = j + i)
			{
				if (v[j] == 0)
				{
					v[j] = i;
				}
			}
		}
		else {
			cout << v[i] << " ";
		}
	}
}
void num_to_bin(int n) {
	if (n == 0) {return; }
	num_to_bin(n / 2);
	cout << n % 2;
}
bool str_palli(string s, int start, int end) {
	if (start >= end) {
		return true;
	}
	return (s[start] == s[end]) && str_palli(s, start + 1, end - 1);
}
//=============================================Sample Codes=============================================

void print_per(string s, int i = 0)
{
	if (i == s.length() - 1) {
		cout << s << "\n";
	}
	for (int j = i; j < s.length(); j++)
	{
		swap(s[i], s[j]);
		print_per(s, i + 1);
		swap(s[i], s[j]);
	}
}

void subset(string s, string curr = "", int index = 0)
{
	if (index == s.length())
	{
		cout << curr << " ";
		return;
	}
	subset(s, curr, index + 1);
	subset(s, curr + s[index], index + 1);
}

//=============================================MAIN CODE=============================================

int trap(vector<int>& arr) {
	int res = 0;
	if (arr.size() == 0)
	{
		return 0;
	}
	int lmax[arr.size()], rmax[arr.size()];
	lmax[0] = arr[0];
	for (int i = 1; i < arr.size(); i++)
	{
		lmax[i] = max(arr[i], lmax[i - 1]);
	}
	rmax[arr.size() - 1] = arr[arr.size() - 1];
	for (int i = arr.size() - 2; i >= 0; i--)
	{
		rmax[i] = max(arr[i], rmax[i + 1]);
	}
	for (int i = 1; i < arr.size() - 1; i++)
	{
		res += min(lmax[i], rmax[i]) - arr[i];
	}
	return res;
}

void chalochale() {
	ci(n);
	vi v;
	rep(i, 0, n)
	{
		ci(x);
		v.pb(x);
	}
	cout << trap(v);
}

int32_t main()
{
	start_func();
	//kitnalega
	{
		chalochale();
		//newl
	}
	return 0;
}


Maximum area of histogram


#include<bits/stdc++.h>

//#include <ext/pb_ds/assoc_container.hpp>
//#include <ext/pb_ds/tree_policy.hpp>
//using namespace __gnu_pbds;

using namespace std;

//=============================================CONSTANTS=============================================

const long long SZ = 1e5 + 7;
const long long inf = 1e18;
const long long mod = 1e9 + 7;
const long long MOD = 998244353;
const long long PI = 3.1415926535897932384;

//=============================================MACROS=============================================

#define FastIO 					ios_base::sync_with_stdio(0); cin.tie(0); cout.tie(0)
#define kitnalega           	long long ___tc=1; cin >> ___tc; while (___tc--	)

#define rep(i,x,y)				for(int i=x;i<y;i++)
#define rep_Eq(i,x,y)			for(int i=x;i<=y;i++)
#define rep_Rev(i,x,y)			for(int i=x-1;i>=y;i--)
#define ll						long long
#define lli						long long int

#define ci(X)               	ll X; 			cin >> X
#define cii(X, Y)           	ll X, Y; 		cin >> X >> Y
#define ciii(X, Y, Z)       	ll X, Y, Z;		cin >> X >> Y >> Z
#define ciiii(A,X,Y,Z)			ll A,X,Y,Z;		cin >> A >> X >> Y >> Z
#define cs(s)					string s; 		cin>>s;



#define pb 						push_back
#define pf 						push_front
#define eb 						emplace_back
#define endl					"\n"
#define	newl					cout<<endl;
#define sep						cout<<"-----------------"<<endl;

#define mp 						make_pair
#define pq 						priority_queue

#define ff 						first
#define ss 						second

#define Max(a,b)            	((a > b) ? a : b)
#define Min(a,b)            	((a < b) ? a : b)

#define lb 						lower_bound
#define ub 						upper_bound
#define mx 						*max_element
#define mn 						*min_element



typedef vector<int> 			vi;
typedef vector<vi> 				vvi;
typedef vector<ll> 				vll;
typedef pair<int, int>			pii;
typedef pair<ll, ll>			pll;
typedef vector<pii>				vpii;
typedef vector<pll>				vpll;
typedef pair<lli, lli>			pll;



//=============================================FUNCTIONS=============================================

#define srt(a)			sort(a,a+n);
#define srt2(a)			sort(a.begin(),a.end());
#define rev(a)			reverse(a.begin(),a.end());

//=============================================Templates=============================================

template <typename ForwardIterator, class T>
ForwardIterator search(ForwardIterator start, ForwardIterator end, T key) {
	while (start != end) {
		if (*start == key) {
			return start;
		}
		start++;
	}
	return end;
}

//=============================================Input/Output=============================================

void start_func()
{	FastIO;
#ifndef ONLINE_JUDGE
	freopen("input.txt", "r", stdin);
	freopen("output.txt", "w", stdout);
#endif
}

//=============================================Sieve=============================================

vll prime;
bool isPrime(int n)
{
	if (n == 1) {
		return false;
	}
	if (n == 2 || n == 3) {
		return true;
	}
	if (n % 2 == 0 || n % 3 == 0) {
		return false;
	}
	for (int i = 5; i * i <= n; i = i + 6) {
		if (n % i == 0 || n % (i + 2) == 0) {
			return false;
		}
		return true;
	}
}
void sieve(int n)
{
	vector <bool> isPrime(n + 1, true);
	rep(i, 2, n + 1) {
		if (isPrime[i]) {
			prime.push_back(i);
			for (ll j = i * i; j <= n; j++) {
				isPrime[j] = false;
			}
		}
	}
}
void segSieve(int l, int h)
{
	ll sq = sqrt(h);
	sieve(sq);
	vector<bool>isPrime(h - l + 1, true);
	for (ll p : prime) {
		ll sm = (l / p) * p;
		if (sm < l)
			sm += p;
		for (ll m = sm; m <= h; m += p)
			isPrime[m - l] = false;
	}
	int cc = 0;
	int ans = 0;
	rep(i, l, h + 1) {
		if (isPrime[i - l] == true) {
			cout << i << " ";
			//cc++;
		}
		else {
			//cout << i << " ";
		}
	}
	//cout << cc << endl;
	newl
}
//=============================================GCD=============================================

int gcd(int a, int b) {
	return b == 0 ? 0 : gcd(b, a & b);
}
int gcd2(int a, int b) {
	while (b != 0) {
		a %= b;
		swap(a, b);
	}
	return a;
}
//lcm finder
int lcm(int a, int b) {
	return (a * b) / gcd(a, b);
}
//extended Euclidian Algorithm  	to find linear Diophatine solution 		(ax+by=g) ==> g=gcd(a,b)
int gcdExt(int a, int b, int &x, int &y) {
	if (b == 0) {
		x = 1, y = 0;
		return a;
	}
	int x1, y1;
	int g = gcdExt(b, a % b, x1, y1);
	x = y1, y = x1 - (a / b) * y1;
	return g;
}


int smallestPrime(int n)
{
	cout << 1 << " ";
	vi v(n + 1, 0);
	for (int i = 2; i <= n; i++)
	{
		if (v[i] == 0)
		{
			cout << i << " ";
			for (int j = i * i; j <= n; j = j + i)
			{
				if (v[j] == 0)
				{
					v[j] = i;
				}
			}
		}
		else {
			cout << v[i] << " ";
		}
	}
}
void num_to_bin(int n) {
	if (n == 0) {return; }
	num_to_bin(n / 2);
	cout << n % 2;
}
bool str_palli(string s, int start, int end) {
	if (start >= end) {
		return true;
	}
	return (s[start] == s[end]) && str_palli(s, start + 1, end - 1);
}
//=============================================Sample Codes=============================================

void print_per(string s, int i = 0)
{
	if (i == s.length() - 1) {
		cout << s << "\n";
	}
	for (int j = i; j < s.length(); j++)
	{
		swap(s[i], s[j]);
		print_per(s, i + 1);
		swap(s[i], s[j]);
	}
}

void subset(string s, string curr = "", int index = 0)
{
	if (index == s.length())
	{
		cout << curr << " ";
		return;
	}
	subset(s, curr, index + 1);
	subset(s, curr + s[index], index + 1);
}

//=============================================MAIN CODE=============================================

#define R 4
#define C 4

int maxHist(int row[])
{
	stack<int> result;

	int top_val;
	int max_area = 0;
	int area = 0;
	int i = 0;
	while (i < C) {
		if (result.empty() || row[result.top()] <= row[i])
			result.push(i++);

		else {
			top_val = row[result.top()];
			result.pop();
			area = top_val * i;

			if (!result.empty())
				area = top_val * (i - result.top() - 1);
			max_area = max(area, max_area);
		}
	}

	while (!result.empty()) {
		top_val = row[result.top()];
		result.pop();
		area = top_val * i;
		if (!result.empty())
			area = top_val * (i - result.top() - 1);

		max_area = max(area, max_area);
	}
	return max_area;
}

int maxRectangle(int A[][C])
{
	int result = maxHist(A[0]);

	for (int i = 1; i < R; i++) {

		for (int j = 0; j < C; j++)

			if (A[i][j])
				A[i][j] += A[i - 1][j];
		result = max(result, maxHist(A[i]));
	}

	return result;
}
void chalochale() {
	int A[][C] = {
		{ 0, 1, 1, 0 },
		{ 1, 1, 1, 1 },
		{ 1, 1, 1, 1 },
		{ 1, 1, 0, 0 },
	};

	cout << "Area of maximum rectangle is " << maxRectangle(A);
}

int32_t main()
{
	start_func();
	//kitnalega
	{
		chalochale();
		//newl
	}
	return 0;
}


6. Rain water trapping.

#include<bits/stdc++.h>

//#include <ext/pb_ds/assoc_container.hpp>
//#include <ext/pb_ds/tree_policy.hpp>
//using namespace __gnu_pbds;

using namespace std;

//=============================================CONSTANTS=============================================

const long long SZ = 1e5 + 7;
const long long inf = 1e18;
const long long mod = 1e9 + 7;
const long long MOD = 998244353;
const long long PI = 3.1415926535897932384;

//=============================================MACROS=============================================

#define FastIO 					ios_base::sync_with_stdio(0); cin.tie(0); cout.tie(0)
#define kitnalega           	long long ___tc=1; cin >> ___tc; while (___tc--	)

#define rep(i,x,y)				for(int i=x;i<y;i++)
#define rep_Eq(i,x,y)			for(int i=x;i<=y;i++)
#define rep_Rev(i,x,y)			for(int i=x-1;i>=y;i--)
#define ll						long long
#define lli						long long int

#define ci(X)               	ll X; 			cin >> X
#define cii(X, Y)           	ll X, Y; 		cin >> X >> Y
#define ciii(X, Y, Z)       	ll X, Y, Z;		cin >> X >> Y >> Z
#define ciiii(A,X,Y,Z)			ll A,X,Y,Z;		cin >> A >> X >> Y >> Z
#define cs(s)					string s; 		cin>>s;



#define pb 						push_back
#define pf 						push_front
#define eb 						emplace_back
#define endl					"\n"
#define	newl					cout<<endl;
#define sep						cout<<"-----------------"<<endl;

#define mp 						make_pair
#define pq 						priority_queue

#define ff 						first
#define ss 						second

#define Max(a,b)            	((a > b) ? a : b)
#define Min(a,b)            	((a < b) ? a : b)

#define lb 						lower_bound
#define ub 						upper_bound
#define mx 						*max_element
#define mn 						*min_element



typedef vector<int> 			vi;
typedef vector<vi> 				vvi;
typedef vector<ll> 				vll;
typedef pair<int, int>			pii;
typedef pair<ll, ll>			pll;
typedef vector<pii>				vpii;
typedef vector<pll>				vpll;
typedef pair<lli, lli>			pll;



//=============================================FUNCTIONS=============================================

#define srt(a)			sort(a,a+n);
#define srt2(a)			sort(a.begin(),a.end());
#define rev(a)			reverse(a.begin(),a.end());

//=============================================Templates=============================================

template <typename ForwardIterator, class T>
ForwardIterator search(ForwardIterator start, ForwardIterator end, T key) {
	while (start != end) {
		if (*start == key) {
			return start;
		}
		start++;
	}
	return end;
}

//=============================================Input/Output=============================================

void start_func()
{	FastIO;
#ifndef ONLINE_JUDGE
	freopen("input.txt", "r", stdin);
	freopen("output.txt", "w", stdout);
#endif
}

//=============================================Sieve=============================================

vll prime;
bool isPrime(int n)
{
	if (n == 1) {
		return false;
	}
	if (n == 2 || n == 3) {
		return true;
	}
	if (n % 2 == 0 || n % 3 == 0) {
		return false;
	}
	for (int i = 5; i * i <= n; i = i + 6) {
		if (n % i == 0 || n % (i + 2) == 0) {
			return false;
		}
		return true;
	}
}
void sieve(int n)
{
	vector <bool> isPrime(n + 1, true);
	rep(i, 2, n + 1) {
		if (isPrime[i]) {
			prime.push_back(i);
			for (ll j = i * i; j <= n; j++) {
				isPrime[j] = false;
			}
		}
	}
}
void segSieve(int l, int h)
{
	ll sq = sqrt(h);
	sieve(sq);
	vector<bool>isPrime(h - l + 1, true);
	for (ll p : prime) {
		ll sm = (l / p) * p;
		if (sm < l)
			sm += p;
		for (ll m = sm; m <= h; m += p)
			isPrime[m - l] = false;
	}
	int cc = 0;
	int ans = 0;
	rep(i, l, h + 1) {
		if (isPrime[i - l] == true) {
			cout << i << " ";
			//cc++;
		}
		else {
			//cout << i << " ";
		}
	}
	//cout << cc << endl;
	newl
}
//=============================================GCD=============================================

int gcd(int a, int b) {
	return b == 0 ? 0 : gcd(b, a & b);
}
int gcd2(int a, int b) {
	while (b != 0) {
		a %= b;
		swap(a, b);
	}
	return a;
}
//lcm finder
int lcm(int a, int b) {
	return (a * b) / gcd(a, b);
}
//extended Euclidian Algorithm  	to find linear Diophatine solution 		(ax+by=g) ==> g=gcd(a,b)
int gcdExt(int a, int b, int &x, int &y) {
	if (b == 0) {
		x = 1, y = 0;
		return a;
	}
	int x1, y1;
	int g = gcdExt(b, a % b, x1, y1);
	x = y1, y = x1 - (a / b) * y1;
	return g;
}


int smallestPrime(int n)
{
	cout << 1 << " ";
	vi v(n + 1, 0);
	for (int i = 2; i <= n; i++)
	{
		if (v[i] == 0)
		{
			cout << i << " ";
			for (int j = i * i; j <= n; j = j + i)
			{
				if (v[j] == 0)
				{
					v[j] = i;
				}
			}
		}
		else {
			cout << v[i] << " ";
		}
	}
}
void num_to_bin(int n) {
	if (n == 0) {return; }
	num_to_bin(n / 2);
	cout << n % 2;
}
bool str_palli(string s, int start, int end) {
	if (start >= end) {
		return true;
	}
	return (s[start] == s[end]) && str_palli(s, start + 1, end - 1);
}
//=============================================Sample Codes=============================================

void print_per(string s, int i = 0)
{
	if (i == s.length() - 1) {
		cout << s << "\n";
	}
	for (int j = i; j < s.length(); j++)
	{
		swap(s[i], s[j]);
		print_per(s, i + 1);
		swap(s[i], s[j]);
	}
}

void subset(string s, string curr = "", int index = 0)
{
	if (index == s.length())
	{
		cout << curr << " ";
		return;
	}
	subset(s, curr, index + 1);
	subset(s, curr + s[index], index + 1);
}

//=============================================MAIN CODE=============================================


stack<int> st;
stack<int> minSt;
void push(int x)
{
	st.push(x);
	if (minSt.empty() || minSt.top() > x)
	{
		minSt.push(x);
	}
	else
	{
		minSt.push(minSt.top());
	}
}
void pop()
{
	st.pop();
	minSt.pop();
}
int top()
{
	return st.top();
}
int getMin()
{
	return minSt.top();
}

void chalochale() {
	push(-2);
	push(0);
	cout << getMin() << endl;
	push(-3);
	pop();
	cout << top() << endl;
	cout << getMin() << endl;
}

int32_t main()
{
	start_func();
	//kitnalega
	{
		chalochale();
		//newl
	}
	return 0;
}

7. max area of rectangle in binary matrix

#include<bits/stdc++.h>

//#include <ext/pb_ds/assoc_container.hpp>
//#include <ext/pb_ds/tree_policy.hpp>
//using namespace __gnu_pbds;

using namespace std;

//=============================================CONSTANTS=============================================

const long long SZ = 1e5 + 7;
const long long inf = 1e18;
const long long mod = 1e9 + 7;
const long long MOD = 998244353;
const long long PI = 3.1415926535897932384;

//=============================================MACROS=============================================

#define FastIO 					ios_base::sync_with_stdio(0); cin.tie(0); cout.tie(0)
#define kitnalega           	long long ___tc=1; cin >> ___tc; while (___tc--	)

#define rep(i,x,y)				for(int i=x;i<y;i++)
#define rep_Eq(i,x,y)			for(int i=x;i<=y;i++)
#define rep_Rev(i,x,y)			for(int i=x-1;i>=y;i--)
#define ll						long long
#define lli						long long int

#define ci(X)               	ll X; 			cin >> X
#define cii(X, Y)           	ll X, Y; 		cin >> X >> Y
#define ciii(X, Y, Z)       	ll X, Y, Z;		cin >> X >> Y >> Z
#define ciiii(A,X,Y,Z)			ll A,X,Y,Z;		cin >> A >> X >> Y >> Z
#define cs(s)					string s; 		cin>>s;



#define pb 						push_back
#define pf 						push_front
#define eb 						emplace_back
#define endl					"\n"
#define	newl					cout<<endl;
#define sep						cout<<"-----------------"<<endl;

#define mp 						make_pair
#define pq 						priority_queue

#define ff 						first
#define ss 						second

#define Max(a,b)            	((a > b) ? a : b)
#define Min(a,b)            	((a < b) ? a : b)

#define lb 						lower_bound
#define ub 						upper_bound
#define mx 						*max_element
#define mn 						*min_element



typedef vector<int> 			vi;
typedef vector<vi> 				vvi;
typedef vector<ll> 				vll;
typedef pair<int, int>			pii;
typedef pair<ll, ll>			pll;
typedef vector<pii>				vpii;
typedef vector<pll>				vpll;
typedef pair<lli, lli>			pll;



//=============================================FUNCTIONS=============================================

#define srt(a)			sort(a,a+n);
#define srt2(a)			sort(a.begin(),a.end());
#define rev(a)			reverse(a.begin(),a.end());

//=============================================Templates=============================================

template <typename ForwardIterator, class T>
ForwardIterator search(ForwardIterator start, ForwardIterator end, T key) {
	while (start != end) {
		if (*start == key) {
			return start;
		}
		start++;
	}
	return end;
}

//=============================================Input/Output=============================================

void start_func()
{	FastIO;
#ifndef ONLINE_JUDGE
	freopen("input.txt", "r", stdin);
	freopen("output.txt", "w", stdout);
#endif
}

//=============================================Sieve=============================================

vll prime;
bool isPrime(int n)
{
	if (n == 1) {
		return false;
	}
	if (n == 2 || n == 3) {
		return true;
	}
	if (n % 2 == 0 || n % 3 == 0) {
		return false;
	}
	for (int i = 5; i * i <= n; i = i + 6) {
		if (n % i == 0 || n % (i + 2) == 0) {
			return false;
		}
		return true;
	}
}
void sieve(int n)
{
	vector <bool> isPrime(n + 1, true);
	rep(i, 2, n + 1) {
		if (isPrime[i]) {
			prime.push_back(i);
			for (ll j = i * i; j <= n; j++) {
				isPrime[j] = false;
			}
		}
	}
}
void segSieve(int l, int h)
{
	ll sq = sqrt(h);
	sieve(sq);
	vector<bool>isPrime(h - l + 1, true);
	for (ll p : prime) {
		ll sm = (l / p) * p;
		if (sm < l)
			sm += p;
		for (ll m = sm; m <= h; m += p)
			isPrime[m - l] = false;
	}
	int cc = 0;
	int ans = 0;
	rep(i, l, h + 1) {
		if (isPrime[i - l] == true) {
			cout << i << " ";
			//cc++;
		}
		else {
			//cout << i << " ";
		}
	}
	//cout << cc << endl;
	newl
}
//=============================================GCD=============================================

int gcd(int a, int b) {
	return b == 0 ? 0 : gcd(b, a & b);
}
int gcd2(int a, int b) {
	while (b != 0) {
		a %= b;
		swap(a, b);
	}
	return a;
}
//lcm finder
int lcm(int a, int b) {
	return (a * b) / gcd(a, b);
}
//extended Euclidian Algorithm  	to find linear Diophatine solution 		(ax+by=g) ==> g=gcd(a,b)
int gcdExt(int a, int b, int &x, int &y) {
	if (b == 0) {
		x = 1, y = 0;
		return a;
	}
	int x1, y1;
	int g = gcdExt(b, a % b, x1, y1);
	x = y1, y = x1 - (a / b) * y1;
	return g;
}


int smallestPrime(int n)
{
	cout << 1 << " ";
	vi v(n + 1, 0);
	for (int i = 2; i <= n; i++)
	{
		if (v[i] == 0)
		{
			cout << i << " ";
			for (int j = i * i; j <= n; j = j + i)
			{
				if (v[j] == 0)
				{
					v[j] = i;
				}
			}
		}
		else {
			cout << v[i] << " ";
		}
	}
}
void num_to_bin(int n) {
	if (n == 0) {return; }
	num_to_bin(n / 2);
	cout << n % 2;
}
bool str_palli(string s, int start, int end) {
	if (start >= end) {
		return true;
	}
	return (s[start] == s[end]) && str_palli(s, start + 1, end - 1);
}
//=============================================Sample Codes=============================================

void print_per(string s, int i = 0)
{
	if (i == s.length() - 1) {
		cout << s << "\n";
	}
	for (int j = i; j < s.length(); j++)
	{
		swap(s[i], s[j]);
		print_per(s, i + 1);
		swap(s[i], s[j]);
	}
}

void subset(string s, string curr = "", int index = 0)
{
	if (index == s.length())
	{
		cout << curr << " ";
		return;
	}
	subset(s, curr, index + 1);
	subset(s, curr + s[index], index + 1);
}

//=============================================MAIN CODE=============================================

int celebrity(vector<vector<int> >& M, int n)
{
	stack<int>s;
	for (int i = 0; i < n; i++)
	{
		s.push(i);
	}
	while (s.size() >= 2)
	{
		int a = s.top();
		s.pop();
		int b = s.top();
		s.pop();
		if (M[a][b] == 0)
			s.push(a);
		else
			s.push(b);
	}
	int ans = s.top();
	for (int i = 0; i < n; i++)
	{
		if (i != ans)
		{
			if (M[i][ans] == 0 || M[ans][i] == 1)
				return -1;
		}
	}
	return ans;
}

void chalochale() {
	int n;
	cin >> n;
	vector<vector<int> > M( n , vector<int> (n, 0));
	for (int i = 0; i < n; i++)
	{
		for (int j = 0; j < n; j++)
		{
			cin >> M[i][j];
		}
	}
	cout << celebrity(M, n) << endl;
}

int32_t main()
{
	start_func();
	//kitnalega
	{
		chalochale();
		//newl
	}
	return 0;
}

8. Implementation of min stack 

#include<bits/stdc++.h>

//#include <ext/pb_ds/assoc_container.hpp>
//#include <ext/pb_ds/tree_policy.hpp>
//using namespace __gnu_pbds;

using namespace std;

//=============================================CONSTANTS=============================================

const long long SZ = 1e5 + 7;
const long long inf = 1e18;
const long long mod = 1e9 + 7;
const long long MOD = 998244353;
const long long PI = 3.1415926535897932384;

//=============================================MACROS=============================================

#define FastIO 					ios_base::sync_with_stdio(0); cin.tie(0); cout.tie(0)
#define kitnalega           	long long ___tc=1; cin >> ___tc; while (___tc--	)

#define rep(i,x,y)				for(int i=x;i<y;i++)
#define rep_Eq(i,x,y)			for(int i=x;i<=y;i++)
#define rep_Rev(i,x,y)			for(int i=x-1;i>=y;i--)
#define ll						long long
#define lli						long long int

#define ci(X)               	ll X; 			cin >> X
#define cii(X, Y)           	ll X, Y; 		cin >> X >> Y
#define ciii(X, Y, Z)       	ll X, Y, Z;		cin >> X >> Y >> Z
#define ciiii(A,X,Y,Z)			ll A,X,Y,Z;		cin >> A >> X >> Y >> Z
#define cs(s)					string s; 		cin>>s;



#define pb 						push_back
#define pf 						push_front
#define eb 						emplace_back
#define endl					"\n"
#define	newl					cout<<endl;
#define sep						cout<<"-----------------"<<endl;

#define mp 						make_pair
#define pq 						priority_queue

#define ff 						first
#define ss 						second

#define Max(a,b)            	((a > b) ? a : b)
#define Min(a,b)            	((a < b) ? a : b)

#define lb 						lower_bound
#define ub 						upper_bound
#define mx 						*max_element
#define mn 						*min_element



typedef vector<int> 			vi;
typedef vector<vi> 				vvi;
typedef vector<ll> 				vll;
typedef pair<int, int>			pii;
typedef pair<ll, ll>			pll;
typedef vector<pii>				vpii;
typedef vector<pll>				vpll;
typedef pair<lli, lli>			pll;



//=============================================FUNCTIONS=============================================

#define srt(a)			sort(a,a+n);
#define srt2(a)			sort(a.begin(),a.end());
#define rev(a)			reverse(a.begin(),a.end());

//=============================================Templates=============================================

template <typename ForwardIterator, class T>
ForwardIterator search(ForwardIterator start, ForwardIterator end, T key) {
	while (start != end) {
		if (*start == key) {
			return start;
		}
		start++;
	}
	return end;
}

//=============================================Input/Output=============================================

void start_func()
{	FastIO;
#ifndef ONLINE_JUDGE
	freopen("input.txt", "r", stdin);
	freopen("output.txt", "w", stdout);
#endif
}

//=============================================Sieve=============================================

vll prime;
bool isPrime(int n)
{
	if (n == 1) {
		return false;
	}
	if (n == 2 || n == 3) {
		return true;
	}
	if (n % 2 == 0 || n % 3 == 0) {
		return false;
	}
	for (int i = 5; i * i <= n; i = i + 6) {
		if (n % i == 0 || n % (i + 2) == 0) {
			return false;
		}
		return true;
	}
}
void sieve(int n)
{
	vector <bool> isPrime(n + 1, true);
	rep(i, 2, n + 1) {
		if (isPrime[i]) {
			prime.push_back(i);
			for (ll j = i * i; j <= n; j++) {
				isPrime[j] = false;
			}
		}
	}
}
void segSieve(int l, int h)
{
	ll sq = sqrt(h);
	sieve(sq);
	vector<bool>isPrime(h - l + 1, true);
	for (ll p : prime) {
		ll sm = (l / p) * p;
		if (sm < l)
			sm += p;
		for (ll m = sm; m <= h; m += p)
			isPrime[m - l] = false;
	}
	int cc = 0;
	int ans = 0;
	rep(i, l, h + 1) {
		if (isPrime[i - l] == true) {
			cout << i << " ";
			//cc++;
		}
		else {
			//cout << i << " ";
		}
	}
	//cout << cc << endl;
	newl
}
//=============================================GCD=============================================

int gcd(int a, int b) {
	return b == 0 ? 0 : gcd(b, a & b);
}
int gcd2(int a, int b) {
	while (b != 0) {
		a %= b;
		swap(a, b);
	}
	return a;
}
//lcm finder
int lcm(int a, int b) {
	return (a * b) / gcd(a, b);
}
//extended Euclidian Algorithm  	to find linear Diophatine solution 		(ax+by=g) ==> g=gcd(a,b)
int gcdExt(int a, int b, int &x, int &y) {
	if (b == 0) {
		x = 1, y = 0;
		return a;
	}
	int x1, y1;
	int g = gcdExt(b, a % b, x1, y1);
	x = y1, y = x1 - (a / b) * y1;
	return g;
}


int smallestPrime(int n)
{
	cout << 1 << " ";
	vi v(n + 1, 0);
	for (int i = 2; i <= n; i++)
	{
		if (v[i] == 0)
		{
			cout << i << " ";
			for (int j = i * i; j <= n; j = j + i)
			{
				if (v[j] == 0)
				{
					v[j] = i;
				}
			}
		}
		else {
			cout << v[i] << " ";
		}
	}
}
void num_to_bin(int n) {
	if (n == 0) {return; }
	num_to_bin(n / 2);
	cout << n % 2;
}
bool str_palli(string s, int start, int end) {
	if (start >= end) {
		return true;
	}
	return (s[start] == s[end]) && str_palli(s, start + 1, end - 1);
}
//=============================================Sample Codes=============================================

void print_per(string s, int i = 0)
{
	if (i == s.length() - 1) {
		cout << s << "\n";
	}
	for (int j = i; j < s.length(); j++)
	{
		swap(s[i], s[j]);
		print_per(s, i + 1);
		swap(s[i], s[j]);
	}
}

void subset(string s, string curr = "", int index = 0)
{
	if (index == s.length())
	{
		cout << curr << " ";
		return;
	}
	subset(s, curr, index + 1);
	subset(s, curr + s[index], index + 1);
}

//=============================================MAIN CODE=============================================

int longestValidParentheses(string s) {
	int n = s.length(), longest = 0;
	stack<int> st;
	for (int i = 0; i < n; i++) {
		if (s[i] == '(') st.push(i);
		else {
			if (!st.empty()) {
				if (s[st.top()] == '(') st.pop();
				else st.push(i);
			}
			else st.push(i);
		}
	}
	if (st.empty()) longest = n;
	else {
		int a = n, b = 0;
		while (!st.empty()) {
			b = st.top(); st.pop();
			longest = max(longest, a - b - 1);
			a = b;
		}
		longest = max(longest, a);
	}
	return longest;
}

void chalochale() {
	cs(s);
	cout << longestValidParentheses(s);
}

int32_t main()
{
	start_func();
	//kitnalega
	{
		chalochale();
		//newl
	}
	return 0;
}

9. The celebrity problem

#include<bits/stdc++.h>

//#include <ext/pb_ds/assoc_container.hpp>
//#include <ext/pb_ds/tree_policy.hpp>
//using namespace __gnu_pbds;

using namespace std;

//=============================================CONSTANTS=============================================

const long long SZ = 1e5 + 7;
const long long inf = 1e18;
const long long mod = 1e9 + 7;
const long long MOD = 998244353;
const long long PI = 3.1415926535897932384;

//=============================================MACROS=============================================

#define FastIO 					ios_base::sync_with_stdio(0); cin.tie(0); cout.tie(0)
#define kitnalega           	long long ___tc=1; cin >> ___tc; while (___tc--	)

#define rep(i,x,y)				for(int i=x;i<y;i++)
#define rep_Eq(i,x,y)			for(int i=x;i<=y;i++)
#define rep_Rev(i,x,y)			for(int i=x-1;i>=y;i--)
#define ll						long long
#define lli						long long int

#define ci(X)               	ll X; 			cin >> X
#define cii(X, Y)           	ll X, Y; 		cin >> X >> Y
#define ciii(X, Y, Z)       	ll X, Y, Z;		cin >> X >> Y >> Z
#define ciiii(A,X,Y,Z)			ll A,X,Y,Z;		cin >> A >> X >> Y >> Z
#define cs(s)					string s; 		cin>>s;



#define pb 						push_back
#define pf 						push_front
#define eb 						emplace_back
#define endl					"\n"
#define	newl					cout<<endl;
#define sep						cout<<"-----------------"<<endl;

#define mp 						make_pair
#define pq 						priority_queue

#define ff 						first
#define ss 						second

#define Max(a,b)            	((a > b) ? a : b)
#define Min(a,b)            	((a < b) ? a : b)

#define lb 						lower_bound
#define ub 						upper_bound
#define mx 						*max_element
#define mn 						*min_element



typedef vector<int> 			vi;
typedef vector<vi> 				vvi;
typedef vector<ll> 				vll;
typedef pair<int, int>			pii;
typedef pair<ll, ll>			pll;
typedef vector<pii>				vpii;
typedef vector<pll>				vpll;
typedef pair<lli, lli>			pll;



//=============================================FUNCTIONS=============================================

#define srt(a)			sort(a,a+n);
#define srt2(a)			sort(a.begin(),a.end());
#define rev(a)			reverse(a.begin(),a.end());

//=============================================Templates=============================================

template <typename ForwardIterator, class T>
ForwardIterator search(ForwardIterator start, ForwardIterator end, T key) {
	while (start != end) {
		if (*start == key) {
			return start;
		}
		start++;
	}
	return end;
}

//=============================================Input/Output=============================================

void start_func()
{	FastIO;
#ifndef ONLINE_JUDGE
	freopen("input.txt", "r", stdin);
	freopen("output.txt", "w", stdout);
#endif
}

//=============================================Sieve=============================================

vll prime;
bool isPrime(int n)
{
	if (n == 1) {
		return false;
	}
	if (n == 2 || n == 3) {
		return true;
	}
	if (n % 2 == 0 || n % 3 == 0) {
		return false;
	}
	for (int i = 5; i * i <= n; i = i + 6) {
		if (n % i == 0 || n % (i + 2) == 0) {
			return false;
		}
		return true;
	}
}
void sieve(int n)
{
	vector <bool> isPrime(n + 1, true);
	rep(i, 2, n + 1) {
		if (isPrime[i]) {
			prime.push_back(i);
			for (ll j = i * i; j <= n; j++) {
				isPrime[j] = false;
			}
		}
	}
}
void segSieve(int l, int h)
{
	ll sq = sqrt(h);
	sieve(sq);
	vector<bool>isPrime(h - l + 1, true);
	for (ll p : prime) {
		ll sm = (l / p) * p;
		if (sm < l)
			sm += p;
		for (ll m = sm; m <= h; m += p)
			isPrime[m - l] = false;
	}
	int cc = 0;
	int ans = 0;
	rep(i, l, h + 1) {
		if (isPrime[i - l] == true) {
			cout << i << " ";
			//cc++;
		}
		else {
			//cout << i << " ";
		}
	}
	//cout << cc << endl;
	newl
}
//=============================================GCD=============================================

int gcd(int a, int b) {
	return b == 0 ? 0 : gcd(b, a & b);
}
int gcd2(int a, int b) {
	while (b != 0) {
		a %= b;
		swap(a, b);
	}
	return a;
}
//lcm finder
int lcm(int a, int b) {
	return (a * b) / gcd(a, b);
}
//extended Euclidian Algorithm  	to find linear Diophatine solution 		(ax+by=g) ==> g=gcd(a,b)
int gcdExt(int a, int b, int &x, int &y) {
	if (b == 0) {
		x = 1, y = 0;
		return a;
	}
	int x1, y1;
	int g = gcdExt(b, a % b, x1, y1);
	x = y1, y = x1 - (a / b) * y1;
	return g;
}


int smallestPrime(int n)
{
	cout << 1 << " ";
	vi v(n + 1, 0);
	for (int i = 2; i <= n; i++)
	{
		if (v[i] == 0)
		{
			cout << i << " ";
			for (int j = i * i; j <= n; j = j + i)
			{
				if (v[j] == 0)
				{
					v[j] = i;
				}
			}
		}
		else {
			cout << v[i] << " ";
		}
	}
}
void num_to_bin(int n) {
	if (n == 0) {return; }
	num_to_bin(n / 2);
	cout << n % 2;
}
bool str_palli(string s, int start, int end) {
	if (start >= end) {
		return true;
	}
	return (s[start] == s[end]) && str_palli(s, start + 1, end - 1);
}
//=============================================Sample Codes=============================================

void print_per(string s, int i = 0)
{
	if (i == s.length() - 1) {
		cout << s << "\n";
	}
	for (int j = i; j < s.length(); j++)
	{
		swap(s[i], s[j]);
		print_per(s, i + 1);
		swap(s[i], s[j]);
	}
}

void subset(string s, string curr = "", int index = 0)
{
	if (index == s.length())
	{
		cout << curr << " ";
		return;
	}
	subset(s, curr, index + 1);
	subset(s, curr + s[index], index + 1);
}

//=============================================MAIN CODE=============================================

string minRemoveToMakeValid(string s)
{
	vector<char> stack;
	int left = 0, right = 0;
	for (int i = 0; i < s.size(); i++)
	{
		if (s[i] == '(')
		{
			left++;
		}
		if (s[i] == ')')
		{
			if (right >= left)
			{
				cout << right << endl;
				continue;
			}
			right++;
		}
		stack.push_back(s[i]);
	}
	string res;
	while (left > right)
	{
		int flag = stack.size() - 1;
		while (stack[flag] != '(')
		{
			flag--;
		}
		stack.erase(stack.begin() + flag);
		left--;
	}
	for (int i = 0; i < stack.size(); i++)
	{
		res += stack[i];
	}
	return res;
}
void chalochale() {
	cs(s);
	cout << minRemoveToMakeValid(s);
}

int32_t main()
{
	start_func();
	//kitnalega
	{
		chalochale();
		//newl
	}
	return 0;
}

10. Longest valid parentesis

#include<bits/stdc++.h>

//#include <ext/pb_ds/assoc_container.hpp>
//#include <ext/pb_ds/tree_policy.hpp>
//using namespace __gnu_pbds;

using namespace std;

//=============================================CONSTANTS=============================================

const long long SZ = 1e5 + 7;
const long long inf = 1e18;
const long long mod = 1e9 + 7;
const long long MOD = 998244353;
const long long PI = 3.1415926535897932384;

//=============================================MACROS=============================================

#define FastIO 					ios_base::sync_with_stdio(0); cin.tie(0); cout.tie(0)
#define kitnalega           	long long ___tc=1; cin >> ___tc; while (___tc--	)

#define rep(i,x,y)				for(int i=x;i<y;i++)
#define rep_Eq(i,x,y)			for(int i=x;i<=y;i++)
#define rep_Rev(i,x,y)			for(int i=x-1;i>=y;i--)
#define ll						long long
#define lli						long long int

#define ci(X)               	ll X; 			cin >> X
#define cii(X, Y)           	ll X, Y; 		cin >> X >> Y
#define ciii(X, Y, Z)       	ll X, Y, Z;		cin >> X >> Y >> Z
#define ciiii(A,X,Y,Z)			ll A,X,Y,Z;		cin >> A >> X >> Y >> Z
#define cs(s)					string s; 		cin>>s;



#define pb 						push_back
#define pf 						push_front
#define eb 						emplace_back
#define endl					"\n"
#define	newl					cout<<endl;
#define sep						cout<<"-----------------"<<endl;

#define mp 						make_pair
#define pq 						priority_queue

#define ff 						first
#define ss 						second

#define Max(a,b)            	((a > b) ? a : b)
#define Min(a,b)            	((a < b) ? a : b)

#define lb 						lower_bound
#define ub 						upper_bound
#define mx 						*max_element
#define mn 						*min_element



typedef vector<int> 			vi;
typedef vector<vi> 				vvi;
typedef vector<ll> 				vll;
typedef pair<int, int>			pii;
typedef pair<ll, ll>			pll;
typedef vector<pii>				vpii;
typedef vector<pll>				vpll;
typedef pair<lli, lli>			pll;



//=============================================FUNCTIONS=============================================

#define srt(a)			sort(a,a+n);
#define srt2(a)			sort(a.begin(),a.end());
#define rev(a)			reverse(a.begin(),a.end());

//=============================================Templates=============================================

template <typename ForwardIterator, class T>
ForwardIterator search(ForwardIterator start, ForwardIterator end, T key) {
	while (start != end) {
		if (*start == key) {
			return start;
		}
		start++;
	}
	return end;
}

//=============================================Input/Output=============================================

void start_func()
{	FastIO;
#ifndef ONLINE_JUDGE
	freopen("input.txt", "r", stdin);
	freopen("output.txt", "w", stdout);
#endif
}

//=============================================Sieve=============================================

vll prime;
bool isPrime(int n)
{
	if (n == 1) {
		return false;
	}
	if (n == 2 || n == 3) {
		return true;
	}
	if (n % 2 == 0 || n % 3 == 0) {
		return false;
	}
	for (int i = 5; i * i <= n; i = i + 6) {
		if (n % i == 0 || n % (i + 2) == 0) {
			return false;
		}
		return true;
	}
}
void sieve(int n)
{
	vector <bool> isPrime(n + 1, true);
	rep(i, 2, n + 1) {
		if (isPrime[i]) {
			prime.push_back(i);
			for (ll j = i * i; j <= n; j++) {
				isPrime[j] = false;
			}
		}
	}
}
void segSieve(int l, int h)
{
	ll sq = sqrt(h);
	sieve(sq);
	vector<bool>isPrime(h - l + 1, true);
	for (ll p : prime) {
		ll sm = (l / p) * p;
		if (sm < l)
			sm += p;
		for (ll m = sm; m <= h; m += p)
			isPrime[m - l] = false;
	}
	int cc = 0;
	int ans = 0;
	rep(i, l, h + 1) {
		if (isPrime[i - l] == true) {
			cout << i << " ";
			//cc++;
		}
		else {
			//cout << i << " ";
		}
	}
	//cout << cc << endl;
	newl
}
//=============================================GCD=============================================

int gcd(int a, int b) {
	return b == 0 ? 0 : gcd(b, a & b);
}
int gcd2(int a, int b) {
	while (b != 0) {
		a %= b;
		swap(a, b);
	}
	return a;
}
//lcm finder
int lcm(int a, int b) {
	return (a * b) / gcd(a, b);
}
//extended Euclidian Algorithm  	to find linear Diophatine solution 		(ax+by=g) ==> g=gcd(a,b)
int gcdExt(int a, int b, int &x, int &y) {
	if (b == 0) {
		x = 1, y = 0;
		return a;
	}
	int x1, y1;
	int g = gcdExt(b, a % b, x1, y1);
	x = y1, y = x1 - (a / b) * y1;
	return g;
}


int smallestPrime(int n)
{
	cout << 1 << " ";
	vi v(n + 1, 0);
	for (int i = 2; i <= n; i++)
	{
		if (v[i] == 0)
		{
			cout << i << " ";
			for (int j = i * i; j <= n; j = j + i)
			{
				if (v[j] == 0)
				{
					v[j] = i;
				}
			}
		}
		else {
			cout << v[i] << " ";
		}
	}
}
void num_to_bin(int n) {
	if (n == 0) {return; }
	num_to_bin(n / 2);
	cout << n % 2;
}
bool str_palli(string s, int start, int end) {
	if (start >= end) {
		return true;
	}
	return (s[start] == s[end]) && str_palli(s, start + 1, end - 1);
}
//=============================================Sample Codes=============================================

void print_per(string s, int i = 0)
{
	if (i == s.length() - 1) {
		cout << s << "\n";
	}
	for (int j = i; j < s.length(); j++)
	{
		swap(s[i], s[j]);
		print_per(s, i + 1);
		swap(s[i], s[j]);
	}
}

void subset(string s, string curr = "", int index = 0)
{
	if (index == s.length())
	{
		cout << curr << " ";
		return;
	}
	subset(s, curr, index + 1);
	subset(s, curr + s[index], index + 1);
}

//=============================================MAIN CODE=============================================


class Stack {
	queue<int> q1, q2;
	int curr_size;

public:
	Stack()
	{
		curr_size = 0;
	}

	void pop()
	{
		if (q1.empty())
			return;
		while (q1.size() != 1) {
			q2.push(q1.front());
			q1.pop();
		}
		q1.pop();
		curr_size--;
		queue<int> q = q1;
		q1 = q2;
		q2 = q;
	}

	void push(int x)
	{
		q1.push(x);
		curr_size++;
	}

	int top()
	{
		if (q1.empty())
			return -1;

		while (q1.size() != 1) {
			q2.push(q1.front());
			q1.pop();
		}

		int temp = q1.front();
		q1.pop();
		q2.push(temp);
		queue<int> q = q1;
		q1 = q2;
		q2 = q;
		return temp;
	}

	int size()
	{
		return curr_size;
	}
};

void chalochale() {
	Stack s;
	s.push(1);
	s.push(2);
	s.push(3);
	s.push(4);
	cout << "current size: " << s.size() << endl;
	cout << s.top() << endl;
	s.pop();
	cout << s.top() << endl;
	s.pop();
	cout << s.top() << endl;
	cout << "current size: " << s.size() << endl;
}

int32_t main()
{
	start_func();
	//kitnalega
	{
		chalochale();
		//newl
	}
	return 0;
}


11. minimum number of deletion required to balance the parantesis


#include<bits/stdc++.h>

//#include <ext/pb_ds/assoc_container.hpp>
//#include <ext/pb_ds/tree_policy.hpp>
//using namespace __gnu_pbds;

using namespace std;

//=============================================CONSTANTS=============================================

const long long SZ = 1e5 + 7;
const long long inf = 1e18;
const long long mod = 1e9 + 7;
const long long MOD = 998244353;
const long long PI = 3.1415926535897932384;

//=============================================MACROS=============================================

#define FastIO 					ios_base::sync_with_stdio(0); cin.tie(0); cout.tie(0)
#define kitnalega           	long long ___tc=1; cin >> ___tc; while (___tc--	)

#define rep(i,x,y)				for(int i=x;i<y;i++)
#define rep_Eq(i,x,y)			for(int i=x;i<=y;i++)
#define rep_Rev(i,x,y)			for(int i=x-1;i>=y;i--)
#define ll						long long
#define lli						long long int

#define ci(X)               	ll X; 			cin >> X
#define cii(X, Y)           	ll X, Y; 		cin >> X >> Y
#define ciii(X, Y, Z)       	ll X, Y, Z;		cin >> X >> Y >> Z
#define ciiii(A,X,Y,Z)			ll A,X,Y,Z;		cin >> A >> X >> Y >> Z
#define cs(s)					string s; 		cin>>s;



#define pb 						push_back
#define pf 						push_front
#define eb 						emplace_back
#define endl					"\n"
#define	newl					cout<<endl;
#define sep						cout<<"-----------------"<<endl;

#define mp 						make_pair
#define pq 						priority_queue

#define ff 						first
#define ss 						second

#define Max(a,b)            	((a > b) ? a : b)
#define Min(a,b)            	((a < b) ? a : b)

#define lb 						lower_bound
#define ub 						upper_bound
#define mx 						*max_element
#define mn 						*min_element



typedef vector<int> 			vi;
typedef vector<vi> 				vvi;
typedef vector<ll> 				vll;
typedef pair<int, int>			pii;
typedef pair<ll, ll>			pll;
typedef vector<pii>				vpii;
typedef vector<pll>				vpll;
typedef pair<lli, lli>			pll;



//=============================================FUNCTIONS=============================================

#define srt(a)			sort(a,a+n);
#define srt2(a)			sort(a.begin(),a.end());
#define rev(a)			reverse(a.begin(),a.end());

//=============================================Templates=============================================

template <typename ForwardIterator, class T>
ForwardIterator search(ForwardIterator start, ForwardIterator end, T key) {
	while (start != end) {
		if (*start == key) {
			return start;
		}
		start++;
	}
	return end;
}

//=============================================Input/Output=============================================

void start_func()
{	FastIO;
#ifndef ONLINE_JUDGE
	freopen("input.txt", "r", stdin);
	freopen("output.txt", "w", stdout);
#endif
}

//=============================================Sieve=============================================

vll prime;
bool isPrime(int n)
{
	if (n == 1) {
		return false;
	}
	if (n == 2 || n == 3) {
		return true;
	}
	if (n % 2 == 0 || n % 3 == 0) {
		return false;
	}
	for (int i = 5; i * i <= n; i = i + 6) {
		if (n % i == 0 || n % (i + 2) == 0) {
			return false;
		}
		return true;
	}
}
void sieve(int n)
{
	vector <bool> isPrime(n + 1, true);
	rep(i, 2, n + 1) {
		if (isPrime[i]) {
			prime.push_back(i);
			for (ll j = i * i; j <= n; j++) {
				isPrime[j] = false;
			}
		}
	}
}
void segSieve(int l, int h)
{
	ll sq = sqrt(h);
	sieve(sq);
	vector<bool>isPrime(h - l + 1, true);
	for (ll p : prime) {
		ll sm = (l / p) * p;
		if (sm < l)
			sm += p;
		for (ll m = sm; m <= h; m += p)
			isPrime[m - l] = false;
	}
	int cc = 0;
	int ans = 0;
	rep(i, l, h + 1) {
		if (isPrime[i - l] == true) {
			cout << i << " ";
			//cc++;
		}
		else {
			//cout << i << " ";
		}
	}
	//cout << cc << endl;
	newl
}
//=============================================GCD=============================================

int gcd(int a, int b) {
	return b == 0 ? 0 : gcd(b, a & b);
}
int gcd2(int a, int b) {
	while (b != 0) {
		a %= b;
		swap(a, b);
	}
	return a;
}
//lcm finder
int lcm(int a, int b) {
	return (a * b) / gcd(a, b);
}
//extended Euclidian Algorithm  	to find linear Diophatine solution 		(ax+by=g) ==> g=gcd(a,b)
int gcdExt(int a, int b, int &x, int &y) {
	if (b == 0) {
		x = 1, y = 0;
		return a;
	}
	int x1, y1;
	int g = gcdExt(b, a % b, x1, y1);
	x = y1, y = x1 - (a / b) * y1;
	return g;
}


int smallestPrime(int n)
{
	cout << 1 << " ";
	vi v(n + 1, 0);
	for (int i = 2; i <= n; i++)
	{
		if (v[i] == 0)
		{
			cout << i << " ";
			for (int j = i * i; j <= n; j = j + i)
			{
				if (v[j] == 0)
				{
					v[j] = i;
				}
			}
		}
		else {
			cout << v[i] << " ";
		}
	}
}
void num_to_bin(int n) {
	if (n == 0) {return; }
	num_to_bin(n / 2);
	cout << n % 2;
}
bool str_palli(string s, int start, int end) {
	if (start >= end) {
		return true;
	}
	return (s[start] == s[end]) && str_palli(s, start + 1, end - 1);
}
//=============================================Sample Codes=============================================

void print_per(string s, int i = 0)
{
	if (i == s.length() - 1) {
		cout << s << "\n";
	}
	for (int j = i; j < s.length(); j++)
	{
		swap(s[i], s[j]);
		print_per(s, i + 1);
		swap(s[i], s[j]);
	}
}

void subset(string s, string curr = "", int index = 0)
{
	if (index == s.length())
	{
		cout << curr << " ";
		return;
	}
	subset(s, curr, index + 1);
	subset(s, curr + s[index], index + 1);
}

//=============================================MAIN CODE=============================================



struct Queue {
	stack<int> s;
	void enQueue(int x)
	{
		s.push(x);
	}
	int deQueue()
	{
		if (s.empty()) {
			cout << "Q is empty";
			exit(0);
		}
		int x = s.top();
		s.pop();
		if (s.empty())
			return x;
		int item = deQueue();
		s.push(x);
		return item;
	}
};


void chalochale() {
	Queue q;
	q.enQueue(1);
	q.enQueue(2);
	q.enQueue(3);

	cout << q.deQueue() << '\n';
	cout << q.deQueue() << '\n';
	cout << q.deQueue() << '\n';
}

int32_t main()
{
	start_func();
	//kitnalega
	{
		chalochale();
		//newl
	}
	return 0;
}


12. Stack using queue

#include<bits/stdc++.h>

//#include <ext/pb_ds/assoc_container.hpp>
//#include <ext/pb_ds/tree_policy.hpp>
//using namespace __gnu_pbds;

using namespace std;

//=============================================CONSTANTS=============================================

const long long SZ = 1e5 + 7;
const long long inf = 1e18;
const long long mod = 1e9 + 7;
const long long MOD = 998244353;
const long long PI = 3.1415926535897932384;

//=============================================MACROS=============================================

#define FastIO 					ios_base::sync_with_stdio(0); cin.tie(0); cout.tie(0)
#define kitnalega           	long long ___tc=1; cin >> ___tc; while (___tc--	)

#define rep(i,x,y)				for(int i=x;i<y;i++)
#define rep_Eq(i,x,y)			for(int i=x;i<=y;i++)
#define rep_Rev(i,x,y)			for(int i=x-1;i>=y;i--)
#define ll						long long
#define lli						long long int

#define ci(X)               	ll X; 			cin >> X
#define cii(X, Y)           	ll X, Y; 		cin >> X >> Y
#define ciii(X, Y, Z)       	ll X, Y, Z;		cin >> X >> Y >> Z
#define ciiii(A,X,Y,Z)			ll A,X,Y,Z;		cin >> A >> X >> Y >> Z
#define cs(s)					string s; 		cin>>s;



#define pb 						push_back
#define pf 						push_front
#define eb 						emplace_back
#define endl					"\n"
#define	newl					cout<<endl;
#define sep						cout<<"-----------------"<<endl;

#define mp 						make_pair
#define pq 						priority_queue

#define ff 						first
#define ss 						second

#define Max(a,b)            	((a > b) ? a : b)
#define Min(a,b)            	((a < b) ? a : b)

#define lb 						lower_bound
#define ub 						upper_bound
#define mx 						*max_element
#define mn 						*min_element



typedef vector<int> 			vi;
typedef vector<vi> 				vvi;
typedef vector<ll> 				vll;
typedef pair<int, int>			pii;
typedef pair<ll, ll>			pll;
typedef vector<pii>				vpii;
typedef vector<pll>				vpll;
typedef pair<lli, lli>			pll;



//=============================================FUNCTIONS=============================================

#define srt(a)			sort(a,a+n);
#define srt2(a)			sort(a.begin(),a.end());
#define rev(a)			reverse(a.begin(),a.end());

//=============================================Templates=============================================

template <typename ForwardIterator, class T>
ForwardIterator search(ForwardIterator start, ForwardIterator end, T key) {
	while (start != end) {
		if (*start == key) {
			return start;
		}
		start++;
	}
	return end;
}

//=============================================Input/Output=============================================

void start_func()
{	FastIO;
#ifndef ONLINE_JUDGE
	freopen("input.txt", "r", stdin);
	freopen("output.txt", "w", stdout);
#endif
}

//=============================================Sieve=============================================

vll prime;
bool isPrime(int n)
{
	if (n == 1) {
		return false;
	}
	if (n == 2 || n == 3) {
		return true;
	}
	if (n % 2 == 0 || n % 3 == 0) {
		return false;
	}
	for (int i = 5; i * i <= n; i = i + 6) {
		if (n % i == 0 || n % (i + 2) == 0) {
			return false;
		}
		return true;
	}
}
void sieve(int n)
{
	vector <bool> isPrime(n + 1, true);
	rep(i, 2, n + 1) {
		if (isPrime[i]) {
			prime.push_back(i);
			for (ll j = i * i; j <= n; j++) {
				isPrime[j] = false;
			}
		}
	}
}
void segSieve(int l, int h)
{
	ll sq = sqrt(h);
	sieve(sq);
	vector<bool>isPrime(h - l + 1, true);
	for (ll p : prime) {
		ll sm = (l / p) * p;
		if (sm < l)
			sm += p;
		for (ll m = sm; m <= h; m += p)
			isPrime[m - l] = false;
	}
	int cc = 0;
	int ans = 0;
	rep(i, l, h + 1) {
		if (isPrime[i - l] == true) {
			cout << i << " ";
			//cc++;
		}
		else {
			//cout << i << " ";
		}
	}
	//cout << cc << endl;
	newl
}
//=============================================GCD=============================================

int gcd(int a, int b) {
	return b == 0 ? 0 : gcd(b, a & b);
}
int gcd2(int a, int b) {
	while (b != 0) {
		a %= b;
		swap(a, b);
	}
	return a;
}
//lcm finder
int lcm(int a, int b) {
	return (a * b) / gcd(a, b);
}
//extended Euclidian Algorithm  	to find linear Diophatine solution 		(ax+by=g) ==> g=gcd(a,b)
int gcdExt(int a, int b, int &x, int &y) {
	if (b == 0) {
		x = 1, y = 0;
		return a;
	}
	int x1, y1;
	int g = gcdExt(b, a % b, x1, y1);
	x = y1, y = x1 - (a / b) * y1;
	return g;
}


int smallestPrime(int n)
{
	cout << 1 << " ";
	vi v(n + 1, 0);
	for (int i = 2; i <= n; i++)
	{
		if (v[i] == 0)
		{
			cout << i << " ";
			for (int j = i * i; j <= n; j = j + i)
			{
				if (v[j] == 0)
				{
					v[j] = i;
				}
			}
		}
		else {
			cout << v[i] << " ";
		}
	}
}
void num_to_bin(int n) {
	if (n == 0) {return; }
	num_to_bin(n / 2);
	cout << n % 2;
}
bool str_palli(string s, int start, int end) {
	if (start >= end) {
		return true;
	}
	return (s[start] == s[end]) && str_palli(s, start + 1, end - 1);
}
//=============================================Sample Codes=============================================

void print_per(string s, int i = 0)
{
	if (i == s.length() - 1) {
		cout << s << "\n";
	}
	for (int j = i; j < s.length(); j++)
	{
		swap(s[i], s[j]);
		print_per(s, i + 1);
		swap(s[i], s[j]);
	}
}

void subset(string s, string curr = "", int index = 0)
{
	if (index == s.length())
	{
		cout << curr << " ";
		return;
	}
	subset(s, curr, index + 1);
	subset(s, curr + s[index], index + 1);
}

//=============================================MAIN CODE=============================================


class twoStacks {
private:
	int* arr;
	int size;
	int top1, top2;

public:
	twoStacks(int n) {
		size = n;
		arr = new int[n];
		top1 = -1;
		top2 = size;
	}

	void push1(int x) {
		if (top1 < top2 - 1) {
			top1++;
			arr[top1] = x;
		}
		else {
			cout << "Stack Overflow";
			exit(1);
		}
	}
	void push2(int x)
	{
		if (top1 < top2 - 1) {
			top2--;
			arr[top2] = x;
		}
		else {
			cout << "Stack Overflow";
			exit(1);
		}
	}
	int pop1()
	{
		if (top1 >= 0) {
			int x = arr[top1];
			top1--;
			return x;
		}
		else {
			cout << "Stack UnderFlow";
			exit(1);
		}
	}
	int pop2()
	{
		if (top2 < size) {
			int x = arr[top2];
			top2++;
			return x;
		}
		else {
			cout << "Stack UnderFlow";
			exit(1);
		}
	}
};

void chalochale() {
	twoStacks ts(5);
	ts.push1(5);
	ts.push2(10);
	ts.push2(15);
	ts.push1(11);
	ts.push2(7);
	cout << "Popped element from stack1 is "
	     << ts.pop1();
	ts.push2(40);
	cout << "\nPopped element from stack2 is "
	     << ts.pop2();
}

int32_t main()
{
	start_func();
	//kitnalega
	{
		chalochale();
		//newl
	}
	return 0;
}
