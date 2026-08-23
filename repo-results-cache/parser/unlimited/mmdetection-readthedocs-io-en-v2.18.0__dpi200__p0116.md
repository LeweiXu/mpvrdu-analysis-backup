CHAPTER
EIGHTEEN
LOG ANALYSIS
tools/analysis_tools/analyze_logs.py plots loss/mAP curves given a training log file. Run pip install seaborn first to install the dependency.
python tools/analysis_tools/analyze_logs.py plot_curve [--keys ${KEYS}] [--title ${TITLE} --] [--legend ${LEGEND}] [--backend ${BACKEND}] [--style ${STYLE}] [--out ${OUT_FILE}]

age
Examples:
- Plot the classification loss of some run.
python tools/analysis_tools/analyze_logs.py plot_curve log.json --keys loss_cls --legend loss_cls
- Plot the classification and regression loss of some run, and save the figure to a pdf.
109