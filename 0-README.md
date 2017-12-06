# NETWORK-COMMAND-LINE
#### Tables of contents
 * [iftop](#1-iftop---kiểm-tra-lưu-lượng-mạng-trên-linux-với-iftop)
 * [netstat](#2-netstat)
 * contrack table
 * dig domain
 * Atop, on
 * bm
 * ss
 * dd
 * nslookup
## 1. iftop - Kiểm tra lưu lượng mạng trên Linux với iftop
Iftop được sử dụng để xem băng thông hiện tại trên một giao diện mạng (network interface). Nó lắng nghe lưu lượng mạng trên một interface và hiển thị mức sử dụng băng thông hiện tại. Iftop phải được thực thi bởi user root hoặc user có đủ quyền hạn để theo dõi băng thông mạng.

**Cài đặt**

Trên Debian/Ubuntu:

    sudo apt-get install iftop

Trên CentOS/RHEL:
```
yum -y install epel-release
yum -y install iftop
```
**Sử dụng**

iftop sử dụng rất đơn giản. Chỉ cần gõ lệnh iftop trên terminal với quyền root để hiển thị mức sử dụng băng thông của interface đầu tiên. Nhấn q để thoát khỏi đầu ra của lệnh iftop

    iftop
![fig1](https://tailieu.123host.vn/wp-content/uploads/2017/03/iftop-command-line.png)

Để xem ip nguồn port đích, chỉ cần nhấn phím SHIFT + S và phím SHIFT + D. Nó sẽ hiển thị lưu lượng mạng truy cập cùng với các port nguồn và đích.

![fig2](https://tailieu.123host.vn/wp-content/uploads/2017/03/iftop-02.png)

Để xem lưu lượng băng thông của một interface cụ thể, sử dụng lệnh sau:

    iftop -i venet0

![fig3](https://tailieu.123host.vn/wp-content/uploads/2017/03/iftop-i-venet0.png)

Theo mặc định iftop sẽ hiển thị tất cả lưu lượng truy cập theo kilo/mega/giga bits mỗi giây. Để hiển thị lưu lượng truy cập theo byte thay vì bit thì thêm tham số -B (Capital B).

    iftop -i venet0 -B

![fig4](https://tailieu.123host.vn/wp-content/uploads/2017/03/iftop-ivenet0-B.png)

Để hiển thị lưu lượng truy cập đang xảy ra trên port nào, sử dụng tham số -P và -N

    iftop -i venet0 -P -N

![fig5](https://tailieu.123host.vn/wp-content/uploads/2017/03/iftop-ivenet0-P-N.png)

Tham số -N hiển thị số port.

Để xem luồng gói tin trong và ngoài của mạng, sử dụng lệnh sau.

    iftop -F 103.255.236.0/24
s
![fig6](https://tailieu.123host.vn/wp-content/uploads/2017/03/iftop-F103.255.236.0.png)

Để biết thêm thông tin về lệnh iftop, hãy tham khảo trang man bằng cách sử dụng lệnh sau:

    man iftop

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
