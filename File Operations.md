## File Operations

**The [`java.nio.file.Files`](https://docs.oracle.com/javase/9/docs/api/java/nio/file/Files.html) is a utility class that provides several useful file operations.** It relies on the [`java.nio.file.Paths`](https://docs.oracle.com/javase/9/docs/api/java/nio/file/Paths.html) file to generate `Path` objects that represent file paths.

 This example uses the `Files` class to copy file `data/fruits.txt` to `temp/fruits2.txt` and delete the file `data/fruits.txt`.

```Java
import java.io.IOException;
import java.nio.file.Files;
import java.nio.file.Paths;

public class FilesClassDemo {

    public static void main(String[] args) throws IOException{
        Files.copy(Paths.get("data/fruits.txt"), Paths.get("temp/fruits2.txt"));
        Files.delete(Paths.get("temp/fruits2.txt"));
    }

}
```
