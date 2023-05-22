## Context

A system is required to execute a number of commands, each doing a different task. For example, a system might have to support `Sort`, `List`, `Reset` commands.

## Problem

It is preferable that some part of the code executes these commands without having to know each command type. e.g., there can be a `CommandQueue` object that is responsible for queuing commands and executing them without knowledge of what each command does.

## Solution

The essential element of this pattern is to have a general `<<Command>>` object that can be passed around, stored, executed, etc without knowing the type of command (i.e. via [[Polymorphism]]).

![[Pasted image 20230425142041.png]]

