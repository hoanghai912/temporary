# Các cách sử dụng useState()

```javascript
const [counter, setCounter] = userState(<init_value>)
```

- Khi hàm setCounter() được gọi sẽ thay đổi giá trị cho biến counter

    - VD: Thay đổi giá trị cho biến thành ```counter+ 1```
        ```javascript
        setCounter(counter + 1)
        ``` 

- Nếu muốn thay đổi giá trị cho biến ```counter``` nhiều lần trong 1 hàm, nên sử dụng hàm ```setCounter()``` ở dạng truyền callback

    - VD: 
    ```javascript
        setCounter(function(prevState) {
            return prevState + 1
        })
    ```
    hoặc sử dụng Arrow Function cho gọn

    ```javascript
        setCounter(prevState => prevState + 1)
    ```

    - Trong đó ```prevState``` sẽ giữ giá trị của ```counter``` trong state trước đó. (có thể đổi tên của ```prevState``` thành bất cứ gì)

    - **Ứng dụng**: Nếu muốn tăng ```counter``` lên 3 lần 
        - Code như này sẽ không chạy được. ```counter``` sẽ chỉ được cộng 1.
        ```javascript
            setCounter(counter + 1)
            setCounter(counter + 1)
            setCounter(counter + 1)
        ```

        - Code này sẽ cập nhật giá trị của ```counter``` lên 3.
        ```javascript
            setCounter(prevCounter => prevCounter + 1)
            setCounter(prevCounter => prevCounter + 1)
            setCounter(prevCounter => prevCounter + 1)
        ```
