---
tags:
  - toProcess
course: CS4215
type: tutorial
date: 2025-02-07 Friday
---

### Homework 2

Question 1:

```js
const pred = while_loop_predicate(component);
const bod = while_loop_body(component);
let res = undefined;
while (evaluate(pred, env)) {
	res = evaluate(bod, env);
}
return res;
```

Question 2:

```js
function analyze_while_loop(component) { // CHANGED
    const predfun = analyze(while_loop_predicate(component)); // CHANGED
    const bodyfun = analyze(while_loop_body(component)); // CHANGED
    return env => { // CHANGED
        let res = undefined;
        while(predfun(env)) {
            res = bodyfun(env);
        }
        return res;
    };
}
```


What is wrong with my solution: There is repeated syntactic analysis when I call `evaluate(component, env)'

```js
function analyze_while_loop(component) { // CHANGED
    const predfun = analyze(while_loop_predicate(component)); // CHANGED
    const bodyfun = analyze(while_loop_body(component)); // CHANGED
    const evaluate_loop = env => { // CHANGED
	    if (predfun(env)) { // CHANGED
            const res = bodyfun(env); // CHANGED
            if (predfun(env)) {
                return evaluate_loop(env); // CHANGED 
            } else {
                return res;
            }
        } else { // CHANGED
            return undefined; // CHANGED
        }
    };
	return env => evaluate_loop(env);
}
```