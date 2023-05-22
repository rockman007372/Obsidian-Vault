## Context

Components need to access functionality deep inside other components.

## Problem

Access to the component should be allowed without exposing its internal details. e.g. the `UI` component should access the functionality of the `Logic` component without knowing that it contains a `Book` class within it.

## Solution

Include a Façade class that sits between the component internals and users of the component such that all access to the component happens through the Facade class.

![[Pasted image 20230425141739.png]]