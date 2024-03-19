
.. Instance Segmentation for Waste Segregation-documentation:

=======================================
Waste Segregation using Instance Segmentation 🗑️
=======================================

.. contents:: Table of Contents
   :depth: 2

Overview
========

This Project utilizes Detectron2, a versatile framework developed by Facebook AI Research for object detection and instance segmentation tasks. This project aims to address waste management challenges by accurately classifying and segmenting waste items into their respective categories, based on the color of dustbins they are supposed to be disposed into. The architecture and configurations are tailored to adapt Detectron2 to our specific use-case of waste item detection and categorization.

Architecture
============

The project is based on the Mask R-CNN architecture provided by Detectron2, which combines Convolutional Neural Networks (CNNs) with Region Proposal Networks (RPNs) for efficient and accurate instance segmentation. Mask R-CNN extends Faster R-CNN by adding a branch for predicting segmentation masks on each Region of Interest (RoI), parallel to the existing branch for classification and bounding box regression.

Configuration Parameters
========================

The following subsections detail the configuration parameters set for training our model and the rationale behind each choice.

Model Configuration
-------------------

- **Model Type**: ``mask_rcnn_R_50_FPN_3x.yaml``
- **Pretrained Weights**: ``detectron2://COCO-InstanceSegmentation/mask_rcnn_R_50_FPN_3x/137849600/model_final_f10217.pkl``

We chose the ResNet-50 backbone with Feature Pyramid Networks (FPN) for an optimal balance between speed and accuracy. The model is pretrained on the COCO dataset to leverage transfer learning for better feature extraction capabilities.

Training Configuration
----------------------

- **Dataset**: Custom dataset comprising 480 high-quality images of various waste items.
- **Iterations**: ``3000``
- **Learning Rate**: ``0.001``
- **Batch Size**: ``2`` per image
- **Checkpoint Period**: Every ``250`` iterations

The chosen number of iterations and learning rate reflects a balance between sufficient model training and preventing overfitting. The batch size is set considering the memory constraints of typical hardware setups.

Solver Configuration
--------------------

- **Base Learning Rate**: ``0.001``
- **Optimizer**: SGD with momentum ``0.9``
- **Weight Decay**: ``0.0001``
- **Learning Rate Scheduler**: StepLR with steps at ``[1000, 2000]`` and gamma ``0.1``

The SGD optimizer with momentum is used for stable and efficient training. The learning rate scheduler helps in fine-tuning the model by gradually reducing the learning rate.

Data Augmentation
-----------------

Several data augmentation techniques are applied to increase the robustness and generalization capability of the model:

- **Resizing and Cropping**: Adjusting image sizes and random cropping.
- **Flipping**: Horizontal flipping of images.
- **Color Jitter**: Random adjustments to the brightness, contrast, saturation, and hue of images.

These augmentations simulate a variety of scenarios and conditions that waste items might be photographed in, enhancing the model's adaptability to different environments.

Evaluation
==========

Model performance is evaluated using a separate test set, which is crucial for assessing the model's ability to generalize to unseen data. The COCOEvaluator provided by Detectron2 is used for comprehensive evaluation metrics, including Average Precision (AP) and Intersection over Union (IoU).

.. note:: Ensure to evaluate the model periodically using validation checkpoints to monitor progress and adjust configurations as necessary.

Conclusion
==========

This demonstrates the effectiveness of using Detectron2 for the societal benefit of waste management. Through careful configuration and training, the project showcases how deep learning can be harnessed to improve waste sorting and recycling processes, contributing to environmental sustainability.
