1.To a set a Kth bit in a number
```
 x = (1<<k) | x
```
2.To a clear a Kth bit in a number
```
 x = ~(1<<k) & x
```
3.To a Toggle a Kth bit in a number
```
 x = (1<<k) ^ x
```
4.Lets say 11011000 => want to 1101 0000 , want to make all clear include right most set bit
```
 x = x &(x-1)
x =     11011000
x-1 =   11010111
x & (x-1) = 1101 0000
```
5.Lets say 11011000 => want to 1101 1111 , want to make all set include right most set bit
```
 x = x | (x-1)
x =     11011000
x-1 =   11010111
x | (x-1) = 1101 0000
```
6 . MOst impoetent propery == additive inverse == 2's complement
```
-x = (~x)+ 1
```
7.
