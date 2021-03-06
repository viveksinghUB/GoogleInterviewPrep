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


---



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



---


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
  
````

 for(i = 1; i < n; i++)
   xor ^= arr[i];
 
  /* Get the rightmost set bit in set_bit_no */
  set_bit_no = xor & ~(xor-1);
  //or
  //set_bit_no=xor ^ (xor & (xor -1));
  // xor number with its value with right most set bit as unset. Only right most set bit will be chhanged thus will be retained doing xor.
 
  /* Now divide elements in two sets by comparing rightmost set    bit of xor with bit at same position in each element. */
  for(i = 0; i < n; i++)
  {
    if(arr[i] & set_bit_no)
     *x = *x ^ arr[i]; /*XOR of first set */
    else
     *y = *y ^ arr[i]; /*XOR of second set*/
  }
  
````


---

14. ##### . 	[License Key Formatting ](https://leetcode.com/problems/license-key-formatting/description/)

Input: S = "5F3Z-2e-9-w", K = 4

Output: "5F3Z-2E9W"

Explanation: The string S has been split into two parts, each part has 4 characters.
Note that the two extra dashes are not needed and can be removed.

````
public String licenseKeyFormatting(String S, int K) {
    StringBuilder temp = new StringBuilder();
    for(int i=S.length()-1;i>=0;i--){
        char ch=S.charAt(i);
        if(ch!='-')
            temp.append(temp.length()%(K+1) == K ? "-" : "").append(ch);
    }
    return temp.reverse().toString().toUpperCase();
}
````
Or it can be done by replacing all - with blank and then inserting after every k count


---

---

15. ##### 581. [Shortest Unsorted Continuous Subarray](https://leetcode.com/problems/shortest-unsorted-continuous-subarray/discuss/103057)

````
class Solution {
    public int findUnsortedSubarray(int[] nums) {
        //find the breakage point from left
        int start,end,i,j,left=-1,right=-1,maxval=Integer.MIN_VALUE,minval=Integer.MAX_VALUE;
        for(i=1;i<nums.length;i++){
            if(nums[i]<nums[i-1]) {
                left=i-1;
                break;
            }
        }
            
                
        for(j=nums.length-2;j>=0;j--){
            if(nums[j]>nums[j+1]){
                right=j+1;
                break;   
            }
        }
        //If already sorted return 0
        if(left<0)
            return 0;
            
        start=Math.min(left,right);
        end=Math.max(left,right);
        
        //find min and max in the subarray
        for(i=start;i<=end;i++){
            maxval=Math.max(maxval,nums[i]);
            minval=Math.min(minval,nums[i]);
        }
        start=-1;end=-1;
        //check which value contradicts with min and max of subarray, this will find breakage of looks like sorted array
        for(i=0;i<nums.length;i++){
            if(nums[i]>minval && start==-1)
                start=i;
            if(nums[nums.length-1-i]<maxval && end==-1)
                end=nums.length-1-i;
            if(start!=-1 && end!=-1)
                break;
        }
        return end-start+1;
    }
}

````

---

16. ##### 	[Design Compressed String Iterator](https://leetcode.com/problems/design-compressed-string-iterator/solution/)

````
class StringIterator {
    int index;
    int count;
    char ch=' ';
    String str;
    public StringIterator(String compressedString) {
        index=0;
        count=0;
        str=compressedString;
        
    }
    
    public char next() {
        if(!hasNext())
            return ' ';
        if(count==0){
            ch=str.charAt(index);
            index+=1; //move to digit;
            while(index<str.length() && Character.isDigit(str.charAt(index)))
                count = count*10 + (str.charAt(index++)-'0');
        }
        count--;
        return ch;
        
    }
    public boolean hasNext() {
        return index!=str.length() || count!=0;
    }
}
````


---




17. ##### 	[Plus One](https://leetcode.com/problems/plus-one/description/)

````
class Solution {
    public int[] plusOne(int[] digits) {
        int start=digits.length-1,end=0;
        while(start>=0 && digits[start]==9){
            start--;
        }
    
        if(start<0){
            int[] ans = new int[digits.length+1];
            ans[0]=1;
            return ans;
        }
        digits[start++]+=1;
        while(start<digits.length)
            digits[start++]=0;
        return digits;
        
    }
}
````


---

18. ##### 	[Find a peak element](https://www.geeksforgeeks.org/find-a-peak-in-a-given-array/)

We can use Divide and Conquer to find a peak in O(Logn) time. The idea is Binary Search based, we compare middle element with its neighbors. If middle element is not smaller than any of its neighbors, then we return it. If the middle element is smaller than the its left neighbor, then there is always a peak in left half (Why? take few examples). If the middle element is smaller than the its right neighbor, then there is always a peak in right half (due to same reason as left half).
//if neighbour exist check if its greater than neighbour
if( (mid==0 || a[mid] > a[mid-1] ) && (mid==arr.length-1 && a[mid] > a[mid+1]))
        return a[mid];
`````
int findPeak(int [] arr){
    return getPeak(arr,0,arr.length-1);
}

int getPeak(int[] arr, int i, int j){
    int mid=(i+j)/2
    
    if( (mid==0 || a[mid] > a[mid-1] ) && (mid==arr.length-1 && a[mid] > a[mid+1]))
        return a[mid];
    else
        if(mid>0 && a[mid] < a[mid-1])
            return getPeak(arr,i,mid-1);
        else 
            return getPeak(arr,mid+1,j)l;
    
}

`````


---


---

19. ##### [Count maximum collinear points](https://www.geeksforgeeks.org/count-maximum-points-on-same-line/)

We can solve above problem by following approach – For each point p, calculate its slope with other points and use a map to record how many points have same slope, by which we can find out how many points are on same line with p as their one point. For each point keep doing the same thing and update the maximum number of point count found so far.

Advance

Some things to note in implementation are:
1) if two point are (x1, y1) and (x2, y2) then their slope will be (y2 – y1) / (x2 – x1) which can be a double value and can cause precision problems. To get rid of the precision problems, we treat slope as pair ((y2 – y1), (x2 – x1)) instead of ratio and reduce pair by their gcd before inserting into map. In below code points which are vertical or repeated are treated separately


````
//  looping for each point
    for (int i = 0; i < N; i++)
    {
        curMax = overlapPoints = verticalPoints = 0;
 
        //  looping from i + 1 to ignore same pair again
        for (int j = i + 1; j < N; j++)
        {
            //  If both point are equal then just
            // increase overlapPoint count
            if (points[i] == points[j])
                overlapPoints++;
 
            // If x co-ordinate is same, then both
            // point are vertical to each other
            else if (points[i].first == points[j].first)
                verticalPoints++;
 
            else
            {
                int yDif = points[j].second - points[i].second;
                int xDif = points[j].first - points[i].first;
                int g = __gcd(xDif, yDif);
 
                // reducing the difference by their gcd
                yDif /= g;
                xDif /= g;
 
                // increasing the frequency of current slope
                // in map
                slopeMap[make_pair(yDif, xDif)]++;
                curMax = max(curMax, slopeMap[make_pair(yDif, xDif)]);
            }
 
            curMax = max(curMax, verticalPoints);
        }
 
        // updating global maximum by current point's maximum
        maxPoint = max(maxPoint, curMax + overlapPoints + 1);
 
 
 `````
 
 
 20. ##### (word boggle game)[https://www.geeksforgeeks.org/boggle-find-possible-words-board-characters/]
 
Pick one character and call function to deep traverse from this character.

Util function
check if word present
Mark index visited
Call same finction to all 8 locations accross this character

clear string

````

void findWordsUtil(char boggle[M][N], bool visited[M][N], int i,
                   int j, string &str)
{
    // Mark current cell as visited and append current character
    // to str
    visited[i][j] = true;
    str = str + boggle[i][j];
 
    // If str is present in dictionary, then print it
    if (isWord(str))
        cout << str << endl;
 
    // Traverse 8 adjacent cells of boggle[i][j]
    for (int row=i-1; row<=i+1 && row<M; row++)
      for (int col=j-1; col<=j+1 && col<N; col++)
        if (row>=0 && col>=0 && !visited[row][col])
          findWordsUtil(boggle,visited, row, col, str);
 
    // Erase current character from string and mark visited
    // of current cell as false
    str.erase(str.length()-1);
    visited[i][j] = false;
}

````


20.1 ##### Auto complete using (trie)[https://www.geeksforgeeks.org/auto-complete-feature-using-trie/]

---

21. ##### (Boggle | Set 2 (Using Trie))[https://www.geeksforgeeks.org/boggle-set-2-using-trie/]


---


22. ##### (Deepest node in left subtree)

Keep a boolean variable to see if its left or right
if left then only compare max

`````
	Node root;
	int maxLvl;
	Node result;

	void deepestLeftLeafUtil(Node node,int lvl,boolean isLeft) 
	{
		// Base case
		if (node == null) 
			return;

		if(isLeft){
		    if(lvl>maxLvl){
		        maxLvl=lvl;
		        result=node;
		    }
		}
		deepestLeftLeafUtil(node.left, lvl + 1, true);
		deepestLeftLeafUtil(node.right, lvl + 1,false);
	}
`````

23. ##### Biggest Square with all ones in it
24. ##### Bigges rectangle with all ones
25. ##### Biggest rectangle in histogram
26. ##### Maximum height of tree
27. ##### Minimum height tree
28. ##### Longest increasing consecutive subtree ||(leetcode)[https://leetcode.com/problems/binary-tree-longest-consecutive-sequence-ii/description/]

`````
class Solution {
    int maxval = 0;
    public int longestConsecutive(TreeNode root) {
        longestPath(root);
        return maxval;
    }
    
    int[] longestPath(TreeNode root){
        if(root==null)
            return new int[] {0,0};
        int[] inrdcr={1,1};
        if(root.left != null ){
            int [] childs=longestPath(root.left);
            if(root.left.val==root.val-1){
                inrdcr[1]+=childs[1];
            }
            else if(root.left.val==root.val+1){
                inrdcr[0]+=childs[0];
            }
        }
        if(root.right != null ){
            int [] childs=longestPath(root.right);
            if(root.right.val==root.val-1){
                inrdcr[1]=Math.max(childs[1]+1,inrdcr[1]);
            }
            else if(root.right.val==root.val+1){
                inrdcr[0]=Math.max(childs[0]+1,inrdcr[0]);
            }
        }
        maxval=Math.max(maxval,inrdcr[0]+inrdcr[1]-1);
        return inrdcr;
    }
}


`````
29. ##### longest consecutive sequence subtree  (leetcode)[https://leetcode.com/problems/binary-tree-longest-consecutive-sequence-ii/description/]

`````
class Solution {
    
    int max=1;
    
    public int longestConsecutive(TreeNode root) {
        util(root,1,null);
        return root==null ? 0 : max;
    }
    public void util(TreeNode node,int count,TreeNode pre){
        if(node==null)
            return;
        if(pre!=null && pre.val+1==node.val){
                count+=1;
                max=Math.max(max,count);
        }
        else
            count=1;
        util(node.left,count,node);
        util(node.right,count,node);
    }
}
``````


30. ##### Minimum height tree from graph (leetcode)[https://leetcode.com/problems/minimum-height-trees/description/]

Create adjecency list since nodes are numbered from 0 to n thus instead of hashmap we can make array of linked list.
where arr[i] shows list of nodes attached to node i

create distance array that stores the distance of node, eventually when we go deep, dist will store the distance from root
create a parent array to store the parent of each node , will help us in tracking down the longest path from v to u

then call dfs with starting node as any random node, we pick 0, 
	keep a visited array, mark start as visited and insert in queue
	while q is not empty, pop from q, traverse in its list, 
		if a partiular value is not visited
			update distance of values of list, mark visited, insert in queue, mark parent 
after dfs , find the node with max distance = u
make this node as start node and call dfs
find node with max distance = v
insert all the values from v to u using parent array into a list
if length of list is even, return the mid,mid-1 values
if odd return mid vakue

`````
class Solution {
    public List<Integer> findMinHeightTrees(int n, int[][] edges) {
        
        if(n==0)
            return new ArrayList<>();
        if(n==1 && edges.length==0)
            return Arrays.asList(0);
        //create adj list
        HashMap<Integer,ArrayList<Integer>> adj=new HashMap<>();
        for(int[] pairs : edges){
            if(!adj.containsKey(pairs[0]))
                adj.put(pairs[0],new ArrayList<Integer>());
            if(!adj.containsKey(pairs[1]))
                adj.put(pairs[1],new ArrayList<Integer>());
            adj.get(pairs[0]).add(pairs[1]);
            adj.get(pairs[1]).add(pairs[0]);
        }
        
        int[] dist1=new int[n];
        Integer[] parent=new Integer[n];//to store parent
        
        bfs(0,dist1,adj,parent);//pick any random node as start node
        //find the node with largest distance
        int max1=0;
        for(int i=0;i<n;i++){
            if(dist1[i] >  dist1[max1]){
                max1=i;                
            }
        }
        
        //traverse from this node
        int[] dist2=new int[n];
        
        bfs(max1,dist2,adj,parent);
        //find the node with largest distance from previous max
        int max2=0;
        for(int i=0;i<n;i++){
            if(dist2[i] >  dist2[max2]){
                max2=i;                
            }
        }
        // max1 is at one end and max2 is at other
        //if num of element in longest path is odd then middle+1 is the answer; 5-> 0,1,2,3,4  | 5/2=2
        //if num of element in longest path is even then mid and mid+1 is the answer 4-> 0,1,2,3 | 4/2=2,1
        int count=0;
        int ptr=max2;
        ArrayList<Integer> pathnodes = new ArrayList<>();
        while(ptr!=-1){
            System.out.println(ptr);
            pathnodes.add(ptr);
            ptr=parent[ptr];
            
        }
        int listSize=pathnodes.size();
        if(listSize%2==0){
            return Arrays.asList(pathnodes.get(listSize/2),pathnodes.get((listSize/2)-1));
        }
        else
            return Arrays.asList(pathnodes.get(listSize/2));
            
    }
    
    void bfs(int start,int [] dist,HashMap<Integer,ArrayList<Integer>> adj,Integer[] parent){
        boolean[] visited = new boolean[dist.length];
        Queue<Integer> queue=new LinkedList<Integer>();
        queue.add(start);//supposingly root for bfs
        parent[start]=-1; //to mark the start of longest path
        dist[start]=0;//root is at distance 0
        visited[start]=true;
        while(!queue.isEmpty()){
            Integer node = queue.poll();
            for(Integer n :  adj.get(node)){
                if(!visited[n]){
                    dist[n]=dist[node]+1;
                    visited[n]=true;
                    queue.add(n);
                    parent[n]=node;
                }
            }
        }
    }
    
    
    
}

`````
			
31. ##### Balanced binary tree (leetcode)[https://leetcode.com/problems/balanced-binary-tree/description/]

`````

class Solution {
    public boolean isBalanced(TreeNode root) {
        return util(root)!=-1;
        
    }
    
    int util(TreeNode root){
        if(root==null)
            return 0;
        if(root.left==null && root.right==null)
            return 1;
        int heightLeft=root.left==null ? 0 : util(root.left);
        int heightRight=root.right==null ? 0 : util(root.right);
        if(heightLeft==-1 || heightRight==-1 || Math.abs(heightLeft-heightRight)>1)
            return -1;
        else 
            return 1+Math.max(heightLeft,heightRight);
    }
        
}

`````


32. Largest BST in binary tree (gfg)[https://leetcode.com/problems/largest-bst-subtree/description/]

#VERY IMP

````
class Solution {
    private int largestBSTSubtreeSize = 0;
    public int largestBSTSubtree(TreeNode root) {
        helper(root);
        return largestBSTSubtreeSize;
    }
    
    public int[] helper(TreeNode root){
        //define the values to be passed,
        //0th is the size, -1 means not a bst, 1 will be min, 2 will be max
        int [] result=new int[3];
        if(root==null)
            return result; // index 0 will hold 0 value
        int[] left=helper(root.left);
        int[] right = helper(root.right);
        if( (left[0]==0 || (left[0]>0 && root.val > left[2]) ) && (right[0]==0 || (right[0]>0 && root.val < right[1]) ) )
        {
            result[0]=left[0]+right[0]+1;
            largestBSTSubtreeSize=Math.max(largestBSTSubtreeSize,result[0]);
            result[1]=left[0]==0 ? root.val : left[1];
            result[2]=right[0]==0 ? root.val : right[2];
        }
        else
            result[0]=-1;
        return result;
    }
}

````


32. Task Scheduler with idle or other task(leetcode)[https://leetcode.com/problems/task-scheduler/solution/]

````

public class Solution {
    public int leastInterval(char[] tasks, int n) {
        int[] map = new int[26];
        for (char c: tasks)
            map[c - 'A']++;
        PriorityQueue < Integer > queue = new PriorityQueue < > (26, Collections.reverseOrder());
        for (int f: map) {
            if (f > 0)
                queue.add(f);
        }
        int time = 0;
        while (!queue.isEmpty()) {
            int i = 0;
            List < Integer > temp = new ArrayList < > ();
            while (i <= n) {
                if (!queue.isEmpty()) {
                    if (queue.peek() > 1)
                        temp.add(queue.poll() - 1);
                    else
                        queue.poll();
                }
                time++;
                if (queue.isEmpty() && temp.size() == 0)
                    break;
                i++;
            }
            for (int l: temp)
                queue.add(l);
        }
        return time;
    }
}

````


33. #### Course schedule 1

Courses numbered from 0 to n-1; some with dependencies and some withnot, check if all can be completed.
count number of dependencies of each course
check which course dont have depedencies
	count them and add them to the queue
	while queue is not empty
		for the polled value of queue, reduce dependency of dependent ones
		if any dependency becomes 0, add it to count and add it to queue
check is count==numberOFCOurses

`````
class Solution {
    public boolean canFinish(int numCourses, int[][] prerequisites) {
        //course numbered from 0 to n-1
        int[] depen=new int[numCourses];
        for(int[] p : prerequisites){
            depen[p[0]]++;
        }
        //out of courses numbered 0 to n-1 some might be having 0 dependencies,
        //add them to queue
        Queue<Integer> queue=new LinkedList<>();
        int count=0;
        for(int i=0;i<numCourses;i++){
            if(depen[i]==0){
                queue.add(i);
                count++;
            }
        }
        
        while(!queue.isEmpty()){
            int pre=queue.poll();
            for(int[] p : prerequisites){
                if(p[1]==pre){
                    depen[p[0]]--;
                    if(depen[p[0]]==0){
                        //all prerequisites done ad to completed queue
                        queue.add(p[0]);
                        count++;
                    }
                }
            }
        }
        return count==numCourses;
    }
}

`````

34. #####(Product array without divisiion)[https://www.geeksforgeeks.org/a-product-array-puzzle/]

A Product Array Puzzle

Given an array arr[] of n integers, construct a Product Array prod[] (of same size) such that prod[i] is equal to the product of all the elements of arr[] except arr[i]. Solve it without division operator and in O(n).


`````
void productArray(int arr[], int n) 
    {
        // Initialize memory to all arrays
        int left[] = new int[n];
        int right[] = new int[n];
        int prod[] = new int[n];
 
        int i, j;
 
        /* Left most element of left array is always 1 */
        left[0] = 1;
 
        /* Rightmost most element of right array is always 1 */
        right[n - 1] = 1;
 
        /* Construct the left array */
        for (i = 1; i < n; i++)
            left[i] = arr[i - 1] * left[i - 1];
 
        /* Construct the right array */
        for (j = n - 2; j >= 0; j--)
            right[j] = arr[j + 1] * right[j + 1];
 
        /* Construct the product array using
           left[] and right[] */
        for (i = 0; i < n; i++)
            prod[i] = left[i] * right[i];
 
        /* print the constructed prod array */
        for (i = 0; i < n; i++)
            System.out.print(prod[i] + " ");
 
        return;
    }
   `````
35. #### Given one string, add char to string and find that character in log n time


Its simple
assuming that there are no duplicates in the string
Google
aGoogle

or
Google
Gooagle

while l<hi
So assume that inserted guy is in the mid
if s1[mid] == s2[mid] 
	lo=mid+1;
else //if mid guys are not equal and before them are equal than the mid one is the new guy
if mid==0 || s1[mid-1] ==s2[mid-1]
	return s1[mid]
else 
	hi=mid-1

//if nothing, 
	return s[n-1]

````

def solution(s1, s2)
      n = s1.length
      return s2 if n == 0

      lo = 0
      hi = n-1

      while lo <= hi # todo
        mid = lo+((hi-lo)/2)
        c1 = s1[mid]
        c2 = s2[mid]
        if c1 == c2
          lo = mid+1
        else
          if mid == 0 || (s1[mid-1] == s2[mid-1])
            return s2[mid]
          else
            hi = mid
          end
        end
      end
      return s2[-1]
    end

````

36 #### Given a number, find all number composed of 0 and 1 that are less than it

call with prefix
check if < n if yes call aain if no return
`````

public class Main {
    public static void main(String[] args) {
        printAll("1",123);
        
        printAll("0",123);
    }
    static void printAll(String suff,int n){
        int val= Integer.valueOf(suff);
        if(val > n)
            return;
        else{
            System.out.println(val); 
            if(val!=0){
                printAll(suff+"1",n);
                printAll(suff+"0",n);
            }
                
           
        }
  }
}

`````



37. #### LCA in a  binary tree (gfg)[https://www.geeksforgeeks.org/lowest-common-ancestor-binary-tree-set-1/]_


if node.data==n1 || node.data==n2
	return node // the lca node gets carried over
else
Node left = lca(node.left,n1,n2)
Node right = lca(node.right,n1,n2)
if (left_lca!=null && right_lca!=null)
            return node;
if(left==null && right==null)
return null

if left!=null return left else return right;



````
 

public class BinaryTree
{
    //Root of the Binary Tree
    Node root;
 
    Node findLCA(int n1, int n2)
    {
        return findLCA(root, n1, n2);
    }
 
    // This function returns pointer to LCA of two given
    // values n1 and n2. This function assumes that n1 and
    // n2 are present in Binary Tree
    Node findLCA(Node node, int n1, int n2)
    {
        // Base case
        if (node == null)
            return null;
 
        // If either n1 or n2 matches with root's key, report
        // the presence by returning root (Note that if a key is
        // ancestor of other, then the ancestor key becomes LCA
        if (node.data == n1 || node.data == n2)
            return node;
 
        // Look for keys in left and right subtrees
        Node left_lca = findLCA(node.left, n1, n2);
        Node right_lca = findLCA(node.right, n1, n2);
 
        // If both of the above calls return Non-NULL, then one key
        // is present in once subtree and other is present in other,
        // So this node is the LCA
        if (left_lca!=null && right_lca!=null)
            return node;
 
        // Otherwise check if left subtree or right subtree is LCA
        return (left_lca != null) ? left_lca : right_lca;
    }

}

40. #### Directed acylic graphs: longest paths

Longest path will tell max number of semester to complete the course or max numbetr of dependent intervals to complete the course

for each node keep the count of the indegree and maxpath till now 
update maxpath till now to  max(current , max of incoming+1)
max of all maxpath is m


41 #### detect cycle in a dag

dfs in a dag, 
push a guy when you visit it
as soon as you would have visited all its out degrees remove it from stack/Arraylist
thus stack keeps edges in mind and will track backedge

`````
def isCyclicUtil(self, v, visited, recStack):
 
        # Mark current node as visited and 
        # adds to recursion stack
        visited[v] = True
        recStack[v] = True
 
        # Recur for all neighbours
        # if any neighbour is visited and in 
        # recStack then graph is cyclic
        for neighbour in self.graph[v]:
            if visited[neighbour] == False:
                if self.isCyclicUtil(neighbour, visited, recStack) == True:
                    return True
            elif recStack[neighbour] == True:
                return True
 
        # The node needs to be poped from 
        # recursion stack before function ends
        recStack[v] = False
        return False
`````


41.b (Shortest Path in Directed Acyclic Graph)[https://www.geeksforgeeks.org/shortest-path-for-directed-acyclic-graphs/]

single source shortest distances in O(V+E) time for DAGs. The idea is to use Topological Sorting


42. ##### Bellman Ford (Given a graph and a source vertex src in graph, find shortest paths from src to all vertices in the given graph. The graph may contain negative weight edges)[https://www.geeksforgeeks.org/dynamic-programming-set-23-bellman-ford-algorithm/]

Dijkstra doesn’t work for Graphs with negative weight edges, Bellman-Ford works for such graphs. Bellman-Ford is also simpler than Dijkstra and suites well for distributed systems. But time complexity of Bellman-Ford is **O(VE)**, which is more than Dijkstra.

Input: Graph and a source vertex src
Output: Shortest distance to all vertices from src. If there is a negative weight cycle, then shortest distances are not calculated, negative weight cycle is reported.

`````
Following is complete algorithm for finding shortest distances.
1) Initialize dist[] = {INF, INF, ….} and dist[s] = 0 where s is the source vertex.
2) Create a toplogical order of all vertices.
3) Do following for every vertex u in topological order.
………..Do following for every adjacent vertex v of u
………………if (dist[v] > dist[u] + weight(u, v))
………………………dist[v] = dist[u] + weight(u, v)


````
1) This step initializes distances from source to all vertices as infinite and distance to source itself as 0. Create an array dist[] of size |V| with all values as infinite except dist[src] where src is source vertex.

2) This step calculates shortest distances. Do following |V|-1 times where |V| is the number of vertices in given graph.
…..a) Do following for each edge u-v
………………If dist[v] > dist[u] + weight of edge uv, then update dist[v]
………………….dist[v] = dist[u] + weight of edge uv

3) This step reports if there is a negative weight cycle in graph. Do following for each edge u-v
……If dist[v] > dist[u] + weight of edge uv, then “Graph contains negative weight cycle”
The idea of step 3 is, step 2 guarantees shortest distances if graph doesn’t contain negative weight cycle. If we iterate through all edges one more time and get a shorter path for any vertex, then there is a negative weight cycle



43. ##### (Kruskal’s Minimum Spanning Tree Algorithm)[https://www.geeksforgeeks.org/?p=26604]
1. Sort all the edges in non-decreasing order of their weight.
2. Pick the smallest edge. Check if it forms a cycle with the spanning tree formed so far. If cycle is not formed, include this edge. Else, discard it.
3. Repeat step#2 until there are (V-1) edges in the spanning tree.

44. #### (Dijkstra’s shortest path algorithm)[https://www.geeksforgeeks.org/?p=27697]

Below are the detailed steps used in Dijkstra’s algorithm to find the shortest path from a single source vertex to all other vertices in the given graph.
Algorithm
1) Create a set sptSet (shortest path tree set) that keeps track of vertices included in shortest path tree, i.e., whose minimum distance from source is calculated and finalized. Initially, this set is empty.
2) Assign a distance value to all vertices in the input graph. Initialize all distance values as INFINITE. Assign distance value as 0 for the source vertex so that it is picked first.
3) While sptSet doesn’t include all vertices
….a) Pick a vertex u which is not there in sptSetand has minimum distance value.
….b) Include u to sptSet.
….c) Update distance value of all adjacent vertices of u. To update the distance values, iterate through all adjacent vertices. For every adjacent vertex v, if sum of distance value of u (from source) and weight of edge u-v, is less than the distance value of v, then update the distance value of v.



44. ##### Prim’s Minimum Spanning Tree (MST)[https://www.geeksforgeeks.org/?p=27455]
 The idea is to maintain two sets of vertices. The first set contains the vertices already included in the MST, the other set contains the vertices not yet included. At every step, it considers all the edges that connect the two sets, and picks the minimum weight edge from these edges. After picking the edge, it moves the other endpoint of the edge to the set containing MST.
 
 
 
 ## Dynamic programing questions
 
 45. #### Fibinacci series
 
 a. Recursion
 `````
 int fib(int n){
 	if(n<=1) return n;
	return fib(n-1)+fib(n-2);
 }
 `````
 
 b. DP with memoization
 
 `````
 int fib (int n, int [] mem){
 	if( mem[n]!=0) return mem[n];
	int fibn=0;
	if(n==1 || n==0){
		fibn=n;
	}
	fibn=fib[n-1]+fib[n-2];
	mem[n]=fibn;
	return fibn;
 }
 `````
 
 c. Tabulation (Bottom Up):

`````
 int fib(int n){
 	int[] arr = new int[n+1];
	arr[0]=1;arr[1]=1;
	for(int i=2;<=n;i++){
		arr[i]=arr[i-1]+arr[i-2];
	}
	return arr[n];
 }
 `````
46. #### (Ugly number)[https://www.geeksforgeeks.org/ugly-numbers/]

Ugly numbers are numbers whose only prime factors are 2, 3 or 5. The sequence 1, 2, 3, 4, 5, 6, 8, 9, 10, 12, 15, … shows the first 11 ugly numbers. By convention, 1 is included.

````
int getNthUglyNo(int n)
{
	int i2=0,i3=0,i5=0;
	int [] ugly = new int[n+1];
	ugly[0]=1;
	int i=0;
	while(i<n){
		i++;
		ugly[i] = Math.min( Math.min (ugly[i2]*2,ugly[i3]*3),ugly[i5]*5 );
		if(ugly[i]==ugly[i2]*2)i2++;
		if(ugly[i]==ugly[i3]*3)i3++;
		if(ugly[i]==ugly[i5]*5)i5++;
	}
	return ugly[n-1];
}
`````

47. #### (Super ugly number)[https://www.geeksforgeeks.org/super-ugly-number-number-whose-prime-factors-given-set/]

`````
Let k be size of given array of prime numbers.
Declare a set for super ugly numbers.
Insert first ugly number (which is always 1) into set.
Initialize array multiple_of[k] of size k with 0. Each element of this array is iterator for corresponding prime in primes[k] array.
Initialize nextMultipe[k] array with primes[k]. This array behaves like next multiple variables of each prime in given primes[k] array i.e; nextMultiple[i] = primes[i] * ugly[++multiple_of[i]].
Now loop until there are n elements in set ugly.
a). Find minimum among current multiples of primes in nextMultiple[] array and insert it in the set of ugly numbers.
b). Then find this current minimum is multiple of which prime .
c). Increase iterator by 1 i.e; ++multiple_Of[i], for next multiple of current selected prime and update nextMultiple for it.
`````

48. #### (Longest Increasing Subsequence)[https://www.geeksforgeeks.org/longest-increasing-subsequence/]

length of LIS for {10, 22, 9, 33, 21, 50, 41, 60, 80} is 6 and LIS is {10, 22, 33, 50, 60, 80}.

`````
Let arr[0..n-1] be the input array and L(i) be the length of the LIS ending at index i such that arr[i] is the last element of the LIS.
Then, L(i) can be recursively written as:
L(i) = 1 + max( L(j) ) where 0 < j < i and arr[j] < arr[i]; or
L(i) = 1, if no such j exists.
`````

`````

    {
          int lis[] = new int[n];
          int i,j,max = 0;
 
          /* Initialize LIS values for all indexes */
           for ( i = 0; i < n; i++ )
              lis[i] = 1;
 
           /* Compute optimized LIS values in bottom up manner */
           for ( i = 1; i < n; i++ )
              for ( j = 0; j < i; j++ ) 
                         if ( arr[i] > arr[j] && lis[i] < lis[j] + 1)
                    lis[i] = lis[j] + 1;
 
           /* Pick maximum of all LIS values */
           for ( i = 0; i < n; i++ )
              if ( max < lis[i] )
                 max = lis[i];
 
            return max;
    }
    
 `````
 
 49. #### (Longest Common Subsequence)[https://www.geeksforgeeks.org/longest-common-subsequence/]
 
 If last characters of both sequences match (or X[m-1] == Y[n-1]) then
L(X[0..m-1], Y[0..n-1]) = 1 + L(X[0..m-2], Y[0..n-2])

If last characters of both sequences do not match (or X[m-1] != Y[n-1]) then
L(X[0..m-1], Y[0..n-1]) = MAX ( L(X[0..m-2], Y[0..n-1]), L(X[0..m-1], Y[0..n-2])

a. recursive O(2^n)

`````

int lcs(String a, String b , int m , int n){
//m,n to store last index
if(m<0 || n<0)
	return 0;
if(a.charAt(m)==b.charAt(n))
	return 1+lcs(a,b,m-1,n-1);
else
	return Math.max(lcs(a,b,m-1,n),lcs(a,b,m,n-1));
}

`````

b. Tabulation O(m*n)

`````
int lcs(String a, String b, int m,int n){
	int[][] mem= new int[m+1][n+1];
	for(int i=1;i<=m;i++){
		for(int j=1;i<=n;j++){
			if(a.charAt(i-1)==b.charAt(j-1)){
				mem[i][j]=1+mem[i-1][j-1];
			}
			else{
				mem[i][j]=Math.max(mem[i-1][j],mem[i][])
			}
		}
	}
	return mem[m-1][n-1];
}
`````

50. #### (Longest Repeated Subsequence)[https://www.geeksforgeeks.org/longest-repeated-subsequence/]

Given a string, print the longest repeating subseequence such that the two subsequence don’t have same string character at same position, i.e., any i’th character in the two subsequences shouldn’t have the same index in the original string.

Input: str = "aabb"
Output: "ab"

Input: str = "aab"
Output: "a"
The two subssequence are 'a'(first) and 'a' 
(second). Note that 'b' cannot be considered 
as part of subsequence as it would be at same
index in both.

