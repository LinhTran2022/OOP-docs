# **SFML & Game theory**

## **1. SFML** (Simple and Fast Multimedia Library)

Là một thư viện đa phương tiện viết từ C++, gồm 5 modules : Audio, Graphics,  Network, System, Window

- System: gồm các class liên quan với hệ thống như làm thời gian, xử lí unicode 
- Window: liên quan tới việc tạo, đóng và xử lí sự kiện cửa số
- Graphics: bao gồm các class về việc render đồ họa 
- Audio: bao gồm các class về xử lí âm thanh

## **2. Lý thuyết game**

### ***Game 2D***

- Game 2D là game không thể xoay góc quay và không có ấn tượng ba chiều rõ rệt. Game này cuộn bản đồ theo hai chiều là ngang và thẳng
- Đồ họa hai chiều có ít hoặc không có sự tham gia của các hiệu ứng ba chiều đặc trưng như ánh sáng, đổ bóng hay phản chiếu


### ***Một số thể loại game***

- Game nhập vai : người chơi nhập vai vào một nhân vật và kiểm soát nhiều hành động của nhân vật đó
- Game chiến thuật : người chơi được toàn quyền kiểm soát cả một đế chế, không chỉ tham gia vào các trận chiến mà còn quản lý kinh tế, giao thương, quân sự, … của đế chế mà mình sở hữu
- Game thể thao : gắn với một môn thể thao cụ thể nào đó có ngoài đời sống. Người chơi sẽ trở thành một vận động viên hoặc một người quản lý 1 nhóm vận động viên

### ***Game loop***

![MarineGEO circle logo](https://gameprogrammingpatterns.com/images/game-loop-simple.png "MarineGEO logo")

Một vòng lặp game sẽ chạy một cách liên tục trong suốt phần chơi. Mỗi lượt của vòng lặp, nó sẽ xử lý đầu vào người chơi mà không dừng việc nghe các dữ liệu đầu vào tiếp theo, cập nhật lại trạng thái trò chơi và xuất đồ họa của trò chơi.

### ***Delta time***

Delta time là thời gian cần để hiển thị khung hình

### ***Sprite & Texture***

**1. Sprite**

![MarineGEO circle logo](https://image.shutterstock.com/image-vector/different-colors-cats-pixel-art-260nw-2135690409.jpg "MarineGEO logo")


- Sprite là các đối tượng đồ hoạ 2D sử dụng cho các nhân vật , đạo cụ, đạn, và các thành phần khác của một trò chơi 2D
- Lớp Sprite chủ yếu xác định các thành phần của hình ảnh nên sử dụng cho một hình ảnh cụ thể
- 2 loại Sprite là single Sprite và multiple Sprite 
-Single sprite : Muốn sử dụng trọn vẹn nội dung của bức ảnh cho một đối tượng game . - Multiple sprite : Khi file ảnh chứa nhiều hình ảnh và mỗi hình ảnh dùng cho một đối tượng 
- Ví dụ như một file ảnh chứa các bộ phận tay, chân, đầu … của một nhân vật game hoặc file ảnh chứa các ảnh của một animation – hình ảnh động thì thường chọn là multiple sprite .

**2. Texture**

Texture trong game là một tấm ảnh hai chiều, chứa thông tin màu sắc cho một đối tượng Sprite. Có thể được hiểu là Texture được ánh xạ lên bề mặt của Sprite.

### ***Animation***

![MarineGEO circle logo](https://thumbs.dreamstime.com/b/game-sprite-actions-walking-illustration-game-sprite-actions-walking-124391223.jpg "MarineGEO logo")


Animation trong game 2D là việc vẽ lần lượt các ảnh trong một chuỗi ảnh của một hoặc nhiều đối tượng theo một đơn vị thời gian. Mỗi animation hoặc nhiều animation có thể đại diện cho một hành động, ứng xử cụ thể của nhân vật.


