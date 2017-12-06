# NETWORK-COMMAND-LINE
## 2. netstat
Netstat là một công cụ hữu ích của Linux cho phép kiểm tra những dịch vào nào đang kết nối đến hệ thống của bạn. Nó rất hữu ích trong việc phân tích cái gì đang xảy ra trên hệ thống khi ta cố gắng ngăn chặn một cuộc tấn công nhằm vào nó. Ta có thể tìm thêm thông tin như có bao nhiêu kết nối được tạo ra trên một cổng, địa chỉ IP nào đang kết nối đến và nhiều thông tin khác nữa. 

 * netstat -a: Hiển thị tất cả các kết nối và các cổng nghe
```
    netstat -a
```
 * netstat -b: Hiển thị thực thi liên quan đến việc tạo ra mỗi kết nối hay lắng nghe cổng
```
    netstat -b
```
 * netstat -e: Hiển thị Ethernet thống kê. Điều này có thể được kết hợp với các tùy chọn-s
```
    netstat -e
```
 * netstat -f: Hiển thị Fully Qualified Tên miền (FQDN) cho các địa chỉ nước ngoài
```
    netstat -f
```
 * netstat -n: Hiển thị các địa chỉ và số cổng
```
    netstat -n
```
 * netstat -o: Hiển thị quá trình ID sở hữu liên kết với mỗi kết nối.( Tham số này có thể được kết hợp với các tham số -a,-n,-p)
```
    netstat -o
```
 * netstat -p: Hiển thị các kết nối cho giao thức theo quy định của protocol Protocol có thể là bất kỳ: TCP, UDP, TCP v6 hoặc UDPv6. (Nếu tham số này được sử dụng với-s để hiển thị các số liệu thống kê bởi giao thức, Nghị định thư có thể được tcp, udp, icmp, ip, tcpv6, udpv6, ICMPv6, hoặc ipv6)
```
    netstat -proto
``` 
 * netstat -r: Hiển thị bảng định tuyến
```
    netstat -r
```
 * netstat -s: Hiển thị số liệu thống kê cho mỗi giao thức. Theo mặc định, các số liệu thống kê được hiển thị cho TCP, UDP và IP, tuỳ chọn-p có thể được sử dụng để chỉ định một tập hợp con của mặc định.
 
 * netstat – interval: Hiển thị lại lựa chọn số liệu thống kê, ngừng lại giây khoảng thời gian giữa mỗi màn hình. Nhấn phím Ctrl + C để ngăn chặn thống kê redisplaying. Nếu bỏ qua, netstat sẽ in thông tin cấu hình hiện tại một lần.

**Một số ví dụ khi kết hợp lệnh:**

 * Để hiển thị cả số liệu thống kê Ethernet và các số liệu thống kê cho tất cả các giao thức, gõ lệnh sau:
```
    netstat -e -s
```
 * Để hiển thị các số liệu thống kê cho các giao thức TCP và UDP, gõ lệnh sau:
``` 
    netstat -s -p tcp udp
```
 * Để hiển thị các hoạt động kết nối TCP và quá trình ID mỗi 5 giây, gõ lệnh sau:
``` 
    netstat -o 5
```
 * Để hiển thị các hoạt động kết nối TCP và ID quá trình này bằng cách sử dụng hình thức số, gõ lệnh sau:
``` 
    netstat -n -o
```
 * Để hiển thị tất cả các kết nối và số cổng
``` 
    netstat -ant
```
 Có thể kết hợp netstat với các lệnh khác để nhìn được các thông số cần thiết một cách dễ dàng hơn như grep, awk, sort, uniq, wc -l. Tuy nhiên sử dụng netstat khi server gặp sự cố là rất khó khăn vì nestat ngốn nhiều tài nguyên CPU. Trick ở đây là ta cứ netstat một lần rồi xuất kết quả ra text, sau đó xử lý file text đó để ra kết quả 
 
 **Một vài lưu ý:** cổng 80/443 là cổng mặc định http/https, cổng 22 là cổng mặc định ssh, 3306 là cổng mặc định của mysql

**Giải thích tham số**
 
 * Proto: Cho biết kế nối là TCP hay UDP
 * Local address: Địa chỉ IP của máy tính địa phương và số cổng được sử dụng. Tên của máy tính địa phương tương ứng với địa chỉ IP và tên của cảng được hiển thị trừ khi tham số -n được quy định cụ thể. Nếu cổng chưa được thành lập, số cổng phải được thể hiện như là một dấu sao (*).
 * Foreign address: Địa chỉ IP và số cổng của máy tính từ xa mà ổ cắm được kết nối. Các tên tương ứng với địa chỉ IP và cổng được hiển thị trừ khi tham số -n được quy định cụ thể. Nếu cổng chưa được thành lập, số cổng phải được thể hiện như là một dấu sao (*)
 
 * State: Cho biết trang thái cổng: Cho biết trạng thái của một kết nối TCP. Các trạng thái có thể là như sau:
  * CLOSE_WAIT
  * CLOSED
  * ESTABLISHED
  * FIN_WAIT_1
  * FIN_WAIT_2
  * LAST_ACK
  * LISTEN
  * SYN_RECEIVED
  * SYN_SEND
  * TIMED_WAIT
