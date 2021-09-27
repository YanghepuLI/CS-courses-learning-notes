## Preview of STL
```
//STL means Standard Template library
using namespace std;
vector<int> vec;
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
+ 
