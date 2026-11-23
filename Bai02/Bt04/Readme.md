# 📱 MultiScreenApp - React Native Navigation

Bài tập **Bt04** - Môn Lập trình Di động với React Native.

## 🔗 Liên kết ứng dụng
* **Expo Snack Link:** https://snack.expo.dev/@grondwalker/multiscreenapp

---

## 🛠️ Cấu trúc và Thành phần Ứng dụng

Ứng dụng được thiết kế gồm **3 màn hình chính** theo yêu cầu đề bài, kết hợp thêm Tab Navigation nâng cao, theo chủ đề **Đại dương và Sinh học biển**:

1. **`HomeScreen`:** Màn hình trang chủ chào mừng theo chủ đề đại dương, giới thiệu phân tầng độ sâu đại dương, sinh vật tiêu biểu và điều hướng sang danh mục sinh vật biển.
2. **`ListScreen`:** Màn hình danh sách sinh vật biển sử dụng `FlatList` kèm bộ lọc theo tầng sinh thái, cho phép chọn từng sinh vật để xem hồ sơ chi tiết.
3. **`DetailScreen`:** Màn hình chi tiết sinh vật biển nhận tham số `item` qua `route.params` (hiển thị tên khoa học, độ sâu, kích thước, nguồn thức ăn, đặc điểm sinh học, cơ chế thích nghi) và có nút quay lại (`navigation.goBack()`).
4. **`ProfileScreen`:** Màn hình cá nhân (Tab Navigation bổ sung cho sinh viên khá) hiển thị hồ sơ nghiên cứu biển, thống kê mẫu vật/tầng khảo sát và thông tin bài thực hành.
---

## Hình ảnh giao diện (UI Screenshots)

* Màn hình Trang chủ (Home)
<img width="432" height="795" alt="image" src="https://github.com/user-attachments/assets/31c6ce00-6782-4e48-bf76-bcc4065b6265" />

* Màn hình Danh sách (List)
<img width="434" height="795" alt="image" src="https://github.com/user-attachments/assets/225a6e30-7e3e-4b05-9b26-94022c609aa7" />

* Màn hình Chi tiết (Detail)
<img width="428" height="797" alt="image" src="https://github.com/user-attachments/assets/99a5c89e-7c63-4b74-8fa4-8815d4a52da6" />

* Màn hình Cá nhân (Profile)
<img width="431" height="797" alt="image" src="https://github.com/user-attachments/assets/844a36e5-4ee2-42c9-8f5f-61743abfd22e" />
