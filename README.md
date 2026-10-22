# Smart Aeroponics Fenugreek Nutrient-Stress Image Dataset

This repository is for original, whole-plant images of fenugreek grown in a
Smart Aeroponics setup under eight fertilizer-omission treatments. Images will
be collected daily from a fixed camera position across two growth rounds.

## Experimental setup

The treatments vary the supply of calcium nitrate (CN), ammonium phosphate
(AP), and potassium sulphate (KS). Micronutrients are held constant. Four
plants share one nutrient solution in each bucket; each bucket is assigned one
treatment. The eight treatment codes list supply status in the order
**CN–AP–KS**, where `1` means supplied and `0` means omitted:

| Code | Calcium nitrate | Ammonium phosphate | Potassium sulphate |
|------|-----------------|--------------------|--------------------|
| `000` | Omitted | Omitted | Omitted |
| `001` | Omitted | Omitted | Supplied |
| `010` | Omitted | Supplied | Omitted |
| `011` | Omitted | Supplied | Supplied |
| `100` | Supplied | Omitted | Omitted |
| `101` | Supplied | Omitted | Supplied |
| `110` | Supplied | Supplied | Omitted |
| `111` | Supplied | Supplied | Supplied |

These codes describe fertilizer-omission conditions. They do not, by
themselves, establish that an individual plant has a deficiency of a particular
element or prove a causal diagnosis.

## Images and metadata

- Keep original image files unmodified in the matching plant folder under
  `images/round_1/` or `images/round_2/`, using the
  `round/bucket/plant/day` folder structure. Do not add processed or derived
  images as originals.
- Use JPEG filenames `day_001.jpg`, `day_002.jpg`, and so on, with a
  three-digit, one-based growth day. Bucket IDs `B01`–`B08` identify the eight
  treatment buckets within a round, and plant folders `P01`–`P04` identify
  plants within each bucket. Keep each bucket's treatment assignment
  consistent within that round.
- In `metadata.csv`, `image_path` is relative to the repository root, and
  follows the layout, for example `images/round_1/B01/P01/day_001.jpg`.
  `plant_id` is the bucket and plant identifier (for example, `B01-P01`).
  `treatment_code` uses the mapping above. `round_id` is `round_1` or
  `round_2`; `growth_day` is the numeric day since the start of that round.
- Set `image_id` to `R1-` or `R2-` followed by the filename stem, for example
  `R1-B01-P01-day_001`. This keeps IDs unique across rounds.
- Add one metadata row per image. The CSV currently contains only its header;
  no experimental image records are included yet.

## Planned split and limitations

Round 1 is intended for training and validation, with plants grouped so images
of the same plant do not cross those subsets. Round 2 is reserved for final
testing. This round-based split tests transfer to a later growth round, but
round-specific conditions may also affect the result.

There is one bucket per treatment, so plants sharing a bucket are not
independent treatment-level replicates. Any treatment effect may be confounded
with that bucket. Buckets and reservoirs are cleaned and reused between rounds;
cleaning may not eliminate all carryover, and reuse can make round comparisons
less independent. Interpret findings with these limitations in mind.
