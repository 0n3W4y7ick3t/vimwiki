# arrays, slices, maps, structs

## arrays
- initialization
  1. `var arr [num]Type`, arr will be an array contains num zeroes values of Type.
  2. `arr := [num]Type{...init list}` same as above
- arrays are comparable, two arrs report equal when they have the same size, same type, same values of the same order.
## slices 
- initialization
  1. `var s1 []Type`, s1 == nil, but it's ready to be append to, cap == len == 0.
  2. `s2 := []Type{}`, s2 != nil, it's an empty slice, its cap == len == 0.
  3. `s3 := make([]Type, l, c)`, create a slice with the capacity of c, contains l items whose values are zero values of Type, append happens at s3[l], after the last item in this slice.
  4. `s4 := make([]Type, l)`, capacity is also l, append happens at s4[l], at the end of the whole slice.
- slicing 
  - slicing slices share the same underlying array, if you want to prevent append to a slicing one from overwriting the underlying array, use `s[a:b:c]`, where the third arg c determines the slicing's capacity. eg:
    ```go
    s1 := []int{1,2,3,4,5}
    s2 := s1[:2]
    s3 := s1[:2:2]
    s2[0] = 0 // changes s1, s3[0] = 0 will also change s1.
    s2 = append(s2, 30) // results s1 become [ 0 2 30 4 5 ]
    s3 = append(s3, 40) // s1 will not be changed, a new slice will be alloced for s3.
    ```
    or you can use copy(s2, s1[a:b]) to get a whole new slice, and to modify it.
- slices are not comparable
## maps 
- initialization
  1. `var m1 map[K]V`, m1 == nil, you can NOT assign value to a key which is not presented in this nil map.
  2. `m2 := map[K]V{}`, same as `m3 := make(map[K]V)`(it doesn't matter much if you provide a second arg to the make() or not, len() will both return 0, if nothing is inserted yet.), this kind of map is not nil, it's ready to be inserted into using m[k] = v fashion.
  3. note that you can always use m[k] to take value out of a map, even from a nil map.
- use map as set 
  1. `map[K]bool`,  insert using `m[k] = true`, and read using `m[k]` (those not in the map return false, which is also the zero value.)
  2. `map[K]struct{}`, insert using `m[k] = struct{}{}`, read using `_, ok := m[k]`, this saves a little mem but looks a lot messier, use the above fashion instead.
- delete(m, k), if m is nil or k is not in m, do nothing
- `v, ok := m[k]`, just for map.
- maps are not comparable
## structs 
- initialization
  1. `var foo struct{f Type}{f:value}` create an anon struct val, which is suitable when you only need one instance, eg marshal/unmarshal json.
  2. `type foo struct{f Type}` to define a struct type foo and `var f foo`, `f := foo{}` will both create a struct with zero values.
  3. use a instance of struct to assign to another one, the primitive type fileds will be copy by default, but slices, arrays, and maps types fileds will not be copied, they share the same underlying mem.
- converting \
  two struct instances can be converted from each other, only if their prototypes have the same fileds names, the same types, the same order (i.e. they have the same type)
- comparing \
  you can not compare two struct instances using == directly even if they meet the conditions above. But if at least one of them is also anon, then you can use == to compare, as well as directly assign between them, without the need to convert them first.
