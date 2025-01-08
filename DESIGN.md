1. Configure Benchmarks with the following:
   - Instance Type (Available options: 8cpu-linux-x64, 16cpu-linux-x64, 32cpu-linux-x64)
   - Programs (Comma-separated list of programs to benchmark)
   - Benchmark Docker Image Tag
   - Prover (sp1 or risc0)
   - Use Cache (whether to use GitHub Actions Rust cache)
2. Run Benchmark
   - Start EC2 Instance (Handled by runs-on.com using compute-optimized instances)
   - Setup Rust cache if enabled
   - Pull Docker Image from registry
   - Run Benchmark for each specified program
   - Upload Results from Telemetry folder as GitHub artifact

Usage:
1. The workflow can be triggered manually from the GitHub Actions tab
2. Select the desired instance type from the dropdown (8, 16, or 32 CPU options)
3. Provide the Docker image tag
4. Enter the programs to benchmark as a comma-separated list
5. Select the prover to use (sp1 or risc0)
6. Choose whether to use Rust caching
7. Results will be available as a downloadable artifact after the workflow completes

Available Programs:
- fibonacci
- rsa
- ecdsa
- json
- regex
- sha
- tendermint
- zkquiz
- bubble_sort
- iseven (sp1 only)
