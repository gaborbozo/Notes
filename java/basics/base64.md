# Base64
Many protocols (like _HTTP_, _SMTP_, or _JSON_) are designed to work with text, not raw binary. _Base64_ allows to encode binary files (like images or documents) into text so they can be safely transmitted (**Preserving special characters while transferring text**).

**It takes three characters of input and produces four characters of output**.

| Value | _Base64_ index |
|--|--|
| _A_ | _0_ |
| _B_ | _1_ |
| ... | ... |
| _8_ | _60_ |
| _9_ | _61_ |
| _+_ | _62_ |
| _/_ | _63_ |
## Encoding
| B | y | e |
|--|--|--|
| _66_ | _121_ | _101_ |
| _01000010_ | _01111001_ | _01100101_ |
After encoding to binary _ASCII_ concat the binary values and instead of groupping it into _8_, group into _6_ and map to _Base64_ alphabet.
 
| Q | n | l | l |
|--|--|--|--|
| _16_ | _39_ | _37_ | _37_ |
| _010000_ | _100111_ | _100101_ | _100101_ |

**If the input is not a number of three it will use a filler character instead**. _Byee_ -> _QnllZQ==_
## Java
`java.util.Base64_`

Static methods for encoding and decoding.

```java
encodedStr = Base64.getEncoder().encodeToString("Bye".getBytes());

Base64.getMimeEncoder()
Base64.getUrlEncoder()

Base64.getDecoder().decode()
```
<!--stackedit_data:
eyJoaXN0b3J5IjpbMjUxNTY4MzU2XX0=
-->