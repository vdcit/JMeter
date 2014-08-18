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

## Ví dụ sử dụng JMeter kiểm thử hiệu năng Website

#### Mô hình kiểm thử

#### Quá trình thực hiện

## Tài liệu tham khảo

