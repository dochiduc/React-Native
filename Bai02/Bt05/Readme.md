# BÁO CÁO BÀI TẬP 02 - BT05: ỨNG DỤNG THEO DÕI MỤC TIÊU & HIỆU ỨNG ĐỘNG (AnimateApp)

## 1. Thông tin bài nộp
* **Tên ứng dụng:** AnimateApp (Chủ đề: Theo dõi mục tiêu học tập, rèn luyện tích hợp hiệu ứng động Animated API)
* **Link ứng dụng trên Expo Snack:** http://snack.expo.dev/@grondwalker/animateapp
* **Học phần:** Phát triển ứng dụng di động với React Native (Bài 2: Component hóa, State & Animations)

---

## 2. Mô tả thiết kế và sự thay đổi giao diện
* **Kiến trúc Component:** Ứng dụng được chia tách thành các component độc lập để tối ưu hóa khả năng tái sử dụng:
  * **`ProgressCard.js`**: Thẻ hiển thị tiến độ hoàn thành mục tiêu trực quan kèm thanh trạng thái (`progress bar`).
  * **`ActionButton.js`**: Component nút bấm tùy biến dùng để bắt đầu phiên học hoặc đặt lại trạng thái.
  * **`AnimatedMessage.js`**: Thành phần thông báo kết quả ứng dụng API `Animated` của React Native để tạo hiệu ứng phóng to (`scale`) và hiện dần (`opacity`) mượt mà khi người dùng hoàn thành mục tiêu.
* **Sự thay đổi giao diện:** Khi nhấn nút bắt đầu, tiến độ cập nhật từ trạng thái chờ sang hoàn thành 100% và khung thông báo thành công sẽ xuất hiện với hiệu ứng động lò xo bắt mắt.

---

## 3. Mã nguồn chi tiết các thành phần

### 📁 Tệp gốc `App.js`
```javascript
import React, { useState } from 'react';
import { StyleSheet, View, Text, SafeAreaView, StatusBar } from 'react-native';

import ProgressCard from './components/ProgressCard';
import ActionButton from './components/ActionButton';
import AnimatedMessage from './components/AnimatedMessage';

export default function App() {
  const [progress, setProgress] = useState(60);
  const [completedCount, setCompletedCount] = useState(3);
  const [showSuccess, setShowSuccess] = useState(false);
  const [messageText, setMessageText] = useState('');

  // Hàm xử lý khi nhấn nút bắt đầu/hoàn thành
  const handleStartTraining = () => {
    setShowSuccess(false);
    
    // Giả lập hoàn thành phiên rèn luyện/học tập
    setTimeout(() => {
      setProgress(100);
      setCompletedCount(5);
      setMessageText('Bạn đã hoàn thành mục tiêu học tập và rèn luyện trong ngày hôm nay!');
      setShowSuccess(true);
    }, 500);
  };

  // Hàm đặt lại trạng thái ban đầu
  const handleReset = () => {
    setShowSuccess(false);
    setProgress(60);
    setCompletedCount(3);
  };

  return (
    <SafeAreaView style={styles.container}>
      <StatusBar barStyle="dark-content" backgroundColor="#f8fafc" />
      
      {/* Tiêu đề ứng dụng */}
      <View style={styles.header}>
        <Text style={styles.headerTitle}>Goal Tracker 🎯</Text>
        <Text style={styles.headerSubtitle}>Ứng dụng theo dõi mục tiêu học tập & rèn luyện</Text>
      </View>

      <View style={styles.content}>
        {/* 1. Thẻ hiển thị tiến độ */}
        <ProgressCard 
          title="Mục tiêu Kỹ thuật & Phát triển" 
          progress={progress} 
          current={completedCount} 
          total={5} 
        />

        {/* 2. Nút bấm tương tác */}
        <ActionButton 
          title="🚀 Bắt đầu & Hoàn thành phiên học" 
          onPress={handleStartTraining} 
          type="primary"
        />

        <ActionButton 
          title="🔄 Đặt lại tiến độ" 
          onPress={handleReset} 
          type="secondary"
        />

        {/* 3. Thành phần thông báo có hiệu ứng động xuất hiện */}
        <AnimatedMessage 
          visible={showSuccess} 
          message={messageText} 
        />
      </View>
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  container: { flex: 1, backgroundColor: '#f8fafc' },
  header: { padding: 16, backgroundColor: '#ffffff', borderBottomWidth: 1, borderBottomColor: '#e2e8f0' },
  headerTitle: { fontSize: 20, fontWeight: 'bold', color: '#0f172a' },
  headerSubtitle: { fontSize: 12, color: '#64748b', marginTop: 2 },
  content: { padding: 16, flex: 1 },
});
```

📂 Thư mục components/
1. ProgressCard.js (Thẻ hiển thị tiến độ)
```
import React from 'react';
import { View, Text, StyleSheet } from 'react-native';

export default function ProgressCard({ title, progress, current, total }) {
  return (
    <View style={styles.card}>
      <Text style={styles.cardTitle}>{title}</Text>
      
      <View style={styles.progressInfo}>
        <Text style={styles.progressText}>Đã hoàn thành: {current}/{total} mục tiêu</Text>
        <Text style={styles.percentageText}>{progress}%</Text>
      </View>

      {/* Thanh tiến độ */}
      <View style={styles.progressBarBg}>
        <View style={[styles.progressBarFill, { width: `${progress}%` }]} />
      </View>
    </View>
  );
}

const styles = StyleSheet.create({
  card: {
    backgroundColor: '#ffffff',
    borderRadius: 16,
    padding: 16,
    marginBottom: 20,
    borderWidth: 1,
    borderColor: '#e2e8f0',
    shadowColor: '#000',
    shadowOpacity: 0.05,
    shadowRadius: 4,
    elevation: 2,
  },
  cardTitle: { fontSize: 16, fontWeight: 'bold', color: '#1e293b', marginBottom: 12 },
  progressInfo: { flexDirection: 'row', justifyContent: 'space-between', marginBottom: 8 },
  progressText: { fontSize: 13, color: '#64748b' },
  percentageText: { fontSize: 13, fontWeight: 'bold', color: '#0284c7' },
  progressBarBg: { height: 8, backgroundColor: '#f1f5f9', borderRadius: 4, overflow: 'hidden' },
  progressBarFill: { height: '100%', backgroundColor: '#0284c7', borderRadius: 4 },
});
```

2. ActionButton.js (Nút bấm thao tác)
```
import React from 'react';
import { TouchableOpacity, Text, StyleSheet } from 'react-native';

export default function ActionButton({ title, onPress, type = 'primary' }) {
  const isPrimary = type === 'primary';
  return (
    <TouchableOpacity 
      style={[styles.button, isPrimary ? styles.primaryBtn : styles.secondaryBtn]} 
      onPress={onPress}
    >
      <Text style={[styles.text, isPrimary ? styles.primaryText : styles.secondaryText]}>
        {title}
      </Text>
    </TouchableOpacity>
  );
}

const styles = StyleSheet.create({
  button: {
    paddingVertical: 14,
    borderRadius: 10,
    alignItems: 'center',
    marginBottom: 12,
  },
  primaryBtn: { backgroundColor: '#0284c7' },
  secondaryBtn: { backgroundColor: '#f8fafc', borderWidth: 1, borderColor: '#cbd5e1' },
  text: { fontSize: 15, fontWeight: 'bold' },
  primaryText: { color: '#ffffff' },
  secondaryText: { color: '#334155' },
});
```

3. AnimatedMessage.js (Thành phần thông báo có hiệu ứng động)
```
import React, { useEffect, useRef } from 'react';
import { Animated, Text, StyleSheet } from 'react-native';

export default function AnimatedMessage({ visible, message }) {
  const scaleAnim = useRef(new Animated.Value(0)).current;
  const opacityAnim = useRef(new Animated.Value(0)).current;

  useEffect(() => {
    if (visible) {
      // Hiệu ứng lò xo phóng to & xuất hiện
      Animated.parallel([
        Animated.spring(scaleAnim, {
          toValue: 1,
          friction: 5,
          useNativeDriver: true,
        }),
        Animated.timing(opacityAnim, {
          toValue: 1,
          duration: 200,
          useNativeDriver: true,
        }),
      ]).start();
    } else {
      // Thu nhỏ và biến mất
      Animated.parallel([
        Animated.timing(scaleAnim, {
          toValue: 0,
          duration: 150,
          useNativeDriver: true,
        }),
        Animated.timing(opacityAnim, {
          toValue: 0,
          duration: 150,
          useNativeDriver: true,
        }),
      ]).start();
    }
  }, [visible]);

  if (!visible) return null;

  return (
    <Animated.View 
      style={[
        styles.container, 
        { 
          opacity: opacityAnim, 
          transform: [{ scale: scaleAnim }] 
        }
      ]}
    >
      <Text style={styles.icon}>🎉</Text>
      <Text style={styles.title}>Hoàn thành xuất sắc!</Text>
      <Text style={styles.message}>{message}</Text>
    </Animated.View>
  );
}

const styles = StyleSheet.create({
  container: {
    backgroundColor: '#f0fdf4',
    borderWidth: 1,
    borderColor: '#bbf7d0',
    borderRadius: 12,
    padding: 16,
    alignItems: 'center',
    marginTop: 20,
  },
  icon: { fontSize: 32, marginBottom: 4 },
  title: { fontSize: 16, fontWeight: 'bold', color: '#166534', marginBottom: 4 },
  message: { fontSize: 13, color: '#15803d', textAlign: 'center' },
});
```

---

## 4. Hình ảnh minh họa sự thay đổi giao diện (Screenshot)
Giao diện ban đầu:
<img width="340" height="612" alt="image" src="https://github.com/user-attachments/assets/05928fb2-9ae3-499b-9482-f2179b40ff99" />

Giao diện sau khi hoàn thành mục tiêu:
<img width="336" height="608" alt="image" src="https://github.com/user-attachments/assets/86961f44-149f-4d3d-98fd-4c75312c9fb3" />
