# 📻 Radio QC — tìm quảng cáo trong file phát sóng radio

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/nguyenthanhhai-rf/radio-qc-colab/blob/main/RadioQC.ipynb)

Bỏ file phát sóng (dài 1–3 giờ) vào Google Drive, bấm chạy, nhận về **một file Excel**: có những quảng cáo nào, phát lúc
mấy giờ, dài bao lâu, **chỗ nào nên nghe lại**, kèm lời cả chương trình. Chạy trên Google Colab bằng tài khoản Google
của bạn, không cần cài gì.

## ▶️ Mỗi lần dùng: 3 bước

1. **Bỏ file phát sóng** vào thư mục **`RadioQC/2_FilePhatSong`** trong Google Drive (kéo thả trên drive.google.com, hoặc
   cài *Google Drive cho máy tính* để file tự tải lên).
2. Bấm nút **Open in Colab** ở trên → menu **Runtime → Run all** (hoặc **Ctrl+F9**).
   - Colab báo *notebook không do Google viết* → bấm **Run anyway**.
   - Colab xin vào Google Drive → chọn tài khoản của bạn → **Cho phép**.
3. **Đợi đến khi hiện ✅ Xong.** File Excel **tự tải về máy** (thư mục *Tải xuống*) và có một bản trong
   **`RadioQC/3_KetQua`**. Bảng kết quả hiện ngay dưới ô 3️⃣: bấm ▶ để nghe từng quảng cáo.

- ⏱️ Bước chép lời lâu nhất: file 2–3 giờ có thể mất vài chục phút (ô 2️⃣ in ra tốc độ chép lời). **Để nguyên tab Colab
  mở** đến khi xong.
- Mỗi lần chạy, notebook chỉ làm **file mới** và **làm tiếp file còn dở**. Muốn làm lại tất cả: tick
  **CHAY_LAI_TAT_CA** ở ô ⚙️ Tuỳ chọn.

## 📁 Chuẩn bị một lần

### Các thư mục trong Drive

Lần đầu cứ bấm **Run all**: notebook tự tạo các thư mục này trong `RadioQC` rồi nhắc bạn.

| Thư mục | Bỏ gì vào | Cần không |
|---|---|---|
| `2_FilePhatSong` | File phát sóng cần soát | Có |
| `4_SoTheoDoi` | Sổ theo dõi quảng cáo của tháng (file Excel đang dùng) | Nên có |
| `1_ThuVienQC` | File quảng cáo gốc (spot), **tên file = tên spot**, ví dụ `Honda Vision 30s.mp3` | Nếu có |
| `3_KetQua` | Notebook ghi kết quả vào đây | — |
| `_tu_hoc` | Trí nhớ quảng cáo, notebook tự quản lý | Đừng sửa |

### Sổ theo dõi quảng cáo (nên có)

Có sổ, notebook biết **hôm đó kênh có lịch những sản phẩm nào**: báo cáo ghi tên quảng cáo **đúng như trong sổ** (cột
*Tên trong sổ*) và nhận ra trọn vẹn hơn các chuyên mục, thông điệp. Quảng cáo không có lịch vẫn được tìm. Mỗi tháng bỏ
sổ tháng mới vào thay sổ cũ. Không có sổ thì notebook vẫn chạy như thường.

- **Kênh VOV1, VOV2:** tên file sổ chỉ cần **bắt đầu bằng tên kênh** như file phát sóng (`VOV1_TheodoiQC_2026.xlsb`
  cho các file `VOV1_2026...mp3`).
- **Kênh có tên sổ khác tên file phát sóng** (Giao thông, Cao điểm, Mekong): người phụ trách tạo **một lần** tệp
  **`kenh_so.txt`** trong `4_SoTheoDoi`, mỗi dòng: *đầu tên file phát sóng* `=` *tên file sổ* `|` *các sheet*. Ví dụ:

  ```
  CAO DIEM = So theo doi cao diem T{thang}.{nam}.xlsx | Ha Noi; Chuyen muc:chuyen_muc; Dai HN:thong_diep
  MEKONG = So theo doi Mekong {nam}.xlsx | Tháng {thang}
  ```

  `{thang}`, `{nam}` được thay bằng tháng, năm của file phát sóng, nên sang tháng mới không phải sửa tệp. Sheet ghi
  chuyên mục, bản tin thì thêm `:chuyen_muc`; sheet thông điệp thêm `:thong_diep`; còn lại là sheet quảng cáo. Dòng
  bắt đầu bằng `#` là ghi chú.

Sheet *Thông tin* của file kết quả ghi sổ nào đã dùng.

### Key Gemini riêng (khi AI hay quá tải)

AI có sẵn của Colab miễn phí nhưng dùng chung cho mọi người, nên có lúc quá tải. Key riêng cũng miễn phí, làm một lần:

1. Mở [aistudio.google.com/apikey](https://aistudio.google.com/apikey) bằng tài khoản Google của bạn → **Create API key**
   → sao chép key.
2. Trong Colab, bấm biểu tượng 🔑 (**Secrets**) ở thanh bên trái → **Add new secret** → *Name*: `GEMINI_API_KEY`,
   *Value*: dán key → bật **Notebook access**.
3. Chạy lại. Notebook hỏi key riêng trước, AI của Colab làm dự phòng.

Key là của riêng bạn: đừng dán vào ô code, đừng gửi cho người khác.

## 🏷️ Tên file phát sóng

Tên file cần có **ngày và giờ bắt đầu** để báo cáo ghi giờ thật, ví dụ:

- `CAO DIEM CHIEU 25.9.2026 16H30.mp3`
- `VOV1_20261014_050218.mp3` (dạng máy ghi tự đặt: năm tháng ngày, rồi giờ phút giây)

Thiếu giờ thì báo cáo ghi giờ tính từ đầu file (`+00:12:30`) và có cảnh báo.

## 👀 Đọc file Excel

Xem theo thứ tự:

| Sheet | Xem gì |
|---|---|
| **Dòng thời gian** | Cả chương trình chia thành khối liền nhau: khối quảng cáo, chuyên mục, tin tức, tin có dấu hiệu PR, nhạc, đài tự giới thiệu. Cột **Nghi vấn** chỉ chỗ **nên nghe lại** |
| **Quảng cáo** | Mỗi dòng một quảng cáo: giờ, nhãn hàng, sản phẩm, *Tên trong sổ*, loại, lời quảng cáo, căn cứ. Dòng có cột **Cần nghe lại** thì nghe kiểm |
| **Tổng hợp** | Mỗi nhãn hàng phát mấy lần, lúc nào |
| **Chép lời** | Lời cả chương trình theo giờ |
| **Thông tin** | File, thời lượng, sổ đã dùng, đoạn chưa đọc được |

Cột **Nghi vấn** (sheet Dòng thời gian) ghi lý do nên nghe lại:

- *nhạc ngắn sát khối quảng cáo* hoặc *lặp lại trong file*: có thể là **quảng cáo dạng bài hát**.
- *khối quảng cáo nhưng chưa tách được spot nào*.
- *có thể là tin PR*.
- *AI chưa chia được đoạn này*: nghe lại hoặc chạy lại.

Các ghi chú khác:

- **⚠️ CHƯA PHÂN TÍCH** (sheet Quảng cáo): AI chưa đọc được đoạn đó, có thể sót quảng cáo. Chạy lại sau.
- **⚠️ KHÔNG CHÉP ĐƯỢC LỜI** (sheet Chép lời): thường là bài hát; nghi có quảng cáo thì nghe lại.
- Cột *Căn cứ* ghi **Nhớ từ lần trước**: tìm ra nhờ trí nhớ tự học.
- Loại **Bản tin quảng cáo** và **QC đọc trực tiếp** (MC đọc) luôn ghi *Cần nghe lại*, vì ranh giới là AI đoán.

Quảng cáo tìm bằng file spot có cột **Tình trạng**:

- **Đủ**: phát trọn spot.
- **Phát thiếu: thiếu đầu/cuối ~X s**: spot bị cắt ngắn khi phát.
- **Cần nghe lại**: chỉ khớp một phần, thường là spot khác dùng chung nhạc hiệu.
- **Không kiểm được đủ**: spot nằm ở mép file ghi.

## 🆘 Gặp sự cố

| Thấy gì | Làm gì |
|---|---|
| Colab báo *không do Google viết* | Bấm **Run anyway** |
| Chưa vào được Google Drive | Bấm **Run all** lại, chọn **Cho phép** |
| ⏳ AI đang quá tải | Không cần làm gì: notebook **tự đợi và hỏi lại** (tối đa khoảng 9 phút) |
| ⏳ Xong mà vẫn *còn đoạn chưa phân tích* | Lúc khác bấm **▶ ở ô 3️⃣**: chỉ các đoạn còn thiếu được hỏi lại |
| ⚠️ Có file chép lời bị lỗi | Bấm **▶ ở ô 2️⃣**, rồi **▶ ở ô 3️⃣** |
| Colab mất kết nối giữa chừng | Mở lại, bấm **Run all**: bản chép lời và câu trả lời của AI đã lưu trong `3_KetQua/_tam` |
| AI quá tải thường xuyên | Dùng **key Gemini riêng** (phần trên) |
| Drive sắp đầy | Xoá bớt file đã xử lý trong `2_FilePhatSong`; kết quả vẫn còn trong `3_KetQua` |

Notebook nhắc khi file đã xử lý chiếm quá 2 GB và **không bao giờ tự xoá file của bạn**. Drive miễn phí có 15 GB (dùng
chung với Gmail và Google Photos); mỗi file 3 giờ khoảng 165 MB.

## 🧠 Tự học (bạn không cần làm gì)

Quảng cáo AI tìm được, notebook **tự nhớ bằng âm thanh** trong `RadioQC/_tu_hoc`. Từ file sau, nó nhận ra chúng bằng
vân tay âm thanh, kể cả khi AI quá tải hoặc lời hát không chép được. Quảng cáo nhớ sai hoặc **60 ngày không phát** thì
tự xoá. Không muốn dùng: bỏ tick **TU_HOC_SPOT** ở ô ⚙️ Tuỳ chọn. File spot gốc của bạn (nếu có) luôn được ưu tiên hơn
trí nhớ.

## ❓ Hỏi nhanh

- **Không muốn dùng Drive?** Ở ô ⚙️ Tuỳ chọn chọn `NGUON_FILE` = *Tải lên từ máy*, rồi bấm **Choose Files**. Chậm với
  file lớn, và file mất khi đóng Colab.
- **Spot ngắn hơn 5 giây** (sound logo) không dò được tin cậy: notebook báo và bỏ qua.
- **File dài quá 5 phút** được coi là file phát sóng, không phải spot.
- **Muốn nghe lại clip sau khi đóng Colab?** Tick **CHAY_LAI_TAT_CA** rồi chạy lại.
- **Dùng thư mục khác thay cho `RadioQC`?** Đổi `THU_MUC_DRIVE` ở ô ⚙️ Tuỳ chọn.
- **Muốn chạy nhanh hơn?** Bỏ tick **DONG_THOI_GIAN** ở ô ⚙️ Tuỳ chọn (không có sheet Dòng thời gian).
