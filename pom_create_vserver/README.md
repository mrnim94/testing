# Automation Test Web UI

[![N|Solid](https://drive.nimtechnology.com/apps/theming/image/logo?useSvg=1&v=16)](https://----)

# Main!
Ở đây là nơi chưa file main để khởi chạy 1 Job test.
file ở đây nơi tập hợp các actions cho 1 bài test.

## file:
### -create_ubuntu_random_version.yml
Job test dùng để tạo VM bao gồm các action:

| Actions | Description |
| ------ | ------ |
| start_testing | đánh dấu 1 job bắt đầu. |
| login_portal | thực hiện diền user password và login |
| basic_configuration_create_vm| đặt tên và chọn hệ diều hành cho |
| instance_type_create_vm| chọn kiểu instance và RAM and CPU |
| volume_settings | Chọn volume mặc định |
| other_settings| Chọn network security, SecGroup và SSH key mặc định, Hiển thị giá. |
| summary_settings| Kiểm tra thông tin sau cùng |
| waiting_and_check| Chờ và Kiểm tra tạo đã active hay chưa |
| screen_shot| chụp ảnh |
| end_testing | đánh dấu 1 job kết thúc |


### -delete_ubuntu_random_version.yml

Delete VM theo chỉ định name.
| Actions | Description |
| ------ | ------ |
| start_testing | đánh dấu 1 job bắt đầu. |
| login_portal | thực hiện diền user password và login |
| delete_vm_on_list| xóa VM trong list và trong thùng rác |
| screen_shot| chụp ảnh |
| end_testing | đánh dấu 1 job kết thúc |
