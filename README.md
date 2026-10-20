# AudioNovel Studio - Google / YouTube landing site

Bộ website tĩnh độc lập dành cho phần Google / YouTube của **AudioNovel Studio**. Không cần Node.js, npm, build hay database. Các trang đã dùng đường dẫn tương đối, phù hợp để deploy bằng GitHub Pages từ thư mục gốc repository.

## Cấu trúc file

```text
google-pages/
├── index.html      # Homepage
├── privacy.html    # Privacy Policy
├── terms.html      # Terms of Service
├── styles.css      # Giao diện responsive
├── favicon.svg     # Biểu tượng AS
├── .nojekyll       # Tắt xử lý Jekyll
└── README.md       # Hướng dẫn này
```

## Đăng lên GitHub Pages

1. Tạo repository **`google-pages`** trong tài khoản GitHub `giaminhNguyen` và chọn **Public** (hoặc tên khác tùy ý).
2. Upload **toàn bộ file ở thư mục này vào ROOT của repo**, không lồng thêm thư mục `audionovel-google-pages`.
3. Vào **Settings → Pages**.
4. Trong **Build and deployment**, chọn **Deploy from a branch**.
5. Chọn nhánh `main` và thư mục `/ (root)`, rồi **Save**.
6. Sau khi GitHub Pages triển khai, mở các URL dự kiến:

| Loại trang | URL nếu repo tên `google-pages` |
|---|---|
| Homepage | https://giaminhnguyen.github.io/google-pages/ |
| Privacy Policy | https://giaminhnguyen.github.io/google-pages/privacy.html |
| Terms of Service | https://giaminhnguyen.github.io/google-pages/terms.html |

Các URL trên **chỉ xuất hiện sau khi bạn tạo repo và bật GitHub Pages**.

Repo TikTok `giaminhNguyen/plugin-pages` không bị sửa và tiếp tục sử dụng URL cũ.

## BẮT BUỘC kiểm tra trước khi dùng cho Google OAuth production

Đây là bản thiết kế website và mẫu nội dung chính sách, **không phải bảo đảm đã được Google xác minh hay phê duyệt**.

- [ ] Kiểm tra địa chỉ email `nguyenming6464@gmail.com` đang dùng ở 3 trang. Email này được lấy từ phần Contact công khai trên website AudioNovel Studio hiện tại; sửa lại nếu cần.
- [ ] Xác nhận ứng dụng thực sự dùng scope `youtube.upload`; nếu yêu cầu thêm scope Google/YouTube, cập nhật trang Privacy Policy cho đúng.
- [ ] Xác nhận cách ứng dụng nhận, lưu và xóa OAuth access/refresh token (lưu máy người dùng, server hay nơi khác); sửa phần 2, 5 và 6 của `privacy.html` theo triển khai thực tế.
- [ ] Xác nhận thời hạn lưu token, video, log, metadata, cách ngắt kết nối và thời gian thực hiện yêu cầu xóa dữ liệu; nêu cụ thể khi có thể.
- [ ] Xác nhận dữ liệu có chuyển cho nhà cung cấp AI, hosting hoặc bên thứ ba nào không, rồi điều chỉnh phần chia sẻ dữ liệu tương ứng.
- [ ] Xác nhận luồng người dùng đồng ý với Privacy Policy, quyền đăng, kênh nhận video và chế độ hiển thị video **trong ứng dụng thực tế**. Landing page tĩnh không tự tạo được các bước này.
- [ ] Kiểm tra sản phẩm thực sự hỗ trợ các tính năng được giới thiệu. Tránh công bố tính năng chưa tồn tại như thể đã phát hành.
- [ ] Mở cả 3 trang từ cửa sổ ẩn danh, thử link nội bộ và địa chỉ email.

### Lưu ý quan trọng về GitHub Pages và tên miền

Mặc dù GitHub Pages lưu trữ site công khai, **Google có thể không chấp nhận `giaminhnguyen.github.io` như tên miền đã xác minh thuộc quyền sở hữu của bạn** trong quy trình OAuth production/verification. Theo hướng dẫn chính thức, trang chủ và URL chính sách phải có thể truy cập công khai và tên miền liên quan cần xác minh quyền sở hữu khi Google yêu cầu.

Nếu mục **Authorized domains** hoặc kiểm tra domain báo lỗi, giải pháp thực tế là **gắn custom domain do bạn sở hữu** vào repo GitHub Pages, sau đó xác minh qua Google Search Console. Vẫn giữ được hosting GitHub Pages, không cần đổi mã nguồn.

Không dùng URL của landing page này làm OAuth redirect URI trừ khi chính ứng dụng đã triển khai xử lý OAuth tại URL đó. OAuth redirect URI phải trỏ về callback thực sự của ứng dụng.

## Liên kết chính sách chính thức

- [Google OAuth: App branding verification](https://developers.google.com/identity/protocols/oauth2/production-readiness/brand-verification)
- [Google OAuth 2.0 policies](https://developers.google.com/identity/protocols/oauth2/policies)
- [YouTube API Services Developer Policies](https://developers.google.com/youtube/terms/developer-policies)
- [YouTube Terms of Service](https://www.youtube.com/t/terms)
- [Google Privacy Policy](https://policies.google.com/privacy)

## Kỹ thuật

- Site tĩnh HTML/CSS; không có form thu thập dữ liệu, backend, OAuth callback hoặc Javascript tracking trên các trang này.
- Các file sử dụng link tương đối; có thể mở `index.html` tại máy để xem trước.
- Không upload API key, client secret, access token hay refresh token lên repository Public.
