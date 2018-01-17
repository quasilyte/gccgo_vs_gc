This file contains benchmarks that were significantly faster on GCCGO.

Legend:
```
[!] - same (or worse) performance on GC Go devel (as opposed to GC 1.8.1).
[~] - performance difference holds on GC Go devel, but is less significant.
[+] - performance difference is resolved (better or same results).
[?] - benchmark was removed (or renamed) in Go devel.
```

### Section A - execution speed. time/op

```
comparing strings...
  [!] ByteByteNoMatch                   529ns ± 0%      327ns ± 0%        -38.19%  (p=0.008 n=5+5)
  [!] MapNoChanges                      354ns ± 0%      277ns ± 2%        -21.81%  (p=0.008 n=5+5)
  [?] Split1                            107ms ± 0%       40ms ± 0%        -62.39%  (p=0.008 n=5+5)
  [?] Split2                           16.8ms ± 0%     11.4ms ± 0%        -32.27%  (p=0.008 n=5+5)
  [+] IndexAnyASCII/256:1               950ns ± 0%      628ns ± 0%        -33.89%  (p=0.000 n=5+4)
  [+] IndexAnyASCII/256:2               954ns ± 0%      630ns ± 0%        -33.96%  (p=0.016 n=4+5)
  [+] IndexAnyASCII/256:4               963ns ± 0%      636ns ± 0%        -34.00%  (p=0.008 n=5+5)
  [+] IndexAnyASCII/256:8               980ns ± 0%      655ns ± 3%        -33.14%  (p=0.008 n=5+5)
  [+] IndexAnyASCII/256:16             1.01µs ± 0%     0.67µs ± 0%        -34.06%  (p=0.008 n=5+5)
  [+] IndexAnyASCII/4096:1             14.7µs ± 0%      7.9µs ± 0%        -45.89%  (p=0.029 n=4+4)
  [+] IndexAnyASCII/4096:2             14.7µs ± 0%      7.9µs ± 0%        -45.88%  (p=0.000 n=5+4)
  [+] IndexAnyASCII/4096:4             14.8µs ± 3%      8.0µs ± 0%        -46.43%  (p=0.008 n=5+5)
  [+] IndexAnyASCII/4096:8             14.7µs ± 0%      8.0µs ± 0%        -45.85%  (p=0.016 n=5+4)
  [+] IndexAnyASCII/4096:16            14.7µs ± 0%      8.0µs ± 0%        -45.83%  (p=0.008 n=5+5)

comparing bytes...
  [!] TrimSpace                   106ns ± 1%       71ns ± 0%        -32.50%  (p=0.008 n=5+5)
  [!] IndexBytePortable/32       63.6ns ± 1%     32.0ns ± 0%        -49.72%  (p=0.008 n=5+5)
  [+] IndexBytePortable/4K       4.11µs ± 1%     2.97µs ± 0%        -27.77%  (p=0.008 n=5+5)
  [+] IndexBytePortable/4M       4.29ms ± 3%     3.05ms ± 0%        -28.97%  (p=0.008 n=5+5)
  [+] IndexBytePortable/64M      68.1ms ± 0%     48.7ms ± 0%        -28.53%  (p=0.008 n=5+5)

comparing crypto/des...
  [+] Encrypt    1.23µs ±10%     0.61µs ±72%   -50.45%  (p=0.000 n=5+10)
  [+] Decrypt    1.18µs ± 1%     0.78µs ± 0%   -33.61%  (p=0.008 n=5+5)

comparing encoding/binary...
  [!] PutUvarint32            58.7ns ± 2%     36.1ns ± 2%    -38.48%  (p=0.000 n=5+11)
  [!] PutUvarint64             161ns ± 1%      127ns ± 5%    -20.80%  (p=0.001 n=5+10)

comparing encoding/json...
  [!] SkipValue              32.9ms ± 5%      22.2ms ± 5%         -32.44%  (p=0.008 n=5+5)

comparing hash/adler32...
  [!] Adler32KB    1.08µs ± 0%    0.89µs ± 0%  -18.17%  (p=0.029 n=4+4)

comparing html...
  [!] EscapeNone        9.46µs ± 3%    7.84µs ± 6%     -17.11%  (p=0.008 n=5+5)

comparing image/color...
  [!] YCbCrToRGBA/0        13.8ns ± 0%     0.7ns ± 0%   -94.78%  (p=0.000 n=5+4)
  [!] YCbCrToRGBA/128      12.8ns ± 0%     0.8ns ±12%   -93.75%  (p=0.008 n=5+5)
  [!] YCbCrToRGBA/255      13.7ns ± 0%     0.8ns ± 9%   -94.44%  (p=0.008 n=5+5)
  [!] NYCbCrAToRGBA/0      18.5ns ± 0%     1.0ns ± 6%   -94.72%  (p=0.008 n=5+5)
  [!] NYCbCrAToRGBA/128    16.8ns ± 0%     1.1ns ± 1%   -93.54%  (p=0.016 n=4+5)
  [!] NYCbCrAToRGBA/255    18.0ns ± 3%     0.8ns ± 7%   -95.74%  (p=0.008 n=5+5)

comparing image/gif...
  [+] QuantizedEncode     1.56s ± 0%     0.87s ± 1%  -43.98%  (p=0.008 n=5+5)

comparing image/jpeg...
  FDCT                 3.41µs ± 0%    1.51µs ± 0%   -55.64%  (p=0.000 n=5+4)
  IDCT                 3.44µs ± 0%    1.82µs ± 0%   -46.99%  (p=0.029 n=4+4)

comparing math...
  [!] Erf                    22.6ns ± 0%    13.9ns ± 0%   -38.50%  (p=0.008 n=5+5)
  [!] Erfc                   25.6ns ± 0%    15.5ns ± 0%   -39.45%  (p=0.008 n=5+5)
  [+] Dim                    8.58ns ± 0%    6.44ns ± 0%   -24.94%  (p=0.008 n=5+5)
  [~] Floor                  5.01ns ± 0%    3.61ns ± 3%   -27.90%  (p=0.008 n=5+5)
  [~] Max                    8.66ns ± 2%    5.72ns ± 0%   -33.92%  (p=0.000 n=5+4)
  [~] Frexp                  14.9ns ± 0%     7.9ns ± 0%   -47.32%  (p=0.000 n=5+4)
  [~] Gamma                  40.7ns ± 0%    19.4ns ± 1%   -52.33%  (p=0.016 n=4+5)
  [~] Ilogb                  13.0ns ± 1%     6.4ns ± 0%   -50.54%  (p=0.008 n=5+5)
  [~] Lgamma                 41.0ns ± 0%    23.2ns ± 0%   -43.41%  (p=0.029 n=4+4)
  [~] Logb                   12.9ns ± 0%     8.6ns ± 0%   -33.43%  (p=0.008 n=5+5)
  [~] Log2                   20.0ns ± 0%    10.7ns ± 0%   -46.50%  (p=0.008 n=5+5)
  [~] Modf                   12.2ns ± 0%     5.7ns ± 0%   -53.11%  (p=0.008 n=5+5)
  [~] Nextafter32            12.0ns ± 0%     8.7ns ± 3%   -28.07%  (p=0.008 n=5+5)
  [!] Nextafter64            10.5ns ± 0%     7.4ns ± 0%   -29.90%  (p=0.008 n=5+5)
  [+] Pow10Pos               97.0ns ± 1%    75.8ns ± 0%   -21.86%  (p=0.008 n=5+5)
  [+] Pow10Neg                117ns ± 0%      80ns ± 0%   -31.54%  (p=0.008 n=5+5)
  [+] Remainder              87.7ns ± 0%    34.6ns ± 1%   -60.57%  (p=0.008 n=5+5)
  [~] Sincos                 46.3ns ± 0%    22.1ns ± 0%   -52.27%  (p=0.008 n=5+5)
  [!] SqrtIndirectLatency    16.4ns ± 0%     7.2ns ± 0%   -56.40%  (p=0.000 n=5+4)

comparing math/big...
  [?] BitLen/0              6.41ns ± 0%    1.47ns ± 3%    -77.02%  (p=0.008 n=5+5)
  [?] BitLen/1              4.33ns ± 0%    1.45ns ± 2%    -66.56%  (p=0.016 n=4+5)
  [?] BitLen/2              4.33ns ± 0%    1.45ns ± 3%    -66.51%  (p=0.008 n=5+5)
  [?] BitLen/3              4.36ns ± 1%    1.44ns ± 1%    -66.85%  (p=0.008 n=5+5)
  [?] BitLen/4              4.33ns ± 0%    1.48ns ± 6%    -65.87%  (p=0.016 n=4+5)
  [?] BitLen/5              4.33ns ± 0%    1.45ns ± 3%    -66.61%  (p=0.008 n=5+5)
  [?] BitLen/8              4.33ns ± 0%    1.47ns ± 8%    -65.96%  (p=0.008 n=5+5)
  [?] BitLen/9              4.33ns ± 0%    1.46ns ± 4%    -66.33%  (p=0.016 n=4+5)
  [?] BitLen/16             4.33ns ± 0%    1.43ns ± 0%    -66.97%  (p=0.008 n=5+5)
  [?] BitLen/17             4.33ns ± 0%    1.43ns ± 0%    -66.97%  (p=0.008 n=5+5)
  [?] BitLen/31             4.36ns ± 1%    1.43ns ± 0%    -67.17%  (p=0.000 n=5+4)

comparing math/rand...
  [!] Int63Threadsafe      70.9ns ± 0%    53.9ns ± 1%   -23.98%  (p=0.016 n=4+5)
  [!] Int63Unthreadsafe    17.3ns ± 0%    10.3ns ± 3%   -40.35%  (p=0.008 n=5+5)
  [!] Int63n1000           68.5ns ± 0%    48.8ns ± 0%   -28.79%  (p=0.008 n=5+5)
  [!] Int31n1000           37.1ns ± 0%    10.4ns ± 0%   -71.97%  (p=0.008 n=5+5)
  [!] Float32              32.9ns ± 0%    12.7ns ± 0%   -61.40%  (p=0.008 n=5+5)
  [!] Float64              25.2ns ± 3%    11.7ns ± 0%   -53.61%  (p=0.008 n=5+5)
  [+] Read1000             5.54µs ± 0%    4.56µs ± 2%   -17.77%  (p=0.016 n=4+5)

comparing mime/quotedprintable...
  [!] Writer    17.9µs ± 7%    14.8µs ± 2%  -17.21%  (p=0.008 n=5+5)

comparing regexp/syntax...
  [!] EmptyOpContext     484ns ± 0%      70ns ± 0%  -85.50%  (p=0.016 n=4+5)

comparing sort...
  [~] Sort1e4               22.6ms ± 0%    18.8ms ± 2%    -16.89%  (p=0.008 n=5+5)
  [!] Sort1e6                3.44s ± 0%     2.81s ± 0%    -18.39%  (p=0.016 n=4+5)

comparing unicode/utf8...
  [!] RuneCountInStringTenJapaneseChars     124ns ± 0%     101ns ± 1%  -18.87%  (p=0.008 n=5+5)
```

### Section B - throughput. mb/sec

```
comparing bytes...
  [!] IndexBytePortable/32      503MB/s ± 1%   1001MB/s ± 0%        +98.91%  (p=0.008 n=5+5)
  [+] IndexBytePortable/4K     1.00GB/s ± 1%   1.38GB/s ± 0%        +38.44%  (p=0.008 n=5+5)
  [+] IndexBytePortable/4M      978MB/s ± 3%   1377MB/s ± 0%        +40.74%  (p=0.008 n=5+5)
  [+] IndexBytePortable/64M     985MB/s ± 0%   1378MB/s ± 0%        +39.92%  (p=0.008 n=5+5)

comparing crypto/des...
  [+] Encrypt  6.49MB/s ±10%  13.21MB/s ±46%  +103.43%  (p=0.001 n=5+9)
  [+] Decrypt  6.79MB/s ± 1%  10.23MB/s ± 0%   +50.56%  (p=0.008 n=5+5)

comparing encoding/binary...
  [!] PutUvarint32            58.7ns ± 2%     36.1ns ± 2%    -38.48%  (p=0.000 n=5+11)
  [!] PutUvarint64             161ns ± 1%      127ns ± 5%    -20.80%  (p=0.001 n=5+10)

comparing encoding/json...
  [!] SkipValue            59.7MB/s ± 0%    88.4MB/s ± 0%         +48.01%  (p=0.008 n=5+5)

comparing hash/adler32...
  [!] Adler32KB   946MB/s ± 0%  1156MB/s ± 0%  +22.15%  (p=0.029 n=4+4)

comparing image/gif...
  [+] QuantizedEncode   790kB/s ± 0%  1412kB/s ± 2%  +78.73%  (p=0.008 n=5+5)

comparing image/jpeg...
  [?] Encode             23.9MB/s ± 2%  28.8MB/s ± 0%   +20.74%  (p=0.008 n=5+5)
```

### Section C - allocations.

```
comparing container/heap...
  [+] Dup      20.0k ± 0%     10.0k ± 0%  -50.00%  (p=0.008 n=5+5)

comparing encoding/binary...
  [+] ReadSlice1000Int32s       3.00 ± 0%       2.00 ± 0%    -33.33%  (p=0.008 n=5+5)
  [+] ReadInts                  8.00 ± 0%       4.00 ± 0%    -50.00%  (p=0.008 n=5+5)
  [+] WriteInts                 16.0 ± 0%        8.0 ± 0%    -50.00%  (p=0.008 n=5+5)
  [+] WriteSlice1000Int32s      3.00 ± 0%       2.00 ± 0%    -33.33%  (p=0.008 n=5+5)

comparing expvar...
  [!] MapAddSame                6.00 ± 0%      5.00 ± 0%   -16.67%  (p=0.008 n=5+5)
  [!] MapAddDifferent           14.0 ± 0%      12.0 ± 0%   -14.29%  (p=0.008 n=5+5)

comparing fmt...
  [+] ManyArgs                           8.00 ± 0%      6.00 ± 0%    -25.00%  (p=0.008 n=5+5)

comparing image/draw...
  [!] RGBA                 120k ± 0%        60k ± 0%   -49.99%  (p=0.008 n=5+5)
  [+] Paletted             120k ± 0%        30k ± 0%   -74.99%  (p=0.008 n=5+5)
  [!] GenericOver          360k ± 0%       180k ± 0%   -50.00%  (p=0.008 n=5+5)
  [!] GenericMaskOver      210k ± 0%        65k ± 0%   -68.90%  (p=0.008 n=5+5)
  [!] GenericSrc           120k ± 0%        60k ± 0%   -49.99%  (p=0.008 n=5+5)
  [!] GenericMaskSrc       360k ± 0%       135k ± 0%   -62.51%  (p=0.008 n=5+5)

comparing image/gif...
  [+] QuantizedEncode      307k ± 0%       77k ± 0%  -74.99%  (p=0.008 n=5+5)

comparing image/png...
  [!] DecodePaletted            309 ± 0%       135 ± 0%   -56.31%  (p=0.008 n=5+5)
  [!] EncodeRGBA               614k ± 0%      154k ± 0%   -74.99%  (p=0.000 n=5+4)
```
