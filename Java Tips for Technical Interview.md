[PDF](file:///C:/Users/rockm/OneDrive%20-%20National%20University%20of%20Singapore/Study/Y1%20Summer/TIPS/Lecture+6b+-+Java+for+Technical+Interviews.pdf)

- Use `StringBuilder` for String concatenation.
- Primitive arrays are filled with default values.
	- `int[]` filled with 0
	- `boolean[]`filled with false 
- Array containing reference types will be filled with `Null` (even String array)
- We can use `Arrays.fill` to fill arrays with non-default values.
```Java
int[] nums = new int[10]; // must initialise first
// Method 2 (better) 
Arrays.fill(nums, 5); // Fill numArr with 5s

// Be careful of reference type
int[][] numArr = new int[10][3]; 
Arrays.fill(numArr, new int[]{1, 2, 3}); 
numArr[1][2] = 10; 
System.out.println(Arrays.toString(numArr[0])); // [1, 2, 10]
// all indices are modified
```

- Ways to copy a new List: 
```Java
// use List interface
List<T> copy = List.copyOf(list);

// use constructor
List<Plant> copy = new ArrayList<>(list);

// use addAll
List<Integer> copy = new ArrayList<>(); 
copy.addAll(list);

// deep copy (not just reference)
private static List<List<Integer>> cloneList(List<List<Integer>> original) {
    List<List<Integer>> copy = new ArrayList<>(original.size());
    for (List<Integer> list : original) {
        copy.add(new ArrayList<>(list)); // create a clone of the element
    }
    return copy;
}
```

- Queue<> is an interface, so we initialise Queue<> with `LinkedList<>()`
- Always use `double` and not `float` to store floating-point numbers.
```Java
float num1 = 1.0; // No :( 
double num2 = 1.0; // Yes :)
```
- Compare floating-point numbers:
```Java
double num1 = ...; // Some number 
double num2 = ...; // Some number 

// Compare relative values 
int comp = Double.compare(num1, num2); 

// Check for equality with small tolerance threshold (i.e. 10^-9) 
double EPS = 1e-9; 
boolean areEqual = Math.abs(num1 - num2) <= EPS
```
- Use constants as necessary
```Java
// E.g. for floating-point comparisons 
private static final double EPS = 1e-9; 

// E.g. for graph algorithms 
private static final int INF = (int) 1e9; 

// Naming convention: all caps with underscores as separators 
private static final int MY_CONSTANT = 100;
```
- Graph Traversal Movement Values
```Java
private static final int[][] MOVES = {{-1, 0}, {1, 0}, {0, -1}, {0, 1}}; 

// Assume that row and col are the current position 
for (int i = 0; i < MOVES.length; i++) { 
	int nextRow = row + MOVES[i][0]; 
	int nextCol = col + MOVES[i][1]; 
	// Do stuff with nextRow and nextCol 
}
```
- Use .equals instead of == to compare reference type (**especially for String**)
```Java
String a = "abc"; 
String b = "def"; 
boolean areEqual = a == b; // Bad :( 
boolean areEqual = a.equals(b); // Good :)
```
- Template code for overring equal method:
```Java
@Override public boolean equals(Object other) { 
	if (this == other) { 
		return true; 
	} else if (!(other instanceof A)) { 
		return false; 
	} else { 
		A otherA = (A) other; 
		return this.val == otherA.val; 
	} 
}
```
- We have to override `hashCode()` method along with `equals()` method when dealing with hash-based data structures
```Java
HashSet storedItems = new HashSet<>(); 
B b = new B(1, "hi"); 
storedItems.add(b); 
storedItems.contains(b); // true or false? 
storedItems.contains(new B(1, "hi")); // true or false?

class B { 
	private final int val; 
	private final String name; 
	// ... constructor 
	@Override 
	public int hashCode() { 
		return Objects.hash(val, name); 
	}
	
	@Override
	public boolean equals(Object o) {
	// ...
	}
}
```
- Overring compareTo method in Comparator/Comparable:
```Java
@Override 
public int compareTo(B other) { 
	if (this.val1 != other.val1) { 
		return this.val1 - other.val1; 
	} 
	return this.val2 - other.val2; 
}
```
- Use method `.valueOf ` to return string to integer and vice versa
```Java
String code = "123"
int x = Integer.valueOf(code[0]); // change character to integer
int y = Character.getNumericValue(c); // change string to integer
```

#### Be careful of generics!
- Cannot create an array of generic types (eg: `T[]`)
	- We must use @SuppressWarnings, then cast the array to an Object array to create generic array!
```Java
class Box<T extends Comparable<T>> {
	private final T[] items;
	
	public Box() {
		@SuppressWarnings
		T[] items = (T[]) new Comparable<T>[];
		this.items = items;
	}
}
```

- Remember PECS (Producer Extends, Consumers Super)
