# Nguyễn Thành Khiêm — AWS Workshop

Báo cáo thực tập và workshop First Cloud AI Journey, viết bằng Hugo với nội dung tiếng Việt và tiếng Anh.

## Chạy local

Cài Hugo Extended 0.167.0, sau đó chạy:

```sh
hugo server
```

## Cấu trúc

- `content/`: nội dung báo cáo, worklog và sự kiện.
- `static/`: ảnh, CSS và tài nguyên tĩnh.
- `layouts/`: giao diện và shortcode tùy chỉnh.
- `themes/hugo-theme-learn/`: mã nguồn theme, được lưu trực tiếp để clone là có đủ.
- `archetypes/`: mẫu nội dung Hugo.
- `config.toml`: cấu hình website và ngôn ngữ.
- `.github/workflows/hugo.yml`: build và triển khai GitHub Pages.

`public/` được Hugo tự sinh khi build và không được đưa vào mã nguồn Git.
Để triển khai, chọn **GitHub Actions** tại **Settings → Pages → Source**.
