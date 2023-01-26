---
tags: processed
course: CS2103T
type: content
date: 2023-01-25 Wednesday
---

**You can organize your _types_ (i.e., classes, interfaces, enumerations, etc.) into _packages_** for easier management

## Creating a Package

**To create a package, you put a package statement at the very top of every source file in that package.** The package statement must be the first line in the source file and there can be no more than one package statement in each source file. Furthermore, **the package of a type should match the folder path of the source file.** Similarly, the compiler will put the `.class` files in a folder structure that matches the package names.

```Java
package seedu.tojava.util;

public class Formatter {
    public static final String PREFIX = ">>";

    public static String format(String s){
        return PREFIX + s;
    }
}
```

The `Formatter` class above (in `<source folder>/seedu/tojava/util/Formatter.java` file) is in the package `seedu.tojava.util`. When it is compiled, the `Formatter.class` file will be in the location `<compiler output folder>/seedu/tojava/util`.

**Package names are written in all lower case** (not camelCase), using the dot as a separator. Packages in the Java language itself begin with `java`. or `javax`. Companies use their reversed Internet domain name to begin their package names.

## Access Public Package Members

**To use a public package member from outside its package, you must do EITHER of the following:**

1.  **Use the fully qualified name** to refer to the member
2.  **Import** the package or the specific package member

```java
package seedu.tojava;

import seedu.tojava.util.StringParser;
import seedu.tojava.frontend.*;

public class Main {

    public static void main(String[] args) {

        // Using the fully qualified name to access the Processor class
        String status = seedu.tojava.logic.Processor.getStatus();

        // Using the StringParser previously imported
        StringParser sp = new StringParser();

        // Using classes from the tojava.frontend package
        Ui ui = new Ui();
        Message m = new Message();

    }
}
```

## Notes

**Importing a package does not import its sub-packages**, as packages do not behave as hierarchies despite appearances.

**A _static import_ can be used to import static members of a type** so that the imported members can be used without specifying the type name.

```java
import static seedu.tojava.util.Formatter.PREFIX;
import static seedu.tojava.util.Formatter.format;

public class Main {

    public static void main(String[] args) {

        String formatted = format("Hello");
        boolean isFormatted = formatted.startsWith(PREFIX);
        System.out.println(formatted);
    }
}
```

Note how we use constant `PREFIX` and method `format()` without specifying `Formatter.PREFIX` and `Formatter.format()`.

---
Links: [[CS2103T]]
