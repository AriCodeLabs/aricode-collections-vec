# aricode-collections-vec

Dynamic integer vector for the
[aricode](https://github.com/Lynx-Boss/aricode) compiler, built on the
`arr_*` heap-array builtins.

## Layout

```
aricode-collections-vec/
├── vec.ari            — vec_new, vec_len, vec_push, vec_get, vec_set, vec_sum
├── examples/
│   └── sum_demo.ari   — push + sum quick tour
└── tests/
    └── test_vec.ari
```

## Design

Backing store is a flat `arr_new` allocation with the first two slots
reserved as a header:

| Slot | Meaning |
|------|---------|
| `arr[0]` | length |
| `arr[1]` | capacity |
| `arr[2..]` | elements |

Current implementation uses a **fixed capacity of 8** (no realloc
builtin yet); `vec_push` returns `-1` when the vector is full. Grow
support is on the roadmap once a resizable-array builtin lands.

## Public API

| Function | Signature | Description |
|----------|-----------|-------------|
| `vec_new()` | `-> i32` | Create empty vector (capacity 8). |
| `vec_len(v)` | `-> i32` | Number of elements. |
| `vec_push(v, x)` | `-> i32` | Append `x`, return new length, or `-1` if full. |
| `vec_get(v, i)` | `-> i32` | Element at index `i`, or `-1` if out of bounds. |
| `vec_set(v, i, x)` | `-> i32` | Write element at index `i`; `0` on success, `-1` on OOB. |
| `vec_sum(v)` | `-> i32` | Sum of all elements. |

## Usage

```
import "aricode-collections-vec/vec.ari" as vec;

fn main() -> i32 {
    let v: i32 = vec.vec_new();
    vec.vec_push(v, 10);
    vec.vec_push(v, 20);
    print_int(vec.vec_sum(v));    // 30
    mem_free(v);
    return 0;
}
```

See [`examples/sum_demo.ari`](examples/sum_demo.ari).

## Running the tests

```
aric tests/test_vec.ari -o /tmp/test_vec
/tmp/test_vec
```

Expected output ends with `ALL TESTS PASSED / Failures: 0`.

## License

Copyright (c) 2026 Edwin F. Veliz Jaramillo. All rights reserved.
