## Introduction

This repository contains code for getting automatic evaluation results as reported for the WebnLG+ 2020 Shared Task: bleu, nltk-bleu, meteor, ter, chrf++, bertScore and bleurt. It uses the original codes of Thiago Castro Ferreira (metrics) and Anastasia Shimorina (data), with some minor modifications for it to run on Colab.

- Information about WebNLG+ can be found on the challenge website (https://synalp.gitlabpages.inria.fr/webnlg-challenge/challenge_2020/);
- The data is available on GitLab (https://gitlab.com/shimorina/webnlg-dataset/-/tree/master/release_v3.0);
- The evaluation scripts, submissions and evaluation results on GitHub (https://github.com/WebNLG).

## Important note on BLEURT
The provided code allows for reproducing exactly the scores reported in the Shared Task report except for BLEURT, for which the scores are slightly lower. When running the original evaluation code, an error was thrown for BLEURT, stating that the scorer does not take positional arguments; the line that calls the scorer was modified accordingly to flag the arguments for reference and candidate files. It remains to be verified if this could affect the scoring.

## Quick instructions to run the evaluation on Colab
1. Select a GPU runtime (needed for bertScore and bleurt; it should be the runtime by default).
2. Run the first cell.
3. Drag the file(s) you want to evaluate in the “hypotheses” folder, located directly in the */content/* folder on the leftside.
4. Run the second cell.
5. Run the third cell.
6. Run the fourth cell.
7. Gather results in */content/log_eval_InputFileName.txt*.

It takes about 15 minutes (+/- 5 min) to evaluate one output file in English (1,779 texts) with all metrics, and about 3 minutes (+/- 1 min) without TER.

**Cell#1**: to download and install metrics, download data and original code, clone repos, install python dependencies.<br>
**Cell#2**: to create a slightly modififed version of the evaluation and reference data creation codes.<br>
**Cell#3**: to create files with the reference texts. There are up to 5 references for each input triple set, each file contains one reference for a given input (5 files in total for English, 3 for Russian).<br>
**Cell#4**: to run the evaluation; the parameter *small_test='yes'* allows for testing the code on a small dataset of 10 texts.

## Input specifications

In the following, the specifications for the files that contains the texts to evaluate; they are exactly the same as for the WebNLG+ shared task (https://synalp.gitlabpages.inria.fr/webnlg-challenge/challenge_2020/#submissions). In a nutshell, in each file:

1. Should be encoded in **utf-8 without BOM**.
2. Should have the **.txt extension**.
3. Should contain **true-cased** and **detokenised** text.
4. Shoud contain **one text per line**:
  - each line corresponds to one output;
  - the outputs must be in the **same order** as the input file;
  - if there is no output for an input, the line should be **empty** (only linebreak);
  - unless there is no output for the last input, the file should NOT end with a linebreak (so the last line contains a text instead of being empty).


For instance, the **English file** must contain **1,779 lines** as the following two:

Aaron Turner plays Post-metal and electric guitar and played with Lotus Eaters. He was active from 1995.<br>
English Without Tears, released on July 28, 1944, has a runtime of 89. Nicholas Brodszky composed its music.
