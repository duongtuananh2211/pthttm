# Project Work Breakdown Structure (WBS)

> Nguồn: `templates/Project_Work Breakdown Structure.xlsx` (sheet `WBS`) · Kế hoạch tổng quát: [project-action-plan.md](project-action-plan.md)

| Field | Value |
| --- | --- |
| Today | `=TODAY()` |
| Project Team Name | Nhóm 11 |
| Project Topic | Hệ thống chấm công thông minh bằng nhận diện khuôn mặt |

**Task Status** (danh sách chọn): `Done` · `In-progress` · `Delayed`. Ô trạng thái để trống nghĩa là task chưa bắt đầu.

## Tasks

Cấp độ task được thể hiện bằng số đánh mục (`1.` → `1.1.` → `1.1.1.` → `1.1.1.1.`). Nhóm có 3 thành viên; tên và vai trò theo mục "Vai trò của từng thành viên" trong kế hoạch dự án.

| Task | Start date | End date | Responsibility | Deliverable | Task Status |
| --- | --- | --- | --- | --- | --- |
| **1. Khởi động và lập kế hoạch** | 12/10/2026 | 21/10/2026 | Dương Tuấn Anh | Kế hoạch dự án, WBS, mô tả nghiệp vụ, môi trường | In-progress |
| &nbsp;&nbsp;1.1. Lập kế hoạch dự án (Action Plan) | 12/10/2026 | 12/10/2026 | Dương Tuấn Anh | `project-action-plan.md` | Done |
| &nbsp;&nbsp;1.2. Lập WBS | 12/10/2026 | 12/10/2026 | Dương Tuấn Anh | `project-work-breakdown-structure.md` | Done |
| &nbsp;&nbsp;1.3. Khảo sát nghiệp vụ chấm công, phát biểu bài toán ML, xác định yêu cầu dữ liệu | 19/10/2026 | 20/10/2026 | Dương Tuấn Anh | Mô tả nghiệp vụ, yêu cầu hệ thống, quy trình thu dữ liệu |  |
| &nbsp;&nbsp;1.4. Chốt công nghệ, dựng repo và môi trường | 20/10/2026 | 21/10/2026 | Dương Tuấn Anh, Bùi Như Quỳnh | Repo, môi trường Python chạy được |  |
| **2. Dữ liệu** | 19/10/2026 | 27/10/2026 | Trần Lâm Phong | Bộ dữ liệu sạch chia theo buổi, báo cáo EDA |  |
| &nbsp;&nbsp;2.1. Chuẩn bị thu thập | 19/10/2026 | 20/10/2026 | Trần Lâm Phong | Phiếu đồng ý, công cụ chụp ảnh |  |
| &nbsp;&nbsp;&nbsp;&nbsp;2.1.1. Soạn phiếu đồng ý, mời người tham gia | 19/10/2026 | 20/10/2026 | Trần Lâm Phong | Phiếu đồng ý đã ký (6 người) |  |
| &nbsp;&nbsp;&nbsp;&nbsp;2.1.2. Công cụ chụp ảnh từ webcam, quy ước đặt tên file và nhãn | 19/10/2026 | 20/10/2026 | Bùi Như Quỳnh | Script chụp ảnh, quy ước đặt tên |  |
| &nbsp;&nbsp;2.2. Thu thập dữ liệu | 20/10/2026 | 23/10/2026 | Trần Lâm Phong | Dữ liệu thô |  |
| &nbsp;&nbsp;&nbsp;&nbsp;2.2.1. Buổi A: chụp khuôn mặt (nhiều góc, ánh sáng, kính, khẩu trang) | 20/10/2026 | 21/10/2026 | Trần Lâm Phong, Cả nhóm | 20–30 ảnh/người (tập đăng ký + validation) |  |
| &nbsp;&nbsp;&nbsp;&nbsp;2.2.2. Tải LFW, tập con CelebA-Spoof và mô hình huấn luyện sẵn (SCRFD, ArcFace, MiniFASNet) | 21/10/2026 | 21/10/2026 | Bùi Như Quỳnh | Dữ liệu công khai, trọng số mô hình |  |
| &nbsp;&nbsp;&nbsp;&nbsp;2.2.3. Chụp ảnh tấn công giả mạo (ảnh in, màn hình) | 22/10/2026 | 22/10/2026 | Trần Lâm Phong, Bùi Như Quỳnh | Tập ảnh giả mạo có nhãn |  |
| &nbsp;&nbsp;&nbsp;&nbsp;2.2.4. Buổi B: chụp lại ở ngày và vị trí khác | 23/10/2026 | 23/10/2026 | Trần Lâm Phong, Cả nhóm | 20–30 ảnh/người (tập test) |  |
| &nbsp;&nbsp;2.3. Làm sạch (dùng SCRFD có sẵn), gán nhãn, loại ảnh gần trùng, chia tập theo buổi | 22/10/2026 | 26/10/2026 | Trần Lâm Phong | Bộ dữ liệu v1: đăng ký/validation (buổi A), test (buổi B), tập giả mạo |  |
| &nbsp;&nbsp;2.4. Phân tích dữ liệu khám phá (EDA) | 26/10/2026 | 27/10/2026 | Trần Lâm Phong | Thống kê, biểu đồ, t-SNE embedding (ArcFace có sẵn) |  |
| **3. Mô hình AI** | 23/10/2026 | 05/11/2026 | Bùi Như Quỳnh | Pipeline nhận diện + chống giả mạo, mô hình đã huấn luyện |  |
| &nbsp;&nbsp;3.1. Pipeline nhận diện khuôn mặt | 23/10/2026 | 29/10/2026 | Bùi Như Quỳnh | Module nhận diện |  |
| &nbsp;&nbsp;&nbsp;&nbsp;3.1.1. Phát hiện và căn chỉnh khuôn mặt (SCRFD) | 23/10/2026 | 26/10/2026 | Bùi Như Quỳnh | Ảnh mặt 112×112 đã căn chỉnh |  |
| &nbsp;&nbsp;&nbsp;&nbsp;3.1.2. Trích xuất embedding (ArcFace) | 27/10/2026 | 27/10/2026 | Bùi Như Quỳnh | Vector 512 chiều |  |
| &nbsp;&nbsp;&nbsp;&nbsp;3.1.3. So khớp cosine, chọn ngưỡng trên validation | 28/10/2026 | 29/10/2026 | Bùi Như Quỳnh | Ngưỡng tương đồng, FAR/FRR trên validation |  |
| &nbsp;&nbsp;3.2. Huấn luyện k-NN, SVM trên embedding, so sánh với cosine | 29/10/2026 | 30/10/2026 | Bùi Như Quỳnh | Mô hình k-NN/SVM, bảng so sánh |  |
| &nbsp;&nbsp;3.3. So sánh baseline: Haar Cascade (phát hiện), FaceNet (embedding) trên dữ liệu nhóm và LFW | 28/10/2026 | 29/10/2026 | Trần Lâm Phong | Bảng so sánh (tỷ lệ phát hiện, độ trễ, độ chính xác, FAR) |  |
| &nbsp;&nbsp;3.4. Khối chống giả mạo | 02/11/2026 | 05/11/2026 | Bùi Như Quỳnh | Module liveness, tỷ lệ chặn giả mạo |  |
| &nbsp;&nbsp;&nbsp;&nbsp;3.4.1. Fine-tune MiniFASNet trên dữ liệu nhóm + CelebA-Spoof, early stopping | 02/11/2026 | 04/11/2026 | Bùi Như Quỳnh | Mô hình đã fine-tune, đường cong loss train/validation |  |
| &nbsp;&nbsp;&nbsp;&nbsp;3.4.2. Đánh giá chống giả mạo (APCER, BPCER); làm kiểm tra chớp mắt nếu chưa đạt | 04/11/2026 | 05/11/2026 | Bùi Như Quỳnh | Bảng kết quả chống giả mạo |  |
| **4. Kiến trúc, CSDL và logic chấm công** | 22/10/2026 | 04/11/2026 | Dương Tuấn Anh | Sơ đồ hệ thống, CSDL, module chấm công |  |
| &nbsp;&nbsp;4.1. Thiết kế kiến trúc tổng thể, sơ đồ hệ thống | 22/10/2026 | 23/10/2026 | Dương Tuấn Anh | Sơ đồ hệ thống (mục 2.4 báo cáo) |  |
| &nbsp;&nbsp;4.2. Thiết kế CSDL SQLite (nhân viên, embedding, ca làm, chấm công, log chỉnh sửa) | 26/10/2026 | 27/10/2026 | Dương Tuấn Anh | Sơ đồ CSDL |  |
| &nbsp;&nbsp;4.3. Module đọc webcam, đưa khung hình vào pipeline | 28/10/2026 | 28/10/2026 | Dương Tuấn Anh | Luồng video vào hệ thống |  |
| &nbsp;&nbsp;4.4. Module đăng ký nhân viên và nhận diện (nối pipeline với CSDL) | 29/10/2026 | 30/10/2026 | Dương Tuấn Anh | Hàm đăng ký/nhận diện dùng chung cho giao diện |  |
| &nbsp;&nbsp;4.5. Logic chấm công: xác nhận nhiều khung hình, chống ghi trùng, ca làm, đi muộn/về sớm | 02/11/2026 | 04/11/2026 | Dương Tuấn Anh | Module chấm công |  |
| **5. Giao diện (Streamlit)** | 30/10/2026 | 05/11/2026 | Trần Lâm Phong | Màn hình chấm công, trang quản trị, kịch bản kiểm thử |  |
| &nbsp;&nbsp;5.1. Wireframe và kịch bản kiểm thử (chức năng, độ chính xác, độ trễ, giả mạo) | 30/10/2026 | 30/10/2026 | Trần Lâm Phong | Wireframe, danh sách test case |  |
| &nbsp;&nbsp;5.2. Màn hình chấm công (camera, kết quả, độ tương đồng, cảnh báo giả mạo) | 02/11/2026 | 03/11/2026 | Trần Lâm Phong | Màn hình chấm công |  |
| &nbsp;&nbsp;5.3. Trang quản trị: đăng ký nhân viên, lịch sử, thống kê, xuất Excel | 03/11/2026 | 05/11/2026 | Trần Lâm Phong | Trang quản trị |  |
| **6. Tích hợp, kiểm thử và phản hồi** | 05/11/2026 | 12/11/2026 | Dương Tuấn Anh | Hệ thống hoàn chỉnh, báo cáo kiểm thử, danh sách cải tiến |  |
| &nbsp;&nbsp;6.1. Tích hợp toàn hệ thống, tối ưu độ trễ (< 1 giây/lượt), demo end-to-end | 05/11/2026 | 06/11/2026 | Dương Tuấn Anh, Bùi Như Quỳnh | Bản demo chạy từ đầu đến cuối, số đo ms/khung hình |  |
| &nbsp;&nbsp;6.2. Dự phòng: sửa lỗi tích hợp, quay lại Modeling nếu chưa đạt mục tiêu trên validation | 09/11/2026 | 09/11/2026 | Cả nhóm | Bản sửa lỗi, ghi chú vòng lặp |  |
| &nbsp;&nbsp;6.3. Dùng thử thực tế 4 ngày, ghi log nhận sai/nhận chậm/chặn nhầm, tinh chỉnh ngưỡng và dữ liệu | 09/11/2026 | 12/11/2026 | Cả nhóm | Danh sách lỗi và cải tiến |  |
| &nbsp;&nbsp;6.4. Kiểm thử trên tập test (rank-1, FAR, FRR, TAR@FAR, APCER, BPCER, độ trễ) | 10/11/2026 | 10/11/2026 | Trần Lâm Phong, Bùi Như Quỳnh | Bảng kết quả kiểm thử |  |
| &nbsp;&nbsp;6.5. Kiểm tra công bằng theo nhóm (giới tính, kính, khẩu trang, ánh sáng) | 11/11/2026 | 11/11/2026 | Trần Lâm Phong | Kết quả theo từng nhóm |  |
| **7. Báo cáo và thuyết trình** | 10/11/2026 | 13/11/2026 | Dương Tuấn Anh | Báo cáo, slide, video demo |  |
| &nbsp;&nbsp;7.1. Viết báo cáo cuối kỳ | 10/11/2026 | 12/11/2026 | Dương Tuấn Anh, Cả nhóm | `project-final-report.md` |  |
| &nbsp;&nbsp;7.2. Làm slide và quay video demo | 11/11/2026 | 12/11/2026 | Bùi Như Quỳnh | Slide, video demo |  |
| &nbsp;&nbsp;7.3. Tập demo và nộp bài | 13/11/2026 | 13/11/2026 | Cả nhóm | Bài nộp hoàn chỉnh |  |

**Ghi chú về thứ tự phụ thuộc:**

- Trọng số SCRFD và ArcFace được tải từ 21/10 (task 2.2.2), nên bước làm sạch (2.3) dùng được detector có sẵn để loại ảnh không thấy mặt, và EDA (2.4) vẽ được t-SNE trước khi pipeline 3.1 hoàn thiện.
- Dữ liệu buổi A dùng cho đăng ký và validation, buổi B chỉ dùng cho kiểm thử cuối (6.4). Tập test không được dùng để chọn ngưỡng hay siêu tham số.
- Module webcam (4.3) và module đăng ký/nhận diện (4.4) xong trước 02/11 để giao diện (5.2, 5.3) gọi trực tiếp, không cần backend API riêng.
- Ngày 09/11 (6.2) để trống cho vòng lặp Evaluation → Modeling của quy trình 10 bước: nếu sau tích hợp chưa đạt mục tiêu thì sửa lỗi hoặc quay lại mô hình trước khi chạy tập test.

## Timeline (4 tuần × 5 ngày)

Đánh dấu `■` vào ngày mà task được thực hiện. Task 1.1 và 1.2 đã xong ngày 12/10/2026, trước khi bắt đầu tuần 1, nên không có trong timeline.

| Task | W1 · D1 | D2 | D3 | D4 | D5 | W2 · D6 | D7 | D8 | D9 | D10 | W3 · D11 | D12 | D13 | D14 | D15 | W4 · D16 | D17 | D18 | D19 | D20 |
| --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- | --- |
| *Ngày* | 19/10 | 20/10 | 21/10 | 22/10 | 23/10 | 26/10 | 27/10 | 28/10 | 29/10 | 30/10 | 02/11 | 03/11 | 04/11 | 05/11 | 06/11 | 09/11 | 10/11 | 11/11 | 12/11 | 13/11 |
| **1. Khởi động và lập kế hoạch** | ■ | ■ | ■ |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| &nbsp;&nbsp;1.3. Khảo sát nghiệp vụ chấm công, phát biểu bài toán ML, xác định yêu cầu dữ liệu | ■ | ■ |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| &nbsp;&nbsp;1.4. Chốt công nghệ, dựng repo và môi trường |  | ■ | ■ |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| **2. Dữ liệu** | ■ | ■ | ■ | ■ | ■ | ■ | ■ |  |  |  |  |  |  |  |  |  |  |  |  |  |
| &nbsp;&nbsp;2.1. Chuẩn bị thu thập | ■ | ■ |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| &nbsp;&nbsp;&nbsp;&nbsp;2.1.1. Soạn phiếu đồng ý, mời người tham gia | ■ | ■ |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| &nbsp;&nbsp;&nbsp;&nbsp;2.1.2. Công cụ chụp ảnh từ webcam, quy ước đặt tên file và nhãn | ■ | ■ |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| &nbsp;&nbsp;2.2. Thu thập dữ liệu |  | ■ | ■ | ■ | ■ |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| &nbsp;&nbsp;&nbsp;&nbsp;2.2.1. Buổi A: chụp khuôn mặt (nhiều góc, ánh sáng, kính, khẩu trang) |  | ■ | ■ |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| &nbsp;&nbsp;&nbsp;&nbsp;2.2.2. Tải LFW, tập con CelebA-Spoof và mô hình huấn luyện sẵn (SCRFD, ArcFace, MiniFASNet) |  |  | ■ |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| &nbsp;&nbsp;&nbsp;&nbsp;2.2.3. Chụp ảnh tấn công giả mạo (ảnh in, màn hình) |  |  |  | ■ |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| &nbsp;&nbsp;&nbsp;&nbsp;2.2.4. Buổi B: chụp lại ở ngày và vị trí khác |  |  |  |  | ■ |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| &nbsp;&nbsp;2.3. Làm sạch (dùng SCRFD có sẵn), gán nhãn, loại ảnh gần trùng, chia tập theo buổi |  |  |  | ■ | ■ | ■ |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| &nbsp;&nbsp;2.4. Phân tích dữ liệu khám phá (EDA) |  |  |  |  |  | ■ | ■ |  |  |  |  |  |  |  |  |  |  |  |  |  |
| **3. Mô hình AI** |  |  |  |  | ■ | ■ | ■ | ■ | ■ | ■ | ■ | ■ | ■ | ■ |  |  |  |  |  |  |
| &nbsp;&nbsp;3.1. Pipeline nhận diện khuôn mặt |  |  |  |  | ■ | ■ | ■ | ■ | ■ |  |  |  |  |  |  |  |  |  |  |  |
| &nbsp;&nbsp;&nbsp;&nbsp;3.1.1. Phát hiện và căn chỉnh khuôn mặt (SCRFD) |  |  |  |  | ■ | ■ |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| &nbsp;&nbsp;&nbsp;&nbsp;3.1.2. Trích xuất embedding (ArcFace) |  |  |  |  |  |  | ■ |  |  |  |  |  |  |  |  |  |  |  |  |  |
| &nbsp;&nbsp;&nbsp;&nbsp;3.1.3. So khớp cosine, chọn ngưỡng trên validation |  |  |  |  |  |  |  | ■ | ■ |  |  |  |  |  |  |  |  |  |  |  |
| &nbsp;&nbsp;3.2. Huấn luyện k-NN, SVM trên embedding, so sánh với cosine |  |  |  |  |  |  |  |  | ■ | ■ |  |  |  |  |  |  |  |  |  |  |
| &nbsp;&nbsp;3.3. So sánh baseline: Haar Cascade (phát hiện), FaceNet (embedding) trên dữ liệu nhóm và LFW |  |  |  |  |  |  |  | ■ | ■ |  |  |  |  |  |  |  |  |  |  |  |
| &nbsp;&nbsp;3.4. Khối chống giả mạo |  |  |  |  |  |  |  |  |  |  | ■ | ■ | ■ | ■ |  |  |  |  |  |  |
| &nbsp;&nbsp;&nbsp;&nbsp;3.4.1. Fine-tune MiniFASNet trên dữ liệu nhóm + CelebA-Spoof, early stopping |  |  |  |  |  |  |  |  |  |  | ■ | ■ | ■ |  |  |  |  |  |  |  |
| &nbsp;&nbsp;&nbsp;&nbsp;3.4.2. Đánh giá chống giả mạo (APCER, BPCER); làm kiểm tra chớp mắt nếu chưa đạt |  |  |  |  |  |  |  |  |  |  |  |  | ■ | ■ |  |  |  |  |  |  |
| **4. Kiến trúc, CSDL và logic chấm công** |  |  |  | ■ | ■ | ■ | ■ | ■ | ■ | ■ | ■ | ■ | ■ |  |  |  |  |  |  |  |
| &nbsp;&nbsp;4.1. Thiết kế kiến trúc tổng thể, sơ đồ hệ thống |  |  |  | ■ | ■ |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |
| &nbsp;&nbsp;4.2. Thiết kế CSDL SQLite (nhân viên, embedding, ca làm, chấm công, log chỉnh sửa) |  |  |  |  |  | ■ | ■ |  |  |  |  |  |  |  |  |  |  |  |  |  |
| &nbsp;&nbsp;4.3. Module đọc webcam, đưa khung hình vào pipeline |  |  |  |  |  |  |  | ■ |  |  |  |  |  |  |  |  |  |  |  |  |
| &nbsp;&nbsp;4.4. Module đăng ký nhân viên và nhận diện (nối pipeline với CSDL) |  |  |  |  |  |  |  |  | ■ | ■ |  |  |  |  |  |  |  |  |  |  |
| &nbsp;&nbsp;4.5. Logic chấm công: xác nhận nhiều khung hình, chống ghi trùng, ca làm, đi muộn/về sớm |  |  |  |  |  |  |  |  |  |  | ■ | ■ | ■ |  |  |  |  |  |  |  |
| **5. Giao diện (Streamlit)** |  |  |  |  |  |  |  |  |  | ■ | ■ | ■ | ■ | ■ |  |  |  |  |  |  |
| &nbsp;&nbsp;5.1. Wireframe và kịch bản kiểm thử (chức năng, độ chính xác, độ trễ, giả mạo) |  |  |  |  |  |  |  |  |  | ■ |  |  |  |  |  |  |  |  |  |  |
| &nbsp;&nbsp;5.2. Màn hình chấm công (camera, kết quả, độ tương đồng, cảnh báo giả mạo) |  |  |  |  |  |  |  |  |  |  | ■ | ■ |  |  |  |  |  |  |  |  |
| &nbsp;&nbsp;5.3. Trang quản trị: đăng ký nhân viên, lịch sử, thống kê, xuất Excel |  |  |  |  |  |  |  |  |  |  |  | ■ | ■ | ■ |  |  |  |  |  |  |
| **6. Tích hợp, kiểm thử và phản hồi** |  |  |  |  |  |  |  |  |  |  |  |  |  | ■ | ■ | ■ | ■ | ■ | ■ |  |
| &nbsp;&nbsp;6.1. Tích hợp toàn hệ thống, tối ưu độ trễ (< 1 giây/lượt), demo end-to-end |  |  |  |  |  |  |  |  |  |  |  |  |  | ■ | ■ |  |  |  |  |  |
| &nbsp;&nbsp;6.2. Dự phòng: sửa lỗi tích hợp, quay lại Modeling nếu chưa đạt mục tiêu trên validation |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  | ■ |  |  |  |  |
| &nbsp;&nbsp;6.3. Dùng thử thực tế 4 ngày, ghi log nhận sai/nhận chậm/chặn nhầm, tinh chỉnh ngưỡng và dữ liệu |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  | ■ | ■ | ■ | ■ |  |
| &nbsp;&nbsp;6.4. Kiểm thử trên tập test (rank-1, FAR, FRR, TAR@FAR, APCER, BPCER, độ trễ) |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  | ■ |  |  |  |
| &nbsp;&nbsp;6.5. Kiểm tra công bằng theo nhóm (giới tính, kính, khẩu trang, ánh sáng) |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  | ■ |  |  |
| **7. Báo cáo và thuyết trình** |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  | ■ | ■ | ■ | ■ |
| &nbsp;&nbsp;7.1. Viết báo cáo cuối kỳ |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  | ■ | ■ | ■ |  |
| &nbsp;&nbsp;7.2. Làm slide và quay video demo |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  | ■ | ■ |  |
| &nbsp;&nbsp;7.3. Tập demo và nộp bài |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  |  | ■ |

> Lịch dự kiến 19/10/2026 – 13/11/2026 (chỉ tính ngày làm việc thứ 2 – thứ 6), cần chỉnh lại theo lịch thực tế của lớp.
