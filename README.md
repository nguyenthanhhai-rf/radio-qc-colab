# 📻 Radio QC — tìm quảng cáo trong file phát sóng radio

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/nguyenthanhhai-rf/radio-qc-colab/blob/main/RadioQC.ipynb)

Đưa vào file phát sóng dài 1–3 giờ, nhận về **một file Excel**: có những quảng cáo nào, phát lúc mấy giờ, dài bao lâu,
kèm **bản chép lời** cả chương trình.

Notebook chạy trên Google Colab bằng **tài khoản Google của bạn**. Không cần cài gì.

## Mỗi lần dùng

1. Bấm nút **Open in Colab** ở trên, rồi **Runtime → Run all** (Ctrl+F9).
2. Lần đầu, Colab báo notebook *không do Google viết* → bấm **Run anyway** (Vẫn chạy).
3. Bấm **Choose Files**, chọn file phát sóng trên máy (chọn được nhiều file).
   Có file quảng cáo gốc (spot) thì chọn kèm luôn.
4. Đợi xong: **file Excel tự tải về máy** (thư mục Tải xuống / Downloads). Bảng kết quả hiện ngay bên dưới,
   bấm ▶ để nghe từng quảng cáo.

File của bạn chỉ nằm trong phiên Colab này, **không lưu vào đâu cả**; đóng Colab là mất.

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

## Kho spot trên Google Drive (tuỳ chọn)

Nếu ngày nào cũng dò cùng một bộ spot, có thể để sẵn chúng trong Google Drive thay vì chọn lại mỗi lần:
bỏ file spot vào thư mục `RadioQC/1_ThuVienQC` trong Drive (**tên file = tên spot**, ví dụ `Honda Vision 30s.mp3`),
rồi ở ô **⚙️ Tuỳ chọn** tick **DUNG_KHO_SPOT_TREN_DRIVE**. Colab sẽ xin quyền vào Drive: chọn tài khoản của bạn → **Cho phép**.

## Hỏi nhanh

- **Tên file phát sóng không có giờ?** Báo cáo dùng giờ tính từ đầu file (`+00:12:30`) và ghi cảnh báo.
- **Spot ngắn hơn 5 giây** (sound logo) không dò được tin cậy: notebook báo "quá ngắn" và bỏ qua file đó.
- **File quá 5 phút** được coi là file phát sóng, không phải spot.
- **Muốn nghe lại sau khi đóng Colab?** File tải lên đã mất; tải lên lại rồi chạy lại.
