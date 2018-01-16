# GCCGO vs GC (6g)

Comparing GCCGO 1.8.1 (GCC 7.2) vs GC 1.8.1 (and GC 1.10) on `x86` (AMD64).

## Benchmarking info

Benchmarks are executed by [run_bench](run_bench) script.

It expects particular `src` layout inside same directory. More precisely,
you must run it under a directory that is a valid GCCGO GOROOT.

[gccgo_tree](gccgo_tree) script can help in GOROOT preparations.

GCCGO passed `-O3 -march=native` options.

Most benchmarks are executed 5 times `-count=5` (never less than 5, sometimes more).

Results are expected to be analyzed by [benchstat](https://godoc.org/golang.org/x/perf/cmd/benchstat).

The whole process is quite simple:
1. Run benchmarks with Go GC 1.8.1; compiling Go 1.8.1 stdlib
2. Run benchmakrs with Go GCCGO 1.8.1; compiling gccgo versions stdlib
3. Compare results
4. For each benchmark that runs faster (or with much less allocs) run Go devel benchmarks on it's own version of stdlib

First two steps guarantee that same versions of stdlib are compared. Only implementations are different.
If something interesting is found, benchmarks are executed on upstream Go version *and* GCCGO on the same machine.
Relative performance is measured again to make [final conclusions](human-readable).

## List of benchmarks

See [packages.txt](packages.txt).

Basically, most stdlib packages benchmarks plus `test/bench/go1`.

```
test/bench/go1

src/archive/zip
src/strings
src/bytes
src/bufio
src/compress/bzip2
src/compress/flate
src/compress/lzw
src/container/heap
src/context
src/crypto/aes
src/crypto/cipher
src/crypto/des
src/crypto/ecdsa
src/crypto/elliptic
src/crypto/hmac
src/crypto/md5
src/crypto/rand
src/crypto/rc4
src/crypto/rsa
src/crypto/sha1
src/crypto/sha256
src/crypto/sha512
src/database/sql
src/encoding/asn1
src/encoding/base32
src/encoding/base64
src/encoding/binary
src/encoding/csv
src/encoding/gob
src/encoding/hex
src/encoding/json
src/encoding/pem
src/encoding/xml
src/expvar
src/fmt
src/hash/adler32
src/hash/crc32
src/hash/crc64
src/hash/fnv
src/html
src/html/template
src/image/color
src/image/draw
src/image/gif
src/image/jpeg
src/image/png
src/index/suffixarray
src/log
src/math
src/math/big
src/math/cmplx
src/math/rand
src/mime
src/mime/quotedprintable
src/net/url
src/net/rpc
src/net/textproto
src/regexp
src/regexp/syntax
src/sort
src/strconv
src/unicode/utf8
src/unicode/utf16
src/go/parser
src/go/printer
src/go/scanner
```

## Results

Each result is a full or partial benchmark suite run by a particular machine.  
Visit [stats](stats) to view all benchmark stats.

Under each machineX folder, there is `machine.txt` file of this structure:
```
$OS $ARCH
$CPUINFO
CPUs: $NUMCPU
Turbo: $TURBO_BOOST
$LATEST_SIMD
```

For example:
```
Linux 4.4.0-53-generic Ubuntu x86_64
Intel Core i5-4260U 1.40GHz
CPUs: 4
Turbo: disabled
Has AVX2
```

Inside machineX folder, there are `gc` and `gccgo` sub-directories.
They contain respective benchmark results.

Note that all machines are from x86 family.
No tests are run for `GOARCH=386`, only `GOARCH=AMD64` is covered.

## Other resources

* [Go GCC vs GC](http://losinggeneration.com/2016/01/11/go-gcc-vs-gc/) at losinggeneration.
