# Table

Baseline: the Task 2 model.
Every row is the mean and spread of 3 seeds.

* Val: 28 validation images.
* Camera: the same images randomly cropped, rotated and with changed colours, 5 copies of each.
* Last years: 120 validation photos from last year. Too optimistic in every row with added photos: these photos are similar to the ones it trained on.

One change at a time:

|Variant|Val|Camera|Last years|
|-|-|-|-|
|Baseline|0.548 +- 0.109|0.543 +- 0.122|0.467 +- 0.046|
|Only last layer trained|0.667 +- 0.055|0.681 +- 0.011|0.586 +- 0.017|
|Geometric augmentation|0.762 +- 0.041|0.719 +- 0.073|0.583 +- 0.068|
|Geometric + colour augmentation|0.583 +- 0.021|0.621 +- 0.052|0.617 +- 0.038|
|Cosine, 30 epochs|0.667 +- 0.090|0.598 +- 0.107|0.544 +- 0.013|
|Best epoch|0.595 +- 0.082|0.581 +- 0.086|0.472 +- 0.042|
|AdamW|0.536 +- 0.094|0.533 +- 0.123|0.456 +- 0.073|
|Label smoothing|0.667 +- 0.074|0.631 +- 0.022|0.539 +- 0.051|
|Dropout 0.5|0.595 +- 0.055|0.564 +- 0.021|0.464 +- 0.025|
|Learning rate 1e-4|0.631 +- 0.021|0.607 +- 0.019|0.464 +- 0.032|
|Last years' photos added|0.762 +- 0.055|0.695 +- 0.041|0.906 +- 0.025|

Combinations:

|Variant|Val|Camera|Last years|
|-|-|-|-|
|Last layer + geometric|0.619 +- 0.055|0.695 +- 0.015|0.589 +- 0.021|
|Geometric + colour + cosine 30|0.786 +- 0.036|0.769 +- 0.034|0.656 +- 0.034|
|Added photos + geometric|0.667 +- 0.074|0.669 +- 0.035|0.886 +- 0.005|
|Added photos + geometric + colour|0.690 +- 0.109|0.714 +- 0.047|0.856 +- 0.038|
|Added photos + last layer + geometric|0.548 +- 0.055|0.664 +- 0.000|0.833 +- 0.008|
|Added photos + smoothing|0.821 +- 0.036|0.710 +- 0.041|0.914 +- 0.029|
|Added photos + geometric + cosine 30|0.798 +- 0.021|0.743 +- 0.050|0.897 +- 0.021|
|Added photos + geometric + colour + cosine 30|0.821 +- 0.000|0.798 +- 0.035|0.900 +- 0.014|
|Added photos + geometric + colour + cosine 30 + smoothing|0.845 +- 0.074|0.833 +- 0.021|0.914 +- 0.017|

# What each change brought compared with the baseline

* Geometric augmentation: val +0.214, camera +0.176, last years +0.116.
* Added photos: val +0.214, camera +0.152. The last years number is not fair here, those photos are similar to the ones it trained on.
* Only last layer trained: val +0.119, camera +0.138, last years +0.119.
* Label smoothing: val +0.119, camera +0.088, last years +0.072.
* Cosine, 30 epochs: val +0.119, camera +0.055, last years +0.077.
* Colour next to geometric: val +0.035, camera +0.078, last years +0.150. Alone it is not better than geometric only, it helped with more epochs.
* Learning rate 1e-4: val +0.083, camera +0.064, last years -0.003.

# Is the difference greater than the noise

One validation image is worth 0.036 of accuracy (1 of 28).

* Greater than the noise: geometric augmentation, added photos, the best combinations.
* About the size of the noise: only last layer, label smoothing, cosine, learning rate 1e-4.
* The top two combinations differ by less than the noise, so smoothing may not add anything.

# What did not help

* AdamW: no change.
* Dropout 0.5: no change.
* Best epoch: no change.
* Only last layer combined with geometric augmentation: not better than either alone.

# Which model I would put on the phone

Added photos + geometric + colour + cosine 30 + smoothing (best on val and camera; on last years it ties with added photos + smoothing at 0.914).

Exported as an ONNX model, seed 0: val 23 of 28, last years 112 of 120.

Course camera app:
did not work

Class: Maple
Scores:
apple 0.003
cherry 0.049
chestnut 0.008
maple 0.940

