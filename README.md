JMeter
======

Hướng dẫn sử dụng JMeter

## 1. Giới thiệu

Apache JMeter là một phần mềm nguồn mở được viết bằng Java nhằm mục đích kiểm thử chức năng và hiệu suất. Mục đích ban đầu JMeter được thiết kế chỉ để kiểm thử các ứng dụng web nhưng hiện nay nó đã được mở rộng thêm nhiều chức năng khác.

Cha đẻ của JMeter là Stefano Mazzocchi, một lâp trình viên tại Apache Software Foundation. Ông ta viết JMeter với mục đích là kiểm thử hiệu năng của Apache JServ (bây giờ là Apache Tomcat). Sau đó Apache đã thiết kế lại để cải tiến hơn giao diện đồ họa cho người dùng và khả năng kiểm thử hướng chức năng.

Nó là một ứng dụng Java với phần dao diện sử dụng Java Swing, do đó nó có thể chạy được trên mọi nền tảng có hỗ trợ JVM, ví dụ như Windows, Linux, Mac,…

Các giao thức mà JMeter hỗ trợ:
- Web: HTTP, HTTPS sites 'web 1.0' web 2.0 (ajax, flex and flex-ws-amf)
- Web Services: SOAP / XML-RPC
- Database: JDBC
- Directory: LDAP
- Messaging Oriented service: JMS
- Service: POP3(s), IMAP(s), SMTP(s)
- TCP
- MongoDB (NoSQL)

Các tính năng nổi bật của JMeter:
- Nguồn mở, miễn phí
- Giao diện đơn giản, trực quan dễ sử dụng
- Có thể kiểm thử nhiều kiểu server: Web - HTTP, HTTPS, SOAP, Database - JDBC, LDAP, JMS, Mail - POP3,…
- Một công cụ độc lập có thể chạy trên nhiều nền tảng hệ điều hành khác nhau, trên Linux chỉ cần chạy bằng một shell scrip, trên Windows thì chỉ cần chạy một file .bat
- JMeter lưu các kịch bản kiểm thử của nó dưới dạng các file XML, do đó ta có thể tự tạo các kịch bản kiểm thử của mình bằng một trình soạn thảo bất kỳ và load nó lên
- Đa luồng, giúp xử lý tạo nhiều request cùng một khoảng thời gian, xử lý các dữ liệu thu được một cách hiệu quả
- Đặc tính mở rộng, có rất nhiều plugin được chia trẻ rộng rãi và miễn phí
- Một công cụ tự động để kiểm thử hiệu năng và tính năng của ứng dụng.

Cách thức hoạt động: nó giả lập một nhóm người dùng gửi các yêu cầu tới một máy chủ mục tiêu, nhận và xử lý các response từ máy chủ và trình diễn các kết quả đó cho người dùng dưới dạng bảng biểu, đồ thị,…

## 2. Hướng dẫn sử dụng

Đầu tiên ta cần cài đặt java cho hệ điều hành đang sử dụng: Windows, Linux, MacOS,...

Tiếp theo ta tải mã nguồn của chương trình về tại [địa chỉ](http://jmeter.apache.org/download_jmeter.cgi)

Giải nén file vừa tải về và chuyển vào thư mục bin/
- Đối với Windows thì chỉ cần chạy file jmeter.bat
- Đối với Linux thì chỉ cần chạy file jmeter.sh

Giao diện chính của chương trình: 

<img src=http://i.imgur.com/U3DfbXB.png border="1">

Trước khi bắt đầu test ta cần lập một Test Plan để JMeter thực hiện. Có một vài thông số quan trọng trong JMeter như Thread Groups, Listeners, Assertions, Sample Generating Controller, Logic Controllers,… Những thông số này sẽ được mô tả dưới bảng sau:

| Thành phần   | Mục đích |
| -------------|----------------|
| Samples | Những phần tử này gửi các yêu cầu tới server. Có những samplers cho những kiểu request: HTTP/HTTPS, FTP, SOAP, JDBC, "Java", LDAP, MongoDB, TCP,… |
| Listeners Timers | Tập các kết quả của việc run test, cung cấp cho người dùng các công cụ hiển thị một cách trực quan, dễ hiểu |
| Logic Controllers | Nếu những request được định nghĩa trong các test plan của bạn được thực thi dựa phụ thuộc vào một vài logic, lúc đó sẽ cần đến Logic Controllers. Chúng thích hợp với cấu trúc if-then-else và loop trong Java hay các ngôn ngữ khác. |
| Configuration Elements | Chúng làm việc với Samples bằng cách thêm những thông tin chung với những Request |
| Assertions | Cho phép bạn kiểm tra nếu responses bạn lấy chứa dữ liệu mong đợi hay nhận trong phạm vi thời gian đã định sẵn |

Một điều cần lưu ý đó là mọi Test Plan đều cần ít nhất một Thread Groups. Do mỗi Thread Groups sẽ tạo ra được các yêu cầu để gứi tới server, nếu không có Thread Groups thì không có yêu cầu nào được gửi nên không thể tiến hành việc test.

Với mỗi mục đích kiểm thử khác nhau thì sẽ xây dựng các Test Plan khác nhau, tránh trường hợp chúng ta thêm tất cả các thành phần vào Test Plan. Điều đó sẽ làm “rối” và có các thành phần không được sử dụng đến gây lãng phí tài nguyên. Mỗi Test Plan cần có ít nhất hai thành phần chính trong Thread Groups là một Sampler để tạo các request và một Listeners để hiển thị kết quả cho người dùng.

Do JMeter có rất nhiều chức năng như đã trình bày ở trên nên rất khó có thể trình bày hết trong một sớm một chiều được. Tôi xin phép được trình bày những kiến thức học được dưới một ví dụ cụ thể dưới đây.

## 3. Ví dụ sử dụng JMeter kiểm thử hiệu năng Website

#### 3.1. Mô hình kiểm thử

    --------------                  ----------------
    |   TestPC   |- ----------------|  Web Server  |
    --------------                  ----------------
     172.16.69.140                   172.16.69.122

TestPC:

    Windows 7 64bit
    IP: 172.16.69.140
    Cài Java 7 và JMeter

Web Server:

    Windows Server 2008
    IP: 172.16.69.122
    Cài đặt Website để thử nghiệm

Giao diện Website:
<img src=http://i.imgur.com/GQ2Kkj1.png>

#### 3.2. Kịch bản kiểm thử

- Test với một user truy cập web (không đăng nhập)
- Test với 10 user đăng nhập vào web và thực hiện các chức năng sau:

    Đăng nhập
    Liệt kê danh mục
    Liệt kê văn bản
 
#### 3.3. Quá trình thực hiện

##### 3.3.1. Test với một user truy cập web (không đăng nhập)

###### Khai báo thông số của JMeter

Tạo một thread group bằng cách click chuột phải vào Test plan, sau đó chọn ADD rồi chọn Thread group option. Sau khi chọn Thread group option thì một thread group element sẽ được sinh ra. Căn cứ vào đó chúng ta sẽ giả lập được số lượng người test và số lần test plan được lặp lại. 
<img src=http://i.imgur.com/gxN7mNU.png>

Thread group element
<img src=http://i.imgur.com/26U5twM.png>

- Name: Tên của Thread, có thể tạo tên bất kỳ để dễ phân biệt
- Number of Threads: số các thread được giả lập, mỗi thread giả lập tương đương với một user. Ví dụ nếu để tham số này là 10 thì tương đương với đó sẽ là 10 user được giả lập để gửi các request.
- Ramp-Up Period: cho biết thời gian để JMeter tạo ra tất cả những thread cần thiết. Ví dụ nếu tham số này là 10 thì trong 10 giây tất cả các Number of Threads đã khai báo ở trên sẽ được gửi đi trong 10 giây, nếu đặt tham số này là 0 thì tất cả các yêu cầu sẽ được gửi đi cùng một lúc. Nếu trong thời gian này mà tất các request không được gửi hết thì các request còn lại sẽ được đẩy vào một hàng đợi.
- Loop Count: số lần lặp lại việc kiểm thử. Nếu checkbox Forever được chọn thì việc lặp sẽ diễn ra liên tục cho đến khi người dùng dừng bằng tay.
- Ngoài ra ta có thể sử dung Scheduler để lập lịch cho hành động kiểm thử.

Tiếp theo ta sẽ cần thêm một Sample vào Thread Group vừa tạo bằng cách chọn chuột phải vào Thread Group chọn Add và Sampler. Có rất nhiều Sampler để lựa chọn, với những mục đích test khác nhau thì ta sẽ chọn các Sampler phù hợp. Ở đây với mục đích là test trang web nên tôi chọn HTTP Request.
<img src=http://i.imgur.com/vEm4MYs.png>

Các tham số của HTTP Request gồm:
- Name: đặt tên request
- Server Name or IP: điền vào domain hoặc IP của trang web cần kiểm tra
- Port Number: chỉ ra port của web, để trống sẽ là port mặc định 80.
- Protocol: giao thức được sử dụng HTTP hoặc HTTPS
- Method: phương thức để gửi các HTTP request, các phương thức ở đây bao gồm GET, POST, PUSH, HEAD,…
- Path: đường dẫn nguồn để xử lý các Request. Nếu điền / thì sẽ gửi các yêu cầu tới trang chủ.
- Parameters: biểu diễn danh sách các thông số gửi cùng request, ta có thể thêm hoặc xóa các thông số này.
- Send a file with a request: giả lập việc upload file.
- Retrieve all images and Java Applets: dùng để download các Java Applets được nhúng trên trang.
- Ngoài ra cũng có những tham số để cấu hình thời gian time out cho các request và respone, các cấu hình Redirect, Keep alive, Proxy Server.

Các tham số tôi sử dụng để kiểm thử giống như trong hình trên.

Sau khi nhận được những Request thì Server sẽ gửi trả lại những response, do đó ta sẽ cần thêm những Listener để hiển thị những kết quả đó. Một trong những Listener dễ quan sát nhất là View Results Tree. Ta có thể thêm nó bằng cách chuột phải vào Test Plane, chọn Add Listener, View Results Tree.

Một Listener cũng rất hữu ích đó là View Results Table. Listener này cung cấp một cái nhìn về các Sample đã được tạo ra dưới dạng bảng, ta có thể dễ dàng tìm thấy các thông tin như thời gian bắt đầu của các Sample (tính đến milisecond), dung lượng gói tin, độ trễ,…

Các Listener tôi sử dụng:
<img src=http://i.imgur.com/wMzcYEL.png>

###### Chạy ứng dụng

Sau khi đã khai báo các tham số của JMeter bên trên, ta click vào Run, Start hoặc tổ hợp phím Ctrl + R để chạy ứng dụng.





## Tài liệu tham khảo

