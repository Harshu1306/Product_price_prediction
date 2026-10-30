<<<<<<< HEAD
# Multimodal Product Price Prediction

A multimodal deep learning system for predicting e-commerce product prices using **catalog text and product images**.

The final model combines pretrained text, image, and vision-language encoders with modality-specific neural networks and a multimodal fusion MLP.

---

## 📌 Problem Statement

Given an e-commerce product's:

- **Catalog text**
- **Product image**

predict its **price**.

This is a **multimodal supervised regression** problem.

### Dataset

- Training samples: **75,000**
- Test samples: **75,000**

### Columns

| Column | Description |
|---|---|
| `sample_id` | Unique product identifier |
| `catalog_content` | Product title, value, units, description, bullets, etc. |
| `image_link` | Product image URL |
| `price` | Target price (training only) |

---

# 🏗️ Architecture

```text
                    PRODUCT
                       |
          +------------+------------+
          |                         |
         TEXT                      IMAGE
          |                         |
     +----+----+               +----+----+
     |         |               |         |
     v         v               v         v
   Qwen3    SigLIP2          DINOv3   SigLIP2
    Text      Text            Image     Image
     |         |               |         |
   2560      1536            1280      1536
     |         |               |         |
     v         v               v         v
 Qwen Tower SigLIP Tower   DINO Tower SigLIP Tower
     |         |               |         |
   768       768             768       768
     |         |               |         |
     +---------+-------+-------+---------+
                       |
                       v
                  Concatenate
                       |
                     3072
                       |
                       v
                 Fusion MLP
                       |
              3072 -> 2048
                       |
                    1024
                       |
                     512
                       |
                       1
                       |
                       v
                 Log-Price
                       |
                    expm1()
                       |
                       v
                Predicted Price
=======
# Product_price_prediction
>>>>>>> db753946c72c670ac74c41fe9ff52b6df31dd79e
