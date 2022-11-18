---
title: 'A post processing pipeline to prepare raw data for machine learning algorithms in cardiac magnetic resonance imaging'
authors:
  - agostini-federico
  - Campese Stefano
  - Riccardo Vianello
  - Pizzi Marco
  - Cipriani Alberto
  - Zanetti MArco
author_notes:
  - 'Equal contribution'
  - 'Equal contribution'
date: '2022-08-23'
doi: '10.1093/ehjci/jeac141.017'

# Schedule page publish date (NOT publication's date).
publishDate: '2022-11-18'

# Publication type.
# Legend: 0 = Uncategorized; 1 = Conference paper; 2 = Journal article;
# 3 = Preprint / Working Paper; 4 = Report; 5 = Book; 6 = Book section;
# 7 = Thesis; 8 = Patent
publication_types: ['2']

# Publication name and optional abbreviated publication name.
publication: In *European Heart Journal - Cardiovascular Imaging*
publication_short: 

abstract: ''

# Summary. An optional shortened abstract.
summary: ""

tags:
  - Cardiac Magnetic Resonance
  - Medicine
  - AI
  - Preprocessing
featured: false

#links:
#  - name: Custom Link
#    url: http://example.org
url_pdf: https://academic.oup.com/ehjcimaging/article-pdf/23/Supplement_2/jeac141.017/45503155/jeac141.017.pdf
url_code:
url_dataset:
url_poster: ESC_pipeline_poster.pdf
url_project:
url_slides:
url_source: https://doi.org/10.1093/ehjci/jeac141.017
url_video:

# Featured image
# To use, add an image named `featured.jpg/png` to your page's folder.
#image:
#  caption:
#  focal_point: ''
#  preview_only: false

# Associated Projects (optional).
#   Associate this publication with one or more of your projects.
#   Simply enter your project's folder or file name without extension.
#   E.g. `internal-project` references `content/project/internal-project/index.md`.
#   Otherwise, set `projects: []`.
projects: []

# Slides (optional).
#   Associate this publication with Markdown slides.
#   Simply enter your slide deck's filename without extension.
#   E.g. `slides: "example"` references `content/slides/example/index.md`.
#   Otherwise, set `slides: ""`.
slides:
---

### Funding Acknowledgements

Type of funding sources: None.

### Background

Artificial Intelligence is an emergent tool in clinical practice for post processing of medical images. Machine Learning (ML) pipelines are created for data of interest extraction and algorithm application. A common issue in data extraction is represented by noisy datasets, like those of CMR studies, characterized by multiple images, acquired by different techniques, axis orientation and contrast timing.
Purpose

A ML pipeline for extraction of LGE images from raw DICOM data is presented. Additionally, steps for normalization of image number and automatically heart localization are outlined.
Methods and Results

642 consecutive CMR studies were analyzed.

Pipeline, Part 1. By looking at the metadata in raw files, ‘SequenceName’ tag was used to discard cine images, ‘ScanningSequence’ tag to select Gradient Recall and Inversion Recovery techniques (Inversion Time > 100 ms), ‘SequenceVariant’ tag to discard Steady State images (See Fig. 1). Orientation of the major axis was computed and ‘Axial’ or ‘Coronal’ images removed. Scans were grouped together by image orientation (requesting a min and max number of elements per group) and only the group with the largest number of files was selected. Finally, DICOMs were grouped by image shape (demanding a min number of elements), and only the series with the highest resolution was retained. Then, for each subject, the extracted series consists of a 3D-array (N,H,W), with N number of slices, and (H,W) image resolution. The attributes were not homogeneous between subjects.

Pipeline, Part 2. Given a desired final number of slices and resolution, the 3D-array was reshaped through a spline interpolation. In order to have a focus on the heart, a Region of Interest (ROI) extractor was implemented, based on a YOLO network for object detection. The network was applied on all the slices (Fig. 2); then the images were cropped by keeping the largest bounding box. This step allowed us to remove the background by only selecting the relevant ROIs. To manage the data more easily, images were saved as a NumPy Array, while other useful Dicom metadata (e.g. weight, age, …) were stored using the json standard.

At the end of the ML pipeline, images can be reduced to a common resolution and forwarded to ML algorithms.

By using this pipeline, a great amount of information not needed for LGE analysis can be discarded, granting a significant reduction in terms of data storage. In our series, the original dataset extended for about 200 GB; by requesting 10 slices per subject with a resolution of 128 by 128 pixels (also extracting heart ROI) the final dimension was reduced to 108 MB.

### Conclusions

In this work, we presented a post-processing pipeline for CRM images and LGE analysis. Given in input raw CRM the pipeline is able to (i) remove unuseful data, (ii) extract heart ROIs storing also Dicom metadata, (iii) normalize slices and image resolution, and (iv) store the processed CRM into ready-format for ML techniques.