# SQL functions and other important points

## Peculiarities

If the question demands rounding off to a whole number try all the below

[https://www.hackerrank.com/challenges/average-population-of-each-continent/problem?isFullScreen=true](https://www.hackerrank.com/challenges/average-population-of-each-continent/problem?isFullScreen=true)

  * ```floor()```
  * ```ceil()```
  * ```round(number,decimal points)```

## REGEXP in SQL

[https://www.hackerrank.com/challenges/weather-observation-station-8/problem?isFullScreen=true](https://www.hackerrank.com/challenges/weather-observation-station-8/problem?isFullScreen=true)

```select distinct(city) from station where city regexp '^[aeiou].*[aeiou]$'```

[https://stackoverflow.com/questions/52563952/is-there-a-shorter-way-sql-multiple-like-and-or](https://stackoverflow.com/questions/52563952/is-there-a-shorter-way-sql-multiple-like-and-or)

[https://www.geeksforgeeks.org/mysql-regular-expressions-regexp/](https://www.geeksforgeeks.org/mysql-regular-expressions-regexp/)


* ```^``` matches the start of string
* ```$``` matches the end of string
* ```*``` matches one or more char instances of preceding char, more like repition
* ```.``` matches any character
* ```?``` matches zero or one char instance of preceding string
* ```[a-z]``` match any char from a to z
* ```[^abc]``` anything except a,b and c

## order by last letters

[https://www.hackerrank.com/challenges/more-than-75-marks/problem?isFullScreen=true](https://www.hackerrank.com/challenges/more-than-75-marks/problem?isFullScreen=true)

the format is ```substring(string,start,length)```

```select name from students where marks>75 order by substring(name,length(name)-2,3), id ```

```SELECT NAME FROM STUDENTS WHERE Marks > 75 ORDER BY RIGHT(NAME, 3), ID ASC;```

