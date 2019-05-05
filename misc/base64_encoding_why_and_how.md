## Base64 Encoding

### Why
 In ASCII, there are 256 characters [refer](https://www.ascii-code.com/). When we send data from one place to another place, it will flow through routers. Not all the routers(mostly legacy) will support all 256 characters. It will consider few characters as some instruction and might consume it in a different way. In order to prevent we can reduce the character set by 64 (which are printable ie A-Z,a-z,0-9,+,/), `Encode` the data `Before` transmitting and `Decode` the data `After` transmitting the data.

### How to Encode/Decode data
 Covert each character into 8 bit and then group the bits by 6 and refer the base64 table and represent in it as base64 [refer Examples section](https://en.wikipedia.org/wiki/Base64)

### Length of base64 string
Every 3 character in ASCII will have 4 characters in base64. Length of base64 = 4/3 * (Length of ASCII string)