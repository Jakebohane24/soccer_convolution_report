| Layer | Block | Output (width × height × channels) | Description |
| --- | --- | --- | --- |
| Input | RGB image | 640 × 384 × 3 | One video frame |
| L0 | Conv | 320 × 192 × 16 | 3×3 convolution, stride 2; BatchNorm and SiLU |
| L1 | Conv | 160 × 96 × 32 | 3×3 convolution, stride 2; BatchNorm and SiLU |
| L2 | C3k2 | 160 × 96 × 64 | C3k2 with a bottleneck branch |
| L3 | Conv | 80 × 48 × 64 | 3×3 convolution, stride 2; BatchNorm and SiLU |
| L4 | C3k2 | 80 × 48 × 128 | C3k2 with a bottleneck branch; also passed to the neck |
| L5 | Conv | 40 × 24 × 128 | 3×3 convolution, stride 2; BatchNorm and SiLU |
| L6 | C3k2 | 40 × 24 × 128 | C3k2 with a C3k branch; also passed to the neck |
| L7 | Conv | 20 × 12 × 256 | 3×3 convolution, stride 2; BatchNorm and SiLU |
| L8 | C3k2 | 20 × 12 × 256 | C3k2 with a C3k branch |
| L9 | SPPF | 20 × 12 × 256 | Repeated spatial max pooling |
| L10 | C2PSA | 20 × 12 × 256 | Feature processing with partial self attention; also passed to the neck |
