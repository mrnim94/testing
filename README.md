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

## Sleep.
SleepAction thực hiện sleep trong 1 khoảng thời gian nhất định khi hết thời gian thì nó thực hiện bước tiếp theo.

```sh
- webDriver: SleepAction #set timeout bắt element
  description: 'Thực hiện Sleep trong 120s'
  timeout: 120
```

| Key | Value |
| ------ | ------ |
| webDriver: SleepAction | thực hiện ngủ trong 1 thời gian nhất |
| description: | ghi lại miêu tả action cho bạn dễ hiểu |
| timeout: (s)| khai báo sẽ ngủ bao nhiêu giây |

## Implicit Wait Timeout.
SetImplicitWaitTimeout chờ đến khi hiển thị đầy đủ các element cho bước tiếp theo thì action bước tiếp theo.

```sh
- webDriver: SetImplicitWaitTimeout #set timeout bắt element
  description: 'Thực hiện Implicit Wait Timeout trong vòng 60s'
  timeout: 60
```

| Key | Value |
| ------ | ------ |
| webDriver: SetImplicitWaitTimeout | thực hiện chờ trong 1 thời gian nhất |
| description: | ghi lại miêu tả action cho bạn dễ hiểu |
| timeout: (s)| khai báo sẽ ngủ bao nhiêu giây |

## Switch Window.
SwitchWindow: Khi action đang làm việc ở tab 0 sau đó bạn ấn vào button mở ra 1 tab mới. Lúc đó cần sử dụng SwitchWindow chuyển action lên tab mới đó

```sh
- webDriver: SwitchWindow
  description: 'Chuyển tab'
  tab: 1
```

| Key | Value |
| ------ | ------ |
| webDriver: SwitchWindow | thực hiện chuyển tab |
| description: | ghi lại miêu tả action cho bạn dễ hiểu |
| tab: | thứ tự của tab muốn chuyển qua. Tab đầu tiên là 0 |

## JavaScript.
ExecuteScript sử dụng javascript để thực hiện action

```sh
- webDriver: ExecuteScript
  description: 'Click Next bằng JavaScript'
  script: document.querySelector('div[ng-click="setTab(3)"]').click()
```

| Key | Value |
| ------ | ------ |
| webDriver: ExecuteScript | thực hiện action bằng javascript |
| description: | ghi lại miêu tả action cho bạn dễ hiểu |
| script: | khai báo code javascript ở đây |

## Find Elements and action on these element.
FindElements: dùng để tìm ra 1 list gồm nhiều element cùng loại. Thực hiện kiểm tra các phần tử của list đó.

```sh
- webDriver: FindElements
  description: 'Check list flavor và Click Tạo VM flavor random'
  webElement:
    by: ByCSSSelector
    value: 'tr.ng-scope[ng-repeat="flavor in filteredFlavors"] > td[ng-bind="flavor.name"]'
    ignored: True
  checkElements:
    countElements: 18
    memberOfElements:
      - value: v1.small2x8.b100
      - value: v1.small1x1.b100
      - value: v1.large24x64.b100
    declareElement4Click: 'random'
  actions:
    - action: Click
```
| Key | Value |
| ------ | ------ |
| webDriver: FindElements | thực hiện tìm kiếm list element |
| description: | ghi lại miêu tả action cho bạn dễ hiểu |
| webElement| Khai báo các thông tin cho việc tìm kiếm |
| by| sẽ có 2 kiểu tìm là **ByCSSSelector** và **ByXPATH** |
| value | điền giá trị để action tìm kiếm |
| ignored| **True** thì nếu không tìm thấy sẽ dừng job và báo error, còn **False** là không tìm thấy sẽ bảo Warning và thực hiện bước tiếp theo |
| checkElements| khai báo kiểm tra |
| countElements:| Kiểm tra list có bao nhiều phần tử |
| memberOfElements:| Kiểm tra nội dung của các element |
| declareElement4Click: 'random'| chọn random 1 element cho click |
| action: Click| Click vào element đó |
