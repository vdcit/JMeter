JMeter
======

Hướng dẫn sử dụng JMeter

## Giới thiệu

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
- Meter lưu các kịch bản kiểm thử của nó dưới dạng các file XML, do đó ta có thể tự tạo các kịch bản kiểm thử của mình bằng một trình soạn thảo bất kỳ và load nó lên
- Đa luồng, giúp xử lý tạo nhiều request cùng một khoảng thời gian, xử lý các dữ liệu thu được một cách hiệu quả
- Đặc tính mở rộng, có rất nhiều plugin được chia trẻ rộng rãi và miễn phí
- Một công cụ tự động để kiểm thử hiệu năng và tính năng của ứng dụng.

Cách thức hoạt động: nó giả lập một nhóm người dùng gửi các yêu cầu tới một máy chủ mục tiêu, nhận và xử lý các response từ máy chủ và trình diễn các kết quả đó cho người dùng dưới dạng bảng biểu, đồ thị,…

## Hướng dẫn sử dụng

Đầu tiên ta cần cài đặt java cho hệ điều hành đang sử dụng: Windows, Linux, MacOS,...

Tiếp theo ta tải mã nguồn của chương trình về tại [địa chỉ](http://jmeter.apache.org/download_jmeter.cgi)

Giải nén file vừa tải về và chuyển vào thư mục bin/
- Đối với Windows thì chỉ cần chạy file jmeter.bat
- Đối với Linux thì chỉ cần chạy file jmeter.sh

Giao diện chính của chương trình: 
![img](http://my.metadata.vn/share/s/HUknyPyxQfmhd3BRjYJuFQ/Jmeter_giao_dien.png "img")
## Tài liệu tham khảo

