# BÁO CÁO BÀI TẬP 02 - BT02: ỨNG DỤNG QUẢN LÝ HỌC TẬP (LearningApp)

## 1. Thông tin bài nộp
* **Tên ứng dụng:** LearningApp (Chủ đề: Giao diện Trang chủ Quản lý Học tập)
* **Link ứng dụng trên Expo Snack:** https://snack.expo.dev/@grondwalker/learningapp?platform=web
* **Học phần:** Phát triển ứng dụng di động với React Native (Bài 2: Flexbox, Layout & Component)

---

## 2. Mô tả thiết kế giao diện
Ứng dụng được xây dựng theo mô hình phân rã thành các component độc lập nhằm tối ưu hóa tính tái sử dụng và quản lý mã nguồn:
* **`App.js`**: Component gốc, quản lý bố cục tổng thể của trang Home, tích hợp thanh trạng thái (`StatusBar`) và khung cuộn (`ScrollView`).
* **`Header.js`**: Hiển thị lời chào cá nhân hóa, thông tin sinh viên và trường đại học.
* **`StatCard.js`**: Khối thống kê tổng quan (số môn đang học, hoàn thành, tiến độ trung bình) với hiệu ứng nổi đè lên Header.
* **`CourseCard.js`**: Thẻ hiển thị thông tin chi tiết từng môn học (mã môn, tên môn, giảng viên, phần trăm tiến độ).
* **`BottomMenu.js`**: Thanh điều hướng giả lập ở khu vực đáy màn hình giúp chuyển đổi giữa các tab chức năng.

---

## 3. Hình ảnh minh họa giao diện (Screenshot)
<img width="413" height="791" alt="image" src="https://github.com/user-attachments/assets/3c8c8dfd-1b4c-49c9-a90c-b676f035a97d" />

