# BÁO CÁO BÀI TẬP 02 - BT08: ỨNG DỤNG DU LỊCH ĐA ĐIỀU HƯỚNG (TravellingApp)

## 1. Thông tin bài nộp
* **Tên ứng dụng:** TravellingApp
* **Link ứng dụng từ Expo:** https://snack.expo.dev/@grondwalker/travellingapp

---
## 2. Liệt kê và mô tả thiết kế các file code

### 📁 Cấu trúc thư mục dự án (`TravellingApp`)
* `App.js`
* `data/destinations.js`
* `components/TravelHeader.js`
* `components/CategoryList.js`
* `components/DestinationCard.js`
* `components/FavoriteCard.js`
* `components/ProfileInfo.js`
* `screens/HomeScreen.js`
* `screens/FavoritesScreen.js`
* `screens/ProfileScreen.js`
* `screens/DestinationDetailScreen.js`
* `screens/AboutScreen.js`
* `screens/SettingsScreen.js`
* `screens/ContactScreen.js`

---

### 🧩 Mô tả thiết kế từng file

#### 1. Tệp điều phối & dữ liệu
* **`App.js`**: Điều phối toàn bộ trạng thái danh sách yêu thích (`favoriteIds`), trạng thái mở menu/màn hình phụ và kết hợp các lớp điều hướng (`Tab Navigation` cho khu vực chính, `Stack Navigation` cho màn hình chi tiết địa điểm, cùng hệ thống menu điều hướng tới các mục phụ) trên nền giao diện tối (`#0f172a`).
* **`data/destinations.js`**: Khai báo danh sách danh mục (`CATEGORIES`) và mảng dữ liệu tối thiểu 6 địa điểm du lịch (`DESTINATIONS`) gắn với bối cảnh Nha Trang & Khánh Hòa, gồm tên, danh mục, vị trí, điểm đánh giá, mức giá tham khảo, ảnh minh họa, mô tả và điểm nổi bật.

#### 2. Các Component (`components/`)
* **`components/TravelHeader.js`**: Thiết kế thanh đầu trang theo `Flexbox` ngang cho hàng trên (nút `Menu` mở ngăn kéo/mục phụ và nhãn khu vực `NHA TRANG • KHÁNH HÒA`) kết hợp tiêu đề lớn và dòng mô tả ngắn bên dưới.
* **`components/CategoryList.js`**: Thiết kế dải danh mục cuộn ngang bằng `FlatList` với các chip bo tròn; chip đang được chọn đổi sang nền xanh nổi bật (`#0284c7`) giúp người dùng nhận biết bộ lọc hiện hành.
* **`components/DestinationCard.js`**: Thiết kế thẻ địa điểm dạng card dọc có ảnh bìa bo góc trên, huy hiệu danh mục, nút tim lưu/bỏ yêu thích, tên địa điểm, vị trí, điểm đánh giá/giá ở chân thẻ và hiệu ứng nhấn (`Pressable`).
* **`components/FavoriteCard.js`**: Thiết kế thẻ gọn theo chiều ngang (`flexDirection: 'row'`) cho màn hình Yêu thích, gồm ảnh thu nhỏ bên trái, thông tin tóm tắt ở giữa và nút `Bỏ lưu` bên phải để quản lý nhanh danh sách đã lưu.
* **`components/ProfileInfo.js`**: Thiết kế khối hồ sơ cá nhân gồm thẻ đại diện có avatar chữ viết tắt, hàng 3 ô thống kê (`Địa điểm`, `Yêu thích`, `Lịch trình`) và thẻ chi tiết thông tin/sở thích khám phá.

#### 3. Các Màn hình (`screens/`)
* **`screens/HomeScreen.js`**: Thiết kế màn hình trang chủ với banner du lịch nổi bật, bộ lọc `CategoryList` và danh sách địa điểm hiển thị qua `FlatList` + `DestinationCard`; nhấn thẻ sẽ mở `DestinationDetail` kèm tham số địa điểm.
* **`screens/FavoritesScreen.js`**: Thiết kế màn hình danh sách yêu thích lọc các địa điểm đã lưu để hiển thị bằng `FlatList` + `FavoriteCard`, đồng thời có giao diện trạng thái trống thân thiện khi chưa có mục nào được lưu.
* **`screens/ProfileScreen.js`**: Thiết kế màn hình thông tin cá nhân kết hợp `TravelHeader` và `ProfileInfo`, tự động cập nhật số lượng địa điểm yêu thích theo trạng thái ứng dụng.
* **`screens/DestinationDetailScreen.js`**: Thiết kế màn hình chi tiết mở qua `Stack Navigation`, hiển thị ảnh lớn, thông tin giá/đánh giá/vị trí, đoạn mô tả, danh sách điểm nổi bật, nút thêm/bỏ yêu thích đổi màu theo trạng thái và nút quay lại.
* **`screens/AboutScreen.js`**: Thiết kế màn hình giới thiệu ứng dụng và mô tả cấu trúc điều hướng của dự án.
* **`screens/SettingsScreen.js`**: Thiết kế màn hình cài đặt dạng danh sách tùy chọn tương tác (chuyển đổi đơn vị khoảng cách và gợi ý khung giờ đẹp) cập nhật giá trị ngay khi nhấn.
* **`screens/ContactScreen.js`**: Thiết kế màn hình liên hệ trình bày thông tin phụ trách, khu vực và kênh góp ý địa điểm.

---
## 3. Ảnh chụp giao diện của các component và màn hình

## Hướng dẫn chụp ảnh sự thay đổi giao diện của các component và màn hình

> **Lưu ý khi chụp & chèn ảnh:**
> * Chạy ứng dụng **TravellingApp** trên Expo (mở preview ra tab riêng hoặc chạy trên thiết bị/mô phỏng để thao tác và cuộn mượt).
> * Chụp ảnh màn hình ở từng trạng thái thay đổi giao diện của các component và màn hình bên dưới, sau đó tải ảnh lên kho lưu trữ GitHub và chèn vào cột **Ảnh minh họa**.

| STT | Thành phần / Màn hình / Component | Trạng thái & sự thay đổi giao diện cần chụp | Ảnh minh họa |
| :-: | --- | --- | --- |
| 1 | `TravelHeader` & `HomeScreen` | Giao diện trang chủ ban đầu có banner du lịch, nút mở menu và danh sách các địa điểm. | <img width="418" height="800" alt="image" src="https://github.com/user-attachments/assets/e71429c1-774c-4a25-ad45-45a7f19ca0e7" /> |
| 2 | `CategoryList` & `DestinationCard` | Chạm vào một danh mục (ví dụ `Biển & Đảo` hoặc `Văn hóa & Di tích`) để thấy chip đổi màu active và danh sách `FlatList` lọc theo danh mục. | <img width="424" height="796" alt="image" src="https://github.com/user-attachments/assets/70530a09-52db-48a0-a9f2-d8ff7ee8d5ed" /> |
| 3 | `DestinationCard` & `FavoritesScreen` | Nhấn biểu tượng yêu thích trên thẻ địa điểm, sau đó chuyển sang tab **Yêu thích** qua **Tab Navigation** để thấy thẻ `FavoriteCard` cập nhật danh sách đã lưu. | <img width="416" height="798" alt="image" src="https://github.com/user-attachments/assets/bbb3b60a-26d2-4526-9569-2484aa4dc658" /> |
| 4 | `ProfileScreen` & `ProfileInfo` | Chuyển sang tab **Cá nhân** qua **Tab Navigation** để kiểm tra thông tin hồ sơ và số lượng địa điểm yêu thích đồng bộ trên `ProfileInfo`. | <img width="414" height="790" alt="image" src="https://github.com/user-attachments/assets/655cdc54-7967-4db0-b8e3-7b0041cf22aa" /> |
| 5 | Menu / Màn hình phụ (`Giới thiệu`, `Cài đặt`, `Liên hệ`) | Mở menu từ `TravelHeader`, vào **Cài đặt** và nhấn chuyển đổi tùy chọn để thấy giá trị hiển thị thay đổi trực tiếp; chụp thêm màn hình **Giới thiệu** / **Liên hệ**. | <img width="457" height="803" alt="image" src="https://github.com/user-attachments/assets/e9e86831-f749-4eb4-935c-0801c3afd83f" /> |
