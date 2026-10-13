# Chương 3: Xây dựng và triển khai hệ thống thông minh

> Môn: Phát triển các hệ thống thông minh — PTIT
> Nguồn: `raw/ch3.pdf` (30 slide)

**Mục tiêu:** giới thiệu các bước triển khai hệ thống thông minh.

**Nội dung:**
1. Quy trình xây dựng
2. Thu thập, xử lý dữ liệu
3. Đánh giá mô hình
4. Đạo đức trong trí tuệ nhân tạo

---

## 1. Quy trình xây dựng và triển khai hệ thống thông minh

### Sơ đồ 10 bước

```
Business understanding → Analytic approach → Data requirements → Data collection → Data understanding
                                                                                          ↓
              Feedback ← Deployment ← Evaluation ← Modeling ← Data preparation ←──────────┘
```

Quy trình có tính **lặp**, các vòng quay lại trên sơ đồ gồm:

- Data requirements → Analytic approach
- Data collection ⇄ Data requirements, Data understanding ⇄ Data collection
- Data preparation → Data collection / Data understanding
- Modeling ⇄ Data preparation, Evaluation ⇄ Modeling
- Feedback → Modeling

### Chi tiết từng bước

1. **Business understanding** — Hiểu rõ nhu cầu thực tế cần giải quyết. Nhu cầu có thể nằm ngoài lĩnh vực hiểu biết của ta, nên cần tìm hiểu kỹ.
2. **Analytic approach** — Đưa nhu cầu về một **bài toán ML** được phát biểu rõ ràng. Một nhu cầu có thể ứng với nhiều bài toán ML khác nhau:
   - "Chẩn đoán bệnh viêm gan" → bài toán phân loại, hoặc bài toán khác.
   - "Dự đoán giá nhà" → bài toán hồi quy, hoặc cũng có thể là phân loại.
   - Lựa chọn ở bước này quyết định trực tiếp bước sau.
3. **Data requirements** — Xác định yêu cầu về tập dữ liệu cần thu thập, tùy theo bài toán ML đã chọn. Ví dụ, với bài toán hồi quy thì mỗi mẫu huấn luyện bắt buộc phải có nhãn. Có thể thêm các yêu cầu khác.
4. **Data collection** — Xây dựng hệ thống (bán) tự động hoặc cử người thu thập dữ liệu huấn luyện. Nếu việc thu thập gặp vấn đề (ví dụ quá đắt) thì cần xem xét chỉnh sửa hai bước trước.
5. **Data understanding** — Tính toán đơn giản hoặc trực quan hóa để xem tính chất của dữ liệu: độ đa dạng của thuộc tính, mức độ thiếu giá trị… Hiểu biết về đặc trưng dữ liệu sẽ hữu ích cho các bước sau.
6. **Data preparation** — Tiền xử lý dữ liệu. Dữ liệu thu thập thường ở dạng thô, cần đưa về dạng phù hợp với mô hình ML: lọc nhiễu, loại bỏ…
7. **Modeling** — Từ tập dữ liệu đã tiền xử lý **D**, chọn mô hình ML phù hợp và huấn luyện nó trên **D**.
8. **Evaluation** — Đánh giá hiệu năng (chất lượng) của mô hình bằng chiến lược và độ đo phù hợp. Nếu mô hình chưa tốt, quay lại các bước trước để kiểm tra.
9. **Deployment** — Nếu mô hình tốt, đưa vào triển khai hệ thống (sản phẩm) đầy đủ.
10. **Feedback** — Thu thập phản hồi của người dùng. Nếu hệ thống chưa đủ tốt thì quay lại các bước trước để cải thiện; ngược lại, hệ thống đạt yêu cầu và việc xây dựng thành công.

---

## 2. Thu thập và xử lý dữ liệu

### Thời gian dành cho phân tích dữ liệu (CrowdFlower Inc., 2016)

| Công việc | Tỷ lệ |
|---|---|
| **Thu xếp và làm sạch dữ liệu** | **60%** |
| **Thu thập dữ liệu** | **19%** |
| Khai phá | 9% |
| Khác | 5% |
| Cải thiện thuật toán | 4% |
| Tạo tập dữ liệu huấn luyện | 3% |

→ Gần 80% thời gian dành cho thu thập và làm sạch dữ liệu.

### Tổng quan

- **Thu thập dữ liệu**
  - Lấy mẫu (sampling)
  - Kỹ thuật: crawling, logging, scraping
- **Xử lý dữ liệu**
  - Lọc nhiễu, làm sạch, số hóa,…
- **Input**: vấn đề cần giải quyết → **Output**: mẫu dữ liệu (bảng, văn bản, ảnh…)

### Lấy mẫu (sampling)

| Khía cạnh | Nội dung |
|---|---|
| **WHAT** | Lấy tập mẫu nhỏ, phổ biến để đại diện cho lĩnh vực cần học |
| **WHY** | Không thể học toàn bộ, do giới hạn thời gian và khả năng tính toán |
| **HOW** | Thu thập mẫu từ thực tế, hoặc từ các nguồn chứa dữ liệu: web, database,… |
| **Variety** | Tập mẫu đủ đa dạng để phủ hết các ngữ cảnh của lĩnh vực |
| **Bias** | Dữ liệu cần tổng quát, không bị sai lệch hay thiên vị về một bộ phận nhỏ của lĩnh vực |

### Làm sạch dữ liệu

#### Tính đầy đủ và trung thực

- Mẫu dữ liệu cần được thu thập từ **nguồn đáng tin cậy** và phản ánh đúng vấn đề cần giải quyết.
- Loại bỏ **nhiễu** (ngoại lai, outlier): bỏ các mẫu khác biệt lớn so với các mẫu khác.
- Mẫu dữ liệu có thể **bị trống** (thiếu, chưa đầy đủ), cần chiến lược phù hợp:
  - Bỏ qua, không đưa vào phân tích?
  - Bổ sung các trường còn thiếu cho mẫu?

#### Điền giá trị thiếu

- Điền lại giá trị bằng tay.
- Gán nhãn đặc biệt, hoặc giá trị nằm ngoài khoảng biểu diễn.
- Gán giá trị trung bình.
- Gán giá trị trung bình của các mẫu khác **cùng lớp**.
- Tìm giá trị có xác suất lớn nhất để điền vào (hồi quy, suy diễn Bayes,…).

#### Tính đồng nhất

Các mẫu dữ liệu cần đồng nhất về cách biểu diễn và ký hiệu. Ví dụ **không** đồng nhất:

- Rating dùng cả "1, 2, 3" và "A, B, C".
- Age = 42 nhưng Birthday = 03/08/2020 (mâu thuẫn).

---

## 3. Đánh giá mô hình

Một bài toán ML có thể giải bằng nhiều phương pháp, cho ra nhiều mô hình khác nhau. Để chọn, cần đánh giá **hiệu năng của mô hình trên dữ liệu mới** (evaluate model performance on unseen data).

Đánh giá mô hình giúp trả lời:

- Mô hình đã được huấn luyện thành công chưa?
- Mô hình tốt đến mức nào?
- Khi nào nên dừng huấn luyện?
- Khi nào nên cập nhật mô hình?

### Overfitting, Generalization, Underfitting

| | **Overfitting** (quá khớp) | **Generalization** (tổng quát hóa tốt) | **Underfitting** (chưa khớp) |
|---|---|---|---|
| Hồi quy | Đường cong đi qua mọi điểm, zíc-zắc theo nhiễu | Đường cong bám đúng xu hướng dữ liệu | Đường thẳng không nắm được xu hướng |
| Phân loại | Biên quyết định rất phức tạp, "ôm" từng điểm | Biên quyết định mượt, tách hai lớp hợp lý | Biên quá đơn giản, phân loại sai nhiều |
| Deep learning (Error theo Epochs) | Training error giảm mãi nhưng **validation error tăng trở lại** | Cả training và validation error đều giảm và hội tụ gần nhau | Cả hai error đều **cao** và gần nhau |

---

## 4. Ví dụ thực tế: hệ thống giám định tốc độ phương tiện

### Bối cảnh

- Phần mềm thương mại (Amped FIVE) ước lượng tốc độ từ video bằng cách đánh dấu lưới tham chiếu trên mặt đường. Ví dụ kết quả: *Speed ≈ 25 ± 2 mph*.
- Nguồn video thực tế: camera hành trình (ví dụ VIETMAP, có ghi thời gian, tọa độ GPS và tốc độ 63 km/h).

### Nguyên lý

Dùng hình học phép chiếu phối cảnh: ánh xạ vùng mặt đường trong ảnh (từ camera) sang mặt phẳng thực, từ đó biết quãng đường thực tế mà phương tiện đi được.

### Phần mềm demo (tự xây dựng)

Giao diện gồm:
- **Source**: tải video, Play/Pause/Rewind; hiển thị frame-rate (FPS), tổng số frame, frame hiện tại.
- **Basic Settings**: độ phân giải video (ví dụ 1280×720 hoặc 854×480), độ phân giải vùng ROI, **chiều dài ROI thực tế (mét)**.
- **ROI Settings**: thanh trượt chỉnh Height, Width, Vertical/Horizontal Relocation của vùng quan tâm (ROI).
- Tab **Result**: ảnh phương tiện, có vi phạm hay không, tốc độ, số frame, ID phương tiện.

Cách làm:
1. Đặt **ROI** (khung xanh lá) trên đoạn đường.
2. Khai báo khoảng cách thực tế của ROI dựa vào mốc đã biết:
   - Đường cao tốc: **khoảng cách giữa 2 vạch kẻ đường thực tế là 15 m** → ROI = 15 m.
   - Đường ngõ: **khoảng cách giữa 2 vạch bê tông thực tế là 7 m** → ROI = 7 m.
3. Phát hiện và theo dõi phương tiện (bounding box đỏ) khi đi qua ROI.
4. Tốc độ ≈ chiều dài ROI / thời gian đi qua (số frame ÷ FPS).

### Kết quả thử nghiệm

| STT phương tiện | Tốc độ thực tế (km/h) | Tốc độ hệ thống đo (km/h) | Sai số |
|---|---|---|---|
| 1 | 21 | 20 | 5% |
| 2 | 24 | 23 | 4% |

---

## 5. Đạo đức trong trí tuệ nhân tạo

### Các định nghĩa

- **Viện Alan Turing:** Đạo đức AI là tập hợp các giá trị, nguyên tắc, kỹ thuật dùng các tiêu chuẩn đúng sai được chấp nhận rộng rãi để hướng dẫn hành vi đạo đức trong phát triển và sử dụng công nghệ AI.
- **Diễn đàn Kinh tế Thế giới (WEF):** Đạo đức AI là lĩnh vực nghiên cứu đa nguyên tắc, nhiều bên liên quan, nhằm xác định và thực thi các giải pháp kỹ thuật và phi kỹ thuật để giải quyết mối quan tâm và giảm thiểu rủi ro mà công nghệ này mang lại.
- **UNESCO:** Đạo đức AI là "sự phản ánh có tính hệ thống và tính quy phạm một cách toàn diện, tổng thể và theo khung phát triển các giá trị, nguyên tắc và hành động phụ thuộc lẫn nhau".

### 10 nguyên tắc đạo đức AI

1. **Minh bạch / có thể giải thích được** — Giảm thiểu rủi ro, xác định và khắc phục vi phạm đạo đức thông qua việc hệ thống AI tự kiểm tra chính nó.
2. **Công bằng / bình đẳng** — Mọi người có quyền truy cập và được đối xử công bằng từ hệ thống AI; giám sát, ngăn ngừa, giảm thiểu hành vi không công bằng và thiên vị.
3. **Bảo mật / phòng ngừa** — AI không bao giờ được gây ra tác hại có thể lường trước hoặc ngoài ý muốn.
4. **Trách nhiệm** — Ứng xử chính trực đối với hành động và quyết định của AI. Bao gồm câu hỏi AI có nên chịu trách nhiệm như con người, hay con người là tác nhân duy nhất chịu trách nhiệm cuối cùng.
5. **Quyền riêng tư** — Bảo vệ và tin cậy trong việc thu thập, lưu trữ, sử dụng dữ liệu của cá nhân, tổ chức, doanh nghiệp.
6. **Phúc lợi** — AI đem lại lợi ích cho xã hội và con người; tạo tài nguyên, giá trị, cơ hội mới để thúc đẩy kinh tế xã hội. Vẫn còn chưa chắc chắn về việc bên nào sẽ được hưởng lợi từ AI.
7. **Tự do / tự chủ** — Quyền tự do sử dụng nền tảng, công nghệ ưa thích; quyền cho phép hoặc rút lại sự đồng ý (ví dụ với dữ liệu cá nhân).
8. **Sự tin tưởng** — Nhà phát triển và các bên liên quan áp dụng "các nguyên tắc thiết kế" đáng tin cậy khi triển khai AI.
9. **Tính bền vững** — Triển khai AI để bảo vệ môi trường, tăng cường hệ sinh thái và đa dạng sinh học.
10. **Nhân phẩm** — AI không làm giảm hay hủy hoại phẩm giá con người, mà giúp con người tôn trọng, giữ gìn và nâng cao phẩm giá đó.

---

## Tổng kết chương 3

- Quy trình xây dựng
- Thu thập, xử lý dữ liệu
- Đánh giá mô hình
- Đạo đức trong trí tuệ nhân tạo
