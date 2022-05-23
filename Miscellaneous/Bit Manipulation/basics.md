
# Bit Manipulation Tricks

## Every element occurs as pair except one

* XOR of all the elements gives the answer
* XOR of same number yields a ```0```
* XOR of the even occurences of elements results in a ```0```
* XOR of the odd occurences result in the number ```itself```

## Count the bits to flip from one number to another

* XOR to get the differences in the bits of both numbers
* The result will have the ```1's``` where ever they have same bits
* Hence find the number of ```0's``` to get the differences in them 
* Use ```<<``` to get powers of 2 and ```&``` with the result
* To loop through the number based on its bit size, use ```(int)log2(n)+1```

