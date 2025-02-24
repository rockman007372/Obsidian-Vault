---
tags:
  - toProcess
course: CS4215
type: tutorial
date: 2025-02-14 Friday
---

- RETURN instruction will pop the control until it reaches MARK instruction
- When entering a block (can be function body), generally should push (save) the environment on control to restore later upon exit
- Tail call:

```js
function f() {
	...
	return g(); // tail call
}

```

