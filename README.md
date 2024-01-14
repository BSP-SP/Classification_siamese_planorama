# Product Recognition System

## Overview
This project addresses the challenges associated with product recognition through a two-stage pipeline. The proposed solution involves class-agnostic object detection in the first stage, followed by product recognition in the second stage using a K-NN similarity search. The process is designed to efficiently identify individual product items within an image.

## Proposed Approach
![Multistage Process](proposed.png)

### 1. Detection
The first stage, detection, aims to obtain bounding boxes that accurately localize products in an image, providing a confidence score for each detection. To achieve this, a CNN-based object detector (Detector) is employed. The detector is trained on a large collection of annotated images, focusing on common product features shared across multiple items. This enables product-agnostic detection, making the detector versatile across various stores and products without the need for frequent retraining.

#### 1.1 Siamese Network
As an alternative to conventional CNNs, the project explores the use of Siamese Networks for product recognition. Siamese Networks consist of duplicate subnetworks, learning a similarity function that allows them to estimate the similarity of inputs without requiring retraining for adding or removing classes. Key features and benefits of Siamese Networks include:

- **Identical Subnetworks:** Siamese Networks consist of two or more subnetworks that are identical in configuration, parameters, and weights. Typically, only one subnetwork is trained while the others maintain the same configuration.

- **Handling Class Imbalance:** Siamese Networks are effective in handling class imbalance, making them suitable for scenarios where acquiring a significant amount of data is impractical.

- **Classifier Ensembling:** The networks are compatible with classifier ensembling, providing flexibility in the overall recognition system.

- **Semantic Similarity:** Siamese Networks excel in acquiring knowledge on semantic similarity, making them valuable for tasks like product recognition.

However, it's important to note that Siamese Networks demand more training time compared to conventional networks due to the quadratic pairs they learn from. Additionally, instead of probabilities, they output the distance from each class.

### 2. Image Embedding
In one approach, each region proposal generated by the Detector is cropped from the input image and fed into a CNN (Embedder) to generate a unique image representation. This representation is utilized for product recognition by performing a K-NN similarity search within a precomputed reference database of representations.


## Experimental Results

### 4.1 Datasets and Evaluation Metrics
In our experimental evaluation, we utilized a publicly available dataset containing shelf and product images. This dataset consists of approximately 10 classes of grocery products that are arranged in hierarchical classes. Each product is represented by a single reference image. The dataset contains an average of 200 products per class, and the remaining 10,000 products are not categorized and can be considered as the negative class.
![sample input ](dataset.png)
### Implementation Details - Detection
For the detection stage, we employed a one-stage object detector called Yolov3. We chose this network for its real-time performance on GPUs and the availability of the original implementation. We used the recommended hyperparameters and provided weights to train the network on 243 images and validated it on 111 images for 20 epochs. Below are sample output images with bounding boxes generated by Yolov3.

![Yolov3 bounding box](yolo.png)

## Result from Siamese Network
Add information on the results obtained from the Siamese Network here.
![Yolov3 Sample Output](output.png)
