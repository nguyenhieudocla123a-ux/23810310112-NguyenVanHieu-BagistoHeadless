# GraphQL Queries - Nguyễn Văn Hiếu

**Sử dụng Demo API**: https://demo.bagisto.com/graphql

(Nếu cài local thành công, đổi thành: http://localhost:8000/graphql)

---

## Query 1: Lấy danh sách Categories (id, name, slug)

```graphql
query GetCategories {
  categories {
    data {
      id
      name
      slug
    }
  }
}
```

---

## Query 2: Lấy 05 sản phẩm mới nhất (id, name, price, description, url_key)

```graphql
query GetLatestProducts {
  products(first: 5, page: 1) {
    data {
      id
      name
      price
      description
      url_key
    }
  }
}
```

---

## Query 3 (Nâng cao): Lọc 03 sản phẩm có tên chứa "NguyenVanHieu"

```graphql
query GetMyProducts {
  products(
    first: 10,
    page: 1,
    filters: {
      name: "NguyenVanHieu"
    }
  ) {
    data {
      id
      name
      price
      description
      url_key
    }
  }
}
```

> Lưu ý: Tên sản phẩm phải đặt theo cú pháp NguyenVanHieu_TenSanPham
> (ví dụ: NguyenVanHieu_LaptopGaming, NguyenVanHieu_TaiNghe, NguyenVanHieu_ChuotKhongDay)

---

## Lệnh Console cần chạy khi chụp ảnh kết quả Query 3

Mở tab Console trong DevTools (F12) và chạy:

```js
console.log("Bài làm của: Nguyễn Văn Hiếu")
```

---

## Câu trả lời bắt buộc

### Câu 1: So sánh Payload giữa REST API và GraphQL

REST API trả về toàn bộ dữ liệu của đối tượng (over-fetching), ví dụ một sản phẩm
có thể trả về 30+ trường dù chỉ cần 5 trường. GraphQL chỉ trả về đúng các trường
được khai báo trong query (id, name, price, description, url_key), giúp giảm đáng
kể kích thước payload, tiết kiệm băng thông và tăng tốc độ phản hồi, đặc biệt
hữu ích trên thiết bị di động hoặc mạng chậm.

### Câu 2: Query hay Mutation để thay đổi giá sản phẩm?

Sử dụng Mutation. Trong GraphQL, Query chỉ dùng để đọc dữ liệu (read-only),
còn Mutation dùng để thay đổi dữ liệu trên server (tạo, cập nhật, xóa).
Việc thay đổi giá sản phẩm là một thao tác ghi (write operation) nên bắt buộc
phải dùng Mutation, ví dụ: mutation { updateProduct(id: 1, price: 299000) { id name price } }.
