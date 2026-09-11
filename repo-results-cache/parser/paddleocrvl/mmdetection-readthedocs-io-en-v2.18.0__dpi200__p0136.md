## MISCELLANEOUS

### 27.1 Evaluating a metric

tools/analysis_tools/eval_metric.py evaluates certain metrics of a pkl result file according to a config file.

python tools/analysis_tools/eval_metric.py ${CONFIG} ${PKL_RESULTS} [-h] [--format-only] [--eval ${EVAL[EVAL...]]]
[--cfg-options ${CFG_OPTIONS [CFG_OPTIONS...]}]
[--eval-options ${EVAL_OPTIONS [EVAL_OPTIONS...]]]

### 27.2 Print the entire config

tools/misc/print_config.py prints the whole config verbatim, expanding all its imports.

python tools/misc/print_config.py ${CONFIG} [-h] [--options ${OPTIONS [OPTIONS...]}]