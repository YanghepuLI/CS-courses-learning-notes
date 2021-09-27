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
mylist1.splice(itr, mylist2, itr_a, itr_b); // cut mylist2 from itr_a to itr_b to insert to mylist1 at itr, O(1), no other containers can do this
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
