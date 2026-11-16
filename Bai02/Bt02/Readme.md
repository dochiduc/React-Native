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

## 3. Mã nguồn chi tiết các thành phần

### 📁 Tệp gốc `App.js`
```javascript
import React from 'react';
import { StyleSheet, View, ScrollView, SafeAreaView, StatusBar, Text } from 'react-native';

import Header from './components/Header';
import StatCard from './components/StatCard';
import CourseCard from './components/CourseCard';
import BottomMenu from './components/BottomMenu';

export default function App() {
  return (
    <SafeAreaView style={styles.container}>
      <StatusBar barStyle="light-content" backgroundColor="#1e293b" />
      
      {/* 1. Thanh tiêu đề và thông tin sinh viên */}
      <Header />

      {/* 2. Thẻ thống kê khóa học */}
      <StatCard />

      {/* Nội dung danh sách môn học cuộn được */}
      <ScrollView style={styles.scrollContainer} showsVerticalScrollIndicator={false}>
        <Text style={styles.sectionTitle}>Môn học đang theo đuổi</Text>
        
        <CourseCard 
          code="RN-301" 
          title="Lập trình React Native nâng cao" 
          progress="75%" 
          teacher="Thầy Cô Ngành CNTT" 
        />
        <CourseCard 
          code="NET-402" 
          title="Phát triển Web với ASP.NET Core MVC" 
          progress="90%" 
          teacher="Bộ môn Công nghệ phần mềm" 
        />
        <CourseCard 
          code="DB-202" 
          title="Quản trị cơ sở dữ liệu SQL Server" 
          progress="60%" 
          teacher="Ngành CNTT - Trường Cao đẳng Kỹ thuật Công Nghệ Nha Trang" 
        />
      </ScrollView>

      {/* 4. Thanh menu giả lập ở cuối màn hình */}
      <BottomMenu />
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#f8fafc',
  },
  scrollContainer: {
    flex: 1,
    paddingHorizontal: 16,
    marginTop: 16,
  },
  sectionTitle: {
    fontSize: 16,
    fontWeight: 'bold',
    color: '#1e293b',
    marginBottom: 12,
  },
});
```

---

## 4. Các thư mục components

### Header.js
```
import React from 'react';
import { View, Text, StyleSheet } from 'react-native';

export default function Header() {
  return (
    <View style={styles.container}>
      <View>
        <Text style={styles.greeting}>Xin chào, Đỗ Chí Đức! 👋</Text>
        <Text style={styles.studentInfo}>MSSV: CĐ-CNTT18A | Ngành Công nghệ Thông tin</Text>
        <Text style={styles.university}>Trường Cao đẳng Kỹ thuật Công Nghệ Nha Trang</Text>
      </View>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    backgroundColor: '#1e293b',
    paddingTop: 16,
    paddingBottom: 20,
    paddingHorizontal: 20,
    borderBottomLeftRadius: 20,
    borderBottomRightRadius: 20,
  },
  greeting: {
    fontSize: 20,
    fontWeight: 'bold',
    color: '#f8fafc',
    marginBottom: 4,
  },
  studentInfo: {
    fontSize: 13,
    color: '#94a3b8',
    marginBottom: 2,
  },
  university: {
    fontSize: 12,
    color: '#38bdf8',
    fontWeight: '600',
  },
});
```
### StatCard.js
```
import React from 'react';
import { View, Text, StyleSheet } from 'react-native';

export default function StatCard() {
  return (
    <View style={styles.container}>
      <View style={styles.card}>
        <Text style={styles.number}>6</Text>
        <Text style={styles.label}>Đang học</Text>
      </View>
      <View style={styles.card}>
        <Text style={styles.number}>12</Text>
        <Text style={styles.label}>Hoàn thành</Text>
      </View>
      <View style={styles.card}>
        <Text style={styles.number}>85%</Text>
        <Text style={styles.label}>Tiến độ TB</Text>
      </View>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flexDirection: 'row',
    justifyContent: 'space-between',
    paddingHorizontal: 16,
    marginTop: -15, // Hiệu ứng nổi đè lên header
  },
  card: {
    flex: 1,
    backgroundColor: '#ffffff',
    borderRadius: 12,
    paddingVertical: 14,
    alignItems: 'center',
    marginHorizontal: 4,
    shadowColor: '#000',
    shadowOffset: { width: 0, height: 2 },
    shadowOpacity: 0.1,
    shadowRadius: 4,
    elevation: 3,
  },
  number: {
    fontSize: 18,
    fontWeight: 'bold',
    color: '#0f172a',
    marginBottom: 2,
  },
  label: {
    fontSize: 11,
    color: '#64748b',
    fontWeight: '500',
  },
});
```
### CourseCard.js
```
import React from 'react';
import { View, Text, StyleSheet } from 'react-native';

export default function CourseCard({ title, code, progress, teacher }) {
  return (
    <View style={styles.card}>
      <View style={styles.rowTop}>
        <Text style={styles.courseCode}>{code}</Text>
        <Text style={styles.progressText}>{progress}</Text>
      </View>
      <Text style={styles.courseTitle}>{title}</Text>
      <Text style={styles.teacherText}>Giảng viên: {teacher}</Text>
    </View>
  );
}

const styles = StyleSheet.create({
  card: {
    backgroundColor: '#ffffff',
    borderRadius: 10,
    padding: 14,
    marginBottom: 12,
    borderWidth: 1,
    borderColor: '#e2e8f0',
  },
  rowTop: {
    flexDirection: 'row',
    justifyContent: 'space-between',
    marginBottom: 6,
  },
  courseCode: {
    fontSize: 11,
    fontWeight: 'bold',
    color: '#0284c7',
    backgroundColor: '#e0f2fe',
    paddingHorizontal: 6,
    paddingVertical: 2,
    borderRadius: 4,
  },
  progressText: {
    fontSize: 12,
    fontWeight: '600',
    color: '#10b981',
  },
  courseTitle: {
    fontSize: 15,
    fontWeight: 'bold',
    color: '#1e293b',
    marginBottom: 4,
  },
  teacherText: {
    fontSize: 12,
    color: '#64748b',
  },
});
```
### BottomMenu.js
```
import React from 'react';
import { View, Text, StyleSheet } from 'react-native';

export default function BottomMenu() {
  return (
    <View style={styles.container}>
      <View style={[styles.menuItem, styles.activeItem]}>
        <Text style={styles.activeText}>🏠 Trang chủ</Text>
      </View>
      <View style={styles.menuItem}>
        <Text style={styles.inactiveText}>📖 Khóa học</Text>
      </View>
      <View style={styles.menuItem}>
        <Text style={styles.inactiveText}>📊 Thống kê</Text>
      </View>
      <View style={styles.menuItem}>
        <Text style={styles.inactiveText}>👤 Cá nhân</Text>
      </View>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flexDirection: 'row',
    backgroundColor: '#ffffff',
    borderTopWidth: 1,
    borderTopColor: '#e2e8f0',
    paddingVertical: 10,
    paddingHorizontal: 8,
    justifyContent: 'space-around',
  },
  menuItem: {
    paddingVertical: 6,
    paddingHorizontal: 10,
    borderRadius: 8,
  },
  activeItem: {
    backgroundColor: '#f0f9ff',
  },
  activeText: {
    fontSize: 12,
    fontWeight: 'bold',
    color: '#0284c7',
  },
  inactiveText: {
    fontSize: 12,
    fontWeight: '500',
    color: '#64748b',
  },
});
```

---

## 5. Hình ảnh minh họa giao diện (Screenshot)
<img width="400" height="666" alt="image" src="https://github.com/user-attachments/assets/e781ffaa-7ede-4ca8-808b-0b0c8923768e" />
