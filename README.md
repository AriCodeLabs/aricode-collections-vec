# aricode-stdlib / collections-vec

Dynamic integer vector for aricode, built on `arr_*` builtins.

Uses a simple layout: `arr[0]` = length, `arr[1]` = capacity,
`arr[2..]` = elements.

## Functions

| Function | Signature | Description |
|---|---|---|
| `vec_new` | `() -> i32` | Create a new empty vector (capacity 8). |
| `vec_len` | `(v: i32) -> i32` | Return the number of elements. |
| `vec_push` | `(v: i32, value: i32) -> i32` | Append a value; returns new length or -1 if full. |
| `vec_get` | `(v: i32, index: i32) -> i32` | Read element at index. |
| `vec_set` | `(v: i32, index: i32, value: i32) -> i32` | Write element at index. |
| `vec_sum` | `(v: i32) -> i32` | Sum all elements. |

## Usage

```ari
import "vec.ari";

fn main() -> i32 {
    let v: i32 = vec_new();
    vec_push(v, 10);
    vec_push(v, 20);
    vec_push(v, 30);
    print_int(vec_len(v));   // 3
    print_int(vec_sum(v));   // 60
    print_int(vec_get(v, 1)); // 20
    return 0;
}
```

## License

Copyright (c) 2026 Edwin F. Veliz Jaramillo. All rights reserved.
