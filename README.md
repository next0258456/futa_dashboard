# ⚡ EV Charging Station Strategic Analytics Dashboard

[![Data Storage](https://img.shields.io/badge/Raw%20Data-Google%20Drive-blue?style=for-the-badge&logo=googledrive)](https://drive.google.com/drive/folders/1M1btDPvGyFhwT5LloZWJZ3hw0ydVpQqi?usp=sharing)
[![Spatial Index](https://img.shields.io/badge/Spatial%20Index-Uber%20H3-orange?style=for-the-badge)](https://h3geo.org/)
[![Visualization](https://img.shields.io/badge/UI%20Layer-Leaflet%20%7C%20Chart.js-brightgreen?style=for-the-badge)](https://leafletjs.com/)

## 🎯 Tổng Quan Dự Án
Dự án này là bộ **Sa bàn Mô phỏng và Tối ưu hóa Vận hành Trạm Sạc Xe Điện** dành cho đội xe quy mô lớn (Mega-Fleet với hơn 1.500 xe). Hệ thống giải quyết bài toán kinh tế cốt lõi trước khi xuống tiền đầu tư CapEx: **Tìm điểm cân bằng tối ưu giữa Chi phí cơ sở hạ tầng (Đất, Trụ súng, Trạm biến áp) và Chi phí hao tổn vận hành đội xe (Km chạy rỗng, Thời gian tài xế chờ sạc)**.

Dự án được đóng gói dưới dạng **Kiến trúc Độc lập Không phụ thuộc (Zero-Dependency Standalone Architecture)**. Toàn bộ luồng tính toán tài chính, xoay trục kịch bản và hiển thị bản đồ không gian diễn ra trực tiếp trên trình duyệt của người dùng mà không cần cấu hình server phức tạp.

---

## 📂 Kho Dữ Liệu Mô Phỏng Gốc (Raw Datasets)
Do quy mô của luồng dữ liệu mô phỏng kịch bản vận hành và ma trận khoảng cách không gian rất lớn, toàn bộ tệp dữ liệu thô (Raw Data) cấu trúc để thẩm định đã được lưu trữ tập trung tại đây:

👉 **[Truy cập Kho Dữ Liệu Mô Phỏng Gốc (Google Drive)](https://drive.google.com/drive/folders/1M1btDPvGyFhwT5LloZWJZ3hw0ydVpQqi?usp=sharing)**

*Kho lưu trữ bao gồm các tệp ma trận phân tích hành vi đội xe, phân phối thời gian chờ sạc và dữ liệu lưới trạm biến áp nền tảng được trích xuất từ lõi mô phỏng.*

---

## 🛠️ Core Tech Stack (Tối Giản & Hiệu Năng)
Không sử dụng các framework nặng nề hay hệ thống cơ sở dữ liệu cồng kềnh, sa bàn tập trung vào hiệu năng thực thi cốt lõi thông qua:
* **Geospatial Discretization (Uber H3 Index):** Số hóa toàn bộ bản đồ khu vực vận hành thành các ô lưới lục giác Uber H3. Biến các phép toán truy vấn khoảng cách tọa độ liên tục thành các khóa lookup index có tốc độ phản hồi tính bằng mili-giây.
* **Dynamic Client-Side Financial Engine:** Toàn bộ công thức dự toán dòng tiền, khấu hao hạ tầng, chi phí kéo điện theo khoảng cách Trạm biến áp (TBA) và thuật toán tính toán **IRR (Internal Rate of Return)** được xử lý bằng Vanilla JS thời gian thực dựa trên các tham số cấu hình linh hoạt của người dùng.
* **High-Density Pre-computed Scenario Matrix:** Toàn bộ kết quả từ luồng mô phỏng ngẫu nhiên (Monte Carlo Simulation) đối với hành vi đội xe được tính toán trước và nén cấu trúc trực tiếp vào mã nguồn dưới dạng ma trận kịch bản đa mục tiêu.
* **Visualization Layer:** Sử dụng **Leaflet.js** để render bản đồ không gian H3 chia lớp linh hoạt (`Đất`, `Điện`, `IRR Mua`, `IRR Thuê`, `Tối ưu Fleet`) kẹp cùng **Chart.js** để trực quan hóa xu hướng hội tụ của kịch bản vận hành.

---

## 🏗️ Kiến Trúc Thư Mục Repo
```text
├── index.html           # Toàn bộ Não bộ Core Engine, Dữ liệu kịch bản nén và Giao diện Dashboard
└── README.md            # Tài liệu phân tích kiến trúc hệ thống
