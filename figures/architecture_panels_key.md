| Label | Description |
| --- | --- |
| L12 | Nearest neighbor upsampling by a factor of 2; output 40 × 24 × 256 |
| L13 | Channel concatenation of L12, L7; output 40 × 24 × 384 |
| L14 | C3k2; output 40 × 24 × 128 |
| L15 | Nearest neighbor upsampling by a factor of 2; output 80 × 48 × 128 |
| L16 | Channel concatenation of L15, L5; output 80 × 48 × 256 |
| L17 | C3k2; output 80 × 48 × 64 |
| L18 | 3×3 convolution, stride 2, followed by BatchNorm and SiLU; output 40 × 24 × 64 |
| L19 | Channel concatenation of L18, L14; output 40 × 24 × 192 |
| L20 | C3k2; output 40 × 24 × 128 |
| L21 | 3×3 convolution, stride 2, followed by BatchNorm and SiLU; output 20 × 12 × 128 |
| L22 | Channel concatenation of L21, L11; output 20 × 12 × 384 |
| L23 | C3k2; output 20 × 12 × 256 |
| P3, P4, P5 | Neck outputs L17, L20, L23; strides 8, 16, 32 |
| T0, T1, T2 | Independent temporal processing at strides 8, 16, 32 |
| T*.0 | Concatenate previous, current, and next features along channels |
| T*.1 | 1×1 convolution, BatchNorm, SiLU; reduce 3C to C channels |
| T*.2 | No extra operation for 1×1 only; spatial block or C3k2 for other variants |
| F0, F1, F2 | Features supplied to the head after temporal processing |
| L24.1.B, L24.2.B, L24.3.B | Box regression subnetworks, shown by their 64 channel outputs (four distributions with 16 bins each) |
| L24.1.C, L24.2.C, L24.3.C | Classification subnetworks, shown by their 80 channel outputs |
| R0, R1, R2 | Decode boxes and apply sigmoid to class logits; 84 values per location |
| D0 | Combine predictions across resolutions, select person scores, and apply confidence filtering and nonmaximum suppression |
