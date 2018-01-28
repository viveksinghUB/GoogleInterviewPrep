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

3.   ##### Permutation of all character in a string

    `Put entries in HashSet, before printing check if its already present, if not add and print.`
    
4.   ##### Disadvantages of using static variable in JAVA
    
    Static variables defined at global scope of the class and so they also refereed as class member. 
- You can not control creation and destruction of static variable. Usefully they have been created at program loading and destroyed when program unload.
- Since static variable are class member, all threads tries to access them has to be  manage.
- If one thread changes value of a static variable that can possibly break functionality of other threads.
- They donot reflect the true behaviour of OOP concept.

5.   ##### Given a list of ordered distinct integers from [0-99] summarize missing elements in string format.

Input: [0,1,2,50,52,75]
Output: "3-49,51,53-74,76-99" 












