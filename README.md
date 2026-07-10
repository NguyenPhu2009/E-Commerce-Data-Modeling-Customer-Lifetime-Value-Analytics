# E-Commerce Data Modeling & Customer Lifetime Value Analytics

![Python](https://img.shields.io/badge/Python-3776AB?style=for-the-badge&logo=python&logoColor=white)
![Pandas](https://img.shields.io/badge/Pandas-2C2D72?style=for-the-badge&logo=pandas&logoColor=white)
![NumPy](https://img.shields.io/badge/NumPy-013243?style=for-the-badge&logo=numpy&logoColor=white)
![Scikit-Learn](https://img.shields.io/badge/Scikit--Learn-F7931E?style=for-the-badge&logo=scikit-learn&logoColor=black)
![SQL](https://img.shields.io/badge/SQL-003B57?style=for-the-badge&logo=postgresql&logoColor=white)
![Power BI](https://img.shields.io/badge/Power_BI-F2C811?style=for-the-badge&logo=powerbi&logoColor=black)

## Project Overview
Dự án này xây dựng một luồng xử lý dữ liệu (Data Pipeline) hoàn chỉnh từ bộ dữ liệu thương mại điện tử Olist (~100.000 đơn hàng). Mục tiêu của dự án là thiết kế kho dữ liệu chuẩn hóa, phân cụm khách hàng tự động và xây dựng mô hình học máy (Machine Learning) để dự đoán khả năng mua lại của khách hàng (Repeat Purchase Prediction), từ đó đề xuất các chiến dịch giữ chân khách hàng (Retention Campaigns) hiệu quả.

## Tính năng & Workflow
1. **Data Modeling (ETL):** * Làm sạch và hợp nhất 8 bảng dữ liệu quan hệ nguyên bản thành mô hình **Star Schema** tối ưu cho truy vấn phân tích (OLAP).
2. **Customer Segmentation:** * Xây dựng hệ thống chấm điểm **RFM** (Recency, Frequency, Monetary).
   * Ứng dụng thuật toán **K-Means Clustering** để tự động gom cụm khách hàng dựa trên hành vi mua sắm thay vì dùng quy tắc tĩnh (Rule-based).
3. **Predictive Modeling (XGBoost):** * Xây dựng mô hình phân loại để dự đoán khách hàng có quay lại mua lần 2 hay không dựa trên thông tin của đơn hàng đầu tiên.

## Business Insights
* **Xử lý dữ liệu mất cân bằng nghiêm trọng (Extreme Imbalanced Data):** Tỉ lệ khách hàng mua lại của Olist chỉ ở mức **~3%**. Việc này khiến mô hình phân loại thông thường bị sai lệch. 
* **Giải pháp & Đánh đổi (The Trade-off):**
  * Áp dụng kỹ thuật **SMOTE** để tái cân bằng tập huấn luyện và tinh chỉnh **Decision Threshold xuống 0.35**. 
  * Kết quả: Chấp nhận hi sinh Precision để **tăng Recall của nhóm Repeat Customer từ 2% lên 71%**. 
  * **Business Value:** Trong bài toán E-commerce, chi phí gửi Email/Push Notification cho một tập khách hàng là rất thấp (Low False Positive Cost). Việc tăng Recall giúp hệ thống CRM không bỏ sót bất kỳ khách hàng trung thành tiềm năng nào.
* **Top Predictors:** Phân tích *Feature Importances* chỉ ra rằng `review_score` (điểm đánh giá ở đơn hàng đầu tiên) là yếu tố quyết định lớn nhất đến việc khách hàng có tiếp tục mua sắm hay không.

## Cấu trúc Repository
```text
├── data/
│   ├── raw/
|   ├── cleaned/        
│   ├── star_schema/        
│   └── model/            
├── notebooks/
│   └── data_cleaning.ipynb
|   └── star_schema.ipynb
|   └── segmentation_and_modeling.ipynb
├── dashboard/
└── README.md
