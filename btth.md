## phần 1

**tình huống 1:** typosquatting (phishing). domain là githuh-security.com, sai chính tả (githuh thay vì github) và không phải github.com. còn bắt nhập lại mật khẩu.

**tình huống 2:** mã độc crack. tắt windows defender để mã độc không bị phát hiện, máy mất bảo vệ nên mã độc chạy tự do, ăn cắp mật khẩu, dữ liệu.

**quy tắc 5 không:**
- tình huống 1: không bấm link lạ / không nhập mật khẩu qua link trong email
- tình huống 2: không tải phần mềm crack, không tắt antivirus

**4 bước cấp cứu:**
1. ngắt mạng (wifi, dây mạng)
2. dùng thiết bị sạch khác để đổi mật khẩu các tài khoản quan trọng
3. quét và diệt mã độc, nặng thì cài lại máy
4. báo cho nhóm / quản trị viên

## phần 2

- email bị lộ thì github và vercel bị lộ theo vì dùng chung mật khẩu. kiểu tấn công là credential stuffing.
- zero-knowledge: dữ liệu được mã hóa ngay trên máy người dùng bằng master password. server chỉ lưu dữ liệu đã mã hóa và không có khóa, nên hacker lấy được cũng không đọc được.

| thông số | giá trị cấu hình |
|---|---|
| độ dài | 16 ký tự trở lên (chọn 20) |
| chữ hoa (A–Z) | bật |
| chữ thường (a–z) | bật |
| chữ số (0–9) | bật |
| ký tự đặc biệt | bật |

## phần 3

sms otp có 2 nhược điểm:
1. dễ bị sim swap (kẻ xấu chiếm số điện thoại)
2. tin nhắn có thể bị chặn, đọc trộm và phụ thuộc sóng điện thoại

authenticator app (totp) tạo mã ngay trên máy, không qua mạng viễn thông, mã đổi mỗi 30 giây nên an toàn hơn.

**các bước bật 2fa:**
1. vào github, mở settings
2. chọn password and authentication
3. bấm enable two-factor authentication
4. chọn authenticator app
5. mở google authenticator, quét mã qr
6. app hiện mã 6 số, nhập vào github để xác nhận

**mã khôi phục:**
- nên lưu: trong password manager (bitwarden) hoặc in ra giấy cất nơi an toàn
- không nên lưu: email, tin nhắn zalo, ảnh chụp màn hình, file trong repo hay chỗ công khai

## phần 4

2 secrets bị hardcode: `API_KEY` và `DB_PASSWORD`

**code sau khi sửa:**

```js
require("dotenv").config();

const API_KEY = process.env.API_KEY;
const DB_PASSWORD = process.env.DB_PASSWORD;

function connectDatabase() {
  return connect(DB_PASSWORD);
}
```

**.env**

```
API_KEY=sk-proj-abc123456789
DB_PASSWORD=SmartCampus@2026
```

**.gitignore**

```
.env
node_modules/
```

**.env.example**

```
API_KEY=
DB_PASSWORD=
```

**4 bước kiểm tra trước khi push:**
1. kiểm tra .gitignore đã có .env
2. chạy git status, git diff xem file nào sắp push, không có .env
3. tìm trong code còn secret nào sót không (password, key, token)
4. kiểm tra lịch sử commit xem đã lỡ commit secret chưa, nếu có thì đổi key và mật khẩu mới