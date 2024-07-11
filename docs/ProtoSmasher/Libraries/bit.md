# Bit

## bit.tobit
```lua
int bit.tobit(int num)
```
Returns the input as a bit number? (in my testing it just returns the number without a decimal)

## bit.bnot
```lua
int bit.bnot(int num)
```
Performs a bit negate on the input.

## bit.band
```lua
int bit.band(int n1, int n2)
```
Performs a bit and operation on the given inputs.

## bit.bor
```lua
int bit.bor(int n1, int n2)
```
Performs a bit or operation on the given inputs.

## bit.bxor
```lua
int bit.bxor(int n1, int n2)
```
Performs a bit xor operation on the given inputs.

## bit.lshift
```lua
int bit.lshift(int num, int ShiftAmount)
```
Shifts the input left by the given amount.

## bit.rshift
```lua
int bit.rshift(int num, int ShiftAmount)
```
Shifts the input right by the given amount.

## bit.arshift
```lua
int bit.arshift(int num, int ShiftAmount)
```
Performs a arithmetic right shift on the given input by the given amount.

## bit.rol
```lua
int bit.rol(int num, int ShiftAmount)
```
Circular shifts the input left by the given amount.

## bit.ror
```lua
int bit.ror(int num, int ShiftAmount)
```
Circular shifts the input right by the given amount.

## bit.bswap
```lua
int bit.bswap(int num)
```
Performs a byte swap on the given input. (basically reverses the bits).

## bit.tohex
```lua
string bit.tohex(int num)
```
Returns the input as a hexadecimal string.