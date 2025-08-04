Project Overview
This project involves training a UNet model to predict the fill color of geometric shapes such as triangles and squares. The model takes shape outlines as input and predicts either a filled color image or a corresponding color label.

Model Configuration
Model: UNet with skip connections

Optimizer: Adam

Learning Rate: 0.001

Batch Size: 32

Epochs: 15

Loss Function: CrossEntropy (for classification), MSE (for regression)

Key Observations
The model performs well on basic shapes.

Some confusion occurs between similar colors (e.g., beige vs. green).

Minor issues with color accuracy and edge clarity.

Fixes Implemented
Corrected label mismatches.

Augmented the dataset to improve underrepresented color performance.

Retained the original UNet structure after ablation testing.

Conclusions
The UNet architecture is effective for this task.

High-quality, balanced training data is essential.

Color classification is more robust than full image regression for this problem.

Key Learnings
Accurate label mapping is critical for reliable training and evaluation.

Simpler classification tasks often outperform pixel-wise regression in color prediction problems with a limited color palette.

Visualizing intermediate outputs and predictions is essential for debugging model behavior.

Model performance is sensitive to subtle variations in shape input quality and color representation.
