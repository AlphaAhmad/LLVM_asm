# LLVM Loop Interchange Pass

This project demonstrates a basic loop interchange optimization pass using LLVM and Rust. Loop interchange is a compiler optimization technique that swaps nested loops to improve cache locality and memory access patterns. Imagine you have two nested loops where the outer loop runs `i` times and the inner loop runs `j` times - after interchanging them, the `j` loop becomes the outer one and `i` becomes inner. The way this works is by carefully rewiring the control flow graph: we redirect the program's entry point to go into what was previously the inner loop header, then adjust all the branch instructions so that the loops' exit conditions and increment operations happen in the swapped order. Think of it like rearranging train tracks - you're changing which stations (basic blocks) connect to which other stations, but the actual code inside each station stays the same. The program reads LLVM IR from `input.txt`, identifies the nested loop structure by examining the basic blocks, performs the interchange by manipulating branch targets, and writes the transformed IR to `output.txt`. While this implementation uses stub functions for the actual branch rewiring (since the inkwell API has some limitations), it shows the overall architecture of how such an optimization pass would work in a real compiler.

## How to Run

```bash
cargo build
cargo run
```

The program will read `input.txt` (LLVM IR format) and produce `output.txt` with the before and after results.
