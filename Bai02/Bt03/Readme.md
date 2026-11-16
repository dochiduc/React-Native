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

## 3. Mã nguồn chi tiết các thành phần

### 📁 Tệp gốc `App.js`
```javascript
import React from 'react';
import { StyleSheet, View, Text, FlatList, SafeAreaView, StatusBar, Alert } from 'react-native';
import ProductCard from './components/ProductCard';

// Dữ liệu mẫu gồm 6 cuốn sách thể loại lịch sử
const HISTORY_BOOKS = [
  {
    id: '1',
    name: 'Việt Nam Sử Lược',
    author: 'Trần Trọng Kim',
    price: '95.000 đ',
    description: 'Bộ thông sử viết bằng quốc ngữ có giá trị lớn và sớm nhất của lịch sử Việt Nam cận đại.',
    image: 'https://img.newshop.vn/uploads/products/59733/viet-nam-su-luoc-YWIo.jpg',
  },
  {
    id: '2',
    name: 'Đại Việt Sử Ký Toàn Thư',
    author: 'Ngô Sĩ Liên',
    price: '250.000 đ',
    description: 'Bộ sách lịch sử chính thống quý giá ghi chép lại toàn bộ tiến trình lịch sử nước Đại Việt từ thời Kinh Dương Vương.',
    image: 'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQ4neF_Xf-ay4at-_xiexpNjsiMWPWyfV3W8snDxUCLisgYSce98rRhhyZJb0D_hd9ZBvTLEE-u52JVf_Fo_lJA_cuSLJMFBecl2Y4aUQ&s=10',
  },
  {
    id: '3',
    name: 'Binh Pháp Tôn Tử',
    author: 'Tôn Vũ',
    price: '65.000 đ',
    description: 'Binh thư chiến lược quân sự kinh điển của Trung Hoa cổ đại, đúc rút nhiều bài học về nghệ thuật lãnh đạo.',
    image: 'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQafmHmmaUP9hzA29kHbNC5nnbFKruvC251PtJhIxbw6s28zaenoeUIsHlJwAFSBEObRAHuoPZ8Ey8IpSwyiN3F3qm9gdRBhCgMmZkyS_eV&s=10',
  },
  {
    id: '4',
    name: 'Lược Sử Thế Giới',
    author: 'E.H. Gombrich',
    price: '115.000 đ',
    description: 'Hành trình khám phá lịch sử loài người từ thời kỳ đồ đá cho đến thế chiến một cách sống động, dễ hiểu.',
    image: 'https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcRPsq5CCJ1GUYXMHD4gI4NpKGY1SqA5UKxpVF6S0O4uMQ&s=10',
  },
  {
    id: '5',
    name: 'Đệ Nhị Thế Chiến',
    author: 'Abraham Rothberg',
    price: '220.000 đ',
    description: 'Tái hiện toàn cảnh cuộc chiến tranh đẫm máu nhất trong lịch sử nhân loại (1939–1945) giữa phe Đồng Minh và phe Trục.',
    image: 'https://cdn1.fahasa.com/media/catalog/product/i/m/image_241321.jpg',
  },
  {
    id: '6',
    name: 'Sapiens: Lược sử về loài người',
    author: 'Yuval Noah Harari',
    price: '100.000 đ',
    description: 'THành trình khảo cứu cách loài người từ một loài động vật không mấy nổi trội vươn lên thống trị trái đất.',
    image: 'https://cdn1.fahasa.com/media/flashmagazine/images/page_images/sapiens_luoc_su_loai_nguoi/2023_03_21_16_35_44_1-390x510.jpg',
  },
];

export default function App() {
  const handleBuy = (book) => {
    Alert.alert('Giỏ hàng Lịch sử', `Bạn đã đặt mua tác phẩm: "${book.name}"`);
  };

  return (
    <SafeAreaView style={styles.container}>
      <StatusBar barStyle="dark-content" backgroundColor="#fef2f2" />
      
      {/* Tiêu đề ứng dụng */}
      <View style={styles.header}>
        <Text style={styles.headerTitle}>🏛️ History Book Store</Text>
        <Text style={styles.headerSubtitle}>Tàng thư lịch sử - Lưu giữ ngàn năm văn hiến</Text>
      </View>

      {/* Hiển thị danh sách sản phẩm bằng FlatList */}
      <FlatList
        data={HISTORY_BOOKS}
        keyExtractor={(item) => item.id}
        renderItem={({ item }) => (
          <ProductCard product={item} onBuyPress={handleBuy} />
        )}
        contentContainerStyle={styles.listContainer}
        showsVerticalScrollIndicator={false}
      />
    </SafeAreaView>
  );
}

const styles = StyleSheet.create({
  container: {
    flex: 1,
    backgroundColor: '#f8fafc',
  },
  header: {
    paddingHorizontal: 16,
    paddingVertical: 14,
    borderBottomWidth: 1,
    borderBottomColor: '#e2e8f0',
    backgroundColor: '#ffffff',
  },
  headerTitle: {
    fontSize: 20,
    fontWeight: 'bold',
    color: '#9a3412',
  },
  headerSubtitle: {
    fontSize: 12,
    color: '#64748b',
    marginTop: 2,
  },
  listContainer: {
    padding: 16,
  },
});
```
Thư mục components/
ProductCard.js (Component hiển thị thông tin sản phẩm nhận qua props)
```
import React from 'react';
import { View, Text, Image, StyleSheet, TouchableOpacity } from 'react-native';

export default function ProductCard({ product, onBuyPress }) {
  return (
    <View style={styles.card}>
      {/* Hình ảnh bìa sách lịch sử */}
      <Image source={{ uri: product.image }} style={styles.image} resizeMode="cover" />
      
      {/* Thông tin chi tiết */}
      <View style={styles.infoContainer}>
        <Text style={styles.name} numberOfLines={1}>{product.name}</Text>
        <Text style={styles.author} numberOfLines={1}>Tác giả: {product.author}</Text>
        <Text style={styles.description} numberOfLines={2}>{product.description}</Text>
        
        <div style={styles.footerRow}>
          <Text style={styles.price}>{product.price}</Text>
          <TouchableOpacity style={styles.button} onPress={() => onBuyPress(product)}>
            <Text style={styles.buttonText}>Mua ngay</Text>
          </TouchableOpacity>
        </div>
      </View>
    </View>
  );
}

const styles = StyleSheet.create({
  card: {
    backgroundColor: '#ffffff',
    borderRadius: 12,
    borderWidth: 1,
    borderColor: '#e2e8f0',
    marginBottom: 16,
    overflow: 'hidden',
    flexDirection: 'row',
    padding: 10,
    shadowColor: '#000',
    shadowOffset: { width: 0, height: 1 },
    shadowOpacity: 0.1,
    shadowRadius: 2,
    elevation: 2,
  },
  image: {
    width: 80,
    height: 110,
    borderRadius: 6,
    backgroundColor: '#f1f5f9',
  },
  infoContainer: {
    flex: 1,
    marginLeft: 12,
    justifyContent: 'space-between',
  },
  name: {
    fontSize: 15,
    fontWeight: 'bold',
    color: '#1e293b',
  },
  author: {
    fontSize: 12,
    color: '#64748b',
    marginBottom: 2,
  },
  description: {
    fontSize: 12,
    color: '#475569',
    marginVertical: 2,
  },
  footerRow: {
    flexDirection: 'row',
    justifyContent: 'space-between',
    alignItems: 'center',
    marginTop: 4,
  },
  price: {
    fontSize: 14,
    fontWeight: 'bold',
    color: '#9a3412', // Màu cam đất phù hợp với phong cách sách lịch sử
  },
  button: {
    backgroundColor: '#9a3412',
    paddingVertical: 6,
    paddingHorizontal: 12,
    borderRadius: 6,
  },
  buttonText: {
    color: '#ffffff',
    fontSize: 12,
    fontWeight: 'bold',
  },
});
```

---

## 4. Hình ảnh minh họa giao diện (Screenshot)
<img width="468" height="795" alt="image" src="https://github.com/user-attachments/assets/d839071e-9ced-4a6b-95cd-c5c33ae19426" />
