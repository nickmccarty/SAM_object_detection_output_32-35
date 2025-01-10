> Hi there!👋😃
>
> Below you'll find an overview of the deliverables being submitted for your perusal 👇

# Overview

The zip file contains the following, and can be downloaded by clicking [this link](https://github.com/nickmccarty/SAM_object_detection_output_32-35/raw/refs/heads/main/SAM_object_detection_output.zip?download=) (alternatively, you can go to [this page](https://github.com/nickmccarty/SAM_object_detection_output_32-35/blob/main/SAM_object_detection_output.zip) and click the download icon):

```
SAM_object_detection_output.zip
├── tif_32_centroids_wgs84.csv
├── tif_32_deviation_report.xlsx
├── tif_32_filtered_detections.geojson
├── tif_33_centroids_wgs84.csv
├── tif_33_deviation_report.xlsx
├── tif_33_filtered_detections.geojson
├── tif_34_centroids_wgs84.csv
├── tif_34_deviation_report.xlsx
├── tif_34_filtered_detections.geojson
├── tif_35_centroids_wgs84.csv
├── tif_35_deviation_report.xlsx
└── tif_35_filtered_detections.geojson
```

# Results

The recognized limitation with the Hough Circle detection-oriented approach used previously was an unacceptably high number of False Negatives (failures to detect a pot when there was a pot to be detected). Having manually QC'd the SAM-generated `.geojson` output in QGIS, there are a total of 80 pots that were undesireably filtered out by our automated workflow; out of ~16,000 detected pots, that is a Type II (False Negative) error rate of 0.5%.

As for Type I error (False Positive, or detecting a pot when there is no pot to detect), there are 3 polygons (one is a green box next to a pot, and two are squares from the checkerboard ground control objects) that were not filtered out when they should have been; FlyPix's workflow output contained much more undersired geometry, in comparison (too much to easily count).

Regarding accuracy:

* FlyPix average deviation ([`32-35_transparent_mosaic_group1_20241121163322.tif`](https://drive.google.com/file/d/1yk3OA8OIgmL8BYlZnO5rl0ZJhcQzRslA/view?usp=sharing)): 1.394 cm
* SAM average deviation ([`32.tif`](https://drive.google.com/file/d/17TsZtBEhz9w3ymWQb7dllykLDIaCpYPg/view?usp=sharing)): 1.199 cm
* SAM average deviation ([`33.tif`](https://drive.google.com/file/d/1NR6nKKw-MGjxFQQPExBPtURTspkpY1n5/view?usp=sharing)): 1.219 cm
* SAM average deviation ([`34.tif`](https://drive.google.com/file/d/1bWFN69mWeXfez9DtQqapQ6e2EnriSVFy/view?usp=sharing)): 1.181 cm
* SAM average deviation ([`35.tif`](https://drive.google.com/file/d/1u1AOgR9OYWjCsKGLkbHNAHIx5j3UEsm0/view?usp=sharing)): 1.070 cm 

**Total SAM average deviation (32-35)**: 1.167 cm --> <ins>19.52% more accurate</ins>

Finally, regarding compute time and resources:

A single T4 GPU was able to produce the `.geojson` output, the deviation reports, and the centroid CSVs in `WGS84` in under an hour.

# Conclusion

As was mentioned in the last recorded update, further refinement is required to keep all the polygons we want and to filter out all the ones we don't -- the work continues, thank you for your patience!

# References

* FlyPix accuracy check ([link to Colab notebook](https://colab.research.google.com/drive/1LoZu_Lh9QqJCDyTn9d2XPJ8R6BgBAyBB?usp=sharing#offline=true&sandboxMode=true))

| Ortho               | SAM Accuracy Check                                                                                                                |
|--------------------|------------------------------------------------------------------------------------------------------------------------------------|
| [`32.tif`](https://drive.google.com/file/d/17TsZtBEhz9w3ymWQb7dllykLDIaCpYPg/view?usp=sharing)      | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1OUnxhLMZPggSDUSCRIOmL9SdxFM-0Tg8?usp=sharing#offline=true&sandboxMode=true) |
| [`33.tif`](https://drive.google.com/file/d/1NR6nKKw-MGjxFQQPExBPtURTspkpY1n5/view?usp=sharing)      | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1nkpVChniGlSlL22rOsGKso-uk7_-n4JA?usp=sharing#offline=true&sandboxMode=true) |
| [`34.tif`](https://drive.google.com/file/d/1bWFN69mWeXfez9DtQqapQ6e2EnriSVFy/view?usp=sharing)      | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1bphUISx8zppOaMUqFwryZW9R7uGvoOOg?usp=sharing#offline=true&sandboxMode=true) |
| [`35.tif`](https://drive.google.com/file/d/1u1AOgR9OYWjCsKGLkbHNAHIx5j3UEsm0/view?usp=sharing)      | [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/drive/1lOspO6mzrvFjvZK47v-GOiV3znvX0xsy?usp=sharing#offline=true&sandboxMode=true) |
