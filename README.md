# Dự án Biên soạn Tài liệu Toán Học (DHPX PREP)

Chào mừng bạn đến với dự án biên soạn tài liệu Toán học. Dự án này được thiết kế và cấu trúc trên nền tảng **LaTeX** nhằm mục đích tạo ra các tài liệu học tập, lý thuyết, ví dụ minh họa và **hệ thống đề thi trắc nghiệm/tự luận** một cách chuyên nghiệp, đồng bộ và có tính tự động hóa cao.

## 📂 Cấu trúc dự án

Dự án được chia thành các module (tệp nhỏ) để dễ dàng quản lý và chỉnh sửa, tránh việc dồn toàn bộ code vào một tệp duy nhất.

```text
📦 Source_code_bien_soan_TL_dai
 ┣ 📂 Preambles/             # Thư mục chứa các cấu hình và định nghĩa
 ┃ ┣ 📜 Packages.tex       # Nạp tất cả các gói (packages) cần thiết cho dự án.
 ┃ ┣ 📜 Layouts.tex        # Cấu hình giao diện (canh lề, header, footer, font chữ).
 ┃ ┣ 📜 Macros.tex         # Chứa toàn bộ "linh hồn" dự án: các biến, lệnh (macros) tự định nghĩa.
 ┃ ┣ 📜 bia.tex            # Thiết kế trang bìa của tài liệu.
 ┃ ┗ 📜 sections_page.tex  # Thiết kế các trang tiêu đề cho từng phần (Lý thuyết, Bài tập).
 ┣ 📂 build/                 # (Tự động sinh ra) Nơi chứa file PDF kết quả và các file tạm (.aux, .log, .toc).
 ┣ 📂 .vscode/               # Cấu hình môi trường VS Code.
 ┣ 📜 main.tex               # Tệp tin gốc (Entry point) để soạn thảo nội dung.
 ┗ 📜 README.md              # Tài liệu hướng dẫn này.
```

---

## 🛠 Cách Biên dịch (Build)

Dự án được tối ưu hóa để sử dụng **XeLaTeX**.

### Sử dụng VS Code (Khuyên dùng)
Dự án đã được thiết lập sẵn thư mục `.vscode/settings.json`.
1. Cài đặt extension **LaTeX Workshop**.
2. Mở file `main.tex`.
3. Bấm **Ctrl + Alt + B** (hoặc nút Build màu xanh).
4. Hệ thống sẽ tự động chạy XeLaTeX và đẩy toàn bộ tệp tin kết quả vào thư mục `build/`.
5. Mở tệp `build/main.pdf` để xem thành quả.

*Lưu ý:* Việc đẩy các tệp tạm (`.aux`, `.log`...) vào thư mục `build/` giúp thư mục gốc của bạn luôn sạch sẽ, gọn gàng, không bị "rác".

---

## 🚀 Hướng dẫn Soạn thảo (Template Động)

Dự án cung cấp một hệ thống "Template Động" cực kỳ mạnh mẽ để thiết kế đề thi. Thay vì phải copy-paste các cấu trúc header rườm rà, bạn chỉ cần dùng các dòng lệnh ngắn gọn sau.

### 1. Bắt đầu và Kết thúc một Đề thi
Mỗi đề thi sẽ được bọc trong 2 lệnh `\batdaude` và `\ketthucde`. Hệ thống sẽ tự động tạo Header đề thi, tự động đánh số thứ tự từ 0 và gom toàn bộ lời giải để in ra ở cuối đề.

```tex
\batdaude{Số đề}{Tên đề thi}{Mã đề}
... Nội dung đề thi ...
\ketthucde
```

**Ví dụ:**
```tex
\batdaude{1}{ĐỀ ÔN LUYỆN HÀM SỐ}{0101}
% Các câu hỏi của đề 1
\ketthucde

\batdaude{2}{ĐỀ ÔN LUYỆN LOGARIT}{0102}
% Các câu hỏi của đề 2 (số câu hỏi tự động reset lại từ 1)
\ketthucde
```

### 2. Chia Phần (Part)
Dùng để chia đề thi thành nhiều phần (Ví dụ: Trắc nghiệm khách quan, Trắc nghiệm đúng sai, Trả lời ngắn).

```tex
\phan{I}{Thí sinh trả lời từ câu 1 đến câu 12. Mỗi câu hỏi thí sinh chỉ chọn một phương án.}
```

*(Lưu ý: Nếu bạn muốn mỗi phần bắt đầu lại từ Câu 1, hãy gõ `\setcounter{cau}{0}` ngay dưới lệnh `\phan`)*.

### 3. Soạn thảo Câu hỏi & Lời giải
Dự án sử dụng lệnh `\caugiai` để vừa in ra câu hỏi, vừa bí mật lưu lời giải lại và chỉ hiển thị lời giải khi lệnh `\ketthucde` được gọi.

```tex
\caugiai
{
  % --- NỘI DUNG CÂU HỎI ---
  Nội dung câu hỏi ở đây.
  \bonpa{Đáp án A}{Đáp án B}{Đáp án C}{Đáp án D} 
  % \bonpa là macro chia 4 đáp án thành 4 cột đều nhau.
}
{
  % --- NỘI DUNG LỜI GIẢI ---
  Nội dung lời giải chi tiết ở đây.
}
```

### 4. Các môi trường bổ trợ
- `\begin{loigiaividu} ... \end{loigiaividu}`: Dùng để viết lời giải cho các ví dụ minh họa trên lớp (luôn hiển thị, không bị ẩn hay dời xuống cuối).
- `\begin{dungsai} \item ... \end{dungsai}`: Tạo môi trường đánh trắc nghiệm Đúng/Sai (A, B, C, D dưới dạng `a)`, `b)`, `c)`, `d)`).
- `\shortanswerline{Kết quả}`: Tạo đường kẻ ngang điền đáp án ngắn (sẽ hiển thị kết quả nếu bật chế độ giáo viên).

---

## ⚙️ Bật / Tắt Chế độ Giáo viên - Học sinh
Tại tệp `Preambles/Macros.tex`, bạn có thể kiểm soát việc in ra lời giải hay chỉ in ra đề bài trống.

Mở `Macros.tex` và tìm tới đoạn `CHE DO GIAO VIEN / HOC SINH`:
- Dùng `\giaovientrue` (Bật hiển thị Lời giải, đáp án).
- Dùng `\giaovienfalse` (Tắt hiển thị Lời giải, in ra bản trắng cho học sinh làm bài).
