## Preview of STL
```
//STL means Standard Template library
using namespace std;
vector<int> vec; // vec.size() == 0;
vec.push_back(4); // set 4 to the end of vec
vec.push_back(1); // set 1 to the end of vec
vec.push_back(8);
vec.begin(); // 4
vec.end(); // nothing  half-open [begin, end)

vector<int>::iterator itr1 = vec.begin(); // iterator in template is like a pointer
vector<int>::iterator itr2 = vec.end();
for (vector<int>::iterator itr = itr1; itr != itr2; ++itr) {
  cout << *itr << " ";
};  // vec : {4, 1, 8}
sort(itr1, itr2); // vec : {1, 4, 8}
```
## Containers
+ Sequennce containers(array and linked list)
vector, deque, list, forward list, array
+ Associative Containers(binary tree)
set, multiset
map, multimap
+ Unordered Containers(hash table)
unordered set/multiset
unordered map/multimap

headers
```
#include <vector>
#include <deque>
#include <list>
#include <set> // set and multiset
#include <map> // map and multimap
#include <unordered_set> // unordered set/multiset
#include <unordered_map> // unordered map/multimap
#include <iterator>
#include <algorithm>
#include <numeric> // some numeric algorithms
#include <functional>
```
## vector
```
cout << vec.size(); // 3
vector<int> vec2(vec); // copy constructor, ve2 : {4, 1, 8}
vec.clear();  // remove all items in vec; vec.size() == 0
vec2.swap(vec); // swap
```
Properties of Vector:
+ fast insert/remove at the end O(1)
+ slow insert/remove at the beginning or in the middle: O(n)
+ slow search O(n)

## deque
```
deque<int> deq = {4, 6, 7};
deq.push_front(2); // deq {2, 4, 6, 7}
deq.push_back(3); // {2, 4, 6, 7, 3}

//deque has similar interface with vector
cout << deq[2]; // 4
```
Properties of Deque:
+ fast insert/remove at the begining and the end
+ slow insert/remove in the middle: O(n)
+ slow search

## List
double-way linked list, each node has two pointers pointed at each direction
```
list<int> mylist = {5, 2, 9};
mylist.push_back(6); // {5, 2, 9, 6}
mylist.push_front(4); // {4, 5, 2, 9, 6}
list<int>::iterator itr = find(mylist.begin(), mylist.end(), 2); // itr -> 2
mylist.insert(itr, 8); // {4, 5, 8, 2, 9, 6}   very fast
itr++; // itr -> 9
mylist.erase(itr); //mylist: {4, 5, 8, 2, 6} O(1)

```

Properties:
+ fast insert/remove at any place O(1)
+ slow search O(n)
+ no random access, no [] operator

```
mylist1.splice(itr, mylist2, itr_a, itr_b); 
// cut mylist2 from itr_a to itr_b to insert to mylist1 
// at itr, O(1), no other containers can do this
```

## forward list
one direction list

## array
```
int a[3] = {3, 4, 5};
array<int, 3> a = {3, 4, 5}; // fixed size
a.begin();
a.end();
a.size();
a.sort();
array<int, 4> b = {3, 4, 5}; // take care, b and a are different type
```
# Associative Containers
Always sorted, default criteria is <
No push_back(), push_front()

## set
No duplicates
```
set<int> myset;
myset.insert(3); // myset : {3}
myset.insert(1); // {1, 3}
myset.insert(7); // {1, 3, 7} O(log(n))

set<int>::iterator it;
it = myset.find(7);  // O(lgn), it points to 7.   sequence containers search is O(n)
                     // Sequence containers don't have find(n) member function
pair<set<int>::iterator, bool> ret;
ret = myset.insert(3); // no new element inserted
if (ret.second == false)
  it = ret.first; // "it" now points to element 3

myset.insert(it, 9); //myset: {1, 3, 7, 9}  O(lgn) -> O(1),  it works as a hint to guide the insertion
myset.erase(it); // myset: {1, 7, 9}

myset.erase(7); // myset : {1, 7},  7 is the value
                // none of the sequence conatiners have this
```

## multiset
allows duplicated items
set/multiset : value of the elements cannot be modifies,  read-only

Properties:
+ fast search O(lgn)
+ traversing is slow
+ no random access

## map
No duplicated key
```
map<char, int> mymap;
mymap.insert (pair<char, int>('a', 100));
mymap.insert (make_pair('z', 200));

map<char,int>::iterator it = mymap.begin();
mymap.insert(it, pair<char,int>('b', 300)); // "it" is a hint

it = mymap.find('z'); //O(lgn)

//showing contents:
for (it = mymap.begin(); it != mymap.end(); it++)
     cout << (*it).first << "-->" << (*it).second << endl;
```

## multimap
allows duplicated keys
map/multimap:  keys cannot be modifies

```
(*it).first = 'd'; // Error
```

# Unordered Associative Containers
Hash table
Properties:
+ fastest search/insert at any place O(1)   Associative container takes O(lgn)   sequence container takes O(n)
+ unodered set/multiset: element value cannot be changed
+ unodered map/multimap: keys cannot be changed

## unordered set
```
unordered_set<string> myset = {"red", "green", "blue"};
unordered_set<string>::const_iterator itr = myset.find("green"); // O(1)
if (itr != myset.end())  //Important check
   cout << *it << endl;
myset.insert("yellow");  // O(1)

vector<string> vec = {"purple", "pink"};
myset.insert(vec.begin(), vec.end());  // insert every element in vec into myset

// Hash table specific APIs
cout << "load_factor = " << myset.load_factor() << endl; // total number of elements and total number of buckets
string x = "red";
cout << x << " is in the bucket #" << myset.bucket(x) << endl;
cout << "The number of bucket is #" << myset.bucket_count() << endl;
```

## unordered map
```
unordered_map<char, string> day = {{'S', "Sunday"}, {'M', "Monday"}};

cout << day['S'] << endl; // No range check
cout << day.at('S') << endl; // has range check

vector<int> vec = {1, 2, 3};
vec[5] = 5; // Error

day['W'] = "Wednesday"; // Inserting {'W', "Wednesday"}
day.insert(make_pair('F', "Friday")); // allowed

day.insert(make_pair('M', "MONDAY"));  // Fail to modify, it is a unordered_map
day['M'] = "MONDAY" // succeed to modify

void foo (const unordered_map<char, string> &m) {
    // cout << m['S'] << endl;   //failed,  << operator provides a write operation to the container
    auto itr = m.find('S');
    if (itr != m.end())   // important check
        cout << *itr << endl;
}
```

Notes about Associative Array:
+ Search time: unordered_map O(1),  map O(lgn)
+ Unordered_map may degrade to O(n) by hash collision
+ can't use multimap or unordered_multimap, they don't have [] operator


