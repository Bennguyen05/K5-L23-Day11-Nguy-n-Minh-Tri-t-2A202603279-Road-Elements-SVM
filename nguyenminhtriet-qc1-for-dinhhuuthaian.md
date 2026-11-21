# Phiếu QC 1 — Road v1.0

Lô được kiểm (học viên): Đinh Hữu Thái An        Người kiểm (học viên): Nguyễn Minh Triết (2A202603279)  
Ngày: 21/11/2026                                 Phiên bản guideline: Road v1.0  
File được kiểm (tên + `revision` trong manifest): `job_11_annotations_2026_11_20_11_54_01_cvat_for_images_1.1.zip` (export job front, 12 ảnh A01–A12; chưa kèm manifest nên không có `revision`). Phạm vi kiểm theo yêu cầu của coach: A01–A06  
Số ảnh kiểm: 6 (A01–A06) (+ 0 ảnh thêm)   Số nhãn đã kiểm (shape + tag): 53 shape + 24 tag = **77**

Ghi chú về id: cột "Nhãn (label, id)" dùng số thứ tự của shape trong ảnh ở file export (đếm từ 0, giống số `#` mà `road_check lint` in ra), không phải ID hiển thị trong CVAT.

## Tổng hợp theo mã
| Mã | Loại lỗi | Số mục kiểm | Số lỗi | Mức |
| --- | --- | ---: | ---: | --- |
| QC1-01 tag camera | sai thuộc tính / bỏ sót | 24 | 0 | nặng |
| QC1-02 đủ L1, R1 | bỏ sót | 12 | 0 | nặng |
| QC1-03 position | sai thuộc tính / thừa | 15 | 2 | nặng |
| QC1-04 tâm vạch, chiều, điểm dừng | sai phạm vi / bỏ sót | 17 | 3 | chính |
| QC1-05 vạch đứt, che | sai phạm vi / sai thuộc tính | 15 | 0 | chính |
| QC1-06 style, color, kind | sai thuộc tính | 15 | 1 | chính |
| QC1-07 vùng lái | sai phạm vi / bỏ sót / thừa | 18 | 3 | chính |
| QC1-08 đèn, màu | bỏ sót / sai phạm vi / sai thuộc tính | 8 | 0 | nặng / chính |
| QC1-09 facing, type, group, biển phụ | sai thuộc tính | 18 | 1 | chính |
| QC1-10 hình in, đủ biển | bỏ sót / sai phạm vi | 10 | 1 | chính |
| QC1-11 fisheye | sai phạm vi / sai thuộc tính | 0 | 0 | chính |
| QC1-12 file | lỗi file | 1 | 0 | nhẹ / nặng |

Cách đếm số mục kiểm: QC1-01 = 4 tag × 6 ảnh; QC1-02 = L1 + R1 × 6 ảnh; QC1-03/05/06 = 15 lane; QC1-04 = 15 lane + 2 road_curb; QC1-07 = 14 drivable + 4 crosswalk; QC1-08 = 8 đèn; QC1-09 = 8 đèn + 10 biển; QC1-10 = 10 biển; QC1-11 = 0 vì 6 ảnh kiểm đều là front.

## Danh sách lỗi (mỗi lỗi một dòng)
| # | Mã | Ảnh | Nhãn (label, id) | Mức | Mô tả ngắn |
| --- | --- | --- | --- | --- | --- |
| 1 | QC1-03 | A03 | lane, 0 | nặng | Vạch trắng đứt ngăn làn bên phải với dải đỗ xe gán `R1`; R1 thật là lane 7 (vạch giữa) nên lane 0 phải là `R2`. Ảnh có hai lane cùng `R1` |
| 2 | QC1-03 | A06 | lane, 0 | nặng | Vạch trắng bên phải (từ góc phải dưới lên xa) gán `L1`; nằm bên phải làn đang đi nên phải là `R1`. Ảnh có hai lane cùng `L1` và thiếu R1 |
| 3 | QC1-04 | A01 | lane, 0 | chính | L1 vẽ từ xa về gần: điểm đầu (374,498) ở xa, điểm cuối (106,720) sát xe |
| 4 | QC1-04 | A03 | lane, 6 | chính | L1 đặt trên nét phải của vạch vàng đôi (x≈225 ở đáy ảnh), không phải giữa hai nét (x≈195): lệch khoảng 30 px |
| 5 | QC1-04 | A05 | road_curb, 0 | chính | road_curb vẽ từ xa về gần: điểm đầu (909,341) cạnh xe SUV, điểm cuối (1280,429) sát xe |
| 6 | QC1-06 | A03 | lane, 6 | chính | Vạch vàng đôi gán `kind = single`, phải là `double` |
| 7 | QC1-07 | A04 | crosswalk, 5 | chính | Polygon crosswalk phủ lên làn xe đạp sơn xanh bên phải; chỗ đó không có vạch ngựa vằn (thừa) |
| 8 | QC1-07 | A05 | crosswalk, 2 | chính | Polygon crosswalk phủ lên vỉa hè bên phải; ảnh không có vạch ngựa vằn (thừa) |
| 9 | QC1-07 | A06 | crosswalk, 14 | chính | Polygon crosswalk thứ hai phủ dải vỉa hè dọc lề phải, không phải vạch ngựa vằn (thừa); crosswalk thật đã có ở polygon 13 |
| 10 | QC1-09 | A06 | traffic_sign, 5 | chính | Biển "ONE WAY" gán `group = warning`; theo bảng nhóm biển Mỹ trong guideline phải là `mandatory` |
| 11 | QC1-10 | A01 | (thiếu) traffic_sign | chính | Thiếu biển xanh nhỏ ở xa, cạnh lan can trái, khoảng x 432–450, y 464–486 (cao khoảng 22 px ≥ 8 px) |

Ảnh không có lỗi: **A02**. Đã kiểm 4 tag và 6 shape (3 lane, 3 drivable): L1 đứt, R1 liền mép, L2 đứt đúng vị trí và thuộc tính; drivable `direct` / `alternative` đúng làn, không tràn lề.

## Ca mơ hồ
| Ảnh | Câu hỏi cho lead | Lời đáp (nếu có) |
| --- | --- | --- |
| A04, A05, A06 | Crosswalk gán thừa không có mã riêng trong Road v1.0; phiếu xếp vào QC1-07 (lỗi vùng, loại "thừa"). Có đúng mã không? | |
| A05 | Không có vạch sơn nên thiếu L1/R1. Không tính QC1-02 (miễn theo CHECKPOINTS) | |
| A06 | Polygon drivable 3 (`alternative`, góc trái dưới) nằm phía bên kia hàng cột cầu, nơi xe chạy ngược chiều. Đây có phải làn cùng chiều không? | |
| A06 | Đèn đi bộ (traffic_light 6) đang hiện hình người đi bộ trắng, gán `color = unknown`. Nên để `unknown` hay `green`? | |
| A04 | R2 (vạch ngăn làn xe đạp) gán `kind = double`. Đoạn gần có hai nét nên chấp nhận được; không tính lỗi | |
| — | Theo yêu cầu của coach, phiếu chỉ kiểm 6 ảnh A01–A06. File nhận là export job front, tên chưa theo chuẩn `<tên>-front.zip` và chưa kèm manifest; không ảnh hưởng nội dung nhãn đã kiểm | |

## Quyết định
Lỗi nặng: **2**   Lỗi chính: **9** / **77** nhãn = **11,7 %**   Lỗi nhẹ: **0**   Ca chờ lead: **3**  
Quyết định (Release / Hold / Rework): **Rework**  
Lý do (theo luật của phiếu): còn 2 lỗi nặng QC1-03 (A03 lane 0, A06 lane 0). Chỉ một lỗi nặng đã đủ Rework. Ngoài ra lỗi chính 9/77 = 11,7 % cũng vượt ngưỡng 5 %. Các ca chờ lead không đổi kết luận, nên không chọn Hold.

Loại lỗi: bỏ sót = thiếu nhãn phải có; thừa = gán cái không phải đối tượng; sai phạm vi = hình lệch, sai chiều, dừng sai chỗ, tràn vùng. Ba loại này theo cách chia lỗi gán nhãn của ISO/IEC 5259-4 (mục 8.4.2); "sai thuộc tính" và "lỗi file" là khóa học thêm. Cách xếp mức: [thang mức lỗi](../docs/qc_severity_road_v1.0.md).
