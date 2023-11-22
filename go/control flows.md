## if
all else if and else share the same block wth if

## (for) loop
go only has one way to loop: for, but there are four ways of *for* :
1. the complete one `for init; condition; increment {}`
2. condition only `for condition {}`, like a while loop
3. infinite loop `for {}`
4. for-range `for i/k,v := range slices/strings/maps`, use `k := range m` if you only care about the key, use `_, v` if you only care about value.
    - notice that for-range on strings interates over the strings *rune by rune*, in this case if one rune contains more than one bit, the i which stands the offset of currrent rune in the string can increase more than 1

- use for-range when you want to iter through a whole container, use the complete one if you just want to loop a part of it.

## switch
- branches in go switch block don't fallthrough. you dont put break at the end of each case.
- **Blank switch** :`switch init; {}` you can switch over more than just one value by put whole conditions in cases.

## goto
go does support goto suprisingly, with some useful restrictions: goto can't jump over declarations nor can it jump into inner or parallel blocks.
only use it when you're 100% sure it will increase the code structure.
