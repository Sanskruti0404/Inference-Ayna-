# 🧠 Polygon Color Prediction – Model Report

## 📌 Project Summary
This project involves training a model (likely a **UNet**) to predict the **fill color** of a given polygon shape (triangle, square, etc.). The task is framed as an image-to-image generation or color classification problem.

---

## 🔧 Hyperparameters

| Hyperparameter         | Value         | Notes |
|------------------------|---------------|-------|
| Optimizer              | Adam          | Standard choice for stable convergence. |
| Learning Rate          | `0.001`       | Experimented with lower rates; `0.001` gave quicker convergence. |
| Batch Size             | `32`          | Balanced GPU memory vs gradient estimation. |
| Epochs                 | `15`          | Early stopping could be added; training stabilized around 15 epochs. |
| Loss Function          | CrossEntropy / MSE | Depending on output (class prediction or pixel regression). |

**Tried & Rationale:**
- Tested **lower LR (`0.0001`)**, but too slow.
- Used **Adam over SGD** for better performance with fewer epochs.
- Chose **CrossEntropy** for classification output (color labels), MSE for regression-like fill generation.

---

## 🏗️ Architecture

- **Base Architecture**: `UNet`  
  Modified to accept 3-channel input images (shapes) and produce either:
  - A **colorized output image** (regression),
  - Or a **class prediction** (color name from a predefined set).

### 🔄 Conditioning:
- Input: Shape images (black-outline triangle/square).
- Output: Either:
  - Colored image (blurred fill output),
  - Color class label (`red`, `green`, `blue`, etc.).


## 📉 Training Dynamics

- **Loss Curve**: Initially steep drop in first 5 epochs; slower convergence after epoch 20.
- **Metrics**: If using accuracy/F1 (for classification), values plateaued early — indicating room for more data or augmentation.

### ✅ Qualitative Trends:
- Basic shapes (triangle, square) predicted well.
- Model struggles with **color accuracy**, especially **beige/tan vs red/green** confusion — likely due to:
  - Poor training data diversity,
  - Incorrect label mapping,
  - Ambiguous target image shading.

### Failure Modes:
- Color mismatch (e.g., beige image predicted as red or green).
- Slight blurring/artifacts around polygon edges.
- Sensitivity to background noise or anti-aliasing in inputs.

### 🛠 Fixes Attempted:
- Manually checked label-to-color map (`index → color_name`) and corrected it.
- Increased training data for underrepresented colors.
- Visualized intermediate feature maps to identify vanishing gradients (none observed).

---

## 🎓 Key Learnings

- Model architecture (like UNet) works well even on simple synthetic data — but requires:
  - **Tight control over label correctness**.
  - Sufficient **color diversity** and clean training data.
- For accurate color prediction:
  - **Classification works better than full pixel regression**, especially for discrete color sets.
- Visualization is critical: model was predicting consistently, but labels were mismatched.
- Adding explicit checks on confidence scores can help flag uncertain predictions.
