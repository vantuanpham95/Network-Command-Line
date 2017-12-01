# NETWORK-COMMAND-LINE
 ## Tables of contents
 * ![iftop](#1-iftop---kiểm-tra-lưu-lượng-mạng-trên-linux-với-iftop)
 * netstat
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

![fig6](https://tailieu.123host.vn/wp-content/uploads/2017/03/iftop-F103.255.236.0.png)

Để biết thêm thông tin về lệnh iftop, hãy tham khảo trang man bằng cách sử dụng lệnh sau:

    man iftop
