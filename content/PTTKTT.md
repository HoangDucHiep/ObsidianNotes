### May
- PK: MaMay
- FK: MaNhomMay
- TenMay
- TrangThai
### NhomMay
- PK: MaNhomMay
- TenNhomMay
- GiaTienMay
### Log
- PK: MaLog
- FK: MaNguoiDung
- FK: MaMay
- ThaoTac

### PhienDangNhap
- PK: MaDangNhap
- FK: MaNguoiDung
- PK: MaMay
- ThoiGianDangNhap
- ThoiGianDangXuat
### TaiKhoan
- PK: MaTK
- HoTen
- LoaiTK
- SDT
- MatKhau
- TienTK

### TaiKhoan_Quyen
- FK: MaTK
- FK: MaQuyen

### Quyen
- PK: MaQuyen
- TenQuyen

### YeuCauKhieuNai
- PK: MaKN
- NoiDung
- NgayGui
- TrangThai
- PhanHoi

### YCKN_TK
- FK: MaKN
- FK: MaKhachHang

### ThongBao
- PK: MaThongBao
- TieuDe
- NoiDung
- NgayBatDau
- NgayKetThuc

### TaiKhoan_ThongBao
- FK: MaKhachHang
- FK: MaThongBao

### Order
- PK: MaOrder
- FK: MaKhachHang
- ThanhTien
- ThoiGianDat
- ThoiGianThanhToan

### OrderNhanVien
- FK: MaOrder
- FK: MaNhanVien

### Order_DichVu
- FK: MaOrder
- FK: MaDichVu

### DichVu
- PK: MaDichVu
- FK: MaNhomDichVu
- TenDichVu
- GiaDichVu
- AnhDichVu
- TrangThai

### NhomDichVu
- PK: MaNhom
- TenNhom

### ChiTietDichVu
- FK: MaHang
- FK: MaDichVu

### HangHoa
- PK: MaHang
- TenHang
- DonVi
- DonGiaNhap
- AnhHang

### BaoCao
- PK: MaBaoCao
- TenBaoCao
- NgayTao

### BaoCao_TonKho
- FK: MaBaoCao
- FK: MaHang

### BaoCao_DoanhThu
- FK: MaBaoCao
- FK: MaOrder


