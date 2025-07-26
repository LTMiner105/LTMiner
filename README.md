# LTMiner

## Abstract

LTMiner (Long Tail Miner) aims to mine rare patterns from large-scale software systems and check their violations to detect potential bugs. By leveraging large code models and word embeddings, we rank and filter violations of rare patterns based on contextual semantics, highlighting the interesting ones.

## Data

There are eight HTML file in the DataShare.zip. They are the Linux Kernel bug reports in eight different pattern support levels. Each report contains multipel pattern violations. The key elements in the bug report are shown as follow.

- ***vio-rank***: The rank of a pattern violation based on contextual semantics. Those without a vio-rank is the false positives found by antonym functions identification and variant functions identification.
- ***pattern***: The code pattern which the violation breaks.
- ***#violation***: Information about the function containing the violation.
- ***missing_pattern***: The code pattern elements omitted in the violation.
- ***covered_pattern***: The code pattern elements covered in the violation.
- ***vio_func_name***: The name of the function containing the violation.
- ***# most_similar_sup_func***: Information about the function that support the code pattern.


## SourceCode

### Environment

LTMiner is developed based on Ubuntu 22.04, Python 3.10 and LLVM-14. The python environment can be prepared with `pip install -r requirements.txt`.

### Configuration

Before runing this tool, you must complete the configuration in the main.py. The parameter needed to config are shown as follow.

- ***proj_name***: The label of test batch.
- ***datashare_dir***: The absolute path of the 'DataShare' directory, e.g., "<your_workspace_path>/DataShare"
- ***code_dir***: The absolute path of the 'Code' directory, e.g.,"<your_workspace_path>/Code/"
- ***kernel_dir***: The absolute path of the targeted Linux kernel with prepared bitcode files(.bc), e.g.,"<your_workspace_path>/DataShare/LinuxKernel/linux-6.12.1"
- ***fpclose_dir***: The absolute path of the 'FPclose' tool directory, e.g.,"<your_workspace_path>/Code/utils/fpclose/fim_closed"
- ***we_model_name***: The name of the word embedding model.
- ***result_file***: The absolute path of the result file.
- ***support_filter***: The pattern support of the test batch

Now, you can run the tool with 'python3 main.py'.