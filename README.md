# Automation Test Web UI

[![N|Solid](https://drive.nimtechnology.com/apps/theming/image/logo?useSvg=1&v=16)](https://----)

Đây là script test được thiết kế viết theo định dạng file yaml.

# Main!
- Khai báo main chính:
```sh
version: 0.0
nameTest: DeleteUbuntuRandomVersion
browser: chome
web: "https://portal3.vngcloud.vn/servers/list.html"
resizeWindow:
  name: thangta
  width: 500
  height: 300
actions:
  - start_testing
  - login_portal
  - delete_vm_on_list
  - screen_shot
  - end_testing
```

Giải thích:
| Key | Value |
| ------ | ------ |
| version | Đánh version cho file script |
| nameTest | Đặt tên cho bài test |
| browser | Browser sử dụng để chạy bài test |
| web | links Để tiến hành cho bài test |
| resizeWindow | Size của số của browser |
| actions | Các bước test của 1 bài test |

Hình ảnh của POM test chứa nhiều bài test
![enter image description here](https://github.com/mrnim94/testing/raw/master/document/image/trong%201%20POM.PNG)

# Actions!
Thư mục actions là nơi tập hợp của các bước test
![enter image description here](https://github.com/mrnim94/testing/raw/master/document/image/trong%20actions.PNG)

Chi tiết của 1 action
![enter image description here](https://github.com/mrnim94/testing/raw/master/document/image/Chi%20ti%C3%AA%CC%81t%20trong%201%20action.PNG)

# Features!