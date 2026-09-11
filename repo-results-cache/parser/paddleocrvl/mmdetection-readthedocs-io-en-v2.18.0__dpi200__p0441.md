mmdet.models.utils.gaussian_radius(det_size, min_overlap)

Generate 2D gaussian radius.

This function is modified from the official github repo.

Given min_overlap, radius could be computed by a quadratic equation according to Vieta's formulas.

There are 3 cases for computing gaussian radius, details are following:

• Explanation of figure: It and br indicates the left-top and bottom-right corner of ground truth box. x indicates the generated corner at the limited position when radius=r.

• Case1: one corner is inside the gt box and the other is outside.

| < width > |

lt++++
| | | |
+--x+++
| | | | |
| | | | | height
| | overlap | |
| | | | |
| | | | |
| | | | | v
+--br-+
| | | |
+--x+++

To ensure IoU of generated box and gt box is larger than min_overlap:

 $$ \begin{aligned}\frac{(w-r)*(h-r)}{w*h+(w+h)r-r^{2}}&\geq iou\quad\Rightarrow\quad r^{2}-(w+h)r+\frac{1-iou}{1+iou}*w*h\geq0\\a=1,\quad b=-(w+h),\quad c&=\frac{1-iou}{1+iou}*w*hr\leq\frac{-b-\sqrt{b^{2}-4*a*c}}{2*a}\end{aligned} $$ 

• Case2: both two corners are inside the gt box.


<table border=1 style='margin: auto; word-wrap: break-word;'><tr><td style='text-align: center; word-wrap: break-word;'>| &lt; width &gt; |</td></tr><tr><td style='text-align: center; word-wrap: break-word;'>lt-+----+</td></tr><tr><td style='text-align: center; word-wrap: break-word;'>| | |</td></tr><tr><td style='text-align: center; word-wrap: break-word;'>+---x----+ |</td></tr><tr><td style='text-align: center; word-wrap: break-word;'>| | | | |</td></tr><tr><td style='text-align: center; word-wrap: break-word;'>| | | |</td></tr><tr><td style='text-align: center; word-wrap: break-word;'>| | | |</td></tr><tr><td style='text-align: center; word-wrap: break-word;'>| +----x--+</td></tr><tr><td style='text-align: center; word-wrap: break-word;'>| | |</td></tr><tr><td style='text-align: center; word-wrap: break-word;'>+----+br</td></tr></table>

To ensure IoU of generated box and gt box is larger than min_overlap:

 $$ \begin{aligned}\frac{(w-2*r)*(h-2*r)}{w*h}&\geq iou\quad\Rightarrow\quad4r^{2}-2(w+h)r+(1-iou)*w*h\geq0\\a&=4,\quad b=-2(w+h),\quad c=(1-iou)*w*hr\leq\frac{-b-\sqrt{b^{2}-4*a*c}}{2*a}\end{aligned} $$ 

• Case3: both two corners are outside the gt box.