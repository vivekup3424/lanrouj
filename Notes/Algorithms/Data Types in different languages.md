>[!WARNING]
> Largest value of unsigned integer (32-bit) = \( $2^{32}$ - 1 = 4,294,967,295 \)

>[!WARNING]
> Largest value of signed integer (32-bit) = \( $2^{31}$ - 1 = 2,147,483,647 \)

>[!NOTE]
> Smallest value of signed integer (32-bit) = \( -$2^{31}$ = -2,147,483,648 \)

>[!INFO]
> Binary representation of powers of two:
> - \( $2^0$ = 1 \): `0000 0001`
> - \( $2^1$ = 2 \): `0000 0010`
> - \( $2^2$ = 4 \): `0000 0100`
> - \( 2^3 = 8 \): `0000 1000`
> - \( 2^4 = 16 \): `0001 0000`
> - \( 2^5 = 32 \): `0010 0000`
> - \( 2^6 = 64 \): `0100 0000`
> - \( 2^7 = 128 \): `1000 0000`

>[!WARNING]
> Largest value of 64-bit unsigned integer = \( 2^{64} - 1 = 18,446,744,073,709,551,615 \)

>[!WARNING]
> Largest value of 64-bit signed integer = \( 2^{63} - 1 = 9,223,372,036,854,775,807 \)

>[!NOTE]
> Size of common data types in C++:
> - `int` (typically 32 bits): \(-2^{31}\) to \(2^{31} - 1\)
> - `unsigned int` (32 bits): \(0\) to \(2^{32} - 1\)
> - `long long` (typically 64 bits): \(-2^{63}\) to \(2^{63} - 1\)
> - `unsigned long long` (64 bits): \(0\) to \(2^{64} - 1\)
> - `char` (typically 8 bits): `-128` to `127` for signed, `0` to `255` for unsigned
> - `bool`: 1 bit, `true` (1) or `false` (0)

>[!INFO]
> Floating-point precision:
> - `float` (32-bit): Approximately 7 decimal digits of precision.
> - `double` (64-bit): Approximately 15 decimal digits of precision.
> - `long double` (typically 80-128 bits depending on the system): Higher precision than `double`, varies by implementation.

>[!TIP]
> To get the limits of any data type in C++, use `<climits>` (for integer types) or `<cfloat>` (for floating-point types).
> Example: `INT_MAX`, `FLT_MAX`.

When `i` reaches 31, `1 << 31` results in `-2147483648`. This is because you’re working with a 32-bit signed integer, where the highest bit (bit 31) is the sign bit.

### Explanation

In a 32-bit signed integer, shifting `1` to the 31st position (i.e., `1 << 31`) sets the sign bit to `1`, which represents a negative value in two's complement form. The value `1 << 31` becomes `-2147483648` in decimal, which is why you see a negative number in the output.