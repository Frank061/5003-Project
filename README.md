# Replication of "The Case for Learned Index Structures"

**Course Project - Track 2**
**Team:** FLY8CENT

## 📌 Project Overview
This repository contains the replication code for the SIGMOD 2018 paper *[The Case for Learned Index Structures](https://dl.acm.org/doi/10.1145/3183713.3196909)*. 

We successfully implemented the core concepts of "Indexes as Models" using **Python** and **TensorFlow**, verifying that machine learning models can outperform traditional structures (B-Trees, Bloom Filters) in terms of search precision and memory efficiency on structured data.

## 🚀 Key Features & Implementations

1.  **Recursive Model Index (RMI)**: 
    * Implemented a 2-stage hierarchy (Neural Network Root + Linear Regression Leafs).
    * **Critical Optimization**: Solved the "Model Collapse" issue on large integer keys by integrating **Batch Normalization** and **Min-Max Scaling**.
2.  **Hybrid Index Mechanism**:
    * Implemented a dynamic fallback strategy. If a model's prediction error exceeds a threshold ($\tau=128$), the system automatically switches to a B-Tree for that segment.
3.  **Learned Bloom Filter**:
    * Implemented the "Sandwich Structure" (Classifier + Backup Filter) to optimize memory usage.
4.  **Learned Hash Function**:
    * Implemented a CDF-based hash function to reduce collision rates compared to MurmurHash.

## 📊 Experimental Results

We evaluated the system on **982,335 unique integer keys** (Log-normal distribution).

| Metric | Result | Improvement |
| :--- | :--- | :--- |
| **Range Index Precision** | Search range reduced to **~55** | **17,748x** gain vs B-Tree |
| **Hybrid Robustness** | Fallback rate **1.0%** | Proven robustness on outliers |
| **Bloom Filter Memory** | **21.68 KB** (vs 58.5 KB) | **62.93%** space saving |
| **Hash Collision Rate** | **16.92%** (vs 25.74%) | **34.27%** reduction vs MurmurHash |

## 🛠️ Project Structure

```bash
├── Main.ipynb                        # The main code (Data Gen, Training, Evaluation)
├── requirements.txt                  # Python dependencies
├── README.md                         # Project documentation
```
##💻 How to Run

1. Clone the repository:

```bash
git clone [https://github.com/Frank061/5003_Project.git](https://github.com/Frank061/5003_Project.git)
cd 5003_Project
```

2. Install dependencies:
```bash
pip install -r requirements.txt
```

3. Run the Notebook:

- Open Main.ipynb in Jupyter Notebook, JupyterLab, or Google Colab.

- Click "Run All" to reproduce the data generation, model training, and benchmark evaluation.

- Note: The dataset is generated synthetically within the notebook, so no external data download is required.

## 📄 Reference
[1] Kraska, T., Beutel, A., Chi, E. H., Dean, J., & Polyzotis, N. (2018). The Case for Learned Index Structures. Proceedings of the 2018 International Conference on Management of Data (SIGMOD '18), 489–504.

[2] Ioffe, S., & Szegedy, C. (2015). Batch Normalization: Accelerating Deep Network Training by Reducing Internal Covariate Shift. International Conference on Machine Learning (ICML).

[3] Kim, C., et al. (2010). FAST: Fast Architecture Sensitive Tree Search on Modern CPUs and GPUs. Proceedings of the 2010 ACM SIGMOD International Conference on Management of Data, 339–350. (Source of the B-Tree baseline used in the original paper).
