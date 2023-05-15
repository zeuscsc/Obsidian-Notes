![[snapshots/D9w8mFDvHsQ/00-01-04.png]]
# Light-Field Neural Rendering
## Introduction to Light-Field Neural Rendering
![[snapshots/D9w8mFDvHsQ/00-00-20.png]]
Light-Field Neural Rendering is a new image-based rendering method for novel view synthesis, which involves rendering a scene from unseen viewpoints given a collection of input images. This method has been developed to overcome the limitations of previous image-based rendering methods such as neural radiance field (NERF) and NEX when rendering scenes with complex view-dependent effects.

## Light-Field Representation and Limitations
![[snapshots/D9w8mFDvHsQ/00-01-08.png]]
Light-Fields are vector functions on the space of oriented lines that associate a ray to a radiance value. While they can be used to directly learn a mapping from a 4D tuple to color, such a model produces low-quality renderings due to the lack of an inherent notion of multi-view consistency.

![[snapshots/D9w8mFDvHsQ/00-01-33.png]]
## Incorporating Geometric Bias using Epipolar Constraint
![[snapshots/D9w8mFDvHsQ/00-02-33.png]]
To address this limitation, the researchers propose incorporating a geometric bias in the form of an epipolar constraint. Given a target ray, its Light-Field coordinates are computed, and points along epipolar lines in reference images are sampled and used to extract features. These features, along with the target ray encoding, are fed into a feature aggregator that summarizes the features along the epipolar line. The resulting feature vector is used to predict the color, where the epipolar feature transformer and view feature transformer play a crucial role.

![[snapshots/D9w8mFDvHsQ/00-02-18.png]]
## Epipolar Feature Transformer and View Feature Transformer
![[snapshots/D9w8mFDvHsQ/00-03-20.png]]
The epipolar feature transformer reasons about correspondences in the reference views to aggregate features of points along the epipolar line. It refines the features by estimating the weight between each epipolar point and the target ray and uses the weights to obtain a weighted sum of epipolar features. The view feature transformer reasons about occlusions and aggregates features from multiple reference views. It estimates a pairwise attention weight for each view with respect to the target ray and uses the weights to interpolate colors and features from reference views.

![[snapshots/D9w8mFDvHsQ/00-04-19.png]]
## Superior Performance and Conclusion
![[snapshots/D9w8mFDvHsQ/00-04-44.png]]
Experiments on various datasets show that the proposed model outperforms previous state-of-the-art methods such as NERF, NEX, and MIP-NERF. The attention-based aggregation mechanism that interpolates colors and features from reference views or directly predicts it from light field coordinates is the reason behind the model's ability to reconstruct complex view-dependent effects. The researchers provide a project webpage for further details, results, and code.

Source: [CVPR 2022 Light Field Neural Rendering - YouTube](https://www.youtube.com/watch?v=D9w8mFDvHsQ)
