# Báo cáo thực hành Day 3 — điền trực tiếp trong fork của bạn

**Cách dùng:** Thay mọi dấu `…` bằng bài làm thật của bạn trước khi nộp link fork trên [LMS](https://aithucchien.vinuni.edu.vn). Giữ nguyên bốn mục và bảng để coach đọc nhanh. Viết ngắn, cụ thể theo ảnh/vùng; không cần thuật ngữ chuyên sâu. Ví dụ trong [hướng dẫn mẫu](../../reports/REPORT_TEMPLATE.md) chỉ giúp hiểu cách điền, không phải câu trả lời để chép lại.

- Mã học viên theo lớp: 2A202604069
- Họ và tên: Vũ Gia Khang
- Ngày / CVAT local: 11/11/2026 / CVAT
- Công cụ đã dùng: CVAT (Brush, Polygon, Eraser)

Mã học viên là mã lớp cấp; không cần ghi họ tên trong report nếu kênh [LMS](https://aithucchien.vinuni.edu.vn) đã nhận diện bạn. Chỉ ghi công cụ thật sự đã dùng; không có SAM vẫn làm bài bình thường.

## 1. Bài đã nộp

Ghi tên ZIP đúng như file trong `submissions/` và số ảnh đã vẽ, Save. Chưa làm hoặc export lỗi thì ghi `chưa có`, không tạo ZIP rỗng. Cột điểm là điểm tối đa của task, **không phải điểm tự chấm**.

| Task | File ZIP đúng tên | Hoàn thành mấy ảnh | Điểm tối đa (coach chấm sau) |
| --- | --- | ---: | ---: |
| easy_semantic | easy_semantic.zip | 3 / 3 | 20 |
| medium_instance | medium_instance.zip | 3 / 3 | 32 |
| hard_panoptic | hard_panoptic.zip | 2 / 2 | 30 |
| cp1_holes | cp1_holes.zip | 1 / 1 | 3 |
| cp2_slice | cp2_slice.zip | 1 / 1 | 3 |
| cp5_occlusion | cp5_occlusion.zip | 1 / 1 | 3 |
| cp3_thin | cp3_thin.zip | 1 / 1 | 3 |
| cp4_curb | cp4_curb.zip | 1 / 1 | 3 |
| cp6_coverage | cp6_coverage.zip | 1 / 1 | 3 |
| **Tổng tối đa** | | | **100** |

Nếu export lỗi, ghi task, dữ liệu đã Save đến đâu và lỗi đã báo coach.

## 2. Một quyết định trước khi dùng gợi ý

Chọn object đầu tiên bạn tự vẽ ở `medium_instance`, trước khi xem bất kỳ đề xuất tự động nào cho object đó. Ghi ảnh/vị trí đủ để tìm lại; “quy tắc biên” là lý do bạn chọn hoặc dừng mask ở ranh đó.

- Ảnh, vị trí và object Medium đầu tiên tự vẽ: Ảnh 000000181542.jpg, xe ô tô con màu trắng ở làn giữa gần góc nhìn người lái.
- Class và quy tắc tôi dùng để chọn biên: Class car; quy tắc biên: bám sát theo mép thân xe, gương chiếu hậu và lốp tiếp xúc mặt đường; không cắt rời cửa sổ/kính xe ra khỏi thân xe.
- Nếu dùng gợi ý sau đó: vùng gợi ý sai/đúng, hành động sửa/giữ và lý do: Gợi ý nhận diện cơ bản khung xe nhưng viền mép bánh xe bị lẹm vào bóng râm mặt đường; đã dùng công cụ Brush/Polygon tinh chỉnh lại mép tiếp giáp giữa lốp xe và mặt đường.
- Nếu không dùng gợi ý: Đã dùng gợi ý của mô hình và chủ động tinh chỉnh thủ công các đường biên bằng Brush/Polygon như nêu trên.

## 3. Một lỗi tôi tìm thấy và sửa

Chọn một lỗi **có thật** trong bài. Nếu công cụ lỗi khiến bạn chưa sửa được, ghi rõ đã thử gì và cần coach hỗ trợ gì; không ghi “đã sửa” khi chưa sửa.

- Task/ảnh/vùng: Task easy_semantic, ảnh 7ee6d192-89e2408b.jpg, vùng sườn núi/đồi hai bên đường cao tốc.
- Lỗi thuộc loại: sai lớp / thiếu-thừa vật / gộp-tách / biên / phủ vùng / khác: Sai lớp (sườn núi bị nhầm lẫn giữa sidewalk và vegetation/road).
- Bằng chứng tôi nhìn thấy: Vùng đồi núi cây cỏ hai bên đường cao tốc ban đầu bị dán nhãn màu tím hồng của sidewalk dù đây là khu vực ngoài đô thị/không có vỉa hè cho người đi bộ.
- Quy tắc và hành động sửa: Dùng cọ tô lại toàn bộ khu vực sườn đồi và cây cối thành nhãn vegetation (107, 142, 35), mặt đường nhựa thành road (128, 64, 128), xóa bỏ hoàn toàn vùng sidewalk sai lệch.
- Sau sửa đã Save và export lại chưa? Đã Save và export lại thành công định dạng Segmentation mask 1.1 vào submissions/easy_semantic.zip.

Nếu bạn **đã xem Summary tự đánh giá trên GitHub Actions hoặc tự chạy script**, ghi ngắn một kết quả liên quan lỗi vừa sửa (ví dụ task, metric trước/sau nếu có): Chạy `python scripts/inspect_submissions.py --dir submissions` báo [OK] cho toàn bộ 9/9 tasks (0 errors). Cấu trúc file export đạt chuẩn Segmentation mask 1.1 và COCO 1.0, không còn lớp thừa/background hay lỗi phân giải.

## 4. Ba ca chưa chắc hoặc đã cân nhắc

Mỗi ca là một **vùng cụ thể** khiến bạn phải cân nhắc hai cách hiểu. Ghi dấu hiệu nhìn thấy hoặc quy tắc đã dùng, rồi nêu quyết định hoặc câu hỏi cho coach. Không cần ba lỗi; ca đã quyết định được cũng hợp lệ.

| Ảnh/vị trí | Hai cách hiểu có thể | Quy tắc/chứng cứ | Quyết định hoặc câu hỏi cho coach |
| --- | --- | --- | --- |
| 1 | Ảnh 7ee6d192-89e2408b (Easy): Các xe nhỏ phía xa ở đường chân trời | Có nên tô nhãn road đè lên hay tách nhãn riêng | Do schema Easy chỉ gồm 5 lớp (road, sidewalk, building, vegetation, sky) không có car, nên theo quy tắc phân đoạn ngữ cảnh, mặt đường phủ liên tục dưới phương tiện di chuyển. |
| 2 | Ảnh 7d83710e-4697c3b2 (cp4_curb): Ranh giới mép đường và vỉa hè cùng chất liệu asphalt | Khó phân biệt ranh giới vật liệu giữa mép đường và vỉa hè | Dựa vào độ cao mép bó vỉa (curb line) bê tông và công năng dành cho người đi bộ để kẻ ranh giới chia road và sidewalk. |
| 3 | Ảnh 000000350023 (Hard): Cột đèn và biển báo giao thông mảnh trên nền trời | Vẽ chi tiết từng nan cột hay gộp chung | Sử dụng polygon độ phân giải cao bám sát thân cột, phần nền trời lọt qua giữa các thanh kim loại vẫn gán nhãn sky. |
