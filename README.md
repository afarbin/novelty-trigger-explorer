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

## The numbers table (numbers.html)

One screen with every method at every budget. The table is also the control for the plots:

- **Click a method** to draw its capture curve against the unique background rate. The standard trigger (black) and the
  classifier reference (dashed) are always drawn. A thick bar is the statistical error; a thin one is the spread over trainings.
- **Click a budget in the header** to draw the per-process bars at that budget, one panel per budget, and to mark it on the curves.
- **Processes** picks physics processes by group or one by one: on HL-LHC the held-out, dark-photon and sealed groups and
  their 13 channels (second samples pooled into their parents by probe count, a fold still to be ruled); on Run 3 the five
  classifier folds and their 19 families. The table and the curves then show the mean over the selected processes, with the
  error rule stated beside them. H to aa to 4b on Run 3 and the H to invisible control on HL-LHC are drawn apart and are in no mean.
- The label column stays in place while the numbers scroll left and right. The cell colour runs from white to red, lowest to
  highest in its column within the current view.
- The selection is kept in the address after the #, so a view can be shared as a link.
- **The best in each group is underlined.** Within each group of rows (the reference rows, and each level of the table), at
  each budget and footing, the highest unique capture among the rows in view that are cut the same way (held-out half, or whole
  block) is underlined; a value within the combined statistical error of it has a dotted underline. A group with one such row
  is not marked. With processes selected, the means over the selection are ranked the same way.
- **The Run 3 standard trigger is the loosened menu** (since 2026-11-07): the Level-1 menu with its thresholds lowered from the
  CMS menu by one factor until it adds the budget, cut on the held-out half, the same convention as the HL-LHC standard trigger;
  in the rate-neutral footing the menu is raised to give the budget up. It is the black reference on every Run 3 curve and bar,
  per process in the additive footing. The menu at CMS thresholds with a random prescale of its rejects is kept only as a
  labelled floor row; it is not the standard.

Row classes (`numbers_row_classes.json` beside the builder, one place to change them):

| class | HL-LHC | Run 3 |
|---|---|---|
| proposed: the hash density trigger | hashing, random planes, 14 x 20 on the embedding (held-out and whole-block cut); planes chosen with known signals, 14 x 20 on the embedding (targeted use) | hashing, random planes, 16 x 20 on the embedding (held-out, whole-block and first held-out reading); planes chosen with known signals on the embedding |
| comparison | standard trigger; supervised classifier, from scratch (S); Gaussian on the embedding | standard trigger (both cuts); AXOL1TL score (all three readings); Gaussian on the embedding (all three readings); supervised classifier, 57 Level-1 inputs (both cuts); supervised classifier on the embedding |
| always drawn | standard trigger; supervised classifier, from scratch | standard trigger; supervised classifier, 57 Level-1 inputs |
