# LTMiner

## Abstract

LTMiner (Long Tail Miner) aims to mine rare patterns from large-scale software systems and check their violations to detect potential bugs. By leveraging large code models and word embeddings, we rank and filter violations of rare patterns based on contextual semantics, highlighting the interesting ones. This project contain two files as follows.

## Result Data (Result.zip)

There are eight HTML files in the Result.zip. They are the Linux Kernel bug reports in eight different pattern support levels. Each report contains corresponding pattern violations. The key elements in the bug report are shown as follows.

- ***vio-rank***: The rank of a pattern violation based on contextual semantics. Those without a vio-rank are the false positives found by antonym functions or variant functions detection.
- ***pattern***: The code pattern which the violation breaks.
- ***#violation***: Information about the function containing the violation.
- ***missing_pattern***: The code pattern elements omitted in the violation.
- ***covered_pattern***: The code pattern elements covered in the violation.
- ***vio_func_name***: The name of the function containing the violation.
- ***# most_similar_sup_func***: Information about the function that supports the code pattern.


## SourceCode (LTMiner.zip)

### Environment

LTMiner is developed on Ubuntu 22.04, Python 3.10 and LLVM-14.0.6. You can set up the Python environment using `pip install -r requirements.txt`.

### Configuration

Before running this tool, you must complete the configuration in main.py. The parameter needed to config are as follows：

- ***proj_name***: The label of test batch.
- ***kernel_dir***: The absolute path of the targeted Linux kernel with prepared bitcode files(.bc), e.g.,"<your_workspace_path>/DataShare/LinuxKernel/linux-6.12.1".
- ***we_model_name***: The name of the word embedding model.
- ***support_filter***: The pattern support threshold for the test batch.
- ***result_file***: The absolute path of the result file. It is an optional parameter, the default value is "Rules/proj_name" dir.

Now, you can run the tool by executing `python3 main.py`.

