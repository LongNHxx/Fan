# Chuẩn bị 1 công tắc 4 kênh đã add vào home assistant
![z5441476049802_45fc2038ac1e1b1539334f124c978e64](https://github.com/LongNHxx/Fan/assets/102561460/23996156-7424-455c-8cfe-9963fdd1bc78)

# Tạo fan bằng công tắc 4 kênh
- sau khi mua công tắc về add home assistant rồi sửa ID thực thể cho các kênh tương ứng với các số như sau
  + kênh s1 (L1) - số 1: switch.hk_q1_so1
  + kênh s2 (L2) - số 2: switch.hk_q1_so2
  + kênh s3 (L3) - số 3: switch.hk_q1_so1
  + kênh s4 (L4) - đảo gió: switch.hk_q1_dao
 - các kênh trên đấu vào dây quạt số tương ứng các chức năng của quạt số. dây trung tính nối chung nhau
 - 
![z5441476053283_8b347e967f981eb28c83e233faa5fbb5](https://github.com/LongNHxx/Fan/assets/102561460/2e16ac55-ad86-47c0-a4a5-dfae62d2ad85)
![z5441476068096_5a5b2d68c2c476aeecf16990ccd272c8](https://github.com/LongNHxx/Fan/assets/102561460/55e5f7e0-89f6-4e7d-ad01-7024032ef191)

# Thêm đoạn code này vào configuration.yaml [https://github.com/LongNHxx/Fan/blob/main/configuration.yaml](url)

# Tạo automation rồi soạn thảo bằng yaml thêm đoạn code này [https://github.com/LongNHxx/Fan/blob/main/automation.yaml](url)

ok, xong vào khởi động lại homeassistant rồi vào thiết bị -> thực thể tìm fan.hk_fan1
# Thành quả
![z5441476067072_96fd9676abecfce16c229f43b9fe41ce](https://github.com/LongNHxx/Fan/assets/102561460/a8c889ea-6f09-4e44-8f62-0eb1839447dd)
![z5441476065204_0218eb9aaf795bddd71c8aaa7262194f](https://github.com/LongNHxx/Fan/assets/102561460/4da8aaae-3289-4ea8-93a1-e121beadaf76)
