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

## Việc cần làm tiếp trên Mac mini M4 16 GB
1. Render lại ảnh 3D phương án 3 từ file 3d-nha-12x50.html.
2. Cài công cụ tạo ảnh AI chạy local (ví dụ Draw Things từ App Store, hoặc mflux chạy FLUX bằng MLX).
3. Dùng ảnh 3D khối làm ảnh gốc (img2img hoặc ControlNet depth) để sinh ảnh phối cảnh ngoại thất giống ảnh mẫu TikTok. Với 16 GB RAM nên dùng FLUX.1-schnell bản nén 4-bit.
4. Chủ nhà nói tiếng Việt thân mật (mày/tao).
