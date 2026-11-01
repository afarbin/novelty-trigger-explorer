# Strategy Explorer: a novelty trigger built by hashing a contrastive embedding

This page shows every capture curve we have measured for a novelty trigger at the CMS Level-1 and HLT stages. You can tick any
study in the tree of choices, compare it with the standard trigger, and recall the steps of the talk. Everything runs in the
browser and no server is needed. The data are inside the page, and a copy sits beside it as plain JSON for anyone who wants to
read the numbers directly.

## The three elements

1. **Novelty trigger.** A small share of the trigger budget, f, goes to crossings that are rare relative to the background
   recently recorded, whatever their physics content. The standard menu keeps the rest of the budget.
2. **Hashing.** Rarity is estimated by counting cells. Each crossing is placed in a cell by random hyperplanes, giving b bits in
   each of T tables (written b x T, for example 14 x 20). A crossing whose cells are rarely occupied by the background is kept.
   We compare this against fitted densities (a Gaussian, a Gaussian mixture, nearest neighbours, kernels) and against classifiers
   on the same inputs.
3. **Contrastive embedding.** An encoder trained so that physics-similar crossings land close together gives the representation
   that hashing acts on. We compare it with the menu inputs themselves and with other learned representations: an autoencoder's
   latent or the AXOL1TL representation, and a classifier's output mapped onto the square-root softmax sphere.

## How to read a panel

- **Run 3 is on the left and HL-LHC on the right**, always with the same variants side by side. When a study was not run on one
  of them, the panel says so.
- **Standalone capture**: the share of signal events the novelty trigger alone keeps at budget f. The standard trigger at the
  same budget is drawn as the constant reference curve.
- **Unique capture**: the signal the novelty trigger keeps that the standard trigger does not. It is measured against the raised
  menu at the same rate, or against the menu at its full rate, and is never measured against a prescaled menu.
- **Complement capture** (the primary measure): the standard menu keeps (1 - f) of the budget, the novelty trigger takes f, and the
  curve shows what the two together keep.
- **The budget axis.** On HL-LHC the novelty trigger sits at the HLT output, so the axis is **f_hlt_pct**, the budget as a percent
  of the 7.5 kHz HLT output. On Run 3 it replaces part of Level 1, so the axis is **f_l1_pct**, the budget as a percent of the
  recorded Level-1 accept rate.
- **Hashing cell.** Choose a cell for each sample. Every hashing curve then switches to its measurement at that cell, and a study
  with no measurement there is named as "not measured at this cell".
  - HL-LHC opens at the 14 x 20 cell, with 16 x 80 beside it; 8 x 4 is also selectable for the embedding hashing. 22 x 80 was the earlier cell.
  - The talk steps draw the embedding hashing at 14 x 20 with 16 x 80 beside it. The additive mode is measured only at 22 x 80, and its step says so.
  - Run 3 opens at 16 x 20.
- **Every number has its error.** The error bar combines the binomial error on the signal probes with the uncertainty of the cut,
  which comes from bootstrapping the background tail. The spread over encoder trainings and plane draws is printed beside it, and
  the effective number of background crossings behind the cut is given as context.
  - A small effective count makes the error bar large. It never hides the point.
- **Never-trained families.** Signal families the encoder never saw are the population every capture is averaged over. The tree
  says which families were used to choose planes and which were held out.
- **H to aa to 4b is shown apart.** Its sample is simulation without pile-up overlaid on a real zero-bias crossing, so it is never
  trained on and never averaged with the others.

## The saved views

The list on the left holds the talk steps. Click a step to redraw it. You can save your own views and export them, along with the
figures, as files. These are kept in your browser only and are never sent anywhere.

See the NOTICE beside this file for which inputs are simulation and which are CMS Run-3 data.
