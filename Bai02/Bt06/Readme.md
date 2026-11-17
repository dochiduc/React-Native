# BÁO CÁO BÀI TẬP 02 - BT06: ỨNG DỤNG LỊCH HỌC CÁ NHÂN (ScheduleApp)

## 1. Thông tin bài nộp
* **Tên ứng dụng:** ScheduleApp (Chủ đề: Giao diện Lịch học cá nhân theo tuần)
* **Link ứng dụng trên Expo Snack:** https://snack.expo.dev/@grondwalker/scheduleapp
* **Học phần:** Phát triển ứng dụng di động với React Native (Bài 2: Layout, Danh sách linh hoạt & Quản lý State)

---

## 2. Mô tả thiết kế và sự thay đổi giao diện
* **Thiết kế Header:** Hiển thị tên ứng dụng rõ ràng kết hợp thông tin cá nhân hóa của sinh viên và đơn vị trường học.
* **Thanh chọn 7 ngày (Horizontal Strip):** Cho phép người dùng trượt ngang và chọn nhanh các ngày trong tuần từ Thứ 2 đến Chủ Nhật.
* **Phân biệt màu sắc môn học:** Mỗi môn học được định nghĩa một dải màu riêng biệt (`color`) giúp người dùng dễ dàng nhận diện trực quan.
* **Thay đổi trạng thái linh hoạt:** 
  * Khi chọn ngày có lịch học, danh sách môn học tự động lọc và hiển thị thông qua `FlatList`.
  * Khi chọn ngày không có lịch học, giao diện tự động chuyển sang trạng thái thông báo trống (`Empty State`) thân thiện.
