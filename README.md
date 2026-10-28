# Khoi Git

Bộ cài Khoi Git, app git có giao diện kiểu GitKraken.

## 1. Tải về

Vào [bản mới nhất](https://github.com/DinhVietKhoi/khoi-git-releases/releases/latest) và tải đúng file:

| Máy | File |
|---|---|
| Mac chip Apple (M1, M2, M3…) | `Khoi-Git-x.y.z-mac-arm64.dmg` |
| Mac Intel | `Khoi-Git-x.y.z-mac-x64.dmg` |
| Windows | `Khoi-Git-x.y.z-win-x64.exe` |
| Linux (x64) | `Khoi-Git-x.y.z-linux-x86_64.AppImage` (mọi bản Linux) hoặc `Khoi-Git-x.y.z-linux-amd64.deb` (Ubuntu, Debian) |

Không biết Mac chip gì: bấm biểu tượng Apple → About This Mac, dòng Chip ghi "Apple M…" là arm64, ghi "Intel" là x64.

## 2. Cài

**Mac:** mở file `.dmg`, kéo **Khoi Git** vào **Applications**, rồi Eject ổ đĩa Khoi Git trong Finder.

**Windows:** chạy file `.exe`. Nếu Windows SmartScreen chặn thì bấm **More info → Run anyway**.

**Linux:**

- AppImage: cho file quyền chạy rồi mở:

  ```bash
  chmod +x Khoi-Git-*.AppImage
  ./Khoi-Git-*.AppImage
  ```

  Nếu báo thiếu FUSE thì cài `libfuse2` (Ubuntu 22.04 trở lên: `sudo apt install libfuse2t64` hoặc `libfuse2`).
- .deb: `sudo apt install ./Khoi-Git-*.deb`, sau đó mở Khoi Git từ menu ứng dụng.
- Đăng nhập GitHub trên Linux cần kho mật khẩu của máy (GNOME Keyring hoặc KWallet). Không có thì dùng tài khoản `gh`.

## 3. Mở lần đầu trên Mac

App chưa được ký với Apple nên lần đầu macOS sẽ chặn:

- **Báo "Khoi Git is damaged… Move to Trash":** bấm **Cancel** (đừng bấm Move to Trash), mở Terminal và chạy:

  ```bash
  xattr -dr com.apple.quarantine "/Applications/Khoi Git.app"
  ```

  Sau đó mở lại Khoi Git. App không hỏng, lệnh này chỉ gỡ cờ "tải từ internet" mà macOS gắn vào app.

- **Báo "Apple could not verify…":** vào **System Settings → Privacy & Security**, kéo xuống mục Security, bấm **Open Anyway**.

Chỉ phải làm một lần.

## 4. Đăng nhập GitHub

Màn đầu tiên cho chọn:

- **Sign in with GitHub** (nên dùng): app hiện một mã ngắn kèm link github.com/login/device. Bấm link, dán mã vào, bấm **Authorize**, quay lại app là xong. Không cần cài thêm gì.
- **Use the gh account on this machine**: dùng tài khoản của [GitHub CLI](https://cli.github.com) nếu máy đã đăng nhập `gh`.
- **Continue without signing in**: vẫn dùng git bình thường, chỉ thiếu phần Pull Request, avatar và clone/push repo private qua HTTPS.

Token đăng nhập nằm trong Keychain trên Mac và được mã hoá bằng kho bảo mật của Windows trên Windows. Muốn thu hồi thì vào GitHub → Settings → Applications → Authorized OAuth Apps → Khoi Git → Revoke. Đổi tài khoản hoặc đăng xuất ở **Settings** trong app.

## 5. Mở repo

Khi chưa có repo nào, app mở trang **Home**. Bấm **+** trên thanh tab cũng ra trang này:

- Chọn repo có sẵn trong máy, hoặc **Chọn thư mục khác…** nếu repo nằm chỗ khác.
- Hoặc dán link để **clone**: `git@github.com:owner/repo.git` (SSH) hoặc `https://github.com/owner/repo.git` (HTTPS).

## 6. Clone, pull, push với GitHub

Vào **Settings → Kết nối Git tới GitHub** để xem máy đang dùng được cách nào:

- **HTTPS:** đã đăng nhập GitHub ở bước 4 là clone, pull, push được, không cần cài thêm.
- **SSH:** máy cần SSH key đã thêm vào GitHub. Chưa có thì bấm **Tạo SSH key** rồi **Thêm key lên GitHub**. Nếu app báo thiếu quyền thì chạy `gh auth refresh -h github.com -s admin:public_key` rồi bấm lại, hoặc bấm **Copy key** và dán ở trang [SSH keys của GitHub](https://github.com/settings/ssh/new).

## 7. Cập nhật

App tự kiểm tra bản mới khi mở và mỗi 6 tiếng. Có bản mới thì hiện dải thông báo trên đầu app:

Bấm **Tải**, chờ xong rồi bấm **Cài và khởi động lại**:

- **Mac** (từ bản 0.2.6): app tự thay bản trong Applications và mở lại. Nếu app không ghi được vào thư mục Applications, nó mở file `.dmg` để anh kéo Khoi Git vào Applications, chọn **Replace**, rồi mở lại app.
- **Windows:** bộ cài mới tự thay bản cũ.
- **Linux AppImage:** file mới thay file đang chạy rồi mở lại. Bản `.deb` thì cài lại bằng `sudo apt install ./Khoi-Git-*.deb`.

Danh sách repo, đăng nhập và cài đặt được giữ nguyên sau khi cập nhật.

## Gỡ cài đặt

**Mac:** kéo `Khoi Git` trong Applications vào Thùng rác. Muốn xoá sạch dữ liệu thì chạy:

```bash
rm -rf "$HOME/Library/Application Support/Khoi Git" ~/.khoi-git
```

**Windows:** gỡ trong Settings → Apps, rồi xoá thư mục `%USERPROFILE%\.khoi-git`.

**Linux:** xoá file AppImage, hoặc `sudo apt remove khoi-git` với bản .deb, rồi xoá `~/.khoi-git` và `~/.config/Khoi Git`.
