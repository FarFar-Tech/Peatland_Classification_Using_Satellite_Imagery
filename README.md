# Peatland_Classification_Using_Satellite_Imagery
This repo is about using a Multi-Modal ML model to classify different types of Peatlands from satellite imagery. 

# Overview

Peatland classification provides valuable information for greenhouse gas inventory and biodiversity protection. In this repo, we proposed an encoder-decoder-based architecture for peatland classification that fuses two open-source satellite data, Sentinel-1 and Sentinel-2. We show the effect of fusion by comparing the multi-modal fusion architecture with unimodal, which is trained only based on one input data source. We also investigate the influence of skip connections as the main component of the encoder-decoder to recover fine-grained details that are lost during the downsampling process. The experimental results are acquired on a study area in Finland, which covers a variety of minerotrophic aapa mire peatlands. The results demonstrate that multi-modal architecture consistently outperforms uni-modal architectures for peatland classification. In addition, the fusion architecture with one skip connection achieved a total accuracy of 57.44%. This shows 8.51% accuracy improvement compared with the model without skip connections.

# Study Area

The Keminmaa study area, as depicted in the following figure, lies within the southern region of the aapa mire zone in northern Finland [21]. These aapa mires are characterized as minerotrophic vegetation-ecological peatland complexes with flat lawn-level vegetation and concave surface topography. Within this study area, a diversity of peatland site types exists across various fertility classes, attributed to the assortment of local lithologies and, predominantly, glacial till subgrade. These peatlands possess an average depth of 1.1 meters, covering approximately 50% (42800 hectares) of the total land area.

![fig2](https://github.com/user-attachments/assets/5805220c-26ae-49f6-ae22-2bbc22dbf8cb)

# Data 
The classification system followed the Finnish peatland fertility level classification with five classes: Herb rich type/Oxalis-Myrtillus type(FL1), Vaccinium myrtillus type I (FL2), Vaccinium vitis-idaea type II(FL3), Dwarf shrub type (FL4) and Cladina type (FL5). The following table shows the ground truth of the five main fertility levels and two land use classes used in this paper. The total number of labeled samples is 1359 and 706 for drained and undrained, respectively. The labeled dataset is limited, with an imbalanced organization of the classes.

<img width="718" alt="Screenshot 2025-02-14 at 14 24 43" src="https://github.com/user-attachments/assets/f78b556e-f5d8-4a95-87fb-778736d431ee" />

The following table shows the characteristics of the data used in this paper. Synthetic Aperture Radar (SAR) satellite data comprises two distinct types of Sentinel-1 (S1) imagery. 1) The intensity images (i.e., ground range detected products) including both VV and VH polarizations (V= vertical, H=horizontal) were downloaded from the Copernicus Open Access Hub 1 and further processed using the ESA Sentinel Applications Platform (SNAP) software. These intensity images represent the backscattered signals detected, multi-looked, and projected into a single image. For analysis, five intensity images were utilized, each corresponding to a different summer month in 2017 (May-September). 2) The coherence images, derived from single-look complex products, capture the similarity of radar reflections between pairs of individual images. Two distinct sets of coherence images were generated. The first set comprises 12 coherence images calculated for each temporally consecutive pair of Sentinel-1A images, spaced at 12-day intervals between May 9 and September 30, 2017, denoted as ‘repeated overpass’ (RO) in this study. The second set consists of another 12 coherence pairs calculated for the same set of Sentinel-1A images, with the mid image of July 20, 2017, consistently included as a “reference” image in each pair, termed as ‘long-term baseline’ (LB) coherence.

<img width="758" alt="Screenshot 2025-02-14 at 14 24 58" src="https://github.com/user-attachments/assets/aac5b6ca-d692-4d51-8f6c-576f1d999c89" />


# Architecture 
It is a UNet-style encoder-decoder network designed commonly for semantic segmentation, and it has been adopted for the fusion of three input satellite data sets. Our multi-modal architecture has three branches, which separately extract each input data's features and concatenate each branch's output to perform pixel-wise peatland classification. Each branch consists of two parts as follows:

![fig3](https://github.com/user-attachments/assets/fb2a91ee-f628-410e-87ca-7bd110a44264)


# Results 

Our results show that the proposed ED architecture achieves an accuracy of 57.44%, which is significantly higher than the accuracy of the CNN architecture (44.36%). This improvement in accuracy is due to the encode-decoder architecture’s ability to better capture the spatial relationships and hierarchical patterns in the data. We also investigate the effect of skip connection on the performance of our proposed architecture. The collected results indicate the skip connections can improve the accuracy of our fusion architecture since they can transfer low-resolution information from the encoder part to high-resolution information from the decoder.

<img width="1101" alt="Screenshot 2025-02-14 at 14 31 36" src="https://github.com/user-attachments/assets/672d8c5b-8f20-4bc8-886b-3df1d323f9f2" />

### Confusion Matrix 
In the classification of drained subsections (as depicted in the following Fig(a)), the highest number of correct predictions is observed for the FL1 class; 64% of the actual FL1 instances were correctly predicted as FL1 by the model. Conversely, the AFOPS class shows high misclassification rates, with only 18% correctly predicted and substantial portions being incorrectly predicted as FL1 (42%) and FL3 (20%). This misclassification arises due to the similarity in forest cover, primarily dominated by Scots pine and Norway spruce, making it challenging to differentiate using solely S1 and S2 data. Turning to undrained scenarios (illustrated in the following Fig(b)), the highest number of correct predictions aligns with FL2 (74%). However, a considerable proportion of FL2 samples (18%) are misclassified as FL3 (Vaccinium vitis-idaea type).

<img width="911" alt="Screenshot 2025-02-14 at 14 33 06" src="https://github.com/user-attachments/assets/02d27d68-22dd-445b-b683-c9ad74234a11" />

### Prediction Map
<img width="1218" alt="Screenshot 2025-02-14 at 14 36 40" src="https://github.com/user-attachments/assets/f3eb0933-97d7-45a5-9745-6ae0ca902e1f" />


# Code
The code of this project will be available soon!
