# 📱 MultiScreenApp - React Native Navigation

Bài tập **Bt04** - Môn Lập trình Di động với React Native.

## 🔗 Liên kết ứng dụng
* **Expo Snack Link:** https://snack.expo.dev/@grondwalker/multiscreenapp

---

## 🛠️ Cấu trúc và Thành phần Ứng dụng

Ứng dụng được thiết kế gồm **3 màn hình chính** theo yêu cầu đề bài, kết hợp thêm Tab Navigation nâng cao:
1. **HomeScreen:** Màn hình trang chủ chào mừng.
2. **ListScreen:** Màn hình danh sách sản phẩm sử dụng `FlatList`.
3. **DetailScreen:** Màn hình chi tiết sản phẩm nhận tham số qua `route.params` và có nút quay lại (`navigation.goBack()`).
4. **ProfileScreen:** Màn hình cá nhân (Tab Navigation bổ sung cho sinh viên khá).

---

## 💻 Mã nguồn chính (Code Snippets)

### 1. Quản lý Điều hướng (`App.js`)
Kết hợp giữa `Stack Navigation` và `Bottom Tab Navigation`:

```javascript
import React from 'react';
import { NavigationContainer } from '@react-navigation/native';
import { createBottomTabNavigator } from '@react-navigation/bottom-tabs';
import { createStackNavigator } from '@react-navigation/stack';

import HomeScreen from './components/HomeScreen';
import ListScreen from './components/ListScreen';
import DetailScreen from './components/DetailScreen';
import ProfileScreen from './components/ProfileScreen';

const Tab = createBottomTabNavigator();
const Stack = createStackNavigator();

// Stack riêng cho phần Danh sách -> Chi tiết
function ListStackNavigator() {
  return (
    <Stack.Navigator screenOptions={{ headerShown: false }}>
      <Stack.Screen name="ListMain" component={ListScreen} />
      <Stack.Screen name="Detail" component={DetailScreen} />
    </Stack.Navigator>
  );
}

export default function App() {
  return (
    <NavigationContainer>
      <Tab.Navigator 
        screenOptions={{
          headerStyle: { backgroundColor: '#1e293b' },
          headerTintColor: '#ffffff',
          tabBarActiveTintColor: '#0284c7',
          tabBarInactiveTintColor: '#64748b',
        }}
      >
        <Tab.Screen 
          name="Trang chủ" 
          component={HomeScreen} 
          options={{ title: 'Trang chủ' }}
        />
        <Tab.Screen 
          name="ListTab" 
          component={ListStackNavigator} 
          options={{ title: 'Danh sách sản phẩm', headerShown: false }}
        />
        <Tab.Screen 
          name="Cá nhân" 
          component={ProfileScreen} 
          options={{ title: 'Cá nhân' }}
        />
      </Tab.Navigator>
    </NavigationContainer>
  );
}
```

---

## 4. Các Components:
* HomeScreen.js
```
import React from 'react';
import { View, Text, StyleSheet, TouchableOpacity } from 'react-native';

export default function HomeScreen({ navigation }) {
  return (
    <View style={styles.container}>
      <Text style={styles.title}>Chào mừng đến với Ứng dụng!</Text>
      <Text style={styles.subtitle}>
        Đây là màn hình Trang chủ (HomeScreen). Hãy khám phá danh sách các sản phẩm bên dưới.
      </Text>

      <TouchableOpacity
        style={styles.button}
        onPress={() => navigation.navigate('ListTab')}
      >
        <Text style={styles.buttonText}>Xem Danh Sách Ngay</Text>
      </TouchableOpacity>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    padding: 20,
    backgroundColor: '#f5f7fa',
  },
  title: {
    fontSize: 24,
    fontWeight: 'bold',
    color: '#1e293b',
    marginBottom: 10,
    textAlign: 'center',
  },
  subtitle: {
    fontSize: 16,
    color: '#64748b',
    textAlign: 'center',
    marginBottom: 30,
    lineHeight: 22,
  },
  button: {
    backgroundColor: '#2563eb',
    paddingVertical: 14,
    paddingHorizontal: 28,
    borderRadius: 10,
    elevation: 2,
  },
  buttonText: {
    color: '#ffffff',
    fontSize: 16,
    fontWeight: '600',
  },
});
```

* ListScreen.js
```
import React from 'react';
import { View, Text, FlatList, TouchableOpacity, StyleSheet } from 'react-native';

const DATA = [
  {
    id: '1',
    name: 'Laptop Dell XPS 13',
    price: '28.500.000 VNĐ',
    description: 'Màn hình 13.4 inch FHD+, Chip Intel Core i7 thế hệ mới, RAM 16GB, SSD 512GB, thiết kế vỏ nhôm nguyên khối siêu mỏng nhẹ.',
  },
  {
    id: '2',
    name: 'Bàn phím cơ Keychron K2',
    price: '1.850.000 VNĐ',
    description: 'Layout 75% gọn gàng, hỗ trợ kết nối Bluetooth 5.1 và cáp Type-C, tương thích tốt cả Windows và macOS.',
  },
  {
    id: '3',
    name: 'Chuột Logitech MX Master 3S',
    price: '2.390.000 VNĐ',
    description: 'Cảm biến 8000 DPI hoạt động trên mọi bề mặt kể cả kính, cuộn điện từ MagSpeed siêu êm, giảm 90% tiếng ồn click.',
  },
  {
    id: '4',
    name: 'Tai nghe Sony WH-1000XM5',
    price: '6.490.000 VNĐ',
    description: 'Chống ồn chủ động hàng đầu thị trường với 8 micro, thời lượng pin lên đến 30 giờ, hỗ trợ sạc nhanh.',
  },
];

export default function ListScreen({ navigation }) {
  const renderItem = ({ item }) => (
    <TouchableOpacity
      style={styles.card}
      onPress={() => navigation.navigate('Detail', { product: item })}
    >
      <View>
        <Text style={styles.itemName}>{item.name}</Text>
        <Text style={styles.itemPrice}>{item.price}</Text>
      </View>
      <Text style={styles.arrow}>›</Text>
    </TouchableOpacity>
  );

  return (
    <View style={styles.container}>
      <FlatList
        data={DATA}
        keyExtractor={(item) => item.id}
        renderItem={renderItem}
        contentContainerStyle={styles.listContent}
      />
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#f5f7fa',
  },
  listContent: {
    padding: 16,
  },
  card: {
    backgroundColor: '#ffffff',
    padding: 16,
    borderRadius: 12,
    marginBottom: 12,
    flexDirection: 'row',
    justifyContent: 'space-between',
    alignItems: 'center',
    shadowColor: '#000',
    shadowOpacity: 0.05,
    shadowRadius: 5,
    elevation: 2,
  },
  itemName: {
    fontSize: 17,
    fontWeight: 'bold',
    color: '#1e293b',
    marginBottom: 4,
  },
  itemPrice: {
    fontSize: 14,
    color: '#2563eb',
    fontWeight: '600',
  },
  arrow: {
    fontSize: 24,
    color: '#94a3b8',
    fontWeight: 'bold',
  },
});
```

* DetailScreen.js
```
import React from 'react';
import { View, Text, StyleSheet, TouchableOpacity } from 'react-native';

export default function DetailScreen({ route, navigation }) {
  const { product } = route.params;

  return (
    <View style={styles.container}>
      <View style={styles.detailBox}>
        <Text style={styles.label}>Tên sản phẩm:</Text>
        <Text style={styles.name}>{product.name}</Text>

        <Text style={styles.label}>Giá bán:</Text>
        <Text style={styles.price}>{product.price}</Text>

        <Text style={styles.label}>Mô tả chi tiết:</Text>
        <Text style={styles.description}>{product.description}</Text>
      </View>

      <TouchableOpacity
        style={styles.backButton}
        onPress={() => navigation.goBack()}
      >
        <Text style={styles.backButtonText}>← Quay lại danh sách</Text>
      </TouchableOpacity>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    padding: 20,
    backgroundColor: '#f5f7fa',
    justifyContent: 'space-between',
  },
  detailBox: {
    backgroundColor: '#ffffff',
    padding: 20,
    borderRadius: 12,
    elevation: 2,
  },
  label: {
    fontSize: 13,
    color: '#64748b',
    marginTop: 12,
    textTransform: 'uppercase',
    fontWeight: '600',
  },
  name: {
    fontSize: 22,
    fontWeight: 'bold',
    color: '#0f172a',
    marginTop: 4,
  },
  price: {
    fontSize: 18,
    fontWeight: 'bold',
    color: '#16a34a',
    marginTop: 4,
  },
  description: {
    fontSize: 16,
    color: '#334155',
    marginTop: 6,
    lineHeight: 24,
  },
  backButton: {
    backgroundColor: '#475569',
    paddingVertical: 14,
    borderRadius: 10,
    alignItems: 'center',
    marginBottom: 10,
  },
  backButtonText: {
    color: '#ffffff',
    fontSize: 16,
    fontWeight: '600',
  },
});
```

* ProfileScreen.js
```
import React from 'react';
import { View, Text, StyleSheet } from 'react-native';
import { Ionicons } from '@expo/vector-icons';

export default function ProfileScreen() {
  return (
    <View style={styles.container}>
      <Ionicons name="person-circle-outline" size={100} color="#2563eb" />
      <Text style={styles.name}>Sinh Viên Thực Hiện</Text>
      <Text style={styles.info}>Lớp: Lập trình Di động React Native</Text>
      <Text style={styles.info}>Trạng thái: Đang hoạt động</Text>
    </View>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    justifyContent: 'center',
    alignItems: 'center',
    backgroundColor: '#f5f7fa',
    padding: 20,
  },
  name: {
    fontSize: 22,
    fontWeight: 'bold',
    color: '#1e293b',
    marginTop: 12,
    marginBottom: 8,
  },
  info: {
    fontSize: 16,
    color: '#64748b',
    marginBottom: 4,
  },
});
```

---

## 5. Hình ảnh giao diện (UI Screenshots)

* Màn hình Trang chủ (Home)
<img width="318" height="703" alt="image" src="https://github.com/user-attachments/assets/cb8ab4aa-e836-4ace-aca0-1d1879b20553" />

* Màn hình Danh sách (List)
<img width="324" height="701" alt="image" src="https://github.com/user-attachments/assets/35b70be3-ca4b-4668-85f3-b732ade3be55" />

* Màn hình Chi tiết (Detail)
<img width="327" height="695" alt="image" src="https://github.com/user-attachments/assets/8057423b-9f27-486b-a236-24b81640b756" />

* Màn hình Cá nhân (Profile)
<img width="328" height="695" alt="image" src="https://github.com/user-attachments/assets/c5e71d3d-4cbd-498c-9277-8dc4e6c8c328" />
