\*---
created_at: 2025-03-26T22:18:18+02:00
modified_at: 2025-03-26T22:18:18+02:00

---

[Spec](https://go.dev/ref/spec)
Go is strongly type and garbage collected, explicit supp for concurrency.
Dependency management via packages.

Tokens building blocks of the source code:

1. Identifiers - variables,functions
2. Keywords - func var if
3. Operators - + - = , ;
4. Literals - 42, "Hello"

Whitespaces are used to seperate tokens but is ignored.

###### Keywords

break default func interface select
case defer go map struct
chan else goto package switch
const fallthrough if range type
continue for import return var

##### Operators

- & += &= && == != ( )

* | -= |= || < <= [ ]

- ^ \*= ^= <- > >= { }
  / << /= <<= ++ = := , ;
  % >> %= >>= -- ! ... . :
  &^ &^= ~

We can use '\_' to seperate numbers in binary or decimal i.e 1_000_000 , 0b101_010 , 0B1_010

##### Numbers

Exponent and "mantissa" (the freaking . )

- 1.23e4 => $1.23*10^4$
  _some new stuff_
- ox1p-2 hexadecimal (base of 16) for 1 × 2⁻² = 1 × 0.25 = **0.25**
- 0x2.p10 // == 2048.0 (2)

Won't dive deep but we can also use imaginary numbers
i.e 6.67428e-11i

##### Rune Literals

Like chars 'a' , 'א' , also '\n' or \\ or

##### Runes overall

- Runes are alias for int32

```GO
fmt.Println(rune(32))  // ' ' (space character)
fmt.Println(int32(' ')) // 32
```

##### String literals

```GO
`"\xFF\u00FF"`
`"\uD800"  // illegal: surrogate half`
`"\U00110000"  // illegal: invalid Unicode code point`
```

##### Constants

Although numeric constants have arbitrary precision, they may be implemented with limited precision in a compiler, which must represent integer constants with at least 256 bits, and floating-point constants with at least 256-bit mantissa and 16-bit exponent. The compiler will give errors if it can't represent constants precisely or if a constant overflows.

##### Variables

- static type = _size known at compilation time_
- dynamic type = size unknown at compilation time for example via use of interfaces

##### Types

We have many;

- uint8 ... uint64
- int8 ... int64
- float32,float64
- complex64, complex128
- byte **alias for uint8**
- rune **alias for int32**
- predeclared uint is 32 or 64, int same as uint
- uintptr unsinged integer enough for uniterperted bits of a pointer value
- _Strings_ - Immutable amount of bytes according to len of s.
- Arrays, can't contain type of themselves however this works:

```GO
  T5 [10]*T5                // T5 contains T5 as component of a pointer
	T6 [10]func() T6          // T6 contains T6 as component of a function type
	T7 [10]struct{ f []T7 }   // T7 contains T7 as component of a slice in a struct
```

- Slices!
  Slice of an array , also has len but can change during runtime,
  The array it points to can't be changed.
  **Capacity** - Amount of elements from _start of slice_ to _end of arr_
  > make([]T, length, capacity)
  > Equivlents:
  > make([]int, 50, 100)
  > new([100]int)[0:50]
  > **Note -Unlike Multi Dimensional Arrays! Slices of Slices Can vary in size**
  > Meaning we can have 2 lists of 3 elements
  > But we cant have 2 list of varying size.
  > However, we can have slice of slices in different sizes!
  ## _DAY 1 DONE_
