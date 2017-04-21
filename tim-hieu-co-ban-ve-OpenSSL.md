# Mở đầu

OpenSSL là phần mềm mã nguồn mở thực hiện các giao thức SSL và TLS. Được bắt đầu hoạt động vào năm 1998, bắt nguồn từ thư viện SSleay 
do Eric Young và Tim Hudson phát triển.

## SSL là gì?

SSL là một từ viết tắt của Secure Sockets Layer (Tầng các ổ cắm bảo mật). SSL là tiêu chuẩn phía sau truyền thông bảo mật trên Internet, 
tích hợp mật mã dữ liệu vào giao thức. Dữ liệu được mã hóa trước khi nó rời khỏi máy tính của bạn và chỉ được giải mã khi nó đạt đến đích dự định của nó. 
Các chứng nhận và các thuật toán mật mã hỗ trợ tất cả cách mà SSL hoạt động và với OpenSSL, bạn có cơ hội trải nghiệm với cả hai.

Về lý thuyết, nếu dữ liệu mã hóa đã bị thu chặn hoặc nghe trộm trước khi đến đích của nó, không có hy vọng nào về bẻ khóa dữ liệu đó. 
Nhưng cứ sau mỗi năm, các máy tính trở nên nhanh hơn và các cải tiến mới trong việc giải mã được thực hiện, cơ hội bẻ khóa các giao thức mật mã được 
sử dụng trong SSL đang bắt đầu tăng lên.

Kết nối SSL và kết nối bảo mật có thể được sử dụng cho bất kỳ loại giao thức nào trên Internet, cho dù đó là HTTP, POP3 hay FTP. 
Ngoài ra có thể sử dụng SSL để bảo vệ các phiên làm việc Telnet. Trong khi cũng có thể bảo vệ bất kỳ kết nối nào bằng SSL, 
nhưng không nhất thiết phải sử dụng SSL trên mọi loại kết nối. Nó nên được sử dụng nếu kết nối này sẽ mang thông tin nhạy cảm.

## OpenSSL là gì?

OpenSSL không chỉ là SSL. Nó có khả năng về các thuật toán băm (message digest), mã hóa và giải mã các tệp, các chứng nhận số, 
các chữ ký số và các số ngẫu nhiên. Có khá ít thư viện OpenSSL, nhiều hơn nữa về thư viện này có thể được đưa vào một bài báo khác.

OpenSSL không chỉ là API, nó cũng có một công cụ dòng lệnh. Công cụ dòng lệnh này có thể làm những thứ tương tự như API, nhưng tiến 
thêm một bước, cho phép có khả năng kiểm tra các máy chủ và các máy khách SSL. Nó cũng cung cấp một ý tưởng về các khả năng OpenSSL cho nhà phát triển

# Làm việc với OpenSSL

## Tạo ra một Self-signed

Bằng một câu lệnh đơn giản trên server ta có thể tạo ra một xác thực có giá trị trong 10 năm
```sh
openssl req -config /etc/ssl/openssl.cnf -newkey rsa:4096 -nodes -sha512 -x509 -days 3650 -batch -out /tmp/cacert.pem -keyout /tmp/key.pem

openssl req -config /etc/ssl/openssl.cnf -x509 -days 3650 -batch -nodes -newkey rsa:2048 -keyout private/logstash-forwarder.key -out certs/logstash-forwarder.crt

openssl req -x509 -nodes -days 730 -newkey rsa:2048 -keyout /etc/apache2/ssl/glance.key -out /etc/apache2/ssl/glance.crt
```

You can also add `-nodes` if you don't want to protect your private key with a passphrase, otherwise it will prompt you for "at least a 4 character" password.

`req`	PKCS#10 certificate request and certificate generating utility.
`config`
`-newkey arg`	this option creates a new certificate request and a new private key. The argument takes one of several forms. rsa:nbits, where nbits is the number of bits, generates an RSA key nbits in size.
`rsa:4096`	
`-nodes`	if this option is specified then if a private key is created it will not be encrypted.
`sha512`	
`-x509`	this option outputs a self signed certificate instead of a certificate request. This is typically used to generate a test certificate or a self signed root CA.
`-days n`	when the -x509 option is being used this specifies the number of days to certify the certificate for. The default is 30 days.
`batch`
`-out filename`	This specifies the output filename to write to or standard output by default.
`-keyout filename`	this gives the filename to write the newly created private key to.



