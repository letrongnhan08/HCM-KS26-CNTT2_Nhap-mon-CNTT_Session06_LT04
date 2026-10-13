Bài 4 : Xây dựng quy trình lưu nhật ký hệ thống

Bẫy dữ liệu:

\- Nếu An gõ nhầm > thay vì >> thì toàn bộ lịch sử dữ liệu bên trong file sẽ bị xóa toàn bộ do tính năng ghi đè của toán tử >

Phần 1: So sánh

||Toán tử >|Toán tử >>|
|-|-|-|
|Cơ chế hoạt động|Đối với tệp đã tồn tại, lệnh này ghi đè toàn bộ nội dung cũ sẽ bị xóa sạch và thay thế bằng kết quả mới|Đối với tệp đã tồn tại,sử dụng lệnh này thì kết quả mới sẽ được nối tiếp vào cuối tệp, bảo toàn dữ liệu cũ|
|Rủi ro mất dữ liệu|Cao|Thấp|
|Ngữ cảnh sử dụng thực tế|Phù hợp cho việc tạo mới báo cáo từ đầu|Phù hợp cho việc theo dõi hệ thống 24/7,thu thập và tích lũy,cập nhật liên tục mà không làm mất dữ liệu|
|Encoding file đầu ra|UTF-16|UTF-16|



Phần 2:

Giải pháp tối ưu và chuyên nghiệp nhất trong PowerShell là sử dụng Out-File -Append

Lý do: Bảo toàn dữ liệu lịch sử (Tránh mất mát):

Trong hệ thống theo dõi lỗi liên tục (24/7), nhật ký của các thời điểm trước đó trong ngày rất quan trọng cho lập trình viên phân tích sự cố. Toán tử >> (và Out-File -Append) có cơ chế ghi nối tiếp vào cuối tệp, giúp dữ liệu không bị ghi đè hoặc mất mát mỗi khi kịch bản được kích hoạt chạy.

Đề xuất bổ sung: (Out-File -Append -Encoding utf8)

Get-Content server.log | Select-String "ERROR" | Out-File -FilePath "daily\_report.txt" -Append -Encoding utf8

