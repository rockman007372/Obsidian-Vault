Structures are equivalent to classes in Java. They allow grouping of heterogenous members.

![[Pasted image 20220827100729.png]]

#### Structure Type

```c
typedef struct {
	int length, width, height;
} box_t; // name of type, need a semicolon!
```

A type is not a variable; it is similar to a **Data Type** (int, float, char...)
- We are *defining a type*, not declaring a var
- NO memory allocated to a type unlike var

#### Instantiate Structure Variables

Structure variables (objects) are instances of a structure type (class).

```C
result_t resultA = {123, 53.5, 'A'};

card_t cardA = {8888, {31, 12, 2000}}; // initialize structure within structure
```

To access variables (fields), we use dot operator. Eg:  `result.grade`

To write a structure member:

```C
scanf("%d\n", &res1.grade);
```

#### Assigning Structures

Unlike an array, we can do assignment with structures.
- However, this is a **pass-by-value** assignment!
- The entire structure is **copied.**

```C
result_t res1 = {69, 'B'};
result_t res2;

res2 = res1; // allowed

void print_result(result_t res) {
	// ...
}

print_result(res1); // We are copying the entire structure to res → modifying res in the function has no effect on res1
```

To pass-by-reference, we must pass the **address** of the **structure variable** to the function!
- Unlike an array, which can be passed by its name, since its alr a pointer.
- ? Passing an **array of structures** is a different matter!

```c
void modify_result(result_t *res_ptr) {
	//... 
}

result_t res1 = {69, 'B'};
modify_result(&res1); // modify the content of res1 directly


void change_name_and_age(player_t *player_ptr) { // * = pointer declaration
  strcpy((*player_ptr).name, "Alexandra");       // * = pointer dereferencing
  (*player_ptr).age = 25;
}

```

#### Arrow Operator (→)

```C
// To acccess a variable (field) of a structure variable from a pointer:
(*player_ptr).name;


// A syntactic sugar
player_ptr->name; // equivalent

// example
void change_name_and_age(player_t *player_ptr) {
  strcpy(player_ptr->name, "Alexandra");
  player_ptr->age = 25;
}
```