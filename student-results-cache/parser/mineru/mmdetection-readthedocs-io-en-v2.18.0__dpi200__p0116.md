CHAPTER
EIGHTEEN
LOG ANALYSIS
tools/analysis.tools/analyze_logs.py plots loss/mAP curves given a training log file. Run pip install
seaborn first to install the dependency.
python tools/analysis.tools/analyze_logs.py plot_structure [--keys ${KEYS}] [--title ${TITLE} ]
--] [--legend ${LEGEND}] [--frontend ${BACKEND}] [--style ${STYLE}] [--out ${OUT_FILE}]