# Readme
## Introduction
Synthesizable RISC-V processor (COMET) with branch predictor
## Folder structure
```
.
+-- src/    
|   +--simulate/
|   |--synthesize/
|
+-- impl_test/
|
|
+-- README.md
|
+-- LICENSE
```

## Build Setup
### Environment
* Vivado HLS 2019.2
* GCC
* CMake
* GNU Make
* riscv-gnu-toolchain
### Cloning this repo
* Clone this repo and all of submodules
```
$ git clone --recursive https://github.com/s950449/Comet_With_Branch_Predictor.git
```
In Project Directory
### Building Simulator
```
$ cd src/simulate/
$ mkdir build
$ cd build
$ cmake ..
$ make
```
Use `$ ./src/simulate/build/bin/comet.sim --file <test_file.riscv32>` to execute simulator
* Modify `using BranchPredictor = <branch-predictor-type>`
 in `./src/simulate/include/branchPredictor.h` before compiling to use different branch predictor. 
* Branch Predictor Type
    * BitBranchPredictor <BITS,ENTRIES>
    * PerceptronBranchPredictor <SIZE,BITS,ENTRIES,THRESHOLD,LR>
    * PerceptronBranchPredictorV2 <SIZE,BITS,ENTRIES,THRESHOLD,LR>
### Synthesize 
```
$ cd src/synthesize/synthesizable/vivado
$ vivado_hls -f script.tcl
```
Then we finally generate a Vivado IP under `./src/synthesize/synthesizable/vivado/doCore`
* Modify `using BranchPredictor = <branch-predictor-type>`
 in `./src/synthesize/synthesizable/include/branchPredictor.h` before compiling to use different branch predictor. 
* Branch Predictor Type
    * BitBranchPredictor <BITS,ENTRIES>
    * PerceptronBranchPredictor <SIZE,BITS,ENTRIES,THRESHOLD,LR>
    * PerceptronBranchPredictorV2 <SIZE,BITS,ENTRIES,THRESHOLD,LR>

## Test Files
* Test file is under `tests/`(symbolic link points to `src/simulate/tests/basic_tests`)
* Use simulator with those riscv32 files in `tests/`
## Reference
* [What You Simulate Is What You Synthesize: Designing a Processor Core from C++ Specifications](https://hal.archives-ouvertes.fr/hal-02303453/document)
* [A new organization for a perceptron-based branch predictor and its FPGA implementation](https://ieeexplore.ieee.org/document/1430166)
* [RISC-V CPU in HLS](https://www.hanselmandrew.com/projects/risc-v-cpu-in-hls)
* [HL5: A 32-bit RISC-V Processor Designed with High-Level Synthesis](https://www.inf.pucrs.br/~calazans/graduate/SDAC/saltos.pdf)
* [Two-Level Adaptive Training Branch Prediction RISC-V-On-PYNQ](https://github.com/drichmond/RISC-V-On-PYNQ)

## LICENSE

The project is under MIT License.
