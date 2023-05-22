**A simple way to semi-automate testing of a CLI (Command Line Interface) app is by using input/output re-direction.**

-   First, you feed the app with a sequence of test inputs that is stored in a file while redirecting the output to another file.
-   Next, you compare the actual output file with another file containing the expected output.

Let's assume you are testing a CLI app called `AddressBook`. Here are the detailed steps:

1.  Store the test input in the text file `input.txt`.
2.  Store the output you expect from the SUT in another text file `expected.txt`.
3.  Run the program as given below, which will redirect the text in `input.txt` as the input to `AddressBook` and similarly, will redirect the output of AddressBook to a text file `output.txt`. Note that this does not require any code changes to `AddressBook`.  

```
java AddressBook < input.txt > output.txt
```
 
4.  Next, you compare `output.txt` with the `expected.txt`. This can be done using a utility such as Windows' `FC` (i.e. File Compare) command, Unix's `diff` command, or a GUI tool such as _WinMerge_.  

```
FC output.txt expected.txt
```

Note that the above technique is only suitable when testing CLI apps, and only if the exact output can be predetermined. If the output varies from one run to the other (e.g. it contains a time stamp), this technique will not work. In those cases, you need more sophisticated ways of automating tests.