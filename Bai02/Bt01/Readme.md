# BÁO CÁO BÀI TẬP 02 - BT01: ỨNG DỤNG QUẢN LÝ SIÊU XE (MyApp_V2)

## 1. Thông tin bài nộp
* **Tên ứng dụng:** MyApp_V2 (Chủ đề: Quản lý Bộ sưu tập Siêu xe & Bảo dưỡng Garage)
* **Link ứng dụng trên Expo Snack:** https://snack.expo.dev/@grondwalker/myapp_v2
* **Học phần:** Phát triển ứng dụng di động với React Native

---

## 2. Mô tả sự thay đổi giao diện (So với Bài 01)
* **Bài 01:** Khung giao diện thô sơ, tối giản hoàn toàn, chỉ sử dụng các thẻ `<View>` và `<Text>` cơ bản để phân rã component (`Header`, `TaskItem`, `TaskList`, `AddTask`, `TabBar`) mà chưa có định dạng kiểu dáng (StyleSheet).
* **Bài 02 (MyApp_V2):** 
  * Áp dụng mô hình **Flexbox** và **StyleSheet** để tái thiết kế giao diện mang phong cách **cơ khí / kỹ thuật (Mechanical HUD & Carbon Telemetry)** hiện đại, mạnh mẽ.
  * Tối ưu hóa hiển thị trên thiết bị di động thực tế: Xử lý vùng an toàn tránh camera nốt ruồi ở phần `Header` và nâng thanh điều hướng `TabBar` lên để không bị đè bởi phím ảo hệ điều hành Android.

---

## 3. Cấu trúc Component & Mã nguồn

### 📁 Tệp gốc `App.js`
```javascript
import React from 'react';
import { StyleSheet, View, ScrollView, Platform, StatusBar } from 'react-native';

import Header from './components/Header';
import TaskItem from './components/TaskItem';
import TaskList from './components/TaskList';
import AddTask from './components/AddTask';
import TabBar from './components/TabBar';

export default function App() {
  return (
    <View style={styles.screen}>
      {/* Thanh trạng thái chữ sáng trên nền tối */}
      <StatusBar barStyle="light-content" backgroundColor="#090c10" />

      {/* Khu vực Header tự động tránh camera nốt ruồi */}
      <View style={styles.headerContainer}>
        <Header />
      </View>

      {/* Khu vực nội dung cuộn mượt mà */}
      <ScrollView 
        style={styles.body} 
        contentContainerStyle={styles.bodyContent}
        showsVerticalScrollIndicator={false}
      >
        <View style={styles.moduleCard}>
          <TaskItem />
        </View>

        <View style={styles.moduleCard}>
          <TaskList />
        </View>

        <View style={styles.moduleCard}>
          <AddTask />
        </View>
      </ScrollView>

      {/* Thanh điều hướng đáy tránh đè phím ảo Android */}
      <View style={styles.footerContainer}>
        <TabBar />
      </View>
    </View>
  );
}

const styles = StyleSheet.create({
  screen: {
    flex: 1,
    backgroundColor: '#0d1117', // Nền thép tối công nghiệp
  },
  headerContainer: {
    backgroundColor: '#161b22',
    paddingTop: Platform.OS === 'android' ? (StatusBar.currentHeight || 24) + 12 : 50,
    paddingBottom: 14,
    paddingHorizontal: 16,
    borderBottomWidth: 2,
    borderBottomColor: '#f59e0b', // Đường viền hổ phách kỹ thuật
  },
  body: {
    flex: 1,
  },
  bodyContent: {
    padding: 16,
    paddingBottom: 24,
  },
  moduleCard: {
    backgroundColor: '#161b22',
    borderWidth: 1,
    borderColor: '#30363d',
    borderLeftWidth: 4,
    borderLeftColor: '#f59e0b', // Gờ kim loại bên trái
    borderRadius: 6, // Bo góc sắc cạnh cơ khí
    padding: 14,
    marginBottom: 14,
  },
  footerContainer: {
    backgroundColor: '#161b22',
    borderTopWidth: 1,
    borderTopColor: '#30363d',
    paddingTop: 12,
    paddingBottom: Platform.OS === 'android' ? 42 : 24, // Đẩy cao tránh thanh điều hướng Android
    paddingHorizontal: 16,
  },
});
```

---

## 4. Hình ảnh minh họa giao diện (Screenshot)
<img width="328" height="669" alt="image" src="https://github.com/user-attachments/assets/8a254840-0364-44f2-8554-bd118dd3e7ee" />
