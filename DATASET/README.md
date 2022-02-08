## XÂY DỰNG DATASET
**Thu thập dữ liệu:**
1. Dữ liệu từ cuộc thi Datacomp do FPT tổ chức vào tháng 10/2021. Bộ dữ liệu của cuộc thi gồm 1064 ảnh được trích xuất từ camera giám sát của một công ty. Số ảnh này quá ít để huấn luyện một mô hình học sâu hiệu quả với hàng chục triệu trọng số.
2. Để mà giải quyết vấn đề thiếu dữ liệu thì chúng tôi thực hiện công việc thu thập thêm dữ liệu cho bài toán. Chúng tôi tham khảo các bài báo trên Scholar thì tìm được một số nguồn dữ liệu liên quan đến camera giám sát như WILDTRACK, BrainWash, Oxford Town Center. Và trang web EarthCam chuyên chia sẻ dữ liệu các camera giám sát được công khai tại khắp nơi trên thế giới. Sau khi duyệt qua các một số camera trên EarthCam, chúng tôi chỉ chọn được 1 camera có góc nhìn tương tự như bài toán và có thể sử dụng được.  

Ảnh từ tập dữ liệu BrainWash gồm 219 ảnh  
![image BrainWash](https://user-images.githubusercontent.com/81378994/152719845-953aedc0-233c-4579-8962-2957bef21bc0.jpg)

Ảnh từ tập dữ liệu WILDTRACK gồm 572 ảnh

![image WILDTRACK](https://user-images.githubusercontent.com/81378994/152720269-7abf8716-425a-43eb-9dda-c910c3a496a5.jpg)

Ảnh từ quán café Miami trên trang EarthCam gồm 265 ảnh
![cafe Miami](https://user-images.githubusercontent.com/81378994/152720433-f5005fd5-4d23-4a07-8f88-d501fd483f22.jpg)

Ảnh từ bộ dữ liệu Oxford Town Center gồm 96 ảnh

![image Oxford Town Center](https://user-images.githubusercontent.com/81378994/152720405-b484657a-5888-43fc-9967-66a1b049b82d.jpg)


Sau khi quá trình tách khung hình từ video và chọn lọc thì chúng tôi thu được thêm 1152 ảnh. Cộng với dữ liệu từ cuộc thi Datacomp của FPT 1064 ảnh, nâng tổng số ảnh trong tập dữ liệu lên thành 2,216 ảnh.

**Phân bố dữ liệu:**

![pbdl](https://user-images.githubusercontent.com/81378994/152720886-9ff75323-80db-4816-9cbe-6cb608e80a8d.png)

Sau quá trình thu thập thêm dữ liệu thì số lượng không đeo khẩu trang chỉ chưa bằng phân nửa lớp không đeo. Nguyên nhân là do dữ liệu thu thập đa số là dữ liệu có từ những năm trước đại dịch và mọi người thường không có thói quen đeo khẩu trang khi ra đường. Mặc dù vậy, dữ liệu từ quán café Miami được lấy trực tiếp trong năm 2020 – thời điểm dịch COVID – 19 đang bùng phát toàn cầu và mọi người bắt đầu mang khẩu trang khi ra đường nên chúng tôi lấy thêm được một lượng lớp có mang khẩu trang.

**Quy cách gắn nhãn:**

Chúng tôi nhận thức được sự ảnh hưởng xấu của dữ liệu không tốt lên mô hình. Cụ thể là việc gắn nhãn dữ liệu theo nhiều cách khác nhau sẽ khiến mô hình bị bối rối và học không tốt. Bên cạnh đó, chúng tôi sử dụng công cụ **labelImg** để gắn nhãn cho dữ liệu.
Quy tắc gắn nhãn của chúng tôi tuân theo bộ dữ liệu ban đầu, cụ thể là:
*   Đối với các khuôn mặt chính diện hoặc có góc nhìn của đối tượng so với camera trong khoảng [-90°; 90°], thấy rõ mặt thì sẽ được gắn nhãn từ trán xuống dưới phần cằm, bỏ phần tai.
*   Các khuôn mặt có góc nhìn nghiêng lớn hơn 90° nhưng vẫn thấy rõ được có đeo khẩu trang hay không thì vẫn được gắn nhãn từ trán xuống dưới cằm và lấy luôn phần tai.
*   Đối với các khuôn mặt bị khuất một phần nhưng vẫn nhận diện được bởi mắt người thì sẽ gắn nhãn phần không bị khuất.
*   Các khuôn mặt bị khuất quá nhiều, góc quay quá nhiều không thể nhận diện được sẽ bị bỏ qua, không gắn nhãn.
*   Những khuôn mặt nhỏ và quá mờ cũng sẽ bị bỏ qua.

![label img](https://user-images.githubusercontent.com/81378994/152721120-c34590e1-ac19-4a12-aedb-6fead78621f3.png)
![label2 img](https://user-images.githubusercontent.com/81378994/152721127-a957d963-bdec-4dac-87cd-c64ec1a3371d.png)


## SỬ DỤNG DỮ LIỆU

Bộ dữ liệu bao gồm 2.216 ảnh, được chia theo tỉ lệ train:val:test là 8:1:1. Phân bố dữ liệu train gồm 2758 lớp No mask và 1261 lớp Mask, Val gồm 367 lớp No mask và 123 lớp Mask, Test gồm 376 lớp No mask và 164 Mask.

![pbdl chia](https://user-images.githubusercontent.com/81378994/152721770-3f0f6d02-7207-460c-814e-4ac7db30e4d9.png)

![object in img](https://user-images.githubusercontent.com/81378994/152722048-6ef29868-2203-4e9d-b8d3-220dde8f09cb.png)

Phân bố đối tượng trong khung hình

![ti le bb](https://user-images.githubusercontent.com/81378994/152721923-8e2a2262-3b4a-467d-87e9-79729ee3f864.png)

Phân bố tỉ lệ Bouding Box

Sau khi thực hiện huấn luyện với mô hình YOLOv5 với 2.216 ảnh thì cho ra kết quả mAP@0.5 = 0.899 và mAP@0.5:0.95 = 0.535. Tuy nhiên sau sự góp ý của giáo viên hướng dẫn, chúng tôi nhận ra rằng bối cảnh của tập dữ liệu Oxford Town Center chưa được phù hợp với phần dữ liệu còn lại và kết quả khả thi hơn khi mAP@0.5 = 0.918 và mAP@0.5:0.95 = 0.547.


