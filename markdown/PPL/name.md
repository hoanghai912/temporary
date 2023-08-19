# Name
- Là một chuỗi các kí hiệu, thay cho địa chỉ tham khảo đến một thực thể trong ctrình

# Binding
- Sự ràng buộc: Sự kết hợp giữa 2 thực thể khác nhau.

- Binding time:
	+ Early binding: Ràng buộc sớm, khi thiết kế ngôn ngữ đã ràng buộc
	
	+ Late binding: Xảy ra vào thời gian thực thi.
	
	+ Static binding: Những ràng buộc xảy ra trước khi thực thi.
	
	+ Dynamic binding: Xảy ra vào thời gian chạy chương trình
	
	+ Polymorphism: Ràng buộc giữa 1 tên ràng  buộc với nhiều thực thể.
	
	+ Alias: Nhiều tên nhưng ràng buộc với 1 thực thể.
	
	+ Language design time: Thời gian ràng buộc ngôn ngữ từ lúc thiết kế
	
	+ Language implementation time
	
	+ Programming time: Do người lập trình quyết định. VD: Biến x phải là kiểu nguyên.
	
	+ Compilation time: Khi dịch sẽ thực hiện ràng buộc đó.
	
	+ Linking time: Tạo nhiều file object và nối file lại. VD địa chỉ tương đối
	
	+ Load time: Thời gian nạp ctrình từ đĩa cứng vào bộ nhớ trong. VD địa chỉ tuyệt đối.  thời gian nạp là lúc loader nạp chương trình thực thi từ bộ nhớ ngoài vào bộ nhớ trong. Tuỳ theo thực tế của bộ nhớ trong lúc chương trình được nạp mà chương trình sẽ được cấp phát vào một vùng nhớ phù hợp. Sau khi cấp phát thì các biến toàn cục mới có địa chỉ tuyệt đối và khi đó, ràng buộc mới xảy ra,
	
	+ Runtime
	
# Object Lifetime
- Object Lifetime: Thời gian dc tạo ra cho tới khi bị huỷ bỏ.

- Dangling ref (tham chiếu treo): Ràng buộc với đối tượng đó còn nhưng đối tượng đó bị huỷ.

- Leak memory - Garbage (rác): Đối tượng vẫn còn những ràng buộc đã bị huỷ

# Cấp phát đối tượng
- Static: Tĩnh. Tồn tại từ lúc chạy ctrình tới khi kết thúc ctrình (biến toàn cục, hằng)

- Stack Dynamic: Tạo ra trước, huỷ bỏ sau (Được cấp phát huỷ bỏ theo đúng quy luật: biến cục bộ)

- Explicit heap dynamic: Người dùng tạo ra theo qua gọi lệnh, hàm, ...

- Implicit heap dynamic: Ngầm định cấp phát

# Static scope rules
- Tham khảo tới một danh hiệu luôn luôn lấy trong local gần nó nhất

- Một khai báo sẽ không được nhìn thấy ngoài block đó (Khai báo trong block thì bên ngoài block sẽ ko sử dụng được)

- Những khai báo nằm bên ngoài có thể được nhìn thấy bởi các block nằm bên trong, trừ khi block bên trong khai báo lại.