# 📻 Radio QC — dò quảng cáo trong file phát sóng radio

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/nguyenthanhhai-rf/radio-qc-colab/blob/main/RadioQC.ipynb)

Tìm các spot quảng cáo **đã biết** trong file phát sóng dài 1–3 giờ: phát lúc mấy giờ, bao nhiêu lần, phát đủ hay thiếu.
Kết quả là một báo cáo Excel.

Notebook chạy trên Google Colab bằng **tài khoản Google của bạn**. File của bạn nằm trong **Google Drive của bạn**;
notebook không gửi dữ liệu đi đâu khác. Không cần cài gì, không cần GPU.

## Lần đầu

1. Bấm nút **Open in Colab** ở trên.
2. Chọn **Runtime → Run all** (Ctrl+F9).
3. Colab cảnh báo notebook *không do Google viết* → bấm **Run anyway** (Vẫn chạy).
4. Colab xin quyền vào Google Drive → chọn tài khoản của bạn → **Cho phép**.
5. Notebook tạo trong Drive thư mục `RadioQC/`:

   | Thư mục | Để gì |
   |---|---|
   | `1_ThuVienQC/` | File gốc các spot quảng cáo (mp3, wav, m4a…), dài ít nhất 5 giây. **Tên file = tên spot**, ví dụ `Honda Vision 30s.mp3` |
   | `2_FilePhatSong/` | File phát sóng cần dò. Tên file nên có ngày giờ bắt đầu, ví dụ `CAO DIEM CHIEU 25.9.2026 16H30.mp3` |
   | `3_KetQua/` | Báo cáo Excel, mỗi file phát sóng một báo cáo |

## Mỗi lần dùng

1. Bỏ file spot mới vào `1_ThuVienQC`, file phát sóng vào `2_FilePhatSong`.
2. Mở notebook, **Run all**. File đã xử lý sẽ được bỏ qua.
3. Mở báo cáo trong `3_KetQua`. Muốn nghe lại một lần phát: ô **3️⃣ Nghe lại**, nhập **STT** trong báo cáo, bấm ▶.

Vừa thêm spot mới và muốn dò lại các file cũ: tick **CHAY_LAI_TAT_CA** rồi chạy lại.

**Mẹo:** cài *Google Drive for desktop* để kéo thả file vào `RadioQC` như một thư mục trên máy tính.

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
- **Thư viện trống hoặc file hỏng?** Ô kiểm tra đầu notebook báo đỏ trước khi chạy.
