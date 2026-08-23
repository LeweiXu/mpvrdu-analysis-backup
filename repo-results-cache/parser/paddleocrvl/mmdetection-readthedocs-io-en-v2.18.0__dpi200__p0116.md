## LOG ANALYSIS

tools/analysis_tools/analyze_logs.py plots loss/mAP curves given a training log file. Run pip install seaborn first to install the dependency.

python tools/analysis_tools/analyze_logs.py plot_curve [--keys ${KEYS}] [--title ${TITLE}]
[--legend ${LEGEND}] [--backend ${BACKEND}] [--style ${STYLE}] [--out ${OUT_FILE}]

<div style="text-align: center;"><img src="imgs/img_in_chart_box_207_829_1316_1698.jpg" alt="Image" width="65%" /></div>


Examples:

• Plot the classification loss of some run.


<table border=1 style='margin: auto; word-wrap: break-word;'><tr><td style='text-align: center; word-wrap: break-word;'>python tools/analysis_tools/analyze_logs.py plot_curve log.json --keys loss_cls --legend loss_cls</td></tr></table>

• Plot the classification and regression loss of some run, and save the figure to a pdf.