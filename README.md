# Bộ cân bằng âm thanh trên kit DE2 
Thực hiện hệ thống trên Kit DE2 nhằm kiểm chứng, phân tích hoạt động của bộ lọc FIR cho những tính hiệu âm thanh theo tần số xác định 
## Đường đi của tín hiệu
Tín hiệu âm thanh đi từ máy tính từ jack 3.5 đi vào line in của KIT DE2 chạy vào bộ xử lý âm thanh của chip Woflson Wm8731, âm thanh được đi vào bộ ADC chuyển từ tín hiệu analog sang tín hiệu số mã bit nhị phân. Chip âm thanh sẽ gom thành những phần 24 bit để gửi đi (sample valid)
Từng mẫu âm thanh 24bit như vậy sẽ được dịch vào chip FPGA bằng giao thức I2S đi vào bộ chia tần số để chia ra thành 10 giá trị tần số thao dải âm, bằng cách cho đi qua 10 bộ lọc ( mỗi bộ lọc thông dải chỉ cho một tần số xác định đi qua). 
Sau khi thu được 10 tín hiệu âm thanh có giá trị tần số khác nhau, sẽ được tiếp tục đưa qua bộ nhân khuếch đại giá trị biên độ với giá trị khuếch đại nhận được từ giao diện người dùng bằng phương thức giao tiếp uart. Khi đã có biên độ sau điều chỉnh thì sẽ được cộng gộp lại theo cây bộ cộng và biến ngăn tràn bit ( bảo vệ loa ) 
Tín hiệu sau khi tinh chỉnh biên độ sẽ được đi qua bộ DAC chuyển từ tính hiệu số sang tính hiệu analog để đưa ra loa với giao thức  I2S 32 bit để đi ra màng loa phát ra âm thanh.
## Thiết bị sử dụng 
Laptop: gửi tín hiệu âm thanh và tinh chỉnh giá trị biên độ trên giao điện người dùng 
loa: phát tín hiệu âm thanh
CH340:  chuyển đổi cổng USB-A sang giao tiếp uart với kit DE2
