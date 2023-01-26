---
tags: processed
course: CS2103T
type: 
date: 2023-01-25 Wednesday
---

## Examples

**A minimal JavaDoc comment example for methods:**

```Java
/**
 * Returns lateral location of the specified position.
 * If the position is unset, NaN is returned.
 *
 * @param x X coordinate of position.
 * @param y Y coordinate of position.
 * @param zone Zone of position.
 * @return Lateral location.
 * @throws IllegalArgumentException If zone is <= 0.
 */
public double computeLocation(double x, double y, int zone)
    throws IllegalArgumentException {
    // ...
}
```

**A minimal JavaDoc comment example for classes:**

```Java
package ...

import ...

/**
 * Represents a location in a 2D space. A <code>Point</code>    
 * object corresponds to a coordinate represented 
 * by two integers e.g., <code>3,6</code>
 */
public class Point {
    // ...
}
```


---
Links: [[SWE Conventions]]

