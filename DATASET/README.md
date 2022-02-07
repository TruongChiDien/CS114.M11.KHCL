## XÂY DỰNG DATASET
**Thu thập dữ liệu:**
1. Dữ liệu từ cuộc thi Datacomp do FPT tổ chức vào tháng 10/2021. Bộ dữ liệu của cuộc thi gồm 1064 ảnh được trích xuất từ camera giám sát của một công ty. Số ảnh này quá ít để huấn luyện một mô hình học sâu hiệu quả với hàng chục triệu trọng số.
2. Để mà giải quyết vấn đề thiếu dữ liệu thì chúng tôi thực hiện công việc thu thập thêm dữ liệu cho bài toán. Chúng tôi tham khảo các bài báo trên Scholar thì tìm được một số nguồn dữ liệu liên quan đến camera giám sát như WILDTRACK, BrainWash, Oxford Town Center. Và trang web EarthCam chuyên chia sẻ dữ liệu các camera giám sát được công khai tại khắp nơi trên thế giới. Sau khi duyệt qua các một số camera trên EarthCam, chúng tôi chỉ chọn được 1 camera có góc nhìn tương tự như bài toán và có thể sử dụng được. 
![image BrainWash](https://user-images.githubusercontent.com/81378994/152719845-953aedc0-233c-4579-8962-2957bef21bc0.jpg)

    Ảnh từ tập dữ liệu BrainWash gồm 219 ảnh

Sau khi quá trình tách khung hình từ video và chọn lọc thì chúng tôi thu được thêm 1152 ảnh. Cộng với dữ liệu từ cuộc thi Datacomp của FPT 1064 ảnh, nâng tổng số ảnh trong tập dữ liệu lên thành 2,216 ảnh.

**Phân bố dữ liệu:**

Sau quá trình thu thập thêm dữ liệu thì số lượng không đeo khẩu trang chỉ chưa bằng phân nửa lớp không đeo. Nguyên nhân là do dữ liệu thu thập đa số là dữ liệu có từ những năm trước đại dịch và mọi người thường không có thói quen đeo khẩu trang khi ra đường. Mặc dù vậy, dữ liệu từ quán café Miami được lấy trực tiếp trong năm 2020 – thời điểm dịch COVID – 19 đang bùng phát toàn cầu và mọi người bắt đầu mang khẩu trang khi ra đường nên chúng tôi lấy thêm được một lượng lớp có mang khẩu trang.

**Quy cách gắn nhãn:**

Chúng tôi nhận thức được sự ảnh hưởng xấu của dữ liệu không tốt lên mô hình. Cụ thể là việc gắn nhãn dữ liệu theo nhiều cách khác nhau sẽ khiến mô hình bị bối rối và học không tốt. Bên cạnh đó, chúng tôi sử dụng công cụ **labelImg** để gắn nhãn cho dữ liệu.
Quy tắc gắn nhãn của chúng tôi tuân theo bộ dữ liệu ban đầu, cụ thể là:
*   Đối với các khuôn mặt chính diện hoặc có góc nhìn của đối tượng so với camera trong khoảng [-90°; 90°], thấy rõ mặt thì sẽ được gắn nhãn từ trán xuống dưới phần cằm, bỏ phần tai.
*   Các khuôn mặt có góc nhìn nghiêng lớn hơn 90° nhưng vẫn thấy rõ được có đeo khẩu trang hay không thì vẫn được gắn nhãn từ trán xuống dưới cằm và lấy luôn phần tai.
*   Đối với các khuôn mặt bị khuất một phần nhưng vẫn nhận diện được bởi mắt người thì sẽ gắn nhãn phần không bị khuất.
*   Các khuôn mặt bị khuất quá nhiều, góc quay quá nhiều không thể nhận diện được sẽ bị bỏ qua, không gắn nhãn.
*   Những khuôn mặt nhỏ và quá mờ cũng sẽ bị bỏ qua.

## SỬ DỤNG DỮ LIỆU
