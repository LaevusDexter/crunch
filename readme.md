# crunch

[![godoc](https://godoc.org/github.com/superwhiskers/crunch?status.svg)](https://godoc.org/github.com/superwhiskers/crunch)


manipulate bytes and bits in golang with ease

## install

```
$ go get github.com/superwhiskers/crunch
```

## benchmarks

`MiniBuffer` performs on average more than twice as fast as `bytes.Buffer` in both writing and reading
```
BenchmarkBufferWrite-4          	30000000	        36.5 ns/op	       0 B/op	       0 allocs/op
BenchmarkBufferRead-4           	20000000	       106 ns/op	       0 B/op	       0 allocs/op
BenchmarkMiniBufferWrite-4      	200000000	         8.86 ns/op	       0 B/op	       0 allocs/op
BenchmarkMiniBufferRead-4       	1000000000	         2.12 ns/op	       0 B/op	       0 allocs/op
BenchmarkStdByteBufferWrite-4   	100000000	        19.4 ns/op	       0 B/op	       0 allocs/op
BenchmarkStdByteBufferRead-4    	300000000	         4.62 ns/op	       0 B/op	       0 allocs/op
```

## example

```golang
package main

import (
	"fmt"
	"github.com/superwhiskers/crunch"
)

func main() {

	// creates a new buffer with four zeroes
	buf := crunch.NewBuffer([]byte{0x00, 0x00, 0x00, 0x00})
	
	// write the byte `0x01` to the first offset, and move the offset forward one
	buf.WriteByteNext(0x01)
	
	// write the byte `0x01` to the second offset, and move the offset forward one
	buf.WriteByteNext(0x01)
	
	// seek the offset back one
	buf.Seek(-1, true)
	
	// write the bytes `0x02` and `0x03` to the second and third offsets, respectively
	buf.WriteBytesNext([]byte{0x02, 0x03})
	
	// write the byte `0x04` to offset `0x03`
	buf.WriteByte(0x03, 0x04)
	
	// output the buffer's contents to the console
	fmt.Printf("%v\n", buf.Bytes())
	
}
```

## license

[lgplv3](https://www.gnu.org/licenses/lgpl-3.0.en.html)
