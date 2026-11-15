# Hanoi Events

Website tĩnh (static site) để hiển thị danh sách sự kiện Hà Nội trên **Map + List**, không cần backend và không cần API key.

## Dữ liệu

- Nguồn: `Hanoi Event - To Share.xlsx`
- Sheet: `16 Nov`
- Số sự kiện: **138**
- Có tọa độ để đặt marker: **86**
- Chưa có tọa độ: **52** (vẫn hiện trong List view)
- Ngày snapshot dùng khi chuẩn hóa các mốc "Đến ...": **2026-11-16**

Website giữ nguyên `Thời gian` gốc trong file để hiển thị. Các trường `start_date/end_date/start_time/end_time` trong `events.json` được chuẩn hóa để phục vụ lọc/sắp xếp.

## Chức năng

- Bản đồ MapLibre + OpenFreeMap
- Danh sách sự kiện responsive
- Tìm theo tên/địa điểm
- Lọc theo ngày
- Lọc theo loại sự kiện
- Ẩn sự kiện đã kết thúc
- Cluster marker
- Popup chi tiết
- Link nguồn sự kiện
- Link Google Maps
- URL chia sẻ bộ lọc, ví dụ `?date=2026-11-22&type=Bi%E1%BB%83u%20di%E1%BB%85n%20%26%20phim`

## Chạy local

Có thể mở `index.html` trực tiếp bằng trình duyệt (cần Internet để tải MapLibre và bản đồ nền).

Hoặc chạy một local web server:

```bash
python -m http.server 8000
```

Sau đó mở `http://localhost:8000`.

## Đưa lên GitHub Pages

1. Tạo một public repository, ví dụ `hanoi-events`.
2. Upload toàn bộ file trong thư mục này vào root repository.
3. Vào **Settings → Pages**.
4. Chọn **Deploy from a branch**.
5. Chọn branch `main`, folder `/ (root)`.
6. Website sẽ có dạng `https://<username>.github.io/hanoi-events/`.

## Cập nhật dữ liệu

Source dùng bởi website là `events.js`; `events.json` là bản JSON tương đương để dễ tích hợp về sau.

Khi cập nhật dataset, nên regenerate cả hai file để tránh lệch dữ liệu.

## Tọa độ

Các địa điểm chưa xác định chắc tọa độ được liệt kê trong `UNMAPPED_LOCATIONS.md`. Các mục này không có marker nhưng có thể có link Google Maps Search.

## Stack

- MapLibre GL JS 6.18.0
- OpenFreeMap style: `https://tiles.openfreemap.org/styles/liberty`
- HTML/CSS/JavaScript thuần
- GitHub Pages