# Scalar types:
- Nguyên tố
- Được dùng để tạp ra kiểu dữ liệu khác lớn hơn.
- Đôi khi được hỗ trợ bởi phần cứng.
- Bool, char, integer, floating-point, fix-point, complex, void, enum, intervals, ...

# Kiểu nguyên:
- Ngôn ngữ hỗ trợ nhiều kích thước của kiểu nguyên. (byte, short, int, long)
- Một số ngôn ngữ bao hàm kiểu dữ liệu nguyên ko dấu
- Được hỗ trợ bởi phần cứng: Chuỗi các bit nhị phân
- Biểu diễn số âm ở dạng bù 2

# Floating-point
- Dùng để mô hình hoá các giá trị thực, nhưng chỉ là xấp xỉ.
- Hỗ trợ cho tính toán khoa học (float, double)
- Tính chính xác và range
- IEEE floating-point standard 754
- Single precision:
	| S | Exponent | Fraction |
    |:------------|:-------------:|-------------:|
    |      |   8 bits    |        23 bits |

- Double precision:
	| S | Exponent | Fraction |
    |:------------|:-------------:|-------------:|
    |      | 11 bits | 52 bits |

- Ví dụ:
Cho kiểu số thực dấu chấm động tương tự chuẩn IEEE-754. Số bit của miền dấu là 1, exponent là 3, fraction là 5. Hãy viết chuỗi bit của số thực 2.8

    - Phần thực: 2 => 10
    - Phần thập phân: 0.8 => 1100110011001100 ===Lấy 5 bit==> 11001 (Tính bằng cách nhân 2)
    - Dec => Bin: 2.8 => 10.11001
    - Chuyển qua dạng chuẩn: $1.011001 \cdot 2^{1}$ (Dịch dấu chấm bao nhiêu bit thì mũ bấy nhiêu)
    - Số mũ trong IEEE-754 : Số mũ dạng chuẩn * 2^(số bit mũ exponent - 1) = 1 * 2 ^(3 - 1) = 4 => 100

    => Số cần tìm: 010001100
		
# Decimal:
- Sử dụng trong tiền (Cần chính xác)
- Lưu trữ cố định các con số sau dấu chấm.
- Ưu điểm: Chính xác
- Nhược điểm:
	+ Giới hạn range
	+ Lãng phí bộ nhớ

### Chuyển đổi từ Decimal -> Binary (1 byte = 8 bits):
#### Số dương:
1. Chuyển từ Decimal sang binary (số dương) -> Kết quả

#### Số âm:
1. Chuyển từ Decimal sang binary (số dương) -> Kết thúc nếu là số dương
2. Chuyển từ sang bù 1 bằng cách đảo bit (1 thành 0, 0 thành 1)

3. Cộng thêm 1 có được bù 2 -> Kết quả
    

# Boolean
- Đơn giản nhất
- Chỉ có hai giá trị: True hoặc False
- Có thể hiện thực trên bit, nhưng thường hiện thực ở byte

# Character
- Lưu trữ dưới dạng mã hoá.
- Thông thường nhất: Mã ASCII
- Thay thế: Mã Unicode (16-bit)

# Kiểu dữ liệu có thứ tự do người dùng tự định nghĩa
- Là một dạng kiểu là các miền có thể có và kết hợp với các giá trị ngyuyên dương. (int, char, bool)

# Enumtype
- Tất cả các giá trị có thể
- Dễ đọc: Ko cần gán màu cho một số
- Tính tin cậy: 
	+ Operations
	+ Chỉ có thể gán giá trị dựa trên tập danh hiệu
	+ C++: Ko ép enum về nguyên
- Hiện thực như giá trị nguyên

# Subrange Type
- Định nghĩa ra một miền liên tục. VD: type pos = 0 .. MAXINT;
- Được đảm bảo rằng giá trị nhận được nằm trong miền quy định hay không?

# Array type
- Có cùng kiểu dữ liệu
- Rectangular (mọi ô nhớ có kích thước bằng nhau): Fortran, Ada, C#
- Jagged (Cấp phát ko đều): C, C++, Java, C#

# Slices
- Một bộ phận của array (dãy con)
VD:
vector[2,4,6,8,10,12,14,16]
vector[3:6] -> dãy con

# Hiện thực array
- Đặt phần tử của dãy lên trên vùng nhớ
- Có một hàm biến đổi chỉ số ra địa chỉ của phần tử tương ứng.

- **Dãy 1 chiều: Theo thứ tự tăng dần.**

```php
address(list[k]) = address(list[lower_bound]) + ((k - lower_bound) * element_size)
```
	
- **Dãy 2 chiều:** 
    - **Xếp theo hàng: Hầu hết ngôn ngữ**
	```php
    a[lb1..ub1, lb2..ub2]
	Location(a[i,j]) = alpha + (((i - lb1) * (ub2-lb2+1)) + (j - lb2)) * E
	```

        - alpha: địa chỉ đầu
	    - E: element size
        - n: số lượng phần tử của chiều đi sau nó.

    - Sắp xếp các phần tử của dãy: VD: 
    ```var x : array[7..9, 8..10, 4..6] of integer```
    &nbsp;
    ```Các thành viên của mảng x[a,b,c] sẽ được xếp theo thứ tự c tăng dần -> b tăng dần -> a tăng dần. Lần lượt làm vậy cho đến khi nào hết c: x[7,8,4], x[7,8,5], x[7,8,6], x[7,9,4], x[7,9,5], ...```
    &nbsp;
    + **Xếp theo cột: Fortran**
    &nbsp;

- Dãy kết hợp: Đánh chỉ số bằng key (Map trong Scala)
VD: dt = [("name","John"); ("age", "28"); ("address", "1 John st.")]

dt["name"] = "John"

# String type
- Là một chuỗi các ký tự
- Chiều dài chuỗi:
	+ Static: Lúc dịch (compile) thì chiều dài chuỗi là cố định. Compile-time descrtiptor
	
		Python, Java string class
	+ Dynamic: Chiều đài động
	
		-- Limited Dynamic: Có giới hạn. C/C++. Compile-time descrtiptor + run-time descriptor
		
		-- Dynamic: Ko có giới hạn. Run-time descriptor + linked list
	
	+ Compile-time descriptor: Static string, string length, address
	
	+ Run-time descriptor: Limited dynamic string, maximum length, current length, address
	
# Record type
- Cho phép lưu trữ nhiều thành phần khác nhau
- Truy xuất qua name
- OOP sử dụng object như record
- Format:
	+ Fully qualified references: bao gồm tất cả tên của record
	+ Elliptical references: Có thể bỏ một số nhưng ko gây nhập nhằng

- Assignment: Copy vùng nhớ này sang vùng nhớ khác. Đòi hỏi type phải giống nhau

- COBOL cung cấp MOVE CORRESPONDING. Cho phép chép 2 type khác nhau

- Dễ và an toàn

- Hiện thực Record type

Record
         Name
field 1: Type
         Offset

...

         Name
field n: Type
         Offset	 

Address

- Data alignment:
	+ b-byte aligned object có địa chỉ là bội số của b bytes
	
	+ VD:
	-- char (1 byte) là 1-byte aligned
	-- short (2 byte) là 2-byte aligned
	-- int (4 byte) là 4-byte aligned
	-- long (4 byte) là 4-byte aligned
	-- float (4 byte) là 4-byte aligned
	
	+ Padding: Có những khoảng bộ nhớ bù vô
		- Nếu sau đó là thành phần khác có alignment lớn hơn
		- Padding vào cuối struct sao cho kích thước struct là bội số của thành phần lớn nhất.
		
# Union types
- Là kiểu dc cấp các giá trị kiểu khác nhau trong thời điểm khác nhau trong quá trình thực thi

- Discriminatied: Có một thành phần trong union để ghi nhận
- Free union: Ko có type checking. Bỏ vào ở type này nhưng có thể lấy ra ở type khác

# Set types
- Biểu diễn tập hợp
- Có thể có tác vụ: membership, union, intersection, different
- Hiện thực bởi chuỗi bit hoặc bảng băm

# Pointer
- Sẽ nhận giá trị là địa chỉ của ô nhớ hoặc giá trị đặc biệt (nil).
- Truy xuất gián tiếp.
- Quản lý bộ nhớ cấp phát động.

- Assignment: lấy địa chỉ từ con trỏ này cấp cho con trỏ khác.
- Dereferencing (dấu sao *): Dựa vào con trỏ mà đến vị trí mà con trỏ trỏ đến. (nằm bên trái là vị trí mà con trỏ đó trỏ đến, nằm bên phải là giá trị (ô nhớ) mà con trỏ trỏ đến)

- Con trỏ treo (Dangling pointer): Con trỏ trỏ đến đối tượng bị huỷ rồi.

- Lost heap-dynamic variable (garbage): Đối tượng đó còn nhưng ko thể truy cập tới được nữa.

- Cực kì linh hoạt nhưng dễ lỗi
- Pointer có thể trỏ tới bất kì cùng nhớ nào
- Quản lý cấp phát động và địa chỉ

- Pointer to record:
	+ Explicit: Dùng Dereferencing (*). VD: (*p).name
	+ Implicit: p->name
	
# Reference types
- VD:
	int A;
	int &rA = A;

- Pointer tham chiếu tới địa chỉ, reference types tham chiếu

- Biểu diển pointer
	+ Giá trị đơn
	+ 2 thành phần
	
- Giải pháp tránh dangling pointer:
	+ Tombstone
	+ Locks-and-keys
	
# Recursive type
- Khi khai báo 1 kiểu, nó lại refer tới chính nó.


# Biểu thức kiểu (Type expression)
- Biểu thức kiểu (Type expression): Kết hợp nhiều phương pháp

	+ Thành phần cơ bản (scala): bool, char, int, float, void, subrange
	
	+ Một tên kiểu cũng là biểu thức kiểu
	
	+ Kết hợp thông qua phép toán kiểu (type constructor):
		- Array: array(I, T): I là index type, T là element type
		
		- Products (tích đề các): T1 x T2
		
		- Records: record((name1 x T1) x (name2 x T2) x ...)
		
		- Pointer: pointer(T)
		
		- Function: T1 -> T2
		
	+ Biến kiểu là một biểu thức kiểu (template)
	
	+ Ví dụ:
		- int => int
		
		- typedef int siso; => siso
		
		- int t[10]; => array(0..9, int)
		
		- int foo(int a, float b) => (int x float) -> int
		
		- struct int a; int b => record((a x int) x (b x int))
		
		- int *p => pointer(int)
		
		- ```template<class T>``` struct vd {T a; T b[3]} => ```record((a x T) x (b x array(0..2,T)))```
		
# Type checking
- Là một hành động để đảm bảo chương trình tôn trọng tất cả những luật liên quan tới hệ thống kiểu.

- Static time checking: Thực hiện ở thời gian dịch. Đòi hỏi ngôn ngữ phải khai báo kiểu, có những ràng buộc về kiểu mà có thể ktra được ở thời gian dịch. Trong một số ngôn ngữ kiểm tra kiểu tĩnh vẫn có một vào thao tác phải kiểm tra kiểu động.

- Dynamic time checking: Thực hiện trong thời gian thực thi (running). Vận dụng trong những ngôn ngữ dynamic time binding. Khi viết ctrình sẽ ko khai báo kiểu và một biến có thể ở dạng những kiểu khác nhau trong quá trình chạy.

# Suy diễn kiểu
- Suy diễn kiểu là khai báo ko cần khai báo đầy đủ tất cả các kiểu của các đối tượng dữ liệu mà có thể ko khai báo một số phần tử.

- Khi đã suy diễn rồi, sau đó biến dc dùng sẽ sử dụng kiểu đã được suy diễn cho phần tử đó. Không thể thay đổi kiểu của phần tử.

- Ví dụ trên Scala:
	def add(x:Int) = x + 1
	
	kiểu trả về của hàm add được suy diễn là kiểu Int
	
- Cơ chế suy diễn kiểu:

	+ Thực hiện gán kiểu cho các node lá trên AST ((x) và (1))
	
	+ Tạo ra những ràng buộc kiểu cho những node trên AST
	
	+ Giải các ràng buộc kiểu đó.
	
	+ Ví dụ: 
	def foo(x,f) = f(f(x))
	
	1. foo is a function so its type is T1->T2 where T1 is input type and T2 is output type

	2. This function has 2 parameter, so T1 = T3*T4 where T3 is the type of x (2a) and T4 is the type of f (2b)

	3. In the body of the function, there is expression f(x), so f is a function and its type is T5 -> T6 (3a) and x is passed to function f and from (2a) => T5 = T3 (3b)

	4. there is also expression f(f(x)) and (3a) => T5 = T6 (4)

	5. The result of expression is also the result of function foo and (1) and (3a) => T2 =T6 (5)

	6. From (1) and (2a) => type of foo is T3*T4 -> T2 (6)

	7. From (6) and (3a) => type of foo is (T3*(T5->T6)) -> T2 (7)

	8. From (7) and (3b), (4), (5) => type of foo is (T3*(T3->T3))->T3

	There is only one variable type in the result so we can write the type of foo is (T*(T->T))-> T
	
# Tương đương kiểu
- Kiểm tra xem một đối tượng xuất hiện ở đó có phù hợp hay không.

- Một toán hạng có một kiểu này có thể thay thế cho 1 kiểu khác mà ko cần ép kiểu

- Hai cách tiếp cận: Same type name

	+ Tương đương theo tên:
		type Celsius = Float;
		type Fahrenheit = Float;
	
	+ Tương đương cấu trúc: Cấu trúc giống nhau.
	
# Tương thích kiểu
- Kiểu T tương thích với kiểu S nếu giá trị của T được phép xuất hiện ở bất kì vị trí nào xuất hiện S. Nhưng ko có chiều ngược lại.

- T tương thích với S khi:
	
	+ T tương đương với S
	
	+ Giá trị của T là tập con của S
	
	+ Khi tất cả những tác vụ trên S thì 1 giá trị trên có thực hiện dc
	
	+ Những giá trị của T sẽ tương ứng theo 1 hình thức nào đó với giá trị của S
	
	+ Giá trị của T có thể chuyển đổi thành một số giá trị của S
	
# Type conversion
- Chuyển đổi kiểu là chuyển đổi giá trị từ kiểu này qua kiểu khác

	+ Implicit conversion - coercion
	+ Explicit conversion - cast

# Tính đa hình
- Đơn hình: Một đối tượng của ngôn ngữ chỉ có 1 kiểu

- Đa hình: Một đối tượng của ngôn ngữ có nhiều kiểu

VD: +: int x int -> int 
		float x float -> float

- Đạng da hình:
	+ Ad hoc polymorphism: Overloading
	
	+ Universal polymorphism:
		
		-- Đa hình thông số: swap(T& x, T& y)
		
		-- Đa hình kiểu con
		