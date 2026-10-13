# Kế hoạch dự án

> AI Course · Nguồn: `templates/Project_Action Plan.docx`

| Mục | Nội dung |
| --- | --- |
| Môn học | Phát triển hệ thống thông minh |
| Tên nhóm | Nhóm 11 |
| Trưởng nhóm / Các thành viên nhóm | Dương Tuấn Anh / Trần Lâm Phong, Bùi Như Quỳnh |
| Tên đề tài | Hệ thống chấm công thông minh bằng nhận diện khuôn mặt |

## Mục tiêu

- Xây dựng hệ thống chấm công tự động: nhân viên chỉ cần đứng trước camera, hệ thống nhận diện khuôn mặt và ghi giờ vào/ra, không cần thẻ từ hay ký sổ.
- Áp dụng thị giác máy tính (phát hiện, nhận dạng khuôn mặt bằng CNN) vào một bài toán quản lý có thật trong doanh nghiệp và trường học.
- Tỷ lệ nhận diện đúng người đã đăng ký (rank-1) từ 95% trở lên trên tập test của nhóm, tại ngưỡng mà tỷ lệ nhận nhầm người lạ (FAR) không quá 1%; thời gian xử lý mỗi lượt chấm công dưới 1 giây.
- Chống gian lận cơ bản: phát hiện việc dùng ảnh in hoặc ảnh trên điện thoại để chấm công hộ (liveness detection), chặn được từ 90% trở lên các lần tấn công trên tập test.
- Tự huấn luyện hai thành phần: fine-tune mô hình chống giả mạo trên dữ liệu của nhóm, và huấn luyện bộ phân loại trên embedding để so sánh với so khớp cosine.
- Có giao diện quản trị để đăng ký nhân viên, xem lịch sử chấm công và xuất báo cáo.
- Đi đủ quy trình 10 bước xây dựng hệ thống thông minh và tuân thủ các nguyên tắc đạo đức AI, nhất là quyền riêng tư và công bằng.

## Tóm tắt

Chấm công bằng thẻ hoặc vân tay vẫn có thể bị quẹt thẻ hộ, và máy vân tay dùng chung thì phải tiếp xúc. Nhóm xây dựng một hệ thống chấm công dùng camera: hệ thống phát hiện khuôn mặt trong khung hình, căn chỉnh khuôn mặt, trích xuất vector đặc trưng (embedding) bằng mạng CNN đã huấn luyện sẵn, rồi so khớp với cơ sở dữ liệu nhân viên đã đăng ký để xác định danh tính và ghi nhận giờ vào/ra. Một mô hình chống giả mạo do nhóm fine-tune sẽ chặn các lần dùng ảnh in hoặc ảnh trên màn hình. Mỗi nhân viên chỉ cần đăng ký 5–10 ảnh, hệ thống không phải huấn luyện lại khi thêm người mới. Kết quả được hiển thị trên giao diện web cho quản lý theo dõi và xuất báo cáo chấm công. Cách làm này giống bài toán eKYC (khớp khuôn mặt kết hợp chống giả mạo) trong ngân hàng số ở chương 4.

## Phương pháp

Nhóm làm theo quy trình 10 bước xây dựng và triển khai hệ thống thông minh. Quy trình có tính lặp: nếu kết quả đánh giá hoặc phản hồi chưa đạt thì quay lại bước Modeling hoặc bổ sung dữ liệu; lịch trình có dành một ngày dự phòng cho vòng lặp này.

| Bước | Áp dụng vào đề tài |
| --- | --- |
| 1. Business understanding | Khảo sát quy trình chấm công hiện tại (giờ vào/ra, đi muộn, về sớm, báo cáo tháng), xác định người dùng: nhân viên và quản lý/nhân sự. |
| 2. Analytic approach | Phát biểu thành bài toán **định danh khuôn mặt tập mở** (open-set identification) theo hướng **metric learning**: so khớp embedding, người không có trong danh sách phải bị trả về "Không xác định". Không huấn luyện bộ phân loại theo từng người cho hệ thống chính, nhờ vậy thêm nhân viên mới không phải huấn luyện lại. Chống giả mạo là bài toán **phân loại nhị phân** thật/giả. |
| 3. Data requirements | Ảnh khuôn mặt có nhãn danh tính; mỗi người cần đủ góc nghiêng, điều kiện ánh sáng, có/không đeo kính, khẩu trang. Thu ít nhất hai buổi ở hai ngày khác nhau để có tập test độc lập. Thêm ảnh tấn công giả mạo (ảnh in, ảnh trên màn hình) có nhãn thật/giả. |
| 4. Data collection | Dùng bộ dữ liệu công khai và tự thu thập bằng công cụ chụp ảnh từ webcam do nhóm viết (xem mục Dữ liệu). |
| 5. Data understanding | Thống kê số ảnh mỗi người, phân bố góc mặt, độ sáng, kích thước khuôn mặt; trực quan hóa embedding (từ ArcFace huấn luyện sẵn) bằng t-SNE để xem các cụm danh tính có tách nhau không. |
| 6. Data preparation | Phát hiện khuôn mặt, căn chỉnh theo 5 điểm mốc (mắt, mũi, khóe miệng), cắt về 112×112, chuẩn hóa pixel; loại ảnh mờ, ảnh quá tối, ảnh không thấy rõ mặt và các khung hình gần trùng nhau cắt từ cùng một video (lọc nhiễu, ngoại lai). |
| 7. Modeling | Pipeline gồm 4 khối, chi tiết ở bảng dưới; hai phần nhóm tự huấn luyện mô tả ở mục "Phần huấn luyện". |
| 8. Evaluation | Đo tỷ lệ nhận diện đúng (rank-1), FAR (nhận nhầm người lạ), FRR (từ chối nhầm người đúng), TAR@FAR; với chống giả mạo đo APCER (tỷ lệ ảnh giả lọt qua) và BPCER (tỷ lệ người thật bị chặn nhầm); đo độ trễ (ms/khung hình). Chọn ngưỡng và siêu tham số trên validation, chỉ chạy tập test một lần ở cuối để tránh overfitting. |
| 9. Deployment | Đóng gói thành một ứng dụng web Streamlit chạy với webcam: giao diện gọi trực tiếp các module Python (nhận diện, chống giả mạo, chấm công) và cơ sở dữ liệu SQLite, không tách backend API riêng để vừa sức nhóm 3 người. Gồm màn hình chấm công và trang quản trị. |
| 10. Feedback | Cho các thành viên và một nhóm người dùng dùng thử 4 ngày (09–12/11), ghi lại các lần nhận sai, nhận chậm, chặn nhầm để điều chỉnh ngưỡng và bổ sung dữ liệu. Nếu đổi ngưỡng thì đo lại trên tập test. |

**Pipeline mô hình (bước 7):**

| Khối | Phương án chính | Phương án so sánh |
| --- | --- | --- |
| Phát hiện khuôn mặt | SCRFD (InsightFace), huấn luyện sẵn | Haar Cascade (OpenCV) làm baseline |
| Trích xuất đặc trưng | ArcFace (ResNet, huấn luyện sẵn trên MS1M) → vector 512 chiều | FaceNet (Inception-ResNet) |
| So khớp | Độ tương đồng cosine, ngưỡng chọn trên validation; dưới ngưỡng thì trả về "Không xác định" | k-NN, SVM do nhóm huấn luyện trên embedding |
| Chống giả mạo | MiniFASNet (CNN nhẹ) fine-tune trên dữ liệu của nhóm | Kiểm tra chớp mắt (phương án dự phòng nếu fine-tune không đạt) |

**Phần huấn luyện:**

- *Chống giả mạo:* lấy MiniFASNet đã huấn luyện sẵn, fine-tune trên ảnh thật/giả của nhóm cộng với một tập con CelebA-Spoof. Ghi lại training loss và validation loss theo từng epoch, dừng sớm (early stopping) khi validation loss tăng trở lại, để minh họa và tránh overfitting như ở chương 3.
- *Bộ phân loại trên embedding:* huấn luyện k-NN và SVM trên embedding của tập đăng ký, chọn siêu tham số trên validation, so sánh với so khớp cosine về độ chính xác, FAR và việc phải huấn luyện lại khi thêm người mới.
- Nhóm không huấn luyện lại mô hình phát hiện và trích xuất đặc trưng, vì cần hàng triệu ảnh và GPU lớn; hai mô hình này dùng trọng số công khai.

Phần chấm công: một người chỉ được ghi nhận khi được nhận diện đúng và qua kiểm tra chống giả mạo trong nhiều khung hình liên tiếp; mỗi người chỉ có một bản ghi trong khoảng thời gian cấu hình (chống ghi trùng); hệ thống tự tính đi muộn/về sớm theo ca làm.

**Công nghệ dự kiến:** Python, OpenCV, InsightFace, PyTorch (fine-tune MiniFASNet), scikit-learn (k-NN, SVM), SQLite, giao diện web bằng Streamlit (một ứng dụng, không tách frontend/backend).

**Đạo đức AI:**

- *Quyền riêng tư:* ảnh khuôn mặt và embedding đều là dữ liệu sinh trắc học, thuộc nhóm dữ liệu cá nhân nhạy cảm theo quy định bảo vệ dữ liệu cá nhân của Việt Nam. Nhóm chỉ thu thập khi có sự đồng ý bằng văn bản, hệ thống lưu embedding thay cho ảnh gốc, dữ liệu chỉ lưu trên ổ của nhóm.
- *Tự do / tự chủ:* người tham gia có thể rút lại sự đồng ý bất cứ lúc nào; khi đó toàn bộ ảnh và embedding của họ bị xóa.
- *Công bằng:* kiểm tra độ chính xác theo từng nhóm (giới tính, đeo kính, khẩu trang, ánh sáng) để phát hiện thiên lệch. Người tham gia chỉ có 6 sinh viên Việt Nam nên nhóm không đánh giá được thiên lệch theo màu da, và so sánh theo giới tính chỉ mang tính tham khảo; điều này được ghi là một hạn chế trong báo cáo.
- *Minh bạch và trách nhiệm:* hiển thị độ tương đồng và kết quả kiểm tra giả mạo của mỗi lần nhận diện; quản lý có thể sửa bản ghi chấm công sai, mọi chỉnh sửa đều được ghi log.
- *Nhân phẩm:* hệ thống chỉ dùng để chấm công, không ghi hình liên tục, không dùng để theo dõi hành vi hay đánh giá nhân viên ngoài giờ vào/ra.

## Dữ liệu

| Nguồn | Cách lấy | Mục đích sử dụng |
| --- | --- | --- |
| Mô hình huấn luyện sẵn (SCRFD, ArcFace trên MS1M qua InsightFace; MiniFASNet) | Tải từ thư viện mã nguồn mở | Phát hiện khuôn mặt, trích xuất embedding, điểm xuất phát để fine-tune chống giả mạo |
| LFW (Labeled Faces in the Wild) | Tải công khai | Đánh giá chuẩn bài toán xác minh khuôn mặt, so sánh ArcFace với FaceNet |
| Bộ dữ liệu tự thu thập | 6 người (3 thành viên và 3 tình nguyện viên, có ký đồng ý), mỗi người chụp 20–30 ảnh mỗi buổi qua công cụ chụp webcam của nhóm: nhìn thẳng, nghiêng trái/phải, ngẩng/cúi, đeo/không đeo kính, khẩu trang, ánh sáng trong nhà và gần cửa sổ. Thu hai buổi ở hai ngày và vị trí khác nhau | Đăng ký (enroll), chọn ngưỡng và kiểm thử trong điều kiện thực tế |
| Ảnh tấn công giả mạo | Chụp lại ảnh in và ảnh hiển thị trên điện thoại/laptop của chính những người tham gia | Fine-tune và đánh giá khối chống giả mạo |
| CelebA-Spoof (tập con) | Tải bộ dữ liệu công khai cho nghiên cứu | Bổ sung dữ liệu thật/giả khi fine-tune, vì dữ liệu tự thu của 6 người là quá ít |
| Ảnh người lạ | Lấy một phần từ LFW hoặc người không đăng ký | Đo FAR: hệ thống phải trả về "Không xác định" |

**Cách dùng dữ liệu tự thu thập:** chia theo buổi thu, không chia ngẫu nhiên theo ảnh, vì các ảnh trong cùng một buổi gần giống nhau và sẽ làm kết quả cao hơn thực tế. Buổi A: mỗi người lấy 5–10 ảnh làm tập đăng ký, phần còn lại làm validation (chọn ngưỡng, siêu tham số). Buổi B: toàn bộ làm tập test để báo cáo kết quả cuối. Ảnh giả mạo cũng chia theo người: ảnh của 4 người dùng để fine-tune, ảnh của 2 người còn lại chỉ dùng để đánh giá. Vì chỉ có 6 danh tính, nhóm thêm embedding của khoảng 100 người trong LFW vào tập đăng ký làm danh tính gây nhiễu để bài toán định danh không quá dễ. Tập test dự kiến chỉ khoảng 120–180 ảnh (6 người × 20–30 ảnh) nên kết quả có sai số cỡ ±4%; báo cáo sẽ ghi rõ cỡ mẫu. Làm sạch theo chương 3: bỏ ảnh mờ, ảnh trùng lặp, ảnh không phát hiện được khuôn mặt; đặt tên file và nhãn theo một quy ước thống nhất. Dữ liệu không công khai và được xóa sau khi kết thúc môn học.

## Đầu ra mong muốn đạt được

Một hệ thống chấm công chạy được với webcam: nhận diện nhân viên đã đăng ký trong dưới 1 giây, tỷ lệ nhận diện đúng từ 95% trở lên trên tập test (buổi B) với FAR không quá 1%, từ chối được người lạ và chặn từ 90% trở lên các lần dùng ảnh in hoặc ảnh trên màn hình. Đi kèm là trang quản trị (đăng ký nhân viên, lịch sử chấm công, thống kê đi muộn/về sớm, xuất Excel), mô hình chống giả mạo đã fine-tune kèm đường cong huấn luyện, báo cáo đánh giá so sánh các mô hình, và bài thuyết trình demo trực tiếp.

Nếu đạt được, hệ thống giúp doanh nghiệp hoặc nhà trường bỏ việc chấm công thủ công và hạn chế chấm công hộ, không cần tiếp xúc như máy vân tay, chi phí phần cứng thấp vì chỉ cần camera và máy tính. Dữ liệu chấm công số hóa giúp bộ phận nhân sự tính công nhanh hơn, đúng với hướng chuyển đổi số ở chương 1. Theo các lĩnh vực ở chương 4, hệ thống có thể mở rộng sang giáo dục (điểm danh sinh viên, công cụ quản lý lớp học, an ninh khuôn viên trường) và tài chính (xác thực khuôn mặt trong eKYC).

## Vai trò của từng thành viên trong nhóm

| Thành viên | Vai trò | Công việc chính |
| --- | --- | --- |
| Dương Tuấn Anh | Trưởng nhóm, kiến trúc và ứng dụng | Lập kế hoạch và theo dõi WBS, khảo sát nghiệp vụ, thiết kế kiến trúc tổng thể; cơ sở dữ liệu, module webcam, module đăng ký/nhận diện, logic ca làm/chống ghi trùng; tích hợp toàn hệ thống; tổng hợp báo cáo cuối kỳ |
| Trần Lâm Phong | Dữ liệu, giao diện và đánh giá | Phiếu đồng ý, thu thập, làm sạch, gán nhãn, EDA; so sánh với các mô hình baseline; wireframe, màn hình chấm công và trang quản trị (Streamlit); kịch bản kiểm thử, đo kết quả trên tập test, kiểm tra công bằng |
| Bùi Như Quỳnh | Mô hình AI | Công cụ chụp ảnh thu dữ liệu; pipeline phát hiện, căn chỉnh, trích xuất đặc trưng; chọn ngưỡng; huấn luyện k-NN/SVM trên embedding; fine-tune và đánh giá MiniFASNet; tối ưu độ trễ; slide và video demo |

Mọi thành viên cùng tham gia đóng góp dữ liệu khuôn mặt, kiểm thử chéo, dùng thử hệ thống và viết phần báo cáo của mình.

## Tóm tắt lịch trình

Dự kiến 4 tuần, mỗi tuần 5 ngày làm việc, bắt đầu 19/10/2026 (ngày cụ thể sẽ chỉnh theo lịch của lớp).

| Tuần | Thời gian | Công việc | Mốc / sản phẩm |
| --- | --- | --- | --- |
| 1 | 19/10 – 23/10/2026 | Khảo sát nghiệp vụ, phát biểu bài toán, chốt công nghệ; soạn phiếu đồng ý, viết công cụ chụp ảnh; thu dữ liệu buổi A, ảnh giả mạo, buổi B; thiết kế kiến trúc; làm sạch dữ liệu | Mô tả nghiệp vụ, sơ đồ hệ thống, bộ dữ liệu thô hai buổi |
| 2 | 26/10 – 30/10/2026 | Chia tập theo buổi, EDA; pipeline phát hiện, căn chỉnh, trích xuất embedding; chọn ngưỡng; huấn luyện k-NN/SVM; so sánh baseline; song song thiết kế CSDL, module webcam và đăng ký/nhận diện, wireframe, kịch bản kiểm thử | Mô hình nhận diện đạt mục tiêu trên validation, bảng so sánh mô hình |
| 3 | 02/11 – 06/11/2026 | Fine-tune và đánh giá chống giả mạo; logic chấm công; màn hình chấm công và trang quản trị; tích hợp toàn hệ thống và tối ưu độ trễ | Bản demo chạy được từ đầu đến cuối |
| 4 | 09/11 – 13/11/2026 | Ngày dự phòng cho vòng lặp sửa lỗi/quay lại Modeling; dùng thử thực tế 4 ngày; kiểm thử trên tập test, kiểm tra công bằng; viết báo cáo, làm slide, tập demo | Bảng kết quả kiểm thử, báo cáo cuối kỳ, slide, video demo |

Kế hoạch chi tiết theo từng task xem [project-work-breakdown-structure.md](project-work-breakdown-structure.md).

## Nhận xét của giáo viên

`<Comment and assessment **by the instructor.**>`
