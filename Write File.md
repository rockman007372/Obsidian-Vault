
**You can use a [`java.io.FileWriter`](https://docs.oracle.com/javase/9/docs/api/java/io/FileWriter.html) object to write to a file.**

The `writeToFile` method below uses a `FileWrite` object to write to a file. The method is being used to write two lines to the file `temp/lines.txt`.

```java
import java.io.FileWriter;
import java.io.IOException;

public class FileWritingDemo {

    private static void writeToFile(String filePath, String textToAdd) throws IOException {
        FileWriter fw = new FileWriter(filePath);
        fw.write(textToAdd);
        fw.close();
    }

    public static void main(String[] args) {
        String file2 = "temp/lines.txt";
        try {
            writeToFile(file2, "first line" + System.lineSeparator() + "second line");
        } catch (IOException e) {
            System.out.println("Something went wrong: " + e.getMessage());
        }
    }

}
```

 Contents of the `temp/lines.txt`:

```
first line
second line
```

Note that you need to call the `close()` method of the `FileWriter` object for the writing operation to be completed.