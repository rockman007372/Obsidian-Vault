## Context

An object (possibly more than one) is interested in being notified when a change happens to another object. That is, some objects want to ‘observe’ another object.

## Problem

The 'observed' object does not want to be coupled with the objects that are 'observing' it.

For example, when we add a new student to the Student List, we have no way of informing the UI components that are observing it.

![[Pasted image 20230425143402.png]]

## Solution

Force the communication through an interface known to both parties.

![[Pasted image 20230425143454.png]]

Generic description:

![[Pasted image 20230425143623.png]]

-   `<<Observer>>` is an interface: any class that implements it can observe an `<<Observable>>`. Any number of `<<Observer>>` objects can observe (i.e. listen to changes of) the `<<Observable>>` object.
-   The `<<Observable>>` maintains a list of `<<Observer>>` objects. `addObserver(Observer)` operation adds a new `<<Observer>>` to the list of `<<Observer>>`s.
-   Whenever there is a change in the `<<Observable>>`, the `notifyObservers()` operation is called that will call the `update()` operation of all `<<Observer>>`s in the list.