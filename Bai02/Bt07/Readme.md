# BÁO CÁO BÀI TẬP 02 - BT07: ỨNG DỤNG ĐẶT LỊCH DỊCH VỤ (BookingApp)

## 1. Thông tin bài nộp
* **Tên ứng dụng:** BookingApp (Chủ đề: Đặt lịch bảo trì, sửa chữa & thu mua linh kiện máy tính / điện tử tại Nha Trang)
* **Link ứng dụng từ Expo Snack:** https://snack.expo.dev/@grondwalker/bookingapp

---

## 2. Mô tả quy trình & sự thay đổi giao diện giữa các màn hình và component

* **Điều hướng nhiều màn hình (`Stack Navigation`):** Kết nối 4 màn hình `Home`, `ServiceDetail`, `Booking` và `Confirmation` bằng `@react-navigation/stack`, truyền dữ liệu dịch vụ và lịch hẹn qua `route.params`.
* **Màn hình trang chủ (`HomeScreen` + `ServiceCard`):** Hiển thị banner chủ đề kỹ thuật tại Nha Trang cùng danh sách dịch vụ (tên, hình ảnh, thời lượng, giá). Khi nhấn vào một thẻ `ServiceCard`, giao diện chuyển sang `ServiceDetailScreen` mang theo object `service`.
* **Màn hình chi tiết (`ServiceDetailScreen`):** Hiển thị ảnh lớn, mô tả chi tiết và các hạng mục thực hiện của dịch vụ đã chọn; có nút nhấn sang `BookingScreen` hoặc quay lại danh sách.
* **Màn hình đặt lịch (`BookingScreen` + `DateSelector` + `TimeSlot`):** Người dùng nhập tên khách hàng bằng `TextInput`, chọn ngày qua `DateSelector`, chọn khung giờ qua `TimeSlot` và nhập ghi chú. Các nút chọn ngày/giờ đổi màu trạng thái (`selected`) ngay khi nhấn (`Pressable`). Khi nhấn **Xác nhận**, dữ liệu được kiểm tra và chuyển sang `ConfirmationScreen`.
* **Màn hình xác nhận (`ConfirmationScreen` + `BookingSummary`):** Hiển thị mã lịch hẹn cùng toàn bộ thông tin đã đặt qua `BookingSummary`. Hỗ trợ nhấn **Thay đổi lịch hẹn** để quay lại `BookingScreen` kèm giữ nguyên thông tin trước đó để chỉnh sửa, hoặc nhấn **Quay lại** / **Về màn hình trang chủ**.

---

## 3. Hình ảnh giao diện bài tập:
* Giao diện trang chủ dịch vụ:
<img width="433" height="796" alt="image" src="https://github.com/user-attachments/assets/bfc260a8-60e7-44e9-beeb-07ca8c309d48" />

* Giao diện chi tiết dịch vụ:
<img width="433" height="794" alt="image" src="https://github.com/user-attachments/assets/7296a946-641a-44d2-8294-6380989fd885" />

* Giao diện đặt lịch hẹn:
<img width="424" height="799" alt="image" src="https://github.com/user-attachments/assets/923b1d59-3fe3-49c0-b875-4cbbfbc254f1" />

* Giao diện xác nhận đã đặt lịch:
<img width="438" height="797" alt="image" src="https://github.com/user-attachments/assets/acb14a7a-13a4-43df-ac72-b202289e3e47" />
