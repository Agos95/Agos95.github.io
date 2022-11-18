---
title: 'Myocardial fibrosis detection using kernel methods: preliminary results from a cardiac magnetic resonance study'
authors:
  - Campese Stefano
  - agostini-federico
  - Riccardo Vianello
  - Pizzi Marco
  - Cipriani Alberto
  - Zanetti MArco
author_notes:
  - 'Equal contribution'
  - 'Equal contribution'
date: '2022-08-23'
doi: '10.1093/ehjci/jeac141.005'

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
  - Neural Networks
  - Kernel Methods
featured: false

#links:
#  - name: Custom Link
#    url: http://example.org
url_pdf: https://academic.oup.com/ehjcimaging/article-pdf/23/Supplement_2/jeac141.005/45503137/jeac141.005.pdf
url_code:
url_dataset:
url_poster: ESC_analysis_poster.pdf
url_project:
url_slides:
url_source:
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

Asserting the presence of myocardial fibrosis from cardiac magnetic resonance (CMR) images is sometimes a complex task, even for experienced cardiac imagers. The application of artificial intelligence models to the evaluation process can be of help for enhancing diagnostic accuracy.
Purpose

In this work, we tested two different Machine Learning (ML) algorithms, namely kernel methods with Support Vector Machine (SVM) and Convolutional Neural Network (CNN) to a cohort of consecutive CMR studies. The goal was a binary classification task, aimed to identify myocardial scar (present/absent).

### Methods

Dataset consisted of 642 CMR scans, equally divided into healthy and fibrosis-affected. Raw DICOM files were preprocessed through an automated pipeline, in order to retrieve only short-axis post contrast acquisitions. Heart regions were then individuated using a YOLO network, in order to remove the background and focus only on data of interest. Finally, for each subject 10 slices were extracted through interpolation, and all images resized to 128 by 128 pixels. Dataset was divided into training and test sets, with proportions 80%‐20%.
Results

The first analysis was based on state-of-the-art CNN models, pre-trained on the ImageNet dataset. The training of the models was optimized using "reduce learning rate on the plateau", "early stopping", and standard data augmentation techniques. Experiments showed that CNNs-based models led to poor performances.

The second attempt was based on kernel methods and SVM. Before feeding the input to the algorithm, dimensionality reduction was implemented using a Principal Component Analysis retaining 99% of the variance. The resulting 335 features were passed as input to an SVM, testing different kernels (e.g. Linear, Gaussian, Cossim). Models were trained and optimized using a Grid Search with a 5-fold Cross-Validation. The best SVM configuration displayed an accuracy of 68% and a sensitivity of 60%.

Improved results could be obtained using state-of-the-art Multiple Kernel Learning algorithms, leading to 71% accuracy and sensitivity of 72% (with a 12% increment with respect to the previous algorithm).

### Conclusions

Our preliminary results of this study showed the possibility for a ML system to learn to identify myocardial fibrosis, directly from raw CMR images. In particular, kernel methods were able to achieve good and significant results, even with small amounts of data, suggesting room for improvement. In future works, we plan to furtherly explore kernel methods to improve the results and to build an end-to-end solution for cardiac imagers.