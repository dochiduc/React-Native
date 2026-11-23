# BÁO CÁO BÀI TẬP 02 - BT03: ỨNG DỤNG BÁN SÁCH LỊCH SỬ (ProductApp)

## 1. Thông tin bài nộp
* **Tên ứng dụng:** ProductApp (Chủ đề: Ứng dụng cửa hàng sách lịch sử chuyên khảo)
* **Link ứng dụng trên Expo Snack:** https://snack.expo.dev/@grondwalker/productapp
* **Học phần:** Phát triển ứng dụng di động với React Native (Bài 2: Props, FlatList & Component hóa)

---

## 2. Mô tả thiết kế và sự thay đổi giao diện
* **Kiến trúc Component:** Ứng dụng được chia tách thành component `ProductCard` độc lập chuyên trách hiển thị thông tin từng sản phẩm.
* **Truyền dữ liệu (Props):** Dữ liệu của ít nhất 6 sản phẩm sách lịch sử (gồm tên, tác giả, giá tiền, mô tả và hình ảnh) được truyền từ component gốc (`App.js`) xuống `ProductCard` thông qua cơ chế `props`.
* **Hiển thị danh sách (FlatList):** Sử dụng `FlatList` thay thế cho việc hiển thị tĩnh, giúp tối ưu hóa hiệu năng cuộn trang và tự động kết xuất danh sách sản phẩm mượt mà trên thiết bị di động.

---

## 3. Hình ảnh minh họa giao diện (Screenshot)
<img width="528" height="794" alt="image" src="https://github.com/user-attachments/assets/a60dafdb-d822-4614-b68c-2e5807d8d6e0" />

