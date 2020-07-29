# Bits, Bytes and Integer(1)

This course is'bout how integers are represented in the computer and how the arithmetic are operated.

## Bits & Bytes

### Why bits?

- all bits are 0/1
- Analog signal basis determines the binary feature of bits.
- We can interprete sets of bits into other kind of information like a character or even an image
- Represent a data in bits is way much easier than in other forms

#### Data Representations(In Bytes)

| C Data Type     | Typical 32-bit | Typical 64-bit | x86-64 |
| :-------------- | :------------: | :------------: | :----: |
| **char**        |       1        |       1        |   1    |
| **short**       |       2        |       2        |   2    |
| **int**         |       4        |       4        |   4    |
| **long**        |       4        |       8        |   8    |
| **float**       |       4        |       4        |   4    |
| **double**      |       8        |       8        |   8    |
| **long double** |       -        |       -        | 10/16  |
| **pointer**     |       4        |       8        |   8    |
|                 |                |                |        |

### Representings & Manipulating Sets

#### Representation

- 01101001 { 0, 3, 5, 6 }
- 01010101 { 0, 2, 4, 6 }

#### Operations

| Operand | Set Operation        | Binary   | Set           |
| ------- | -------------------- | -------- | ------------- |
| &       | Intersection         | 01000001 | {0,6}         |
| \|      | Union                | 01111101 | {0,2,3,4,5,6} |
| ^       | Symmetric difference | 00111100 | {2,3,4,5}     |
| ~       | Complement           | 10101010 | {1,3,5,7}     |

***Beware! the different between bit Operations and Logic Operations***

while 0x69 && 0x55 = 0x01, 0x69 & 0x55 = 0x41

### Shift Operations

#### Left Shift: x << y

#### Right Shift x >> y

- Logical shift
  - Fill with 0's on left
- Arithmetic shift
  - Replicate most significant bit on left

## Encoding Integers

**Unsigned**
$$
B2U(X) = \sum^{w-1}_{i=0}x_i\cdot2^i
$$
**Two's Complement**
$$
B2T(X) = -x_{w-1}\cdot2^{w-1}+\sum_{i=0}^{w-2}x_i\cdot2^i
$$

#### Conversion of Unsigned and Signed

<img src="https://github.com/Hyiker/CSAPP-Notes/raw/master/1.png" align="center" width="70%">

**Why -1 > 0u ?(in C)**

This will cause a implicit conversion from signed number into unsigned(-1), in which case, -1 will be converted to the maximum number of signed number.

### Sign Extension

#### Task:

1. Given w-bit signed integer x
2. Convert it to w+k-bit integer with same value

#### Rule:

1. Make _k_ copies of sign bit:
2. X' = x<sub>w-1</sub> ,... ,x<sub>w-1</sub>(k copies), x<sub>w-1</sub>, x<sub>w-2</sub>,..., x<sub>0</sub>

### Truncating

1. Unsigned/signed: bits are truncated.
2. Result reinterpreted
3. Unsigned: mod operation
4. Signed: similar to mod
5. For small numbers yields expected behavior.



### Summary

#### Casting Singed <=> Unsigned: Basic Rules

- Bit pattern maintained
- reinterpreted
- Can have unexpected effects: adding or subtracting 2<sup>w</sup>