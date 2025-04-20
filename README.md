# MTL782 Assignment 2: Text-Guided Image Clustering

This was our self-study project for MTL782 Assignment 2 under Prof Niladri Chatterjee.

## Motivation

The goal of this project was to explore and compare various approaches for clustering images from a subset of the Food-101 dataset. We compared traditional computer vision features (like SIFT, HOG, Color Histograms) with features derived from deep learning models (ResNet-50, EfficientNet-B0) and text-guided methods (generating captions/answers with BLIP/VILT and embedding them with SBERT). We were also motivated to see if fine-tuning deep learning models on the specific food dataset could adapt them to the domain distribution and improve clustering performance.

![img](https://github.com/harshit1912003/TGIC/blob/main/dataset.png)
## Results and Inferences

* **Classical Features**: Traditional features generally resulted in poor clustering performance, with very low Adjusted Rand Index (ARI) scores, indicating they weren't sufficiently discriminative for this task.
* **Pre-trained Deep Features**: Features from pre-trained models like ResNet-50 and EfficientNet-B0 offered a significant improvement over classical features, showing the power of learned representations. EfficientNet-B0 performed slightly better and was faster to extract.
* **Text-Guided Features (Pre-trained)**: Using BLIP to generate captions and SBERT to embed them performed comparably to pre-trained visual features. Using VILT for Visual Question Answering ("Which dish is in this image?") was less effective and slower.
* **Fine-tuning**:
    * Fine-tuning EfficientNet-B0 on the food dataset significantly improved visual feature quality and clustering performance (ARI 0.45 vs 0.28 for K-Means), demonstrating the benefit of domain adaptation.
    * Fine-tuning the BLIP captioning model (even with simple template captions like "This is an image of [class_name]") yielded the best results. Features extracted from these fine-tuned captions using SBERT achieved a K-Means ARI of 0.77 on our internal test set, substantially outperforming other methods. Notably, DBSCAN also performed extremely well (ARI 0.77) on these features, indicating they had a structure well-suited for clustering.
* **Final Model**: Training the fine-tuned BLIP model on a larger dataset (20% sample vs 10%) further improved performance, achieving an ARI of ~0.816 on our internal test set.

## Final Score

For the final evaluation on the Kaggle competition test set (9000 images), using features from the final fine-tuned BLIP model (trained on 3360 images) and SBERT embeddings, the following ARI scores were achieved:

* **K-Means**: 0.8036  
* **DBSCAN**: 0.8041  
* **Agglomerative Clustering**: 0.8036

## Contributors

* Ananya Sharma (2023MAS7117)
* Harshit Joshi (2023MAS7141)
