>[danger] # gcrc32

CRC32摘要算法。

使用方式：
```go
import "gitee.com/johng/gf/g/encoding/gcrc32"
```
方法列表：
```go
func EncryptBytes(v []byte) uint32
func EncryptString(v string) uint32
```

>[danger] # gmd5

最常用的MD5摘要算法。

使用方式：
```go
import "gitee.com/johng/gf/g/encoding/gmd5"
```
方法列表：
```go
func Encrypt(v interface{}) string
func EncryptFile(path string) string
func EncryptString(v string) string
```

>[danger] # gsha1

SHA1摘要算法。

使用方式：
```go
import "gitee.com/johng/gf/g/encoding/gsha1"
```
方法列表：
```go
func Encrypt(v interface{}) string
func EncryptFile(path string) string
func EncryptString(s string) string
```