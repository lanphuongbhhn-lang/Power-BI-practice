# Power-BI-practice
# 📊 Sales & Profit Analytics Dashboard Project

[![Excel](https://img.shields.io/badge/Tools-Excel-green?style=flat-square&logo=microsoft-excel)](https://www.microsoft.com/en-us/microsoft-365/excel)
[![Power BI](https://img.shields.io/badge/Tools-Power%20BI-yellow?style=flat-square&logo=power-bi)](https://powerbi.microsoft.com/)
[![Status](https://img.shields.io/badge/Project-Completed-brightgreen?style=flat-square)](#)

Dự án phân tích hiệu suất kinh doanh (Doanh thu & Lợi nhuận) dựa trên tệp dữ liệu giao dịch mẫu. Quy trình thực hiện đi từ khâu lấy mẫu ngẫu nhiên, làm sạch dữ liệu bằng Excel, trực quan hóa tương tác trên Dashboard đến việc trích xuất các insight chiến lược cốt lõi cho doanh nghiệp.

---

## 📋 Mục lục
1. [Phần 1: Làm sạch Dữ liệu & Thống kê Mô tả](#phần-1-làm-sạch-dữ-liệu--thống-kê-mô-tả)
2. [Phần 2: Trực quan hóa & Dashboard Tương tác](#phần-2-trực-quan-hóa--dashboard-tương-tác)
3. [Phần 3: Phân tích Chuyên sâu (Deep-dive Insights)](#phần-3-phân-tích-chuyên-sâu-deep-dive-insights)
4. [Phần 4: Kết luận & Hàm ý Chính sách](#phần-4-kết-luận--hàm-ý-chính-sách)

---

## Phần 1: Làm sạch Dữ liệu & Thống kê Mô tả

### 🧹 1. Quy trình lấy mẫu & Làm sạch (Thực hiện trên Excel)
Để đảm bảo dữ liệu tinh gọn và khách quan trước khi đưa vào công cụ BI, các bước sau đã được thực hiện:
* **Lấy mẫu ngẫu nhiên (Random Sampling):** 
  * Tạo một cột phụ và sử dụng hàm `=RAND()` để gán số ngẫu nhiên cho toàn bộ các dòng giao dịch.
  * Sao chép cột ngẫu nhiên này và dán lại dưới dạng **Value (Giá trị)** ở cột bên cạnh để cố định tập mẫu gồm **3.000 giao dịch**[cite: 3].
* **Làm sạch & Chuẩn hóa cấu trúc:**
  * **Định dạng Ngày tháng:** Chuyển đổi và định dạng lại cột ngày tháng về chuẩn đồng nhất[cite: 3].
  * **Xử lý chuỗi văn bản:** Áp dụng công cụ **Text to Columns** tại thẻ *Data* để phân tách chính xác dữ liệu ngày[cite: 3].
  * **Kiểm tra lỗi hệ thống (QA Benchmarks):** 
    * Xác nhận không có dòng dữ liệu nào bị trùng lặp (No duplicate rows)[cite: 3].
    * Xác nhận không có dữ liệu trống/bị khuyết thiếu (No missing data)[cite: 3].
    * Đảm bảo tất cả các cột định lượng (Sales, Profit,...) đã ở định dạng Số (Number)[cite: 3].

---

### 📉 2. Thống kê Mô tả (Descriptive Statistics)
Dữ liệu sạch sau đó được nạp nguyên trạng vào Power BI. Để phục vụ việc hiển thị các chỉ số trên Table/Matrix, một bảng chứa danh mục chỉ số đã được khởi tạo bằng cấu trúc **DAX**:

```dax
Statistic = 
DATATABLE(
    "Statistic", STRING,
    {
        {"Mean"},
        {"Median"},
        {"Mode"},
        {"StdDev"},
        {"Min"},
        {"Max"}
    }
)

### 📊 Bảng Matrix Thống kê Mô tả (Descriptive Statistics)

| Statistic | Sales Statistics | Profit Statistic |
| :--- | :---: | :---: |
| **Max** | 22,638.48 | 4,946.37 |
| **StdDev** | 634.20 | 172.80 |
| **Mean** | 215.04 | 24.04 |
| **Median** | 50.02 | 8.40 |
| **Mode** | 12.96 | 6.22 |
| **Min** | 0.44 | -2,929.48 |

*Dữ liệu được tổ chức dưới dạng bảng ma trận đa chiều, cho phép lọc tương tác bằng 2 Slicer: **Segment** (Consumer, Corporate, Home Office) và **Category** (Furniture, Office Supplies, Technology)[cite: 3].*

---

## Phần 2: Trực quan hóa & Dashboard Tương tác

`![Dashboard Overview]
<img width="842" height="490" alt="image" src="https://github.com/user-attachments/assets/f7558975-6a87-4a96-b9f8-e6acff785da2" />

<details>
<summary>📐 <b>Xem chi tiết: Thiết kế biểu đồ & Ứng dụng doanh nghiệp</b> (Click để mở rộng)</summary>

1. **Clustered Bar Chart (Ngang) – Doanh thu & Lợi nhuận Trung bình theo Segment**
   * *Ý nghĩa:* So sánh trực tiếp hiệu suất trung bình giữa các phân khúc khách hàng[cite: 3].
   * *Ứng dụng:* Giúp định vị nhóm khách hàng mang lại biên lợi nhuận tốt nhất để tối ưu chi phí phục vụ[cite: 3].
2. **Clustered Bar Chart (Ngang) – Tổng Doanh thu & Tổng Lợi nhuận theo Segment**
   * *Ý nghĩa:* Đánh giá quy mô đóng góp tuyệt đối thay vì giá trị trung bình[cite: 3].
   * *Ứng dụng:* Phát hiện các phân khúc "doanh thu khủng nhưng lợi nhuận mỏng"[cite: 3].
3. **Clustered Column Chart (Dọc) – Tổng Sales theo Region**
   * *Ý nghĩa:* So sánh doanh thu địa lý giữa các vùng (West, South, East, Central), kết hợp Line xu hướng[cite: 3].
   * *Ứng dụng:* Hỗ trợ phân bổ nguồn lực bán hàng, marketing và lập kế hoạch kho bãi[cite: 3].
4. **Donut Chart – Tổng Sales theo Category**
   * *Ý nghĩa:* Thể hiện tỷ trọng đóng góp của 3 nhóm sản phẩm lớn[cite: 3].
   * *Ứng dụng:* Xác định sản phẩm "xương sống" để tập trung đầu tư R&D và Marketing[cite: 3].
5. **Scatter Chart – Ngoại lai Sales theo phân bố Discount**
   * *Ý nghĩa:* Phát hiện các điểm bất thường (outliers) trong mối quan hệ giữa chiết khấu và doanh số[cite: 3].
   * *Ứng dụng:* Kiểm soát tính hiệu quả của chiến dịch giảm giá, ngăn ngừa việc giảm sâu gây lỗ[cite: 3].
</details>

---

## Phần 3: Phân tích Chuyên sâu (Deep-dive Insights)

### 👥 1. Hiệu năng theo Phân khúc Khách hàng (Segment)
* **Corporate:** Là **phân khúc sinh lời tốt nhất** (cả về giá trị trung bình lẫn tổng giá trị đóng góp)[cite: 3]. Đây là nhóm khách hàng ổn định và mang lại giá trị dài hạn[cite: 3].
* **Home Office:** Đang rơi vào bẫy "doanh số ảo"[cite: 3]. Doanh số bán ra tương đối ổn định nhưng lợi nhuận mang lại rất thấp, có thể do chi phí phục vụ hoặc tỷ lệ chiết khấu quá cao[cite: 3].
* **Consumer:** Chiếm volume lớn nhưng biên lợi nhuận mỏng[cite: 3].

### 📉 2. Tác động của Chính sách Chiết khấu (Discount)
* Phân tích cho thấy **Discount có ảnh hưởng cực kỳ tiêu cực đến Profit**[cite: 3].
* **Ngưỡng nguy hiểm:** Khi mức Discount vượt quá **0.3 (30%)**, Profit của doanh nghiệp ngay lập tức bị xói mòn và lao dốc xuống mức âm (thua lỗ)[cite: 3].
* **Điểm ngoại lai (Outliers):** Biểu đồ Scatter phân tán chỉ ra các điểm bất thường: có những đơn hàng được giảm giá cực sâu nhưng Doanh số lại không tăng tương ứng; ngược lại có những giao dịch không cần chiết khấu vẫn phát sinh doanh số lớn[cite: 3].

### 📦 3. Danh mục Sản phẩm & Địa lý vùng miền
* **Technology** là danh mục chiếm tỷ trọng doanh thu cao nhất (khoảng **34.79%**), đóng vai trò là "mũi nhọn" tăng trưởng doanh thu[cite: 3].
* **South** và **West** là các vùng có mức tổng doanh số dẫn đầu, trong đó vùng **Central** có mức đóng góp thấp hơn hẳn, bộc lộ sự hạn chế về mặt thị phần[cite: 3].

---

## Phần 4: Kết luận & Hàm ý Chính sách

┌────────────────────────────────────────────────────────────────────────┐
│                      KẾ HOẠCH HÀNH ĐỘNG CHIẾN LƯỢC                     │
└───────────────────────────────────┬────────────────────────────────────┘
                                    │
         ┌──────────────────────────┼──────────────────────────┐
         ▼                          ▼                          ▼
┌──────────────────┐       ┌──────────────────┐       ┌──────────────────┐
│  ƯU TIÊN NHÓM    │       │ SIẾT CHẶT KHUNG  │       │ BÁN CHÉO SẢN PHẨM│
│    CORPORATE     │       │     DISCOUNT     │       │  (CROSS-SELLING) │
│ Thiết lập dịch vụ│       │ Khống chế mức    │       │ Đóng gói Combo:  │
│ VIP chuyên biệt. │       │ chiết khấu < 30%.│       │ Tech + Furniture.│
└──────────────────┘       └──────────────────┘       └──────────────────┘


1. **Tập trung nguồn lực vào phân khúc Corporate:** Xây dựng chính sách chăm sóc khách hàng VIP, hợp đồng dài hạn để tối ưu dòng tiền ổn định[cite: 3].
2. **Quản trị rủi ro chiết khấu:** Cài đặt hạn mức chiết khấu trên hệ thống bán hàng, kiểm soát chặt chẽ các đơn hàng có mức chiết khấu từ 30% trở lên để ngăn ngừa rủi ro lỗ nặng[cite: 3].
3. **Đẩy mạnh chiến lược Bán chéo (Cross-selling):** Tận dụng sức hút của ngành hàng **Technology** để bán kèm các dòng sản phẩm có dòng tiền ổn định như **Office Supplies** và **Furniture**[cite: 3].
4. **Tái phân bổ nguồn lực vùng miền:** Tập trung giữ chân khách hàng tại các vùng trọng điểm (West, South) và đánh giá lại hiệu quả chi phí vận hành tại vùng Central[cite: 3].
5. **Giám sát rủi ro đuôi (Tail-Risk):** Thiết lập hệ thống cảnh báo sớm khi biên lợi nhuận của một đơn hàng bị rơi vào vùng âm quá sâu[cite: 3].
