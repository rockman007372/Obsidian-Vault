
**You can read from a file using a `Scanner` object that uses a `File` object as the _source_ of data.**

This code uses a `Scanner` object to read (and print) contents of a text file line-by-line:

```java
import java.io.File;
import java.io.FileNotFoundException;
import java.util.Scanner;

public class FileReadingDemo {

    private static void printFileContents(String filePath) throws FileNotFoundException {
        File f = new File(filePath); // create a File for the given file path
        Scanner s = new Scanner(f); // create a Scanner using the File as the source
        while (s.hasNext()) {
            System.out.println(s.nextLine());
        }
    }

    public static void main(String[] args) {
        try {
            printFileContents("data/fruits.txt");
        } catch (FileNotFoundException e) {
            System.out.println("File not found");
        }
    }

}
```

```
5 Apples
3 Bananas
6 Cherries
```