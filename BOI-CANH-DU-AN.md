# Bối cảnh dự án: Nhà vườn 1 tầng mái Nhật, đất 12 x 50 m

## Yêu cầu của chủ nhà
- Đất 12 x 50 m. Nhà 1 tầng, mái Nhật 4 mái, tường trắng, mảng ốp gỗ, cửa kính khung đen, garage mái thép đen, sân vườn có hồ cá (giống ảnh mẫu TikTok, file anh-mau-tiktok.png trong thư mục này).
- Gian trước dài, gian ngang phía sau.
- 4 phòng ngủ, trong đó 2 phòng ngủ chính, mỗi phòng có WC riêng. Thêm 2 WC phụ riêng (WC phụ + WC khách).
- 1 phòng khách thông với bếp. Bếp có đảo dài và bàn ăn.
- 1 gian thờ đặt ở vị trí đầu tiên của nhà, phải tránh WC.
- Sân sau có sân phơi và chòi để nghỉ ngơi hoặc tiệc ngoài trời.
- Hẻm 0,5 m bên hông ra sân sau.
- Nội thất hiện đại tối giản, ít cây xanh, chỉ chậu nhỏ.

## Bố cục hiện tại (phương án 3), tính từ đường vào
| Khu | Sâu | Nội dung |
|---|---|---|
| Sân trước | 13 m | Cổng trượt 5 m, cổng bộ, garage 3,5 x 6, hồ cá |
| Gian trước | 12,5 m, rộng 7,5 m | Hiên 2,5; gian thờ 4,5 x 3,5 (trái) + sảnh vào 4,5 x 4 (phải); phòng khách + sinh hoạt 5,5 x 7,5 |
| Gian ngang | 13,8 m + hiên sau 1,8 m, rộng 11,5 m | Chừa hẻm 0,5 m bên phải |
| Sân sau | 8,9 m | Kho giặt, sân phơi, chòi gỗ 5 x 5 + quầy BBQ |

Gian ngang, chia 3 hàng:
- Hàng trước (sâu 6 m): ngủ 3 (3,2 m) | bếp 5,1 m có đảo 4,8 m + bàn ăn 8 ghế + giếng trời | ngủ 4 (3,2 m).
- Hàng giữa (sâu 2,2 m): kho | sảnh | WC khách.
- Hàng sau (sâu 5,6 m): ngủ chính 1 có WC riêng | sảnh sau, WC phụ, lối ra sân sau, kho nhỏ | ngủ chính 2 có WC riêng.
- Tất cả WC nằm ở nửa sau nhà, cách gian thờ hơn 16 m.

## File có sẵn trong thư mục này
- mat-bang-nha-12x50.html / .png: mặt bằng tổng thể, mặt bằng công năng, bảng diện tích, nội thất, dự toán thô.
- 3d-nha-12x50.html: mô hình khối Three.js, mở bằng trình duyệt. Tham số ?view=front|back|top|side và &roof=0 để ẩn mái.
- 3d-*.png: ảnh chụp mô hình 3D (bản cũ, cần render lại theo phương án 3).
- anh-mau-tiktok.png: ảnh mẫu chủ nhà gửi, dùng làm tham chiếu phong cách.

## VIỆC CẦN LÀM TRÊN MAC MINI M4 16 GB (làm theo đúng thứ tự)

Mục tiêu: tạo ảnh phối cảnh AI trông như ảnh chụp thật, giống anh-mau-tiktok.png.
KHÔNG vẽ lại mặt bằng. KHÔNG viết thêm Three.js. Hai việc đó đã xong ở máy kia.

### Bước 1: Cài mflux (chạy model FLUX bằng MLX của Apple)
```
brew install uv            # nếu chưa có uv
uv tool install --upgrade mflux
mflux-generate --help      # kiểm tra đã cài được
```
Dùng model FLUX.1-schnell. Model này không cần đăng nhập Hugging Face, lần đầu chạy tải khoảng 20–30 GB.
Luôn thêm `--quantize 4` để vừa RAM 16 GB. Trước khi chạy, đóng Chrome và các app nặng.

### Bước 2: Sinh ảnh từ chữ (text-to-image), 4 seed để chọn
```
mflux-generate --model schnell --quantize 4 --steps 4 \
  --width 1344 --height 768 --seed 1 \
  --prompt "aerial drone photo of a modern single-storey Vietnamese garden villa, dark grey flat-tile hip roof (Japanese style) with wide eaves, white rendered walls, warm wood cladding panel at the entrance, black-framed floor-to-ceiling glass doors, a round porthole window on the side wall, long front garden with large concrete paving slabs and grass joints, small koi pond with rocks, black steel cantilever carport with a white car, white boundary walls and black sliding gate, tropical trees and palms, soft afternoon sunlight, architectural photography, photorealistic, 35mm" \
  --output ra-anh/ngoai-that-seed1.png
```
Chạy lại với --seed 2, 3, 4. Tạo thư mục ra-anh trước khi chạy.

Thêm 2 góc khác, đổi phần đầu prompt:
- Sân sau: "rear garden view of ... covered rear veranda, a 5x5 m timber gazebo with dark tile hip roof, BBQ counter, clothes drying yard, lawn, string lights, evening golden hour ..."
- Nội thất: "interior photo, open-plan living room connected to kitchen, 4.8 m long kitchen island in light oak and white quartz, 8-seat oak dining table, skylight above, warm white walls, light oak floor, warm grey sofa, matte black fixtures, a few small potted plants, minimalist, natural daylight ..."

### Bước 3: Bám hình khối thật của nhà (img2img từ ảnh 3D)
Dùng ảnh mô hình khối làm ảnh gốc để AI giữ đúng tỉ lệ nhà:
```
mflux-generate --model schnell --quantize 4 --steps 4 \
  --width 1344 --height 768 --seed 1 \
  --image-path 3d-goc-truoc.png --image-strength 0.45 \
  --prompt "<cùng prompt ngoại thất ở bước 2>" \
  --output ra-anh/img2img-goc-truoc.png
```
Nếu tên cờ khác, xem `mflux-generate --help` (các bản mflux có thể đổi tên cờ img2img).
image-strength thấp (0,3) thì giữ hình khối nhiều hơn, cao (0,6) thì ảnh đẹp hơn nhưng lệch khối hơn.
Lưu ý: các ảnh 3d-*.png hiện là BỐ CỤC CŨ. Chỉ dùng chúng cho phối cảnh ngoại thất tổng thể, vì hình khối bên ngoài gần giống.

### Bước 4: Gom kết quả
Tạo file so-sanh.html hiển thị lưới tất cả ảnh trong ra-anh/ kèm seed và prompt, để chủ nhà chọn.

### Phương án thay thế nếu không muốn dùng dòng lệnh
Cài app Draw Things (miễn phí, App Store). Trong app chọn model FLUX.1 [schnell] bản 8-bit hoặc 4-bit, dán prompt ở trên.
Muốn bám ảnh 3D thì dùng chế độ image-to-image với strength khoảng 40–50%.

Chủ nhà nói tiếng Việt thân mật (mày/tao).
