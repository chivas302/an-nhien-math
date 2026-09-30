# V3.71 – Google Account + Cloud Progress Sync

## Mục tiêu
Tiến độ `an_nhien_math_v2` được giữ local để chạy nhanh/offline và được sao lưu vào Cloud Firestore theo Firebase Authentication UID.

Cloud path:
`users/{uid}/progress/main`

## A. Tạo Firebase project
1. Vào Firebase Console và tạo project, ví dụ `an-nhien-math`.
2. Add app → Web (`</>`).
3. Copy `firebaseConfig`.
4. Mở `firebase-config.js` trong repository và thay các giá trị `PASTE_...`.

## B. Bật Google Login
Firebase Console → Authentication → Sign-in method → Google → Enable.
Chọn support email và Save.

## C. Authorized domains
Authentication → Settings → Authorized domains.
Thêm domain GitHub Pages của bạn, ví dụ:
`TEN-TAI-KHOAN.github.io`

Không thêm `https://` và không thêm path repository.

## D. Tạo Firestore
Firebase Console → Firestore Database → Create database.
Chọn Production mode.

## E. Security Rules
Firestore → Rules.
Copy toàn bộ nội dung `firestore.rules` rồi Publish.

Rules V3.71 chỉ cho UID đang đăng nhập đọc/ghi dữ liệu của chính UID đó.

## F. Upload GitHub
Upload toàn bộ nội dung thư mục `github-pages/` lên root repository V3.71.
Giữ `.github/workflows/deploy-pages.yml`.
Settings → Pages → Source = GitHub Actions.
Commit vào `main` và chờ Actions deploy.

## G. Test bắt buộc
Thiết bị A:
1. Mở GitHub Pages.
2. Bấm Google.
3. Đăng nhập tài khoản thử.
4. Học/hoàn thành hoạt động.
5. Bấm `Lưu Cloud`.
6. Thấy `Đã lưu tiến độ lên Cloud`.

Thiết bị B / browser khác:
1. Mở cùng GitHub Pages.
2. Đăng nhập đúng Google Account.
3. V3.71 tải Cloud và reload.
4. Kiểm tra tiến độ, sao/xu, mastery, Farm/Village/Town.

Sau đó thử một Google Account khác: không được thấy dữ liệu của tài khoản đầu.

## H. Cơ chế an toàn
- Chưa cấu hình Firebase: app vẫn chạy local như V3.70.
- Mất mạng: dữ liệu local vẫn giữ.
- Cloud lỗi: không xóa local.
- Đăng xuất: local không bị xóa.
- Lần đầu chuyển từ V3.70 sang V3.71: nếu local có dữ liệu mà cloud chưa có, V3.71 upload local lên cloud.
- Không đặt service-account private key trong GitHub Pages.

## I. Lưu ý
V3.71 đồng bộ theo Google/Firebase UID. Dữ liệu học không phụ thuộc vào việc Chrome có đang bật Sync hay không.
