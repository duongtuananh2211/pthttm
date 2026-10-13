# Lịch sử thay đổi: project-action-plan.md

> Tài liệu: [../documents/project-action-plan.md](../documents/project-action-plan.md)

| Phiên bản | Ngày | Thay đổi |
| --- | --- | --- |
| v1.0 | 2026-10-12 | Chọn đề tài "Hệ thống chấm công thông minh bằng nhận diện khuôn mặt", tên nhóm FaceIn. Điền các mục: mục tiêu, tóm tắt, phương pháp (quy trình 10 bước chương 3, pipeline RetinaFace/SCRFD → ArcFace → cosine → chống giả mạo, đạo đức AI), dữ liệu (LFW, dữ liệu tự thu 20–30 người, ảnh giả mạo), đầu ra mong muốn, vai trò 5 thành viên, lịch trình 4 tuần (19/10 – 13/11/2026). Tên thành viên và ngày bắt đầu chưa chốt. |
| v1.1 | 2026-10-13 | Sửa theo kết quả review dựa trên `knowledges/`. Thêm phần huấn luyện (fine-tune MiniFASNet có early stopping, huấn luyện k-NN/SVM trên embedding) để khớp với bước Modeling ở chương 3 và mục "Phương pháp huấn luyện" của báo cáo. Định nghĩa lại chỉ tiêu: rank-1 ≥ 95% tại FAR ≤ 1%, chặn giả mạo ≥ 90%, thêm APCER/BPCER. Chia dữ liệu theo buổi thu (buổi A: đăng ký/validation, buổi B: test) để tránh rò rỉ dữ liệu, ghi rõ cỡ mẫu; thêm tập con CelebA-Spoof. Thu hẹp phạm vi: baseline chỉ còn Haar Cascade và FaceNet, chốt Streamlit + SQLite, bỏ camera IP. Đạo đức AI thêm nguyên tắc tự do/tự chủ và nhân phẩm, ghi rõ dữ liệu sinh trắc học là dữ liệu nhạy cảm; phần công bằng bỏ tiêu chí màu da (ghi là hạn chế) và thêm khẩu trang. Thêm liên hệ chương 4 (eKYC, giáo dục). Chia lại vai trò cho đều hơn; feedback đổi thành dùng thử 4 ngày; lịch trình có ngày dự phòng cho vòng lặp. |
