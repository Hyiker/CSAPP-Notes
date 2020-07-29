# Bits, Bytes and Integer(2)

The second course aboud integer and integer arithmetic.

## Unsigned Addition

**Standard Addition Function**

Ignores carry output (when overflow occurs, just drop the most significant bit).
$$
1101_2+0101_2=10010_2
$$
Obviously the result is $15+3=18$,however, due to the overflow,we could only keep 4 bits.Thus, the result is $0010_2 = 2_{10}$

## Two's Complement Addition

**Have identical bit-level behavior to Unsigned integer addition**

### Acceptable overflow

Samely as unsigned addition, the process is: 
$$
1101_2+0101_2=10010_2
$$
Which means: 
$$
-3_{10}+5_{10}=2_{10}
$$
We could see that even if an overflow occurs, the result is still correct.

### Unacceptable overflow

However, if we apply this to the arithmetic below:
$$
-3_{10}-6_{10}=-9_{10}\Leftrightarrow1101_2+1010_2=10111_2=0111_2
$$
The result is +7 instead of -9, this reminds us when the overflow is out of the signed integer range, the result happens to be not what we expected.

We call this situation the ***negitive overflow***, and correspondingly, another kind of overflow is called ***positive overflow***.

## Multiplication

**Product of w-bit numbers x,y**

### Exact results can be bigger than *w* bits

- Unsigned: up to 2w bits
  - $$0\le x*y\le(2^w-1)^2$$

- Two's complement min (negative): up to 2w-1 bits
  - $x*y\ge(-2^{w-1})*(2^{w-1}-1)=-2^{2w-2}+2^{w-1}$

- Two's complement max (positive): up to 2w bits, but only for (*TMin<sub>w</sub>*)<sup>2</sup>
  - $x*y\le (-2^{w-1})^2=2^{2w-2}$

**We have to expand the bits to save the result**

### Signed Multiplication

- Operands: *w*bits
- True Product: 2* *w* bits
- Discard *w* bits (*w* bits will be kept)

**Standard Multiplication Function**

- Ignores high order *w* bits
- Some of which are different for signed vs. unsigned multiplication
- Lower bits are the same

### Work with shift

#### Left shift

- Unsigned: $u << k =u*2^k$

#### Right shift

- Unsigned: $u>>k=\lfloor u/2^k\rfloor$
- Signed: Arithmetic shift, use "1"s to fill the blank, which will cause the negative result to be smaller than what expected.e.g.: $ -3 >> 1 = -2$.Solution: add a bias.

### Proper way of applying a reversed loop

```c
size_t i;
for (i = cnt - 2;i < cnt; i--){
  // operations
}
```

### Byte-Oriented Memory Organization

We could see the memory as a big array of bytes.

In nowadays 64-bit machines, theoretically there should be 2<sup>64</sup> bits addressable.However, only 47 bits are there allowed to use by OS. Any operation trying to access the rest 17 bits leads to a *Segmentation fault*.



### Byte Ordering

![](https://github.com/Hyiker/CSAPP-Notes/raw/master/2.png)

