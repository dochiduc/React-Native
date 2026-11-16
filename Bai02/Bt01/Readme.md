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

## 4. Mã nguồn các Component trong thư mục
components/Header.js
```
import React from 'react';
import { View, Text, StyleSheet } from 'react-native';

export default function Header() {
  return (
    <View>
      <View style={styles.topRow}>
        <Text style={styles.systemTag}>SYS // GARAGE-01</Text>
        <Text style={styles.statusOnline}>● ONLINE</Text>
      </View>
      <Text style={styles.title}>QUẢN LÝ BỘ SƯU TẬP SIÊU XE</Text>
      <Text style={styles.subtitle}>Khu vực: Garage VIP - Chi nhánh trung tâm</Text>
    </View>
  );
}

const styles = StyleSheet.create({
  topRow: {
    flexDirection: 'row',
    justifyContent: 'space-between',
    marginBottom: 4,
  },
  systemTag: {
    fontSize: 11,
    fontWeight: 'bold',
    color: '#f59e0b',
    letterSpacing: 1,
  },
  statusOnline: {
    fontSize: 11,
    fontWeight: 'bold',
    color: '#10b981',
  },
  title: {
    fontSize: 18,
    fontWeight: 'bold',
    color: '#f0f6fc',
    letterSpacing: 0.5,
  },
  subtitle: {
    fontSize: 12,
    color: '#8b949e',
    marginTop: 2,
  },
});
```
components/TaskItem.js
```
import React from 'react';
import { View, Text, StyleSheet } from 'react-native';

export default function TaskItem() {
  return (
    <View>
      <View style={styles.headerRow}>
        <Text style={styles.codeLabel}>[ HẠNG MỤC ƯU TIÊN ]</Text>
        <View style={styles.priorityBadge}>
          <Text style={styles.priorityText}>MỨC ĐỘ: CAO</Text>
        </View>
      </View>
      
      <Text style={styles.heading}>Kiểm tra động cơ Ferrari LaFerrari</Text>
      <Text style={styles.detail}>• Tình trạng: Cần thay dầu và kiểm tra hệ thống điện</Text>
    </View>
  );
}

const styles = StyleSheet.create({
  headerRow: {
    flexDirection: 'row',
    justifyContent: 'space-between',
    alignItems: 'center',
    marginBottom: 6,
  },
  codeLabel: {
    fontSize: 11,
    fontWeight: 'bold',
    color: '#8b949e',
  },
  priorityBadge: {
    backgroundColor: 'rgba(239, 68, 68, 0.15)',
    borderWidth: 1,
    borderColor: '#ef4444',
    paddingHorizontal: 8,
    paddingVertical: 2,
    borderRadius: 4,
  },
  priorityText: {
    fontSize: 10,
    fontWeight: 'bold',
    color: '#f87171',
  },
  heading: {
    fontSize: 15,
    fontWeight: 'bold',
    color: '#f0f6fc',
    marginBottom: 4,
  },
  detail: {
    fontSize: 13,
    color: '#c9d1d9',
    lineHeight: 18,
  },
});
```
components/TaskList.js
```
import React from 'react';
import { View, Text, StyleSheet } from 'react-native';

export default function TaskList() {
  return (
    <View>
      <Text style={styles.codeLabel}>[ DANH SÁCH XE CHỜ BẢO DƯỠNG ]</Text>
      
      <View style={styles.carRow}>
        <Text style={styles.slotNumber}>01</Text>
        <Text style={styles.carName}>Lamborghini Aventador</Text>
        <Text style={styles.carStatus}>CHỜ XỬ LÝ</Text>
      </View>

      <View style={styles.carRow}>
        <Text style={styles.slotNumber}>02</Text>
        <Text style={styles.carName}>Bugatti Chiron</Text>
        <Text style={styles.carStatus}>CHỜ XỬ LÝ</Text>
      </View>

      <View style={[styles.carRow, { borderBottomWidth: 0, paddingBottom: 0 }]}>
        <Text style={styles.slotNumber}>03</Text>
        <Text style={styles.carName}>Porsche 918 Spyder</Text>
        <Text style={styles.carStatus}>CHỜ XỬ LÝ</Text>
      </View>
    </View>
  );
}

const styles = StyleSheet.create({
  codeLabel: {
    fontSize: 11,
    fontWeight: 'bold',
    color: '#8b949e',
    marginBottom: 8,
  },
  carRow: {
    flexDirection: 'row',
    alignItems: 'center',
    paddingVertical: 8,
    borderBottomWidth: 1,
    borderBottomColor: '#21262d',
  },
  slotNumber: {
    fontSize: 12,
    fontWeight: 'bold',
    color: '#f59e0b',
    width: 26,
  },
  carName: {
    flex: 1,
    fontSize: 14,
    fontWeight: '600',
    color: '#e6edf3',
  },
  carStatus: {
    fontSize: 10,
    fontWeight: 'bold',
    color: '#8b949e',
    backgroundColor: '#21262d',
    paddingHorizontal: 6,
    paddingVertical: 2,
    borderRadius: 3,
  },
});
```
components/AddTask.js
```
import React from 'react';
import { View, Text, StyleSheet } from 'react-native';

export default function AddTask() {
  return (
    <View>
      <Text style={styles.codeLabel}>[ NHẬP DỮ LIỆU PHƯƠNG TIỆN MỚI ]</Text>
      <View style={styles.inputBox}>
        <Text style={styles.placeholder}>Nhập tên dòng xe và thông số...</Text>
      </View>
      <View style={styles.buttonMock}>
        <Text style={styles.buttonText}>+ LƯU VÀO HỆ THỐNG</Text>
      </View>
    </View>
  );
}

const styles = StyleSheet.create({
  codeLabel: {
    fontSize: 11,
    fontWeight: 'bold',
    color: '#8b949e',
    marginBottom: 8,
  },
  inputBox: {
    backgroundColor: '#090c10',
    borderWidth: 1,
    borderColor: '#30363d',
    borderRadius: 4,
    padding: 10,
    marginBottom: 10,
  },
  placeholder: {
    fontSize: 13,
    color: '#6e7681',
    fontStyle: 'italic',
  },
  buttonMock: {
    backgroundColor: '#f59e0b',
    paddingVertical: 8,
    borderRadius: 4,
    alignItems: 'center',
  },
  buttonText: {
    fontSize: 12,
    fontWeight: 'bold',
    color: '#090c10',
    letterSpacing: 0.5,
  },
});
```
components/TabBar.js
```
import React from 'react';
import { View, Text, StyleSheet } from 'react-native';

export default function TabBar() {
  return (
    <View style={styles.bar}>
      <View style={[styles.tabItem, styles.activeTab]}>
        <Text style={styles.activeText}>GARAGE</Text>
      </View>
      <View style={styles.tabItem}>
        <Text style={styles.inactiveText}>THÔNG SỐ</Text>
      </View>
      <View style={styles.tabItem}>
        <Text style={styles.inactiveText}>CÀI ĐẶT</Text>
      </View>
    </View>
  );
}

const styles = StyleSheet.create({
  bar: {
    flexDirection: 'row',
    justifyContent: 'space-between',
    gap: 8,
  },
  tabItem: {
    flex: 1,
    paddingVertical: 8,
    borderRadius: 4,
    alignItems: 'center',
    backgroundColor: '#0d1117',
    borderWidth: 1,
    borderColor: '#30363d',
  },
  activeTab: {
    backgroundColor: 'rgba(245, 158, 11, 0.15)',
    borderColor: '#f59e0b',
  },
  activeText: {
    fontSize: 12,
    fontWeight: 'bold',
    color: '#f59e0b',
  },
  inactiveText: {
    fontSize: 12,
    fontWeight: '600',
    color: '#8b949e',
  },
});
```

---
## 5. Hình ảnh minh họa giao diện (Screenshot)
<img width="328" height="669" alt="image" src="https://github.com/user-attachments/assets/8a254840-0364-44f2-8554-bd118dd3e7ee" />
