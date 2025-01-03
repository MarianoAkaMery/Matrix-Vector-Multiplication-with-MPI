# Matrix-Vector Multiplication with MPI

This repository is part of the `features2` module in the `matvet-team-10` project. It implements matrix-vector multiplication using MPI (Message Passing Interface) to parallelize the computation, enhancing performance and scalability.

## What It Does

### Initialization
- A random matrix (A) and vector (x) are created on the main process (rank 0).
- The matrix and vector are distributed to all processes using `MPI_Bcast`.

### Parallel Computation
- Matrix rows are split among the processes.
- Each process computes the dot products for its assigned rows with the vector.

### Gathering Results
- Results from all processes are combined using `MPI_Reduce`.

### Testing
- Both row-major and column-major layouts are tested for performance and correctness.
- Computation times for each layout are measured.

## Why Use MPI?
- **Scalability**: Supports larger matrices by leveraging multiple processes and machines.
- **Efficiency**: Parallel computation reduces processing time.
- **Optimization**: Minimizes inter-process communication delays with MPI.

## Repository Structure
- `src/main_Pmatrix.cpp`: The main program that implements matrix-vector multiplication.
- `src/MatrixTest.hpp`: Header file defining the `MatrixTest` class.
- `examples/`: Directory for sample test cases and outputs.
- `Makefile`: Simplifies the compilation process.

## Compilation
To compile the program, use:
```bash
make
```

## Running the Program
Default execution:
```bash
./main_Pmatrix --dense
```

Specify the number of MPI processes:
```bash
mpirun -n <number_of_processes> ./main_Pmatrix --dense
```

Example:
```bash
mpirun -n 4 ./main_Pmatrix --dense
```

## Example Output
Row-Major Test:
```
Final result vector y: [290, 321, 308, ...]
Computation time: 7.851e-06 seconds
```

Column-Major Test:
```
Final result vector y: [290, 321, 308, ...]
Computation time: 5.579e-06 seconds
```

## Performance Notes
- **Correctness**: Both row-major and column-major tests produce identical results.
- **Computation Time**: Column-major layout demonstrates slightly better performance, potentially due to better cache utilization.

## How It Works
- The `MatrixTest` class handles matrix initialization, computation, and testing.
- Parallelism is achieved through MPI functions like `MPI_Bcast` and `MPI_Reduce`.
