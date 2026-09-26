# 📻 Radio QC — dò quảng cáo trong file phát sóng radio

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/nguyenthanhhai-rf/radio-qc-colab/blob/main/RadioQC.ipynb)

Tìm các spot quảng cáo **đã biết** trong file phát sóng dài 1–3 giờ: phát lúc mấy giờ, bao nhiêu lần, phát đủ hay thiếu.
Kết quả là một báo cáo Excel.

Notebook chạy trên Google Colab bằng **tài khoản Google của bạn**. Không cần cài gì, không cần GPU.

## Mỗi lần dùng

1. Bấm nút **Open in Colab** ở trên, rồi **Runtime → Run all** (Ctrl+F9).
2. Ở ô **2️⃣**, bấm **Choose Files** và chọn file phát sóng trên máy (chọn được nhiều file).
   File chỉ nằm trong phiên Colab này, **không lưu vào Drive**.
3. Kết quả hiện ngay bên dưới; **báo cáo Excel tự tải về máy** (và lưu một bản trong Drive `RadioQC/3_KetQua`).
4. Muốn nghe lại một lần phát: ô **4️⃣ Nghe lại**, nhập **STT** trong báo cáo, bấm ▶.

Lần đầu: Colab cảnh báo notebook *không do Google viết* → bấm **Run anyway** (Vẫn chạy);
Colab xin quyền vào Google Drive (nơi để kho spot) → chọn tài khoản của bạn → **Cho phép**.

Tên file phát sóng nên có ngày giờ bắt đầu, ví dụ `CAO DIEM CHIEU 25.9.2026 16H30.mp3`, để báo cáo ghi giờ thật.

## Kho spot (làm một lần)

Lần chạy đầu, notebook tạo trong Google Drive của bạn thư mục `RadioQC/`:

| Thư mục | Để gì |
|---|---|
| `1_ThuVienQC/` | File gốc các spot quảng cáo **của bạn** (mp3, wav, m4a…), dài ít nhất 5 giây. **Tên file = tên spot**, ví dụ `Honda Vision 30s.mp3` |
| `3_KetQua/` | Bản lưu các báo cáo Excel |
| `2_FilePhatSong/` | Tuỳ chọn: file phát sóng bỏ sẵn trong Drive, thay cho việc tải lên |

Chưa có file nào cũng không sao: notebook chỉ tạo thư mục rồi nhắc bước tiếp theo.

**File lớn:** tải file 3 giờ (~170 MB) qua ô 2️⃣ có thể mất vài phút tuỳ mạng. Nếu thường xuyên dò file lớn, cài
*Google Drive for desktop* và bỏ file vào `RadioQC/2_FilePhatSong` — máy tự tải lên ngầm; khi chạy notebook, bấm
**Cancel upload** ở ô 2️⃣. File đã xử lý được bỏ qua ở lần sau; muốn dò lại (ví dụ vừa thêm spot mới) thì tick **CHAY_LAI_TAT_CA**.

## Đọc báo cáo

Báo cáo có 3 sheet: **Chi tiết** (từng lần phát), **Tổng hợp** (mỗi spot phát mấy lần, lúc nào; spot không phát ghi 0),
**Thông tin** (file, thời lượng, số spot trong thư viện, cảnh báo).

Cột **Tình trạng**:

- **Đủ**: phát trọn spot. Giờ bắt đầu chính xác trong khoảng 0,1 giây.
- **Phát thiếu: thiếu đầu/cuối ~X s**: spot bị cắt ngắn khi phát. Mép bị cắt chính xác trong khoảng 1,5 giây.
- **Cần nghe lại**: chỉ khớp một phần spot, ví dụ khớp nhạc hiệu đầu và cuối nhưng đoạn giữa khác — thường là
  **một spot khác dùng chung nhạc hiệu**. Hãy nghe lại trước khi tính vào đối soát.
- **Không kiểm được đủ**: spot nằm ở mép file ghi (file bắt đầu hoặc kết thúc giữa spot).
- Cột **Cũng khớp**: các spot khác trong thư viện có cùng đoạn âm thanh (ví dụ bản 15 giây cắt từ bản 30 giây).

## Hỏi nhanh

- **Tên file phát sóng không có giờ?** Báo cáo dùng giờ tính từ đầu file (`+00:12:30`) và ghi cảnh báo.
- **Spot ngắn hơn 5 giây** (sound logo) không dò được tin cậy: notebook báo "quá ngắn" và bỏ qua file đó.
- **File spot hỏng?** Ô kiểm tra đầu notebook báo đỏ trước khi chạy.
- **Nghe lại sau khi đóng Colab?** File tải lên mất khi phiên kết thúc; muốn nghe lại thì tải lên lại.
