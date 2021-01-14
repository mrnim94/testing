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

## Start Job.
Đây là action bắt buộc phải có trong 1 job test để đánh dấu việc ghi nhận 1 Job bắt đầu.
```sh
hooks:
  startTesting:
    - webDriver: Title
      description: 'Bắt đầu testing' ##giá trị ở đây có thể thay đổi
```

## End Job.
Đây là action bắt buộc phải có trong 1 job test để đánh dấu việc ghi nhận 1 Job kết thúc.
```sh
hooks:
  endTesting:
    - webDriver: Title # lấy tiêu đề
      description: 'Kết thúc testing'
```

## Get Title Website.
Title dùng để lấy Title  của trang mà action đang thực thi.
```sh
- webDriver: Title # lấy tiêu đề
  description: 'Lấy Tilte của Pages'
```
description: ghi lại miêu tả action cho bạn dễ hiểu

## Find Element and action on these element.
FindElement dùng để tìm đến vị trí trên web và thực hiện action nào đó lên vị trí đó.
có 3 action cụ thể:

 - Sendkeys: khi mà tìm đến ô username và gõ username vào ô đó.
 - Click: Click vào nút đăng nhập sau khi đã điền vào user và pass
 - Text: đăng nhập thành công thì tìm đến ô tên của user lấy tên của user ra kiểm tra

```sh
- webDriver: FindElement
  description: 'Tìm và Điền Tên Cho VM'
  webElement:
    by: ByCSSSelector
    value: 'input[ng-model="createServerRequest.name"]'
    ignored: True
  actions:
    - action: Sendkeys #đánh chữ vào ô input
      value : 'Ubuntu-SE-Random'
    - action: Click
   	- action: Text
      check: ACTIVE
```

| Key | Value |
| ------ | ------ |
| webDriver: FindElement | thực thi action tìm kiếm |
| description: | ghi lại miêu tả action cho bạn dễ hiểu |
| webElement| Khai báo các thông tin cho việc tìm kiếm |
| by| sẽ có 2 kiểu tìm là **ByCSSSelector** và **ByXPATH** |
| value | điền giá trị để action tìm kiếm |
| ignored| **True** thì nếu không tìm thấy sẽ dừng job và báo error, còn **False** là không tìm thấy sẽ bảo Warning và thực hiện bước tiếp theo |
| action: Sendkeys| gửi kí tự đã được khai báo ở **value** |
| action: Click| Click vào element đó |
| action: Text| thực hiện lấy text ở element đó, nếu có **check: ACTIVE** thì lấy text đã lấy được và so sánh với giá trị được khai báo ở **check** |