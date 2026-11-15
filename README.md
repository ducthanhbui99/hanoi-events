# Hanoi Events

Static website hiển thị sự kiện Hà Nội trên **Map + List**, deploy bằng GitHub Pages.

## Kiến trúc

Repository hiện tách thành 3 file chính:

- `index.html` — giao diện, bộ lọc ngày, bản đồ và logic hiển thị.
- `events.json` — danh sách sự kiện; đây là file cần cập nhật thường xuyên.
- `locations.json` — thư viện địa điểm → latitude/longitude; tọa độ được tái sử dụng giữa các tuần.

Website tải `events.json` và `locations.json` khi mở trang, sau đó ghép tọa độ vào event bằng tên địa điểm.

## Dataset hiện tại

- Sự kiện: **177**
- Địa điểm đã lưu tọa độ: **44**
- Sự kiện hiện có marker: **137**
- Sự kiện chưa có marker: **40**

Các event chưa có tọa độ vẫn xuất hiện trong danh sách.

## Quy tắc ngày

- Có ngày bắt đầu và kết thúc: sự kiện tồn tại trong toàn bộ khoảng ngày, tính cả hai đầu.
- Chỉ có ngày bắt đầu: sự kiện tồn tại từ ngày bắt đầu trở đi.
- Chỉ có ngày kết thúc: sự kiện tồn tại đến hết ngày kết thúc.
- Không có cả ngày bắt đầu và kết thúc: sự kiện luôn tồn tại.

## Category

Dữ liệu dùng 4 nhóm:

1. Triển lãm & Trưng bày
2. Trình diễn
3. Trải nghiệm, giao lưu
4. Tọa đàm, workshop, trao đổi

Category hiện không phải là filter trên giao diện nhưng vẫn được lưu trong `events.json`.

## Nguồn dữ liệu master

Google Sheet:
https://docs.google.com/spreadsheets/d/1ZRB-PNCzlr3oUZLuDVxXnS4odvZ5Vzp0u4cA-t8lpz8/edit?usp=sharing

- Sheet sự kiện: `Events`
- Sheet địa điểm: `Locations`
- Output tương ứng: `events.json` và `locations.json`
- Google Sheet này là source of truth cho các lần publish hàng tuần.
## Cập nhật hàng tuần

Workflow đề xuất:

1. Chuẩn hóa danh sách sự kiện tuần mới.
2. Cập nhật `events.json`.
3. Với venue mới, nếu có tọa độ xác minh được thì bổ sung vào `locations.json`.
4. Không cần sửa `index.html` trừ khi thay đổi giao diện hoặc logic.
5. Commit vào branch `main`; GitHub Pages tự deploy.

Một event trong `events.json` không cần chứa latitude/longitude. Website tự tìm tọa độ theo trường `venue` trong `locations.json`.

## Chạy local

Do website dùng `fetch()` để đọc JSON, không nên mở trực tiếp bằng `file://`.

Chạy local server:

```bash
python -m http.server 8000
```

Sau đó mở:

`http://localhost:8000`

## Stack

- HTML/CSS/JavaScript thuần
- CARTO Voyager raster basemap
- GitHub Pages
- Không có backend/database
