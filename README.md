# ZKRust Benchmarks

This repository contains GitHub Actions workflows for running ZKRust benchmarks on various instance sizes using runs-on.com.

## Running Benchmarks

The benchmarks can be run through the GitHub Actions interface:

1. Navigate to the "Actions" tab in the repository
2. Select the "Run Benchmarks" workflow
3. Click "Run workflow"
4. Fill in the following parameters:

### Configuration Options

#### Instance Families
Choose which AWS instance families to benchmark (comma-separated):
- `c7i`: Latest generation Intel compute optimized
- `c7a`: Latest generation AMD compute optimized
- `m7i`: Latest generation Intel general purpose
- `m7a`: Latest generation AMD general purpose

Default: `c7i,c7a`

#### CPU Sizes
Specify which CPU sizes to benchmark (comma-separated). Available sizes:
- `8`: 8 CPU cores
- `16`: 16 CPU cores
- `32`: 32 CPU cores
- `64`: 64 CPU cores (default)
- `96`: 96 CPU cores (where available)

For example:
- `64` (default): Only run on 64 CPU instances
- `32,64`: Run on both 32 and 64 CPU instances
- `8,16,32,64,96`: Run on all available CPU sizes

The workflow will run benchmarks on each CPU size for each selected family. For example, with:
- Instance Families: `c7i,m7i`
- CPU Sizes: `32,64`

The workflow will benchmark:
- c7i: 32 and 64 CPU variants
- m7i: 32 and 64 CPU variants

All instances use spot pricing for cost efficiency.

#### Docker Tag
Specify which version of the zkRust image to use (e.g., `latest`, `v1.0.0`). Images are pulled from `ghcr.io/prooflabdev/zkrust`. Defaults to `main`.

#### Programs
Enter a comma-separated list of programs to benchmark. Available programs:
- `fibonacci`: Fibonacci sequence computation
- `rsa`: RSA encryption/decryption
- `ecdsa`: Elliptic Curve Digital Signature Algorithm
- `json`: JSON parsing and validation
- `regex`: Regular expression matching
- `sha`: SHA hash computation
- `tendermint`: Tendermint consensus
- `zkquiz`: ZK Quiz application
- `bubble_sort`: Bubble sort algorithm
- `iseven`: Simple even number check (SP1 only)

Example: `fibonacci,rsa,ecdsa`

#### Prover
Select the proving system to use:
- `sp1`: SP1 prover
- `risc0`: RISC0 prover

#### Use Cache
Enable or disable Rust caching:
- `true`: Cache Rust dependencies between runs (faster subsequent runs)
- `false`: Clean build every time (useful for clean benchmarks)

### Results

After the workflow completes:
1. Go to the workflow run
2. Download the "benchmark-results" artifact
3. The telemetry data will be in the downloaded zip file

## Technical Details

- Uses runs-on.com for dynamic instance provisioning
- Mounts cargo cache volumes when caching is enabled
- Pulls images from GitHub Container Registry
- Stores results in the telemetry directory
- Uses compute-optimized instances for better performance
- Leverages spot instances for cost optimization

## Example Usage

To benchmark fibonacci and RSA on SP1 with a 16-core instance:
1. Select `16cpu-linux-x64` as Instance Type
2. Enter `fibonacci,rsa` in Programs
3. Select `sp1` as Prover
4. Choose whether to use caching
5. Click "Run workflow"

## Notes

- The iseven program is only available for the SP1 prover
- Larger instance types will generally complete faster but cost more
- Using cache can significantly speed up subsequent runs but may affect benchmark accuracy
- All benchmarks are run with telemetry enabled 