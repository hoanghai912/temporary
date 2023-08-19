# Mã Jasmin
- Jasmin là mã assembler Java

# Java virtual machine
- JVM là stack-base machine: 	
	+ Các giá trị của phép toán dc đưa trên 1 stack 
	
	+ Lấy giá trị trong stack để tính toán.
	
	+ Truyền tham số và nhận giá trị qua stack
	
	+ Code gen trên stack-base dễ hơn so với register-base
	
- Class loader subsystem: Nạp ctrình từ các file vào các vùng:
	
	+ Method area: chứa các class data
	
	+ Heap: Chứa các object
	
	+ Java stacks: Có nhiều stack, trên các stack có những thread. Mỗi chương trình con là 1 stack frame, còn được xem là bản ghi hoạt động.
	
	+ Pc register: Trong mỗi thread sẽ có để đếm chương trình đang chạy đến dòng lệnh nào của thread đó.
	
	+ Native method stacks: Những ngôn ngữ được viết ở mã máy (Ko phải java bytecode)
	
# Data type
- Boolean: {0,1}. **Ký hiệu: Z**

- Byte: -2^7 to 2^7 - 1. **Ký hiệu: B**

- Short: -2^15 to 2^15 - 1. **Ký hiệu: S**

- Int: -2^31 to 2^31 - 1. **Ký hiệu: I**

- Long: -2^63 to 2^63 - 1. **Ký hiệu: L**

- Char: 16 bit không dấu (0 to 2^16 - 1). **Ký hiệu: C**

- Float: 32-bit IEEE. **Ký hiệu: F**

- Double: 64-bit IEEE. **Ký hiệu: D**

- returnAddress: Địa chỉ của một opcode trong method

- Class reference: **Ký hiệu: Lclass-name;**

- Interface reference: **Ký hiệu: Linter-name;**

- Array reference: **[[..[component-type**

- void: **ký hiệu: V**

- Function: 
    - Ví dụ: int foo(int a, int b) -> (II)I
    - Ví dụ: int foo(int a, float b) -> (IF)I
    - Ví dụ: int foo(VD a, float b) -> (LVD;F)I
    - Ví dụ: int foo(int a, float b[]) -> (I[F)I
    - Ví dụ: int foo(int a, float b[][], boolean c) -> (I[[FZ)I

# Operand stack
- Truy cập để push và pop giá trị

	+ Lưu trữ các toán hạng và nhận kết quả của toán tử
	
	+ Truyền tham số và nhận method trả về
	
	+ iload_1: Load giá trị từ biến số 1
	
	+ istore_1: Lưu giá trị vào biến số 1
	
	+ iconst_2: Push số 2 vào stack
	
	+ bipush 40: Push 40 vào stack
	
	+ iadd: Cộng 2 giá trị on top của stack
	
	+ imul: Nhân 2 giá trị on top của stack
	
# Dãy biến cục bộ (Local variable array)

- Cấp phát cho miền cục bộ, khai báo cho các chương trình con. Tạo ra stack frame

- Đánh chỉ số bắt đầu bằng 0

- Instance method:
	+ Slot 0 dành cho this
	+ Param được đánh từ 1
	
- Class method (static):
	+ Param bắt đầu từ 0
	
- 1 slot được cấp cho boolean, byte, short, int, float, reference và returnAddress

- 2 slot được cấp cho long và double

# Instructions
- Arithmetic Instructions
	
	+ Add: iadd, ladd, fadd, dadd
	+ Subtract: isub, ...
	+ Multiply: imul, ...
	+ Divide: idiv, ...
	+ Remainder: irem, ...
	+ Negate: ineg, ...
	+ Shift: ishl, ishr, ...
	+ Bitwise OR: ior, lor
	+ Bitwise AND: iand, land
	+ Bitwise exclusive OR: ixor, lxor
	+ Local variable increment: iinc
	+ Comparision: dcmpg, dcmpl, fcmpg, fcmpl, lcmp
	
- Load và store:

	+ iload, iload_<n>: n=0..3
	+ Taload: Đọc phần tử của một dãy
	
	+ bipush: -2^7 to 2^7 - 1
	+ sipush: -2^15 to 2^15 - 1
	
	+ ldc: long, float hoặc string
	+ ldc_w, ldc2_w: long hoặc double
	
	+ aconst_null: null
	+ iconst_m1: -1
	+ iconst_\<i>: từ 0..5

- Control transfer instructions:
	+ Ko điều kiện: goto, goto_w, jsr, jsr_w, ret

	+ Có điều kiện:
	
		- ifeq, iflt, ifle, ifne, ifgt, ifge: So sánh với 0
		
		- ifnull, ifnonnull: So sánh với null
		
		- if_icmpeq, if_icmpne, if_icmplt, if_icmpgt, if_icmple, if_icmpge : So sánh 2 số
		
		- if_acmpeq, if_acmpne: So sánh 2 reference
		
- Object creation and Manipulation

	+ Tạo một class instance: new
	
	+ Tạo một array: newarray, anewarray, multianewarray
	
	+ Access field: getfield, putfield, getstatic, putstatic
	
- Return:
	+ return: void
	+ ireturn: int, short, char, boolean, byte
	+ ...
	
- Java Directives:
	+ .source source.java
	+ .class current class
	+ .super super class
	+ .limit
	+ .method method description
	+ .field field description
	+ .end
	+ .var var description
	+ .line line number in source code
	
# Code generation Design

- Machine-Dependent code generation: Phụ thuộc vào máy mà mình sẽ sinh ra. Chỉ thay đổi khối này khi muốn đổi mã.

	+ Mỗi phương thức ứng với lệnh của Jasmin

- Intermediate code genteration: Vừa phụ thuộc mã nguồn, vừa phụ thuộc mã máy. Giúp sinh mã dễ hơn

	+ Lựa instructions
	+ Lựa data objects
	+ Giả lập việc thực thi của máy
	
	+ emitVAR(self, index, varName, inType, fromLabel, to Label): Khai báo biến
	
	+ emitATTRIBUTE(self, lexeme, inType, isFinal, value = None): Dùng để khai báo field
	
	+ emitMETHOD(self, lexeme, inType, isStatic): Khai báo method
	
	+ emitENDMETHOD(self, frame): Kết thúc method
	
	+ emitPROLOG(self, name, parent): Dùng để dùng đầu tiên khi bắt đầu sinh mã
	
	+ emitEPILOG(self): Khi kết thúc tất cả việc sinh mã. Đẩy xuống file
	
	+ Các type truyền vào:
	
		- IntType
		- FloatType
		- StringType
		- VoidType
		- BoolType
		- ClassType(Type) #cname:str
		- ArrayType(Type) #eleType:Type, dimen:List[int]
		- MType(Type) #partype:List[Type], rettype:Type
		
	+ emitADDOP(self, lexeme, inType, frame) => iadd, fadd, isub, fsub
	
	+ emitMULOP(self, lexeme, inType, frame) => imul, fmul, idiv, fdiv
	
	+ emitDIV(self, frame) => idev
	
	+ emitMOD(self, frame) => irem
	
	+ emitANDOP(self, frame) => iand
	
	+ emitOROP(self, frame) => ior
	
	+ emitREOP(self, op, inType, frame) => code for >, <, >=, <=, !=, ==
	
	+ emitRELOP(self, op, inType, trueLabel, falseLabel, frame) => code for condition in if statement
	
	+ emitREADVAR(self, name, inType, index, frame) => [ifa]load
	
	+ emitALOAD(self, inType, frame) => [ifa]aload
	
	+ emitWRITEVAR
	+ emitASTORE
	+ emitGETSTATIC
	+ emitGETFIELD
	+ emitPUTSTATIC
	+ emitPUTFIELD
	
	+ emitPUSHICONST(self, input, frame) => iconst, bipush, sipush, ldc
	
	+ emitPUSHFCONST
	
	+ emitINVOKESTATIC(self, lexeme, inType, frame)
	
	+ emitINVOKESPECIAL(self, frame, lexeme=None, inType=None)
	
	+ emitINVIKEVIRTUAL
	
	+ emitIFTRUE(self, label, frame) => ifgt
	
	+ emitIFFALSE => ifle
	
	+ emitDUP => dup
	+ emitPOP => pop
	+ emitI2F => i2f
	+ emitRETURN => return, ireturn
	+ emitLABEL => Label
	
	+emitGOTO(self, label, frame) => goto

- Frame: Khi sinh mã, có nhiều thành phần phụ thuộc vào method, khi sinh mã cho một mã khác phải có những nhóm thành phần khác. Quản lý tập các biến cục bộ cho từng hàm.

	+ Label: Chỉ hợp lệ trong thân của method
		-- getNewLabel(): return a new label
		
		-- getStartLabel(): return the beginning label of scope
		
		-- getEndLabel()
		
		-- getContinueLabel(): trả về 1 label mà lệnh continue sẽ nhảy đến
		
		-- getBreakLabel()
		
		-- enterScope()
		-- exitScope()
		
		-- enterLoop()
		-- exitLoop()
		
	+ Local variable array
		-- getNewIndex: trả về index cho 1 var
		
		-- getMaxIndex: trả về size of local variable array
	
	+ Operand stack
		-- push()
		-- pop()
		
		-- getMaxOpStackSize(): return max size

- Machine-Independent code generation: Mã Jasmin

	+ Dựa vào ngôn ngữ đang làm
	+ Dùng những method được cung cấp trong Frame và Intermediate code gen (emitter)