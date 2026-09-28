# 📻 Radio QC — tìm quảng cáo trong file phát sóng radio

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/nguyenthanhhai-rf/radio-qc-colab/blob/main/RadioQC.ipynb)

Đưa vào file phát sóng dài 1–3 giờ, nhận về **một file Excel**: có những quảng cáo nào, phát lúc mấy giờ, dài bao lâu,
kèm **bản chép lời** cả chương trình.

Notebook chạy trên Google Colab bằng **tài khoản Google của bạn** và đọc file thẳng từ **Google Drive của chính tài
khoản đó**. Không cần cài gì.

## Mỗi lần dùng

1. Bỏ file phát sóng vào thư mục **`RadioQC/2_FilePhatSong`** trong Google Drive (kéo thả trên drive.google.com,
   hoặc cài *Google Drive cho máy tính* để file tự tải lên ngầm). Có file quảng cáo gốc (spot) thì bỏ vào
   **`RadioQC/1_ThuVienQC`** (**tên file = tên spot**, ví dụ `Honda Vision 30s.mp3`).
2. Bấm nút **Open in Colab** ở trên, rồi **Runtime → Run all** (Ctrl+F9).
3. Colab báo notebook *không do Google viết* → bấm **Run anyway** (Vẫn chạy). Colab xin quyền vào Google Drive →
   chọn tài khoản của bạn → **Cho phép**.
4. Đợi xong: **file Excel tự tải về máy** (thư mục Tải xuống / Downloads) và có một bản trong **`RadioQC/3_KetQua`**.
   Bảng kết quả hiện ngay bên dưới, bấm ▶ để nghe từng quảng cáo.

Lần đầu chưa có các thư mục trên thì cứ chạy: notebook tự tạo rồi nhắc bạn bỏ file vào. Mỗi lần chạy, notebook chỉ xử
lý **file mới** (file chưa có kết quả trong `3_KetQua`) và **làm tiếp file còn dở** lần trước; muốn chạy lại tất cả thì
tick **CHAY_LAI_TAT_CA** ở ô **⚙️ Tuỳ chọn**.

Notebook chia thành các ô chạy nối nhau: **2️⃣ Chép lời** (lâu nhất) → **3️⃣ AI đọc và xuất kết quả** →
**4️⃣ Duyệt spot tự học**. Ô nào báo lỗi thì bấm ▶ ở chính ô đó:

- **AI báo quá tải** (dòng ⏳ dưới ô 3️⃣): đợi vài phút rồi bấm ▶ ô 3️⃣. Chỉ các đoạn còn thiếu được hỏi lại, không phải
  chép lời lại (notebook tự đợi và thử lại vài lần trước khi báo).
- **Chép lời lỗi**: bấm ▶ ô 2️⃣ rồi ▶ ô 3️⃣.

Bản chép lời và câu trả lời của AI được giữ trong `3_KetQua/_tam`, nên mở phiên Colab mới cũng không phải chép lời lại.

Không muốn dùng Drive: ở ô **⚙️ Tuỳ chọn** chọn `NGUON_FILE` = *Tải lên từ máy*, rồi bấm **Choose Files** và chọn file
phát sóng (kèm file spot nếu có). Cách này **chậm với file lớn** và file chỉ nằm trong phiên Colab, đóng là mất.

Tên file phát sóng nên có ngày giờ bắt đầu, ví dụ `CAO DIEM CHIEU 25.9.2026 16H30.mp3`, để báo cáo ghi giờ thật.

## Hai cách dò (notebook tự chọn)

| Bạn chọn | Notebook làm gì | Độ tin cậy |
|---|---|---|
| Chỉ file phát sóng | **AI tự nhận diện** quảng cáo từ lời nói: chép lời bằng Whisper, rồi Gemini đọc bản chép lời | Có thể sót hoặc lệch ranh giới vài giây: **nên nghe lại** |
| Thêm file spot (file ngắn, tối đa 5 phút) | **So vân tay âm thanh**: tìm từng lần phát của đúng spot đó, phát đủ hay bị cắt | Chính xác tới 0,1 giây |

Hai cách chạy cùng lúc được. Quảng cáo khớp spot thì lấy kết quả so vân tay.

AI cần máy Colab có **GPU**. Nếu notebook báo không có GPU: bấm **Runtime → Change runtime type → T4 GPU → Save**,
rồi **Run all** lại. Không có GPU vẫn dò được bằng file spot.

File 3 giờ ước mất 10–20 phút, phần lớn là thời gian chép lời.

## Khi AI báo quá tải

AI có sẵn của Colab miễn phí nhưng **dùng chung cho mọi người dùng Colab**, nên có lúc quá tải (dòng ⏳ dưới ô 3️⃣).
Notebook tự hỏi các model Gemini khác của Colab, rồi đợi và thử lại. Vẫn không được thì đoạn đó ghi *CHƯA PHÂN TÍCH*:
đợi vài phút rồi bấm ▶ ô 3️⃣, chỉ các đoạn còn thiếu được hỏi lại.

**Cách bền nhất: dùng key Gemini riêng** (miễn phí, làm một lần, dùng hạn mức của riêng bạn):

1. Mở [aistudio.google.com/apikey](https://aistudio.google.com/apikey) bằng tài khoản Google của bạn → **Create API key**
   → sao chép key.
2. Trong Colab, bấm biểu tượng 🔑 (**Secrets**) ở thanh bên trái → **Add new secret** → *Name*: `GEMINI_API_KEY`,
   *Value*: dán key → bật **Notebook access**.
3. Chạy lại. Notebook hỏi key riêng trước; AI của Colab làm dự phòng. Sheet *Thông tin* ghi model nào đã đọc.

Key là của riêng bạn: đừng dán vào ô code, đừng gửi cho người khác.

## Kho spot tự lớn dần

Mỗi lần chạy (chế độ Drive), quảng cáo mới AI tìm được được lưu làm spot trong **`RadioQC/1_ThuVienQC/Chờ duyệt`**
(file WAV, tên là nhãn hàng kèm ngày giờ). Từ lần sau notebook dò chúng bằng **vân tay**: chính xác tới 0,1 giây và bắt
được cả quảng cáo toàn nhạc mà máy chép lời không nghe ra. Cho tới khi bạn duyệt, kết quả của chúng ghi
**Cần nghe lại: spot tự học chưa duyệt**.

Duyệt ngay trong notebook, ở ô **4️⃣**: mỗi spot có nút ▶ để nghe, ô tên (điền sẵn nhãn hàng) và lựa chọn
*Chưa xét / Đúng / Sai*. Chọn xong bấm **Lưu lựa chọn**: spot *Đúng* vào `1_ThuVienQC` với tên bạn đặt; spot *Sai* chuyển
sang `RadioQC/_Da_loai` và **không bao giờ được đề xuất lại**; spot *Chưa xét* chờ lần sau. Notebook chỉ lưu spot đã tự
kiểm là khớp trọn vẹn, và không bao giờ tự xoá file của bạn. Không muốn học: bỏ tick `TU_HOC_SPOT` ở ô **⚙️ Tuỳ chọn**.

## Đọc file Excel

| Sheet | Nội dung |
|---|---|
| **Quảng cáo** | Mỗi dòng một quảng cáo: giờ bắt đầu và kết thúc, nhãn hàng, loại (*QC thương mại*, *Đài tự giới thiệu*, *Tài trợ*), lời quảng cáo, căn cứ, cột **Cần nghe lại** |
| **Tổng hợp** | Mỗi nhãn hàng phát mấy lần, lúc nào |
| **Chép lời** | Lời cả chương trình theo giờ; dòng thuộc quảng cáo có ghi tên nhãn hàng |
| **Thông tin** | File, thời lượng, cách dò, cảnh báo |

Các dòng cảnh báo:

- **⚠️ CHƯA PHÂN TÍCH** (sheet Quảng cáo): AI không trả lời được đoạn đó, quảng cáo trong đoạn có thể bị sót.
  Hãy chạy lại.
- **⚠️ KHÔNG CHÉP ĐƯỢC LỜI** (sheet Chép lời): đoạn máy không chép được lời, thường là bài hát. Nếu nghi có quảng cáo
  thì nghe lại đoạn đó.

Cột **Tình trạng** của quảng cáo tìm bằng file spot:

- **Đủ**: phát trọn spot.
- **Phát thiếu: thiếu đầu/cuối ~X s**: spot bị cắt ngắn khi phát.
- **Cần nghe lại**: chỉ khớp một phần spot, thường là **một spot khác dùng chung nhạc hiệu**.
- **Không kiểm được đủ**: spot nằm ở mép file ghi (file bắt đầu hoặc kết thúc giữa spot).

## Hỏi nhanh

- **Tên file phát sóng không có giờ?** Báo cáo dùng giờ tính từ đầu file (`+00:12:30`) và ghi cảnh báo.
- **Spot ngắn hơn 5 giây** (sound logo) không dò được tin cậy: notebook báo "quá ngắn" và bỏ qua file đó.
- **File quá 5 phút** được coi là file phát sóng, không phải spot.
- **Drive sắp đầy?** Drive miễn phí có 15 GB (dùng chung với Gmail, Ảnh); mỗi file 3 giờ khoảng 165 MB. Xoá bớt file đã
  xử lý trong `2_FilePhatSong`, kết quả vẫn còn trong `3_KetQua`. Notebook nhắc khi file đã xử lý chiếm quá 2 GB,
  không bao giờ tự xoá file của bạn.
- **Muốn nghe lại sau khi đóng Colab?** File trong Drive vẫn còn: tick **CHAY_LAI_TAT_CA** rồi chạy lại để có lại clip.
- **Để thư mục khác thay cho `RadioQC`?** Đổi `THU_MUC_DRIVE` ở ô **⚙️ Tuỳ chọn**.
