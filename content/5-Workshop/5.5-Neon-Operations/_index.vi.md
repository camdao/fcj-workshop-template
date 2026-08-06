---
title : "Kiểm thử, vận hành và triển khai liên tục"
date : 2024-01-01
weight : 5
chapter : false
pre : " <b> 5.5. </b> "
---
### Mục tiêu

Trong phần này, bạn sẽ vận hành và kiểm tra hệ thống NeonFoodMap theo một luồng end-to-end rõ ràng. Nội dung được tổ chức theo từng bước, từ việc tạo ECS service, bật auto-scaling, cấu hình CloudFront, thiết lập CloudWatch, cho đến kiểm thử toàn bộ workflow người dùng và dọn dẹp tài nguyên nếu cần.

### Tổng quan luồng vận hành

Luồng thực hiện gồm các giai đoạn chính sau:

1. Khởi tạo ECS service và cấu hình rolling update
2. Bật auto-scaling cho backend service
3. Cấu hình CloudFront để phục vụ frontend và proxy API
4. Theo dõi tài nguyên bằng CloudWatch dashboard và alarm
5. Thiết lập log retention, VPC Flow Logs và cost monitoring
6. Chạy end-to-end testing trên các luồng quan trọng
7. Kết thúc bằng dọn dẹp tài nguyên nếu cần

### 5.5.1. Tạo backend ECS service và bật rolling update

1. Truy cập AWS ECS Console.
2. Chọn cluster `NeonFoodmap-cluster`.
3. Vào tab Services → Create.
4. Chọn task definition backend phù hợp.
5. Đặt service name theo chuẩn dự án, ví dụ `svc-neonfoodmap-be`.
6. Chọn số lượng task mong muốn là `2`.
7. Chọn launch type `FARGATE`.
8. Bật `Turn on ECS Exec` để thuận tiện cho troubleshooting sau này.
9. Bật `Availability Zone rebalancing` nếu muốn dịch chuyển task giữa các AZ hiệu quả hơn.
10. Chọn deployment strategy `Rolling update`.
11. Trong phần Networking:

- VPC: chọn VPC dự án
- Subnets: chọn 2 private subnets
- Security Group: chọn security group phù hợp

12. Trong phần Load balancing:

- Load balancer type: `Application Load Balancer`
- Chọn ALB đã tạo
- Chọn target group backend

13. Nhấn Create.

### 5.5.2. Cấu hình auto-scaling cho ECS service

1. Vào ECS Console → cluster → service `svc-neonfoodmap-be`.
2. Chuyển sang tab Service auto scaling.
3. Chọn Update.
4. Bật `Use service auto scaling`.
5. Thiết lập Capacity limits:
   - Minimum number of tasks: `2`
   - Maximum number of tasks: `6`
6. Tạo policy theo CPU target tracking:
   - Policy name: `cpu-70-target-tracking`
   - Metric: `ECSServiceAverageCPUUtilization`
   - Target value: `70`
   - Scale-out cooldown: `60` seconds
   - Scale-in cooldown: `300` seconds

#### Giải thích ý nghĩa các thông số

- `ECSServiceAverageCPUUtilization`: mức sử dụng CPU trung bình của service.
- `Target value = 70`: nếu CPU vượt ngưỡng, service sẽ scale out.
- `Scale-out cooldown = 60s`: sau khi scale out, hệ thống sẽ chờ 60 giây để task mới ổn định.
- `Scale-in cooldown = 300s`: khi tải giảm, hệ thống sẽ chờ 5 phút trước khi scale in để tránh flapping.

### 5.5.3. Cấu hình CloudFront để phục vụ frontend và proxy API

CloudFront đóng vai trò CDN cho frontend và cũng hỗ trợ routing tới backend thông qua ALB.

#### 5.5.3.1. Tạo CloudFront distribution cho frontend

1. Truy cập AWS CloudFront Console.
2. Chọn Create distribution.
3. Chọn Distribution type: `Single website or app`.
4. Thiết lập các thông số chính:
   - Distribution name: `neonfoodmap-frontend-cdn`
   - Description: `CloudFront CDN for NeonFoodmap Frontend and API`
   - Origin type: `Amazon S3`
   - S3 origin: chọn bucket frontend tương ứng
   - Allow private S3 bucket access to CloudFront: bật `Recommended`
5. Giữ nguyên các tùy chọn cache recommended settings.

#### 5.5.3.2. Cấu hình origin tới ALB

Sau khi distribution được tạo, cần vào tab Origins và chỉnh sửa origin liên kết với ALB.

- Chuyển protocol của origin sang `HTTP only` để tránh lỗi request format không đúng khi backend nhận traffic.

#### 5.5.3.3. Routing frontend và backend

- Frontend được phục vụ từ S3 bucket qua CloudFront.
- API request path `/api/*` được route về backend target group qua ALB.
- HTTPS được cung cấp qua CloudFront, trong khi backend bên trong mạng vẫn trao đổi qua HTTP nội bộ.

![Hình 3. Cấu hình CloudFront Distribution](/images/5-Workshop/5.5-neon-operations/placeholder-cloudfront.png)

### 5.5.4. Tạo CloudWatch dashboard và các alarm quan trọng

#### 5.5.4.1. Tạo dashboard

1. Mở CloudWatch Console.
2. Chọn Dashboards → Create dashboard.
3. Đặt tên: `NeonFoodMap-Operational-Dashboard`.
4. Tạo widget cho ECS CPU, Memory và Network metrics.
5. Tạo widget cho ALB target health, response time và request count.
6. Thêm widget cho S3 request count và bandwidth nếu cần.
7. Thêm log table widget cho log group backend/front-end.

#### 5.5.4.2. Tạo alarm cho lỗi 5xx

1. Chọn Alarm → Create alarm.
2. Namespace: `ApplicationELB`.
3. Metric: `HTTPCode_Target_5XX_Count`.
4. Đặt điều kiện: `Greater/Equal >= 10` trong `1 minute`.
5. Đặt tên cảnh báo: `ALB-5XX-Error-Alarm`.
6. Liên kết notification destination như SNS hoặc email.

![Hình 4. Tạo CloudWatch Dashboard và Alarm](/images/5-Workshop/5.5-neon-operations/placeholder-cloudwatch.png)

### 5.5.5. Thiết lập log retention, log subscription và VPC Flow Logs

1. Thiết lập log retention cho log group là `30 days`.
2. Tạo log group cho ALB access logs.
3. Tạo log group cho application logs.
4. Thiết lập log subscriptions để phát hiện bất thường và cảnh báo sớm.
5. Bật VPC Flow Logs để giám sát lưu lượng mạng ở mức L3/L4.
6. Tạo saved query trong CloudWatch Logs Insights để tái sử dụng khi xử lý sự cố.

![Hình 5. Thiết lập logging và flow log](/images/5-Workshop/5.5-neon-operations/placeholder-logging.png)

### 5.5.6. Thiết lập Cost Monitoring và Budget Alerts

1. Tạo AWS Budget với mức `15$/tháng`.
2. Cấu hình alert ở mức `50%`, `70%`, `90%`.
3. Bật Cost Anomaly Detection.
4. Tạo Cost Explorer reports.
5. Tag các tài nguyên với Owner/Project.
6. Xác nhận alert gửi tới email đã cấu hình.

![Hình 6. Cấu hình Cost Monitoring](/images/5-Workshop/5.5-neon-operations/placeholder-cost-monitoring.png)

### 5.5.7. Chạy end-to-end testing trên luồng người dùng

Mục tiêu của phần này là kiểm thử toàn bộ trải nghiệm người dùng từ frontend qua ALB, backend và các dịch vụ phụ trợ như S3, CloudFront, RDS.

#### 5.5.7.1. Test user registration → login flow

1. Truy cập frontend qua CloudFront.
2. Chọn tạo tài khoản.
3. Điền thông tin đầy đủ.
4. Đăng nhập bằng tài khoản vừa tạo.
5. Kiểm tra trạng thái đơn hàng hoặc giao dịch được cập nhật đúng.

Kết quả mong đợi:

- Tạo tài khoản thành công
- Đăng nhập thành công
- Hệ thống cập nhật trạng thái đơn hàng đúng như kỳ vọng

![Hình 7. Test luồng đăng ký và đăng nhập](/images/5-Workshop/5.5-neon-operations/placeholder-auth-flow.png)

#### 5.5.7.2. Test browse POIs và xem mô tả

1. Truy cập trang chủ.
2. Chọn một điểm đến trong bản đồ.
3. Kiểm tra thông tin mô tả, hình ảnh và dữ liệu liên quan.

Kết quả mong đợi:

- Dữ liệu điểm đến hiển thị đầy đủ
- Không có lỗi kết nối API
- Hình ảnh và mô tả tải bình thường

![Hình 8. Test browse POIs](/images/5-Workshop/5.5-neon-operations/placeholder-poi-flow.png)

#### 5.5.7.3. Test audio playback qua CloudFront

1. Chọn một POI để nghe thuyết minh.
2. Chạy audio playback.
3. Kiểm tra âm thanh phát ổn định và đúng file yêu cầu.

Kết quả mong đợi:

- Âm thanh phát mượt
- Không bị lag hoặc lỗi nội dung
- Backend và CloudFront đáp ứng đúng file media

![Hình 9. Test audio playback](/images/5-Workshop/5.5-neon-operations/placeholder-audio-flow.png)

#### 5.5.7.4. Test tour booking flow

1. Chọn một tour trên trang Tour.
2. Bắt đầu hành trình.
3. Di chuyển giữa các địa điểm trong tour.
4. Kiểm tra audio và trạng thái hành trình cập nhật đúng.

![Hình 10. Test tour booking flow](/images/5-Workshop/5.5-neon-operations/placeholder-tour-flow.png)

#### 5.5.7.5. Test payment integration sandbox

1. Chọn một dịch vụ hoặc đơn hàng cần thanh toán.
2. Chọn phương thức thanh toán sandbox.
3. Điền thông tin và xác nhận.
4. Kiểm tra trạng thái thanh toán và đơn hàng cập nhật thành công.

![Hình 11. Test payment integration](/images/5-Workshop/5.5-neon-operations/placeholder-payment-flow.png)

#### 5.5.7.6. Test error scenarios và mobile responsiveness

1. Nhập dữ liệu không hợp lệ để kiểm tra thông báo lỗi.
2. Mô phỏng timeout hoặc mất mạng.
3. Kiểm tra ứng dụng hiển thị thông báo rõ ràng và không sập.
4. Chạy kiểm tra responsive trên mobile và desktop.

![Hình 12. Test lỗi và responsive UI](/images/5-Workshop/5.5-neon-operations/placeholder-error-ui.png)

### 5.5.8. Kết luận vận hành

Sau khi hoàn thành các bước trên, hệ thống đã được kiểm thử và vận hành theo luồng production-like:

- ECS service chạy ổn định với auto-scaling
- CloudFront phục vụ frontend an toàn và nhanh hơn
- CloudWatch dashboard/alarms giúp phát hiện sự cố kịp thời
- Log và flow log hỗ trợ phân tích root cause
- End-to-end testing xác nhận trải nghiệm người dùng cơ bản hoạt động đúng

### 5.5.9. Dọn dẹp tài nguyên sau khi thực hành

Nếu không còn cần sử dụng tài nguyên, hãy thực hiện theo thứ tự sau để tránh phát sinh chi phí:

1. Xóa ECS service
2. Xóa task definition không còn dùng
3. Xóa ALB và target group
4. Xóa CloudFront distribution
5. Xóa CloudWatch alarm/dashboard nếu cần
6. Xóa log group không cần thiết
7. Xóa ECR repositories nếu không còn dùng

![Hình 13. Cleanup tài nguyên sau vận hành](/images/5-Workshop/5.5-neon-operations/placeholder-cleanup.png)
