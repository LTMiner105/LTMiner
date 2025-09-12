# LTMiner

## Abstract

LTMiner (Long Tail Miner) aims to mine rare patterns from large-scale software systems and check their violations to detect potential bugs. By leveraging large code models and word embeddings, we rank and filter violations of rare patterns based on contextual semantics, highlighting the interesting ones. This project contain three ziped files as follows.

## Result (Result.zip)

There are eight HTML files in the Result.zip. They are the Linux Kernel bug reports in eight different pattern support levels. Each report contains corresponding pattern violations. The key elements in the bug report are shown as follows.

- ***vio-rank***: The rank of a pattern violation based on contextual semantics. Those without a vio-rank are the false positives found by antonym functions or variant functions detection.
- ***pattern***: The code pattern which the violation breaks.
- ***#violation***: Information about the function containing the violation.
- ***missing_pattern***: The code pattern elements omitted in the violation.
- ***covered_pattern***: The code pattern elements covered in the violation.
- ***vio_func_name***: The name of the function containing the violation.
- ***# most_similar_sup_func***: Information about the function that supports the code pattern.

## Target Project (linux-6.12.1)

We use the Linux Kernel v6.12.1 as the target project. LTMiner processes LLVM pass on bitcode files(*.bc) to detect bugs. However, we failed to upload all the bitcode files since it is extremely large in size (**19.38GB**). Therefore, we recommand you that use WLLVM to compile the kernel and get the bitcode files. You can conduct WLLVM using following commands:

```
pip install wllvm
export LLVM_COMPILER=clang
make CC=clang allyesconfig
make CC=wllvm LLVM=1
```

## SourceCode and Data (LTMiner.zip)

### Directory Structure

+ LTMiner
    + Code
        + LLM
        + Pass
        + RuleGen
        + utils
    + DataShare
        + Model
        + Passresult
        + Rules

As shown below, LTMiner contain two main sub-directory: Code and DataShare. All the souce code files of LTMiner are in Code directory, and all the intermediate data files are in DataShare directory.

In Code directory:
- **LLM** contains prompt template file.
- **Pass** contains LLVM pass that is used to generate DDGs.
- **RuleGen** contains data processing and violation detection programes.
- **utils** contains fp-close mining programe.

In DataShare directory:
- **Model** contains the word embedding model.
- **Passresult** contains the result of LLVM pass.
- **Rules** contains patterns and violations. 

### Prepare Environment

LTMiner is developed on Ubuntu 22.04, Python 3.10 and LLVM-14.0.6. You can set up the Python environment using `pip install -r requirements.txt`.

### Configuration

Before running this tool, you must complete the configuration in Code/RuleGen/main.py. The parameter needed to config are as follows:

- ***proj_name***: The label of test batch.
- ***kernel_dir***: The absolute path of the targeted Linux kernel with prepared bitcode files(.bc), e.g.,"<your_workspace_path>/DataShare/LinuxKernel/linux-6.12.1".
- ***we_model_name***: The name of the word embedding model.
- ***support_filter***: The pattern support threshold for the test batch.
- ***result_file***: The absolute path of the result file. It is an optional parameter, the default value is "Rules/proj_name" dir.

Now, you can run the tool by executing `python3 main.py`. The result will be in previously defined <***result_file***>.

