
**Struct Type:**

- Custom data structures combining multiple values 
- can obtain arrays and mappings but not themselves 
  e.g: 
```
struct Car {
     string model;
     uint256 year;
}
```



**Mapping Types:**

- Key-value pairs
  e.g 
```
mapping(keyType  =>  ValueType) variablename;
```
- key can be primitive type (uint, bytes, address) 
- Value can be anything, including arrays and structs 
- Mapping are not iterable 
e.g 
```
mapping (address => uint256) public balances;
```
