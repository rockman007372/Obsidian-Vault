## File Object

**You can use the [`java.io.File`](https://docs.oracle.com/javase/9/docs/api/java/io/File.html) class to represent a file object**. It can be used to access properties of the file object.

This code creates a `File` object to represent a file `fruits.txt` that exists in the `data` directory relative to the current working directory and uses that object to print some properties of the file.

```Java
import java.io.File;

public class FileClassDemo {

    public static void main(String[] args) {
        File f = new File("data/fruits.txt"); // use forward slash
        System.out.println("full path: " + f.getAbsolutePath());
        System.out.println("file exists?: " + f.exists());
        System.out.println("is Directory?: " + f.isDirectory());
    }

}
```

```
full path: C:\sample-code\data\fruits.txt
file exists?: true
is Directory?: false
```