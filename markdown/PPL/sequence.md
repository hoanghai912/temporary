#1. Expressions
- Một biểu thức là đơn vị văn phạm:
	+ Tạo ra 1 giá trị
	+ Nếu có sai sót -> ra kết quả ko biết trước được
	
- Cơ chế chồng chất hàm

- Hình thức của biểu thức:
	+ Infix: Trung tố: Phép toán xuất hiện nằm giữa toán hạng của nó. VD: (a+b) * (c-d)
	
		- Có lợi cho phép toán 2 ngôi
		
		- Được dùng nhiều trong các ngôn ngữ thủ tục.
		
		- Gặp vấn đề khi có nhiều hơn 2 toán hạng.
		
		- Vấn đề tính ưu tiên
		
		- Tính kết hợp
		
			++ Có nhiều phép toán có cùng 1 độ ưu tiên. Tính từ trái sang phải. Trừ 1 số phép toán.
			
		- Dùng dấu ( ): 
			++ Lợi: Simple
			++ Hại: Writability và readability
			
		- Biểu thức điều kiện
	
	+ Prefix: Tiền tố: Phép toán đi trước toán hạng. VD: * + a b - c d hoặc (* (+ a b) (- c d)) hoặc *(+(a,b),-(c,d)). Duyệt NLR (N-left-right)
	
	+ Postfix: Hậu tố: Phép toán đi sau, toán hạng đi trước. Duyệt LRN (left-right-N). VD:
		- a b + c d - *
		- ((a b +) (c d -) *)
		
		- ((a,b)+,(c,d)-)*
		
#2. Thứ tự tính toán các toán hạng

- Các cơ chế tính toán:

	+ Eager evaluation:
		
		- Tính hết tất cả toán hạng trước.
		- Sau đó mới tới toán tử
		
	+ Lazy evaluation:
	
		- Truyền những toán hạng chưa được tính toán vào phép toán.
		
		- Phép toán quyết định tính cái nào trước.
		
		- Tốn nhiều chi phí hơn
		
	+ Lazy cho phép toán điều kiện, Eager cho các phép toán còn lại
	
	+ Short-circuit:
	
		- Nếu toán hạng đầu tiên được tính đúng thì toán hạng sau sẽ ko cần tính.
		
#3. Statement
- Phát biểu là một đơn vị văn phạm mà việc thực thi:
	+ Không trả về giá trị
	+ Thay đổi trạng thái hệ thống
	
- Phát biểu gán (Assignment):
leftExpr AssignOperator rightExpr

	+ leftExpr: Địa chỉ
	+ rightExpr: Giá trị
	
	+ Phép gán trên C có thể trả về giá trị. VD: ch = getchar()
	
- Cấu trúc điều khiển:
	+ Cho phép lựa chọn những nhánh điều kiện khác nhau
	+ Cho phép thực thi nhóm phát biểu nhiều lần
	
	+ Cấu trúc điều khiển là tập hợp các phát biểu điều khiển
	
	+Two-way selection:
		```if control_expression
		then clause
		else clause```
	
	+ Multiple-Selection:
		- Chú ý:
			++ Kiểu của biểu thức lựa chọn
			++ Làm cách nào để phát biểu dc lựa chọn
			++ Chỉ thực thi 1 nhóm hay nhiều nhóm
			++ Mô tả dc các giá trị của mỗi trường hợp
			++ Nếu giá trị lựa chọn ko thuộc trường hợp nào thì xử lý như thế nào
	
	+ Phát biểu lặp:
		+ Lặp được điều khiển bởi biến đếm:
			- Biến đếm
			- Giá trị bắt đầu
			- Biến tăng
		
		+ Lặp điều khiển bằng biểu thức luận lý:
			- Tổng quát hơn lặp biến đếm
			
			- Vấn đề kiểm tra trước hay sau vòng lặp
			
			- Có phải một dạng riêng của lặp biến đếm hay ko?
			
		+ User-located loop control:
			- Đơn giản: Vòng lặp vô tận nhưng bao gầm user-located loop exits
			
			- Phải có statement break và continue
		
		+ Vòng lặp dựa trên cấu trúc dữ liệu:
			- Sử dụng iterator
			
		+ Unconditional branching: goto