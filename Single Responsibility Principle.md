
> [!definition]
> A class should have one and only one reason to change

If a class has only one responsibility, it needs to change only when there is a change to that responsibility.

>[!example]
> Consider a `TextUi` class that does parsing of the user commands as well as interacting with the user. That class needs to change when the formatting of the UI changes as well as when the syntax of the user command changes. Hence, such a class does not follow the SRP.