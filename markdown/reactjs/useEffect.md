# Các cách sử dụng useEffect()

- useEffect sẽ gọi hàm ```callback``` ==mỗi khi== component chứa nó được ```mounted```

- Hàm ```callback``` được ==gọi sau khi== component được thêm vào DOM (sau khi render component ra UI rồi mới tiến hành chạy hàm ```callback``` trong useEffect)

- **Ứng dụng**: Sử dụng useEffect để chạy ```callback``` khi xử lý logic sau khi component render, tránh việc xử lý logic lâu sẽ làm chậm trễ việc render UI.

## 1. useEffect(callback) (ít xài)
- Hàm ```callback``` được gọi lại sau ==mỗi lần component re-render== (component re-render khi ```state``` thay đổi)

## 2. useEffect(callback, [])
- Chỉ gọi hàm ```callback``` ==một lần sau khi== component được ```mounted```

- **Ứng dụng**: Tránh việc gọi và lặp vô tận đối với trường hợp chỉ truyền ```callback```

## 3. useEffect(callback, [deps])
- Hàm ```callback``` được gọi lại ==mỗi khi ```deps``` thay đổi==

- **Ứng dụng**: Muốn gọi hàm ```callback``` để call API hoặc thay đổi dữ liệu mỗi khi thay đổi giá trị của ```deps``` (Không thay đổi ```deps``` thì không gọi ```callback```)

## 4. Cleanup Functions
- Cleanup functions luôn được ==gọi trước khi== component được ```unmount```

- Cleanup functions luôn được ==gọi trước khi== ```callback``` được gọi (trừ lần ```mounted```)

- **Ứng dụng**: Dùng để ```removeEnventListener``` cho DOM event sau khi đã unmount ```component```, tránh bị memory leaks.

- **Cách sử dụng**: Trong hàm ```callback``` của ```useEffect```, return về một hàm callback khác, hàm này gọi là Cleanup function.

## 5. useLayoutEffect()
- Gọi ```callback``` rồi mới render UI
- **Ứng dụng**: Xử lý trường hợp khi có thay đổi UI trong khi gọi ```useEffect``` gặp trường hợp bị nhấp nháy. Có thể dùng ```useLayoutEffect``` để thay thế (có thể được hoặc không?)