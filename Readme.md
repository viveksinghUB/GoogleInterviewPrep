# Repository for questions asked in Google Interview

1.  Implement an interface. 
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

3. Permutation of all character in a string
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

4. Permutation of all character in a string
    `Put entries in HashSet, before printing check if its already present, if not add and print.`
