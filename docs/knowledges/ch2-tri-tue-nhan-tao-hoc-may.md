# Chương 2: Trí tuệ nhân tạo, học máy

> Môn: Phát triển các hệ thống thông minh — PTIT
> Nguồn: `raw/ch2.pdf` (21 slide)
>
> Ghi chú: file PDF bắt đầu ngay ở phần "Một số thuật toán", không có slide bìa và mục tiêu chương. Theo slide tổng kết, chương này gồm: Trí tuệ nhân tạo, Học máy, Xử lý ngôn ngữ tự nhiên, Thị giác máy tính. Phần lý thuyết AI và học máy tổng quát không có trong file.

---

## 1. Một số thuật toán

### Mạng nơ-ron nhân tạo (Artificial Neural Network)

Sơ đồ mạng nơ-ron truyền thẳng nhiều lớp, các lớp kết nối đầy đủ (fully connected):

- **Lớp đầu vào** (input layer): nhận dữ liệu.
- **Các lớp ẩn** (hidden layers): trong hình minh họa có 2 lớp ẩn.
- **Lớp đầu ra** (output layer): trả về kết quả.

### Mạng nơ-ron tích chập (Convolutional Neural Network — CNN)

Kiến trúc CNN điển hình, ví dụ phân loại ảnh nhân vật hoạt hình (Donald / Goofy / Tweety):

1. **Input Image** → áp dụng **kernel** (bộ lọc)
2. **Convolution** → *featured maps*
3. **Pooling** → *pooled featured maps*
4. Lặp lại Convolution → Pooling
5. **Flatten layer**: duỗi các feature map thành vector
6. **Fully connected layer**: phân loại
7. **Output**: phân phối xác suất (ví dụ: Donald 0.2, Goofy 0.1, Tweety 0.7)

Ba giai đoạn chính:

| Giai đoạn | Thành phần |
|---|---|
| **Feature Extraction** (trích xuất đặc trưng) | Các lớp Convolution + Pooling |
| **Classification** (phân loại) | Flatten + Fully connected |
| **Probabilistic distribution** | Lớp đầu ra (xác suất từng lớp) |

---

## 2. Xử lý ngôn ngữ tự nhiên (NLP)

### Định nghĩa

Xử lý ngôn ngữ tự nhiên là một nhánh của AI, nghiên cứu sự tương tác giữa máy tính và ngôn ngữ tự nhiên của con người, dưới dạng **tiếng nói (speech)** hoặc **văn bản (text)**.

**Mục tiêu:** giúp máy tính hiểu và thực hiện hiệu quả các nhiệm vụ liên quan đến ngôn ngữ, như tương tác người–máy, cải thiện giao tiếp giữa người với người, hoặc nâng cao hiệu quả xử lý văn bản và lời nói.

### 4 bước xử lý văn bản

1. **Phân tích hình vị** — nhận biết, phân tích và miêu tả cấu trúc hình vị cùng các đơn vị ngôn ngữ khác (từ gốc, biên từ, phụ tố, từ loại…). Với tiếng Việt, hai bài toán điển hình là **tách từ** (word segmentation) và **gán nhãn từ loại** (part-of-speech tagging).
2. **Phân tích cú pháp** — phân tích chuỗi ký hiệu theo văn phạm hình thức. Các văn phạm thường dùng:
   - Văn phạm phi ngữ cảnh (Context-free grammar — CFG)
   - Văn phạm danh mục kết nối (Combinatory categorial grammar — CCG)
   - Văn phạm phụ thuộc (Dependency grammar — DG)
3. **Phân tích ngữ nghĩa** — liên hệ cấu trúc ngữ nghĩa từ cụm từ, mệnh đề, câu, đoạn đến toàn bài với ý nghĩa độc lập của chúng, tức là tìm ra ngữ nghĩa của đầu vào. Gồm hai mức:
   - *Ngữ nghĩa từ vựng*: ý nghĩa của các từ thành phần, phân biệt nghĩa của từ.
   - *Ngữ nghĩa thành phần*: cách các từ liên kết để tạo nghĩa rộng hơn.
4. **Phân tích diễn ngôn** — phân tích văn bản có xét mối quan hệ giữa ngôn ngữ và ngữ cảnh sử dụng (context-of-use), thực hiện ở mức đoạn văn hoặc toàn văn bản thay vì từng câu.

**Ví dụ nhập nhằng cú pháp** — câu *"… understands you like your mother"* có hai cây cú pháp:

```
Cách hiểu 1:          VP                     Cách hiểu 2:        VP
                  /   |    \                                  /     \
                 V    NP    S                                V       S
        understands  you  like your mother (does)    understands  (that) you like your mother
```

- Cách 1: "hiểu bạn như mẹ bạn hiểu bạn".
- Cách 2: "hiểu rằng bạn yêu mẹ bạn".

### Ứng dụng của NLP

1. **Nhận dạng tiếng nói** (Automatic Speech Recognition — ASR, hay Speech-to-Text — STT): chuyển tiếng nói thành văn bản, dùng trong điều khiển bằng giọng nói.
2. **Tổng hợp tiếng nói** (Speech synthesis / Text-to-Speech — TTS): chuyển văn bản thành tiếng nói, dùng để đọc văn bản tự động.
3. **Truy xuất thông tin** (Information Retrieval — IR): tìm tài liệu phi cấu trúc (thường là văn bản) đáp ứng nhu cầu thông tin từ nguồn lớn. Ví dụ: Google, Yahoo, Bing.
4. **Trích chọn thông tin** (Information Extraction — IE): nhận diện thực thể đã định nghĩa trước, quan hệ giữa các thực thể và sự kiện trong văn bản.
5. **Trả lời câu hỏi** (Question Answering — QA): tự động trả lời câu hỏi bằng ngôn ngữ tự nhiên dựa trên việc truy xuất thông tin từ tập tài liệu.
6. **Tóm tắt văn bản tự động** (Automatic Text Summarization): rút gọn văn bản, giữ nội dung quan trọng nhất. Hai phương pháp chính: **trích xuất** (extractive) và **tóm lược ý** (abstractive).
7. **Chatbot**: chương trình trò chuyện, hỏi đáp với con người dưới dạng văn bản.
8. **Dịch máy** (Machine Translation — MT): tự động hóa một phần hoặc toàn bộ việc dịch. Các phương pháp:
   - Dịch dựa trên ví dụ (Example-based — EBMT)
   - Dịch dựa trên luật (Rule-based — RBMT)
   - Dịch máy thống kê (Statistical — SMT)
   - Dịch máy nơ-ron (Neural Machine Translation)
9. **Kiểm lỗi chính tả tự động**: phát hiện lỗi từ vựng, ngữ pháp, ngữ nghĩa và gợi ý sửa.

### Luồng hoạt động của trợ lý giọng nói

```
Người dùng → Nhận dạng tiếng nói → Yêu cầu dạng văn bản → Xử lý yêu cầu
    ↑                                                            ↓
 Âm thanh ← Tổng hợp tiếng nói ← Câu trả lời dạng văn bản ←──────┘
```

---

## 3. Thị giác máy tính (Computer Vision)

### Định nghĩa

Thị giác máy tính là lĩnh vực thuộc AI và Khoa học máy tính: **thu nhận, xử lý dữ liệu hình ảnh từ thế giới thực, rồi phân tích và nhận dạng** để cho ra thông tin, kết quả. Mục tiêu là giúp thiết bị có khả năng nhìn và nhận biết như con người.

### Khả năng hiện nay

- Xác định vật thể (**Identify**)
- Theo dõi vật thể (**Track**)
- Đo đạc (**Measure**)
- Phát hiện vật thể (**Detect**)
- Phân loại vật thể (**Classify**)

### Tính liên ngành

Computer Vision giao thoa với nhiều lĩnh vực:

| Ngành | Chủ đề liên quan |
|---|---|
| Biology | Neuroscience |
| Psychology | Cognitive sciences |
| Computer Science | Algorithms, theory; Systems, architecture |
| Mathematics | Information retrieval; Machine learning |
| Engineering | Robotics; Speech, NLP |
| Physics | Optics; Image processing |

### So sánh thị giác người và máy

| | Con người | Máy tính |
|---|---|---|
| Đầu vào | Ảnh hoặc video | Ảnh hoặc video |
| Thiết bị cảm biến | Mắt | Camera |
| Thiết bị diễn giải | Não | Máy tính |
| Diễn giải | "Vườn, mùa xuân, cây cầu, nước, cây cối, hoa, màu xanh…" | (cùng mục tiêu) |

### Ví dụ ứng dụng

- **Smile Shutter** (máy ảnh Sony Cyber-shot): tự nhận diện khuôn mặt và nụ cười để chụp đúng khoảnh khắc.
- **Nhận dạng chữ số viết tay**: LeNet-5, AT&T Labs.
- **Đọc biển số xe** (Automatic Number Plate Recognition): xác định vùng biển số → chuẩn hóa → tách và nhận dạng từng ký tự (ví dụ `4YCH428`).
- **Hệ thống giám sát giao thông** (Traffic Monitoring System): phát hiện và đếm phương tiện theo lớp (xe máy, người, ô tô, bus, xe tải, xe đạp), ước lượng vận tốc từng phương tiện (km/h) và mật độ giao thông tại một nút giao ở Hà Nội.

---

## 4. Generative AI (AI tạo sinh)

### Định nghĩa

Generative AI là loại AI có thể **tạo ra nhiều loại dữ liệu**: hình ảnh, video, âm thanh, văn bản, mô hình 3D. Nó học các mẫu từ dữ liệu có sẵn rồi dùng kiến thức đó để tạo ra đầu ra mới và duy nhất.

Generative AI có thể bắt chước sự sáng tạo của con người để tạo nội dung phức tạp và rất thực, nên có giá trị cho nhiều ngành như trò chơi, giải trí, thiết kế sản phẩm.

### Ứng dụng phổ biến

- **Ngôn ngữ**: văn bản là gốc rễ của nhiều mô hình Generative AI và là lĩnh vực phát triển nhất. Phổ biến nhất là **mô hình ngôn ngữ lớn (LLM)**, dùng để viết luận, phát triển mã, dịch thuật, thậm chí hiểu trình tự gen.
- **Hình ảnh**: tạo hình ảnh 3D, hình đại diện (avatar), video, đồ thị, hình minh họa.
- **Âm thanh**: tạo bài hát và đoạn âm thanh từ văn bản, nhận dạng đối tượng trong video và tạo tiếng động đi kèm, tạo nhạc tùy chỉnh.
- **Dữ liệu tổng hợp** (synthetic data): rất hữu ích để huấn luyện mô hình AI khi dữ liệu không tồn tại, bị hạn chế, hoặc không đủ để xử lý các trường hợp khó với độ chính xác cao.

### Các nhóm use case

Visual Content · Text Generation · Audio Generation · Code Generation · Knowledge Management · Collaboration · Enterprise Search · Synthetic Data Generation

Các nền tảng tiêu biểu (logo trên slide): OpenAI, Meta, Midjourney…

---

## Tổng kết chương 2

- Trí tuệ nhân tạo
- Học máy
- Xử lý ngôn ngữ tự nhiên
- Thị giác máy tính
