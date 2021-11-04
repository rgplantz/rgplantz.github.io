## Division without using `div` or `idiv` instructions

At the end of Chapter 16 in my x86-64 book I point out that the division instructions can take a long time, and I mention a technique to divide without using them. In the book, I suggest using `gcc` with the `-O1` optimization level to create the assembly language from `intToDec.c` and look at the code.

When I did that, I got the following code sequence for dividing an integer by 10:

```asm
  mov     r8d, 3435973837   ## (2^35)/10
  mov     eax, esi          ## dividend is in `esi`
  imul    rax, r8           ## multiply by (2^35)/10
  shr     rax, 35           ## divide by 2^35
```

The compiler computed the constant (2^35)/10 = 3,435,973,837. Actually, the exact value is 3,435,973,836.8, but since we're using integers, the compiler rounds it.

The number to be divided by 10 is in `esi`.

The compiler multiplies our number by 3,435,973,837.

Then the compiler uses a right shift of 35 bits to divide the result of the mulplication by 2^35 = 34,359,738,368, which is exact.

The net result of this computation is to multiply our number by 3,435,973,837/34,359,738,368 = 0.10000000000582076609134674072266 on the calculator app on my computer.

***Important***: Although this is a very close approximation, it is not exact. You may need to find better approximations for your given application.
