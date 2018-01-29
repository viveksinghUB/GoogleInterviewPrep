# Repository for questions asked in Google Interview

1.  ##### Implement an interface. 
```
public interface Relatable {
        
    // this (object calling isLargerThan)
    // and other must be instances of 
    // the same class returns 1, 0, -1 
    // if this is greater than, 
    // equal to, or less than other
    public int isLargerThan(Relatable other);
}
```
````
public class RectanglePlus implements Relatable {
    public int width = 0;
    public int height = 0;
    
    // a method for computing  the area of the rectangle
    public int getArea() {
        return width * height;
    }
    
    // a method required to implement the Relatable interface
    public int isLargerThan(Relatable other) {
        RectanglePlus otherRect = (RectanglePlus)other;
        if (this.getArea() < otherRect.getArea())
            return -1;
        else if (this.getArea() > otherRect.getArea())
            return 1;
        else
            return 0;               
    }
}
````

---


2.   ##### Permutation of all character in a string
```
    	private void permute(String str, String pre)
	{
		if (str.length()==1)
			System.out.println(pre+str);
		else
		{
			for (int i = 0; i < str.length(); i++)
			{   
			    if(i==0)
			        permute(str.substring(1,str.length()),pre+str.charAt(i));
			    else 
			    	permute(str.substring(0,i)+str.substring(i+1,str.length()),pre+str.charAt(i));
			}
		}
	}
````

---


3.   ##### Permutation of all character in a string

    `Put entries in HashSet, before printing check if its already present, if not add and print.`
 
---

   
4.   ##### Disadvantages of using static variable in JAVA
    
    Static variables defined at global scope of the class and so they also refereed as class member. 
- You can not control creation and destruction of static variable. Usefully they have been created at program loading and destroyed when program unload.
- Since static variable are class member, all threads tries to access them has to be  manage.
- If one thread changes value of a static variable that can possibly break functionality of other threads.
- They donot reflect the true behaviour of OOP concept.

---


5.   ##### Given a list of ordered distinct integers from [0-99] summarize missing elements in string format.

Input: [0,1,2,50,52,75]

Output: "3-49,51,53-74,76-99" 

````
class MyCode {
  public static void main (String[] args) {
    int[] l = {0,1,2,50,75,80};
    missing(l);
  }
  
  public static void missing(int[] ls){
    
    StringBuilder str=new StringBuilder();
    int count=0;
    int i=0;
    while(count<ls.length){
      if(ls[count]>i){
        if(ls[count]==i+1)
          str.append(String.valueOf(i)+ " ");
        else
          str.append(String.valueOf(i)+ " - "+String.valueOf(ls[count]-1)+" , ");
      }
      
      i=ls[count++]+1;
    }
    System.out.println(str);
    
  }
}
````

---


6.   ##### If you're given a list of countries and its corresponding population, write a function that will return a random country but the higher the population of the country, the more likely it is to be picked at random.
````
Sort countries by population.
india 50, china 40, usa 20
generate random number
if number 1 to 50 print india
if number 50 to 90, print china
else print usa
````

---


7.   ##### Check if a given array contains duplicate elements within k distance from each other

[K distance duplicate: GFG ](https://www.geeksforgeeks.org/check-given-array-contains-duplicate-elements-within-k-distance/)

Keep adding to hashset if i less than k else remove the i-kth element, as its at larger distance, and check if i is present, if not add ith  element

````
  public static void dupHash(int[] ls,int k){
    HashSet<Integer> set = new HashSet<>();
    for(int i=0;i<ls.length;i++){
      if(i>k){
        int start = i-k-1;
        set.remove(ls[start]);
      }
      if(set.contains(ls[i])){
        System.out.println("true");
        return;
      }
      set.add(ls[i]);
    }
    System.out.println("false");
    
  }
````

---


8.   ##### Given 3 coins of different values, print all the sums of the coins up to 1000. Must be printed in order.  ex: coins(10, 15, 55)  output 10 15 20 25 30 . . . 1000  

Add 0 to HashSet
Now check for all integers if integer- any of the coin values (or 0 ) is present, add it to HashSet, because this sum can be created by adding any one of the coin.
````
public void printSums(int c1, int c2, int c3) {

        Set<Integer> sums = new HashSet<>();
        sums.add(0);

        for(int sum = 1; sum <= 1000; sum++) {

            if(sums.contains(sum - c1) || sums.contains(sum - c2) || sums.contains(sum - c3)) {
                System.out.println(sum);
                sums.add(sum);
            }
        }
    }
}
````

---



9.   ##### Find the repeating and the missing.

 (Use elements as Index and mark the visited places)
Traverse the array. While traversing, use absolute value of every element as index and make the value at this index as negative to mark it visited. If something is already marked negative then this is the repeating element. To find missing, traverse the array again and look for a positive value.

10.   ##### Find the two repeating elements in a given array.

````
  public static void  twodup(int [] arr){
    int setter=0;     int mask=1;
    for(int n:arr){
      //make sure of braces other wise setter>0 will be evaluaetd first
      if(((mask<<n) & setter) > 0)
        System.out.println(n);
      setter=setter | (mask<<n);
      
    }
  }
  ````

---


11. ##### Notes on Bitwise Operator.

[Stanford](https://graphics.stanford.edu/~seander/bithacks.html)
[Java Doc](https://docs.oracle.com/javase/tutorial/java/nutsandbolts/op3.html)

The signed left shift operator "<<" shifts a bit pattern to the left.
The signed right shift operator ">>" shifts a bit pattern to the right. 
The bit pattern is given by the left-hand operand, and the number of positions to shift by the right-hand operand. 
The unsigned right shift operator ">>>" shifts a zero into the leftmost position, while the leftmost position after ">>" depends on sign extension.

The bitwise & operator performs a bitwise AND operation.

The bitwise ^ operator performs a bitwise exclusive OR operation.

The bitwise | operator performs a bitwise inclusive OR operation.

[Problems on rightmost set bit](http://www.techiedelight.com/bit-hacks-part-3-playing-rightmost-set-bit-number/)

(n & (n-1)) will unset the rightmost set bit of n.

**Problem 1. Check if the number is power of 2 ?**
` If only one bit is set in the number, the right most bit i.e that one bit will result in 0 . Thus (n & (n-1))==0 `

**Problem 2. Find position of rightmost set bit?**
` x= (n & (n-1))  will unset the rightmost set bit. Now, xor x with n to get a number with only right most set bit as set, rest all will be 0. log the result by 2 to get the position. `

**Problem 3. Count number of set bits in a number i.e. parity ?**

Method 1 O(number of bits):

````
while(n){
    if(n & 1)
        count++;
    n=n>>1;
}
````
Method 2 O(number of ones) :
Keep turning off the rightmost 1 until number becomes 0

````
while(n){
    count++;
    n=n & (n-1);
}
````

**Problem 4. Check if number is even?**  (n&1)!=0
**Problem 5. Check if number two numbers have opposite sign or not?**
x^y will be -ve iff x and y are opposite sin, coz if the sign bit is set in one of guys then it will be set in result aswell. [See](http://www.techiedelight.com/bit-hacks-part-1-basic/).

**Problem 6. Swap 2 numbers without using third number**
````
if(x!=y){
    x=x ^ y;
    y=x ^ y;
    x=x ^ y;
}
````

**Playing with the kth bit**

**1. Turn off the kth  bit**
~(1<<(k-1)) will give a mask will all bit set except kth bit.
ans=n & ~(1<<(k-1));

**2. Turn on the kth  bit**
ans=n | (1<<(k-1));

**3.Check if kth bit is set**
if n&(1<<(k-1)) !=0 then set else unset.

**4.Toggle kth bit**
ans= n^ (1<<(k-1))

**5.Check if bits are palindrome**
101 11011
````
rev=0;
while(n){
    rev=(rev<<1) | (n&1); //shift left and or with last bit of n
    n=n>>1; //shift all bits to right
}
if(rev==n) then its palindrome
````

12. ##### Two's Complement
[More read](https://www.cs.cornell.edu/~tomf/notes/cps104/twoscomp.html)
To get the two's complement negative notation of an integer, you write out the number in binary. You then invert the digits, and add one to the result.

If a number is represented in 2's compliment, and its first bit is 1 then its a negative number, if not then its a positive number.

If negative, to get what number its negative of : flip and add 1.
To get negative representation of a number : flip and add 1.

---


13. ##### Find the two non-repeating elements in an array of repeating elements.

Given an array in which all numbers except two are repeated once. (i.e. we have 2n+2 numbers and n numbers are occurring twice and remaining two have occurred once). Find those two numbers in the most efficient way. ? 

   arr[] = {2, 4, 7, 9, 2, 4}
1) Get the XOR of all the elements.
     xor = 2 ^ 4 ^ 7 ^ 9 ^ 2 ^ 4 = 14 (1110)
2) Get a number which has only one set bit of the xor.   
   Since we can easily get the rightmost set bit, let us use it.
     set_bit_no = xor & ~(xor-1) = (1110) & ~(1101) = 0010
   Now set_bit_no will have only set as rightmost set bit of xor.
3) Now divide the elements in two sets and do xor of         
   elements in each set, and we get the non-repeating 
   elements 7 and 9. Please see implementation for this   
   step.
   


---


