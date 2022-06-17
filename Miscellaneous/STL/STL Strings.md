
# Standard STL functions used on strings

C++ has in its definition a way to represent a sequence of characters as an object of the class. This class is called std:: string. 
String class stores the characters as a sequence of bytes with the functionality of allowing access to the single-byte character.

### Perks
  * Memory allocation is automatic and dynamic
  * Strings are represented as objects
  * These are a little slwower than the char array implementation of strgings

#### Some primitves
  * ```string str; getline(cin,str);```
  * ```str.push_back('a')```
  * ```str.pop_back()```

#### Member functions
  
```
#include <iostream>
#include <iterator>
#include <string>
 
int main()
{
  std::string s;
  // assign(size_type count, CharT ch)
  s.assign(4, '=');
  std::cout << s << '\n'; // "===="
 
  std::string const c("Exemplary");
  // assign(basic_string const& str)
  s.assign(c);
  std::cout << c << " == " << s <<'\n'; // "Exemplary == Exemplary"
 
  // assign(basic_string const& str, size_type pos, size_type count)
  s.assign(c, 0, c.length()-1);
  std::cout << s << '\n'; // "Exemplar";
 
  // assign(basic_string&& str)
  s.assign(std::string("C++ by ") + "example");
  std::cout << s << '\n'; // "C++ by example"
 
  // assign(charT const* s, size_type count)
  s.assign("C-style string", 7);
  std::cout << s << '\n'; // "C-style"
 
  // assign(charT const* s)
  s.assign("C-style\0string");
  std::cout << s << '\n'; // "C-style"
 
  char mutable_c_str[] = "C-style string";
  // assign(InputIt first, InputIt last)
  s.assign(std::begin(mutable_c_str), std::end(mutable_c_str)-1);
  std::cout << s << '\n'; // "C-style string"
 
  // assign(std::initializer_list<charT> ilist)
  s.assign({ 'C', '-', 's', 't', 'y', 'l', 'e' });
  std::cout << s << '\n'; // "C-style"
}
```

#### Capacity functions

* ```str.empty()```
* ```str.size()``` or ```str.length()```

#### Operations
> str.substr()


* ```str.substr(pos,size)``` or ```str.substr(pos)``` - extracts from the position until end

> str.erase()

* ```str.erase(pos)``` or ```str.erase(pos,size)``` 

```
#include <algorithm>
#include <iostream>
#include <iterator>
#include <string>
 
int main()
{
    std::string s = "This Is An Example";
    std::cout << "1) " << s << '\n';
 
    s.erase(7, 3); // erases " An" using overload (1)
    std::cout << "2) " << s << '\n';
 
    s.erase(std::find(s.begin(), s.end(), ' ')); // erases first ' '; overload (2)
    std::cout << "3) " << s << '\n';
 
    s.erase(s.find(' ')); // trims from ' ' to the end of the string; overload (1)
    std::cout << "4) " << s << '\n';
 
    auto it = std::next(s.begin(), s.find('s')); // obtains iterator to the first 's'
    s.erase(it, std::next(it, 2)); // erases "sI"; overload (3)
    std::cout << "5) " << s << '\n';
}
```

> str.find()


```#include <string>
#include <iostream>
using namespace std;
 
void print(std::string::size_type n, std::string const &s)
{
    if (n == string::npos) {
        std::cout << "not found\n";
    } else {
        std::cout << "found: " << s.substr(n) << '\n';
    }
}
 
int main()
{
    std::string::size_type n;
    std::string const s = "This is a string";
 
    // search from beginning of string
    n = s.find("is");
    print(n, s);
 
    // search from position 5
    n = s.find("is", 5);
    print(n, s);
 
    // find a single character
    n = s.find('a');
    print(n, s);
 
    // find a single character
    n = s.find('q');
    print(n, s);
}
```

> str.contains()

```str.constains(the substring)```

> stoi -- stol -- stoll --- string to integer and its types

* ```int temp = stoi("123")```
* ```long temp = stol("123434")```
* ```long long temp = stoll("123434123333333333333312")```

> stof -- stod -- stodl --- string to floating values and its types

* ```float temp = stof(3.14)```
* ```double temp = stof(3.143424323)```
* ```long double temp = stof(3.1423424243423423434)```

> to_string() --- numeric to string

* ```string temp = to_string(123)```

### Constants

> npos

* This is a static constant member of the string class which essentially means that there is no match. Much like when, container iterator points to the end when they don't get a match
* You might use this often with the ```str.find()``` function

```
if (found != string::npos) {
 cout << "first " << s2 << " found at: ";
    }
```

## Some of the basic task you might want to know

### Header file - <boost/algorithm/string.hpp> -- using namespace boost::algorithm

####  You may drop on the ```copy``` from all the function names to do the operation inplace with the same string without returning

 > **To split a string based on some delimiter**
 
 ```
 // C++ program to split
// string into substrings
// which are separated by
// separator using boost::split

// this header file contains boost::split function
#include <bits/stdc++.h>
#include <boost/algorithm/string.hpp>
using namespace std;

int main()
{
	string input("geeks\tfor\tgeeks");
	vector<string> result;
	boost::split(result, input, boost::is_any_of("\t"));

	for (int i = 0; i < result.size(); i++)
		cout << result[i] << endl;
	return 0;
}
```

> To fiddle with case of letters

  * ```to_upper(str)```
  * ```to_upper(str)```
  * ```to_upper_copy(str)```
  * ```to_lower_copy(str)```

```
#include <boost/algorithm/string.hpp>
#include <iostream>

using namespace std;
using namespace boost::algorithm;

int main()
{
	string str("Hello");
	string upper_s;
	string lower_s;

	cout << "Actual string: "
		<< str << endl;

	to_upper(str);
	cout << "Actual string converted to uppercase: "
		<< str << endl;

	to_lower(str);
	cout << "Actual string converted to lowercase: "
		<< str << endl;

	str = "Hello";
	upper_s = to_upper_copy(str);
	lower_s = to_lower_copy(str);

	cout << "Converted Uppercase string: "
		<< upper_s << endl;
	cout << "Converted Lowercase string: "
		<< lower_s << endl;

	return 0;
}
```

> To erase some chars in a string

* ```erase_first_copy(str,string to remove)```
* ```erase_nth_copy(str,string to remove,nth copy)```
* ```erase_last_copy(str,string to remove)```
* ```erase_all_copy(str, string to remove)```
* ```erase_head_copy(str, size of first substring to remove)```
* ```erase_tail_copy(str, size of last substring to remove)```

```
#include <boost/algorithm/string.hpp>
#include <cstdlib>
#include <iostream>
#include <string>

using namespace std;
using namespace boost::algorithm;

int main()
{

	string s = "geeksforgeeks";
	cout << erase_first_copy(s, "ge") << '\n';
	cout << erase_nth_copy(s, "g", 0) << '\n';
	cout << erase_last_copy(s, "g") << '\n';
	cout << erase_all_copy(s, "g") << '\n';
	cout << erase_head_copy(s, 5) << '\n';
	cout << erase_tail_copy(s, 1) << '\n';
	return 0;
}
```

> To replace chars from string

* ```replace_first_copy(str, string to replace, replacing string)```
* ```replace_last_copy(str, string to replace, replacing string)```
* ```replace_all_copy(str, string to replace, replacing string)```


```
#include <boost/algorithm/string.hpp>
#include <cstdlib>
#include <iostream>
#include <string>

using namespace std;
using namespace boost::algorithm;

int main()
{

	string s = "geeks_for_geeks";
	cout
		<< replace_first_copy(s, "geek", "c")
		<< '\n';
	cout
		<< replace_last_copy(s, "_", "-")
		<< '\n';
	cout
		<< replace_all_copy(s, "_", "-")
		<< '\n';
	return 0;
}
```

> To join strings from a container

* ```string temp = join(container_vector,delimiter to join with)```






  
