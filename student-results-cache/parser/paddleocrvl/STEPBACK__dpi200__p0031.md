dataset | example
MMLU-Physics | Original Question: A 2  $ \mu $F capacitor is connected directly to a battery. When the capacitor is fully charged, it stores 600  $ \mu $C of charge. An experimenter replaces the 2  $ \mu $F capacitor with three 18  $ \mu $F capacitors in series connected to the same battery. Once the capacitors are fully charged, what charge is stored on each capacitor?
0) 100  $ \mu $C
1) 200  $ \mu $C
2) 600  $ \mu $C
3) 1800  $ \mu $C
Original Answer [Incorrect]: The answer is 100  $ \mu $C. The total capacitance of the three 18  $ \mu $F capacitors in series is 1 / (1 / 18 + 1 / 18 + 1 / 18) = 6  $ \mu $F. The charge stored on the three capacitors in series is 6  $ \mu $F * V = 600  $ \mu $C. The charge stored on each capacitor is 600  $ \mu $C / 3 = 200  $ \mu $C.
Stepback Question: What are the physics principles behind this question?
Principles:
Capacitors: Q = C * V, where Q is the charge, C is the capacitance and V is the voltage.
Capacitors in series: C = 1 / (1/C1 + 1/C2 +... + 1/Cn), where C is the equivalent capacitance and C1, C2, Cn are the capacitances of each capacitor.
Capacitor in parallel: C = C1 + C2 +... + Cn, where C is the equivalent capacitance and C1, C2, Cn are the capacitances of each capacitor.
Final Answer: Using the Principles of Capacitance and Capacitors in series, we can solve the problem as following:
Step 1: Apply Capacitance to find out the voltage of the battery.
We know that the capacitance of the 2  $ \mu $F capacitor is 2  $ \mu $F and the charge stored on the capacitor is 600  $ \mu $C. Using the formula for capacitance, we can find the voltage of the battery:
C = Q / V
2  $ \mu $F = 600  $ \mu $C / V
V = 300 V
Step 2: Apply Capacitors in series to find out the equivalent capacitance of the three 18  $ \mu $F capacitors in series.
We know that the capacitance of each of the three capacitors is 18  $ \mu $F. Using the formula for capacitors in series, we can find the equivalent capacitance of the three capacitors:
1 / C_{eq} = 1 / C_{1} + 1 / C_{2} + 1 / C_{3}
1 / C_{eq} = 1 / 18  $ \mu $F + 1 / 18  $ \mu $F + 1 / 18  $ \mu $F
1 / C_{eq} = 3 / 18  $ \mu $F
C_{eq} = 6  $ \mu $F
Step 3: Apply Capacitance to find out the charge stored on each capacitor.
We know that the equivalent capacitance of the three capacitors is 6  $ \mu $F and the voltage of the battery is 300 V. Using the formula for capacitance, we can find the charge stored on each capacitor:
C = Q / V
6  $ \mu $F = Q / 300 V
Q = 1800  $ \mu $C
Therefore, the charge stored on each capacitor is 1800  $ \mu $C. The correct answer is 3) 1800  $ \mu $C.

<div style="text-align: center;">Table 27: Illustration of wins of STEP-BACK PROMPTING on the MMLU-Physics dataset.</div>