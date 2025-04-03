### **RT-DETR: Bộ phát hiện thời gian thực dựa trên Transformer**  

Dòng mô hình **YOLO** đã trở thành khung phát hiện vật thể thời gian thực phổ biến nhất nhờ sự cân bằng hợp lý giữa tốc độ và độ chính xác. Tuy nhiên, chúng tôi nhận thấy rằng tốc độ và độ chính xác của YOLO bị ảnh hưởng tiêu cực bởi thuật toán **NMS (Non-Maximum Suppression)**.  

Gần đây, các bộ phát hiện dựa trên **Transformer (DETRs)** đã cung cấp một giải pháp thay thế bằng cách loại bỏ NMS. Tuy nhiên, chi phí tính toán cao khiến các mô hình này kém thực tế và không thể khai thác hoàn toàn lợi thế của việc loại bỏ NMS.  

Trong bài báo này, chúng tôi đề xuất **Real-Time DEtection TRansformer (RT-DETR)**, bộ phát hiện vật thể **thời gian thực đầu cuối (end-to-end)** đầu tiên (theo hiểu biết của chúng tôi) có thể giải quyết được vấn đề trên. RT-DETR được xây dựng theo hai bước dựa trên những cải tiến từ DETR:  
1. **Duy trì độ chính xác trong khi cải thiện tốc độ.**  
2. **Duy trì tốc độ trong khi cải thiện độ chính xác.**  

Cụ thể, chúng tôi thiết kế một **bộ mã hóa lai hiệu quả (efficient hybrid encoder)** để xử lý nhanh chóng các đặc trưng đa tỉ lệ bằng cách **tách biệt tương tác trong cùng một tỉ lệ (intra-scale interaction) và kết hợp chéo tỉ lệ (cross-scale fusion)** nhằm cải thiện tốc độ.  

Sau đó, chúng tôi đề xuất **cơ chế chọn truy vấn tối thiểu độ không chắc chắn (uncertainty-minimal query selection)** để cung cấp các truy vấn ban đầu có chất lượng cao hơn cho bộ giải mã (decoder), từ đó cải thiện độ chính xác.  

Ngoài ra, RT-DETR hỗ trợ **điều chỉnh tốc độ linh hoạt**, cho phép thay đổi số lượng lớp trong bộ giải mã mà không cần huấn luyện lại, giúp mô hình thích nghi với nhiều tình huống khác nhau.  

Các kết quả thử nghiệm trên COCO cho thấy:  
- **RT-DETR-R50** đạt **53.1% AP** với **108 FPS** trên GPU **T4**.  
- **RT-DETR-R101** đạt **54.3% AP** với **74 FPS**, vượt trội hơn các phiên bản YOLO tiên tiến trước đây về cả tốc độ lẫn độ chính xác.  
- **RT-DETR-R50** vượt trội hơn **DINO-R50** với **2.2% AP** cao hơn về độ chính xác và nhanh hơn **khoảng 21 lần** về FPS.  
- Sau khi được huấn luyện trước trên **Objects365**, **RT-DETR-R50** và **RT-DETR-R101** đạt **55.3% AP** và **56.2% AP**.  

👉 **Trang dự án**: [https://zhao-yian.github.io/RTDETR](https://zhao-yian.github.io/RTDETR)