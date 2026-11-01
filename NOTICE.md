# NOTICE: what is simulation and what is CMS Run-3 data

**HL-LHC (right-hand panels): all simulation.**
- Background and signal are simulated HL-LHC crossings at pile-up 200.
- The Level-1 stage is emulated at the design thresholds, with its rate scaled to the design value.
- The HLT output of 7.5 kHz is the design figure, not a measured one.
- Every HL-LHC number is a property of that simulation.

**Run 3 (left-hand panels): recorded background, simulated signal.**
- The background is CMS Run 3 recorded zero-bias crossings: 8,355,050 crossings from two runs.
- Rates and thresholds are therefore set on real data, and f_l1_pct is a percent of the Level-1 accept rate those crossings
  record.
- The signal families are simulated events processed through the Level-1 emulation, so captures are simulated signal measured
  against a real-data threshold.
- The standard trigger is the Level-1 menu emulated on the recorded crossings at its CMS thresholds.
- AXOL1TL is the anomaly-detection score of the Level-1 trigger, evaluated in emulation on the same inputs.

**H to aa to 4b (ma = 15 GeV)**
- This sample is simulation without pile-up, overlaid on a real zero-bias crossing.
- It is never used in training and is reported apart from the averages on both samples.

**Not an official result**
- The numbers here are a study in progress.
- They have not been reviewed or approved by the CMS Collaboration and are not CMS results.
