## Append to File

**You can create a `FileWriter` object that appends to the file** (instead of overwriting the current content) by specifying an additional boolean parameter to the constructor.

 The method below appends to the file rather than overwrites.

```Java
private static void appendToFile(String filePath, String textToAppend) throws IOException {
    FileWriter fw = new FileWriter(filePath, true); // create a FileWriter in append mode
    fw.write(textToAppend);
    fw.close();
}
```