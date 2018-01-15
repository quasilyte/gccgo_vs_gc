This file contains benchmarks that were significantly faster on GCCGO.

Legend:
[!] - same (or worse) performance on GC Go devel (as opposed to GC 1.8.1).
[~] - performance difference holds on GC Go devel, but is less significant.
[+] - performance difference is resolved (better or same results).
[?] - benchmark was removed (or renamed) in Go devel.

### Section A - execution speed. time/op

```
comparing strings...
  [!] ByteByteNoMatch                   242ns ± 2%      151ns ± 4%        -37.51%  (p=0.000 n=9+9)
  [?] Split1                           49.6ms ± 6%     22.2ms ± 4%        -55.27%  (p=0.000 n=10+10)
  [?] Split2                           7.75ms ± 4%     5.27ms ± 6%        -31.98%  (p=0.000 n=9+10)
  [+] IndexAnyASCII/256:1               441ns ± 7%      296ns ± 5%        -32.91%  (p=0.001 n=10+5)
  [+] IndexAnyASCII/256:2               448ns ± 7%      289ns ± 0%        -35.42%  (p=0.002 n=10+4)
  [+] IndexAnyASCII/256:4               440ns ± 2%      297ns ± 4%        -32.58%  (p=0.002 n=8+5)
  [+] IndexAnyASCII/256:8               456ns ± 7%      308ns ± 4%        -32.44%  (p=0.001 n=10+5)
  [+] IndexAnyASCII/256:16              474ns ± 8%      315ns ± 5%        -33.68%  (p=0.001 n=10+5)
  [+] IndexAnyASCII/4096:1             6.85µs ± 8%     3.74µs ± 5%        -45.46%  (p=0.001 n=10+5)
  [+] IndexAnyASCII/4096:2             6.86µs ± 5%     3.72µs ± 5%        -45.78%  (p=0.001 n=10+5)
  [+] IndexAnyASCII/4096:4             6.83µs ± 6%     3.74µs ± 6%        -45.25%  (p=0.001 n=10+5)
  [+] IndexAnyASCII/4096:8             6.92µs ± 7%     3.73µs ± 4%        -46.00%  (p=0.001 n=10+5)
  [+] IndexAnyASCII/4096:16            6.83µs ± 6%     3.78µs ± 3%        -44.56%  (p=0.001 n=10+5)

comparing bytes...
  [!] TrimSpace                  50.1ns ± 7%     33.7ns ± 4%        -32.73%  (p=0.008 n=5+5)
  [!] IndexBytePortable/32       31.1ns ± 8%     15.0ns ± 4%        -51.61%  (p=0.008 n=5+5)
  [+] IndexBytePortable/4K       1.99µs ± 6%     1.39µs ± 5%        -30.01%  (p=0.008 n=5+5)
  [+] IndexBytePortable/4M       1.98ms ± 3%     1.42ms ± 4%        -28.28%  (p=0.008 n=5+5)
  [+] IndexBytePortable/64M      33.9ms ± 3%     24.4ms ± 6%        -27.92%  (p=0.008 n=5+5)

comparing crypto/des...
  [+] Encrypt     543ns ± 6%     376ns ± 3%  -30.77%  (p=0.008 n=5+5)
  [+] Decrypt     539ns ± 4%     376ns ± 4%  -30.23%  (p=0.008 n=5+5)

comparing encoding/binary...
  [!] PutUvarint32            27.4ns ± 7%    16.8ns ± 3%    -38.50%  (p=0.008 n=5+5)

comparing encoding/json...
  [!] SkipValue              15.6ms ± 4%      10.6ms ± 5%         -32.23%  (p=0.008 n=5+5)

# 0ns means that GCC was able to do a good joob optimizing constant expressions.
# If more complexity for these tests is added, GCC still will produce better code.
comparing image/color...
  [!] YCbCrToRGB/0         5.72ns ± 3%    0.00ns       -100.00%  (p=0.008 n=5+5)
  [!] YCbCrToRGB/128       5.73ns ± 3%    0.00ns       -100.00%  (p=0.008 n=5+5)
  [!] YCbCrToRGB/255       5.98ns ± 3%    0.00ns       -100.00%  (p=0.008 n=5+5)
  [!] RGBToYCbCr/0         6.07ns ± 5%    0.00ns       -100.00%  (p=0.008 n=5+5)
  [!] RGBToYCbCr/Cb        6.17ns ± 6%    0.00ns       -100.00%  (p=0.008 n=5+5)
  [!] RGBToYCbCr/Cr        6.22ns ± 6%    0.00ns       -100.00%  (p=0.008 n=5+5)
  [!] YCbCrToRGBA/0        6.54ns ± 5%    0.34ns ± 4%   -94.77%  (p=0.008 n=5+5)
  [!] YCbCrToRGBA/128      6.08ns ± 4%    0.34ns ± 4%   -94.48%  (p=0.008 n=5+5)
  [!] YCbCrToRGBA/255      6.46ns ± 5%    0.35ns ± 5%   -94.52%  (p=0.008 n=5+5)
  [!] NYCbCrAToRGBA/0      8.82ns ± 3%    0.34ns ± 7%   -96.19%  (p=0.008 n=5+5)
  [!] NYCbCrAToRGBA/128    7.69ns ± 5%    0.37ns ± 2%   -95.24%  (p=0.008 n=5+5)
  [!] NYCbCrAToRGBA/255    8.41ns ± 2%    0.33ns ± 2%   -96.11%  (p=0.000 n=5+4)

comparing image/gif...
  [+] QuantizedEncode     761ms ± 4%     415ms ± 1%  -45.41%  (p=0.008 n=5+5)

comparing image/jpeg...
  FDCT                 1.64µs ± 3%    0.81µs ± 7%   -50.37%  (p=0.008 n=5+5)
  IDCT                 1.64µs ± 4%    0.97µs ±14%   -40.40%  (p=0.008 n=5+5)

comparing image/png...
  [!] Paeth                  4.43ns ± 5%    0.00ns       -100.00%  (p=0.008 n=5+5)

comparing math...
  [!] Erf                    10.5ns ± 8%     6.6ns ± 5%   -36.54%  (p=0.008 n=5+5)
  [!] Erfc                   11.8ns ± 4%     7.4ns ± 2%   -37.44%  (p=0.008 n=5+5)
  [~] Floor                  2.32ns ± 2%    1.71ns ± 1%   -26.21%  (p=0.008 n=5+5)
  [~] Max                    4.06ns ± 4%    2.76ns ± 2%   -32.05%  (p=0.008 n=5+5)
  [~] Frexp                  7.07ns ± 7%    3.78ns ± 4%   -46.55%  (p=0.008 n=5+5)
  [~] Gamma                  18.9ns ± 4%     9.4ns ± 7%   -50.06%  (p=0.008 n=5+5)
  [~] Ilogb                  5.95ns ± 6%    3.06ns ± 2%   -48.64%  (p=0.008 n=5+5)
  [~] Lgamma                 18.8ns ± 4%    11.1ns ± 6%   -41.08%  (p=0.008 n=5+5)
  [~] Logb                   6.02ns ± 5%    4.16ns ± 5%   -30.94%  (p=0.008 n=5+5)
  [~] Log2                   9.28ns ± 4%    5.21ns ± 3%   -43.83%  (p=0.008 n=5+5)
  [!] Modf                   5.60ns ± 4%    2.77ns ± 2%   -50.64%  (p=0.008 n=5+5)
  [~] Sincos                 21.3ns ± 4%    10.5ns ± 0%   -50.70%  (p=0.000 n=5+4)
  [!] SqrtIndirectLatency    7.44ns ± 2%    3.45ns ± 3%   -53.59%  (p=0.008 n=5+5)

comparing math/big...
  [?] BitLen/0              2.97ns ± 3%    0.72ns ± 5%    -75.61%  (p=0.008 n=5+5)
  [?] BitLen/1              2.00ns ± 3%    0.71ns ± 2%    -64.60%  (p=0.008 n=5+5)
  [?] BitLen/2              1.97ns ± 2%    0.72ns ± 4%    -63.48%  (p=0.008 n=5+5)
  [?] BitLen/3              2.00ns ± 0%    0.71ns ± 7%    -64.40%  (p=0.016 n=4+5)
  [?] BitLen/4              1.97ns ± 3%    0.72ns ± 6%    -63.49%  (p=0.008 n=5+5)
  [?] BitLen/5              1.99ns ± 3%    0.70ns ± 5%    -64.69%  (p=0.008 n=5+5)
  [?] BitLen/8              1.98ns ± 2%    0.72ns ± 7%    -63.57%  (p=0.008 n=5+5)
  [?] BitLen/9              1.97ns ± 2%    0.70ns ± 5%    -64.19%  (p=0.008 n=5+5)
  [?] BitLen/16             1.99ns ± 1%    0.67ns ± 5%    -66.53%  (p=0.008 n=5+5)
  [?] BitLen/17             1.97ns ± 2%    0.66ns ± 6%    -66.43%  (p=0.008 n=5+5)
  [?] BitLen/31             1.99ns ± 2%    0.67ns ± 3%    -66.36%  (p=0.008 n=5+5)

comparing math/cmplx...
  [!] Conj     0.36ns ± 6%    0.00ns        -100.00%  (p=0.008 n=5+5)

comparing math/rand...
  [!] Int63Unthreadsafe    8.30ns ± 4%    4.76ns ± 4%   -42.69%  (p=0.008 n=5+5)
  [!] Intn1000             21.0ns ± 4%     4.9ns ± 5%   -76.60%  (p=0.008 n=5+5)
  [!] Int63n1000           31.9ns ± 0%     4.8ns ± 4%   -84.85%  (p=0.016 n=4+5)
  [!] Int31n1000           17.7ns ± 4%     4.9ns ± 6%   -72.14%  (p=0.008 n=5+5)
  [!] Float32              15.6ns ± 5%     6.0ns ± 4%   -61.17%  (p=0.008 n=5+5)
  [!] Float64              11.8ns ± 5%     5.5ns ± 3%   -53.15%  (p=0.008 n=5+5)
  [+] Read1000             2.58µs ± 5%    1.72µs ± 3%   -33.50%  (p=0.008 n=5+5)

comparing mime/quotedprintable...
  [!] Writer    6.97µs ± 6%    4.92µs ± 6%  -29.46%  (p=0.008 n=5+5)

regexp/syntax...
  [!] EmptyOpContext     229ns ± 6%      21ns ± 3%  -90.66%  (p=0.008 n=5+5)
```

### Section B - throughput. mb/sec

```
comparing bytes...
  [!] IndexBytePortable/32     1.03GB/s ± 7%   2.13GB/s ± 4%       +106.47%  (p=0.008 n=5+5)
  [+] IndexBytePortable/4K     2.06GB/s ± 6%   2.94GB/s ± 5%        +42.87%  (p=0.008 n=5+5)
  [+] IndexBytePortable/4M     2.12GB/s ± 3%   2.96GB/s ± 4%        +39.49%  (p=0.008 n=5+5)
  [+] IndexBytePortable/64M    1.98GB/s ± 3%   2.75GB/s ± 6%        +38.78%  (p=0.008 n=5+5)

comparing crypto/des...
  [+] Encrypt  14.7MB/s ± 5%  21.3MB/s ± 3%  +44.42%  (p=0.008 n=5+5)
  [+] Decrypt  14.8MB/s ± 4%  21.2MB/s ± 4%  +43.24%  (p=0.008 n=5+5)

comparing encoding/binary...
  [!] PutUvarint32           146MB/s ± 7%   238MB/s ± 3%    +62.50%  (p=0.008 n=5+5)
  [!] PutUvarint64           104MB/s ± 5%   134MB/s ± 4%    +29.36%  (p=0.008 n=5+5)

comparing encoding/json...
  [!] SkipValue              15.6ms ± 4%      10.6ms ± 5%         -32.23%  (p=0.008 n=5+5)
  [!] SkipValue             126MB/s ± 4%     188MB/s ± 4%         +49.44%  (p=0.008 n=5+5)

comparing image/gif...
  [+] QuantizedEncode  1.62MB/s ± 4%  2.96MB/s ± 2%  +82.82%  (p=0.008 n=5+5)
```

### Section C - allocations.

```
comparing container/heap...
  [+] Dup      20.0k ± 0%     10.0k ± 0%  -50.00%  (p=0.008 n=5+5)

comparing encoding/binary...
  [+] ReadSlice1000Int32s       3.00 ± 0%      2.00 ± 0%    -33.33%  (p=0.008 n=5+5)
  [+] ReadInts                  8.00 ± 0%      4.00 ± 0%    -50.00%  (p=0.008 n=5+5)
  [+] WriteInts                 16.0 ± 0%       8.0 ± 0%    -50.00%  (p=0.008 n=5+5)
  [+] WriteSlice1000Int32s      3.00 ± 0%      2.00 ± 0%    -33.33%  (p=0.008 n=5+5)

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
  [!] EncodeRGBA               614k ± 0%      154k ± 0%   -74.99%  (p=0.008 n=5+5)

# GCCGO version is allocation-free
comparing unicode/utf16...
  [!] EncodeValidJapaneseChars      1.00 ± 0%      0.00        -100.00%  (p=0.008 n=5+5)
```
