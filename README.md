# Bài 3 : Ngăn chặn quá tải lưu trữ khi đồng bộ mã nguồn

 
## 1. Báo cáo I/O: Luồng dữ liệu (Ctrl+S ➔ Tích xanh)
  
    [Ctrl+S] -> (1) SSD Local -> (2) File Watcher -> (3) Sync Client (Diff/Hash) -> (4) Upload HTTPS -> (5) Tích xanh 
    
  Ghi đĩa: Nhấn Ctrl+S, Editor ghi dữ liệu trực tiếp xuống ổ SSD Local.
  
  Bắt sự kiện: Client đồng bộ (OneDrive/Drive) nhận tín hiệu thay đổi file từ hệ điều hành.
  
  Kiểm tra: Client băm dữ liệu (hash check), xác định phần thay đổi, đổi icon sang trạng thái đang đồng bộ
  
  Tải lên: Nén và upload các khối dữ liệu (chunks) qua HTTPS lên Cloud Server.
  
  Xác nhận: Server lưu thành công và trả về ACK ➔ Icon file đổi thành Tích xanh 

## 2. Xử lý bẫy node_modules & Hybrid Workflow 

  Loại trừ node_modules:
  
  Không đồng bộ folder node_modules lên Cloud Drive.
  
  Sử dụng Git + .gitignore để chỉ quản lý source code sạch và package.json (khi cần chỉ cần chạy npm install).
  
  Tiết kiệm dung lượng (Files On-Demand):
  
  Thư mục đang code: Chọn Always keep on this device để chạy tốc độ cao trên SSD.
  
  Tài liệu, assets cũ: Chuột phải chọn Free up space (biểu tượng đám mây ☁️) để giải phóng ổ cứng.
  
## 3. Sơ đồ tổ chức thư mục Cloud chuẩn 

  Plaintext
   Cloud Workspace/
  ├──  01_Code/                  # Source code thuần, package.json, script (không chứa node_modules)
  ├──  02_Docs/                  # SRS, API docs, tài liệu dự án (bật On-Demand)
  └──  03_Assets/                # File thiết kế (.fig, .psd), hình ảnh, video (bật On-Demand)
