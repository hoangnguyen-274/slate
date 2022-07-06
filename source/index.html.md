---
title: API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell
  - python
  - javascript

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/slatedocs/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true

code_clipboard: true

meta:
  - name: description
    content: Documentation for the Kittn API
---

Tham khảo tài liệu mô tả API Fiin v1.3
[https://docs.google.com/document/d/1NB0qo-ct1N9jWARxxmZHKApLWU6tI6zx/edit#heading=h.mmhpnqp6zume](https://docs.google.com/document/d/1NB0qo-ct1N9jWARxxmZHKApLWU6tI6zx/edit#heading=h.mmhpnqp6zume)

# Giới thiệu chung

## Mục tiêu và phạm vi tài liệu

Mục tiêu của tài liệu là cung cấp thông tin về tính năng của module EKYC mà Techainer cung cấp và cách thức để Fiin tích hợp vào hệ thống của mình.

Nội dung tài liệu tập trung vào liệt kê trường hợp sử dụng, cách thức kiểm thử và đánh giá kết quả các tính năng của module EKYC bao gồm

- Mô tả module eKYC
- Format yêu cầu và trả về
- Xác thực Token
- Mô tả các API sử dụng
- Giới hạn CCU
- Lỗi (error)

Thuật ngữ và các từ viết tắt

|STT|Thuật ngữ/ Viết tắt|Mô tả |
|---|---|---|
|1|	AI|	Artificial Intelligence:  Trí tuệ nhân tạo|
|2|	OCR|	Optical Character Recognition : Nhận dạng ký tự quang học|
|3|	Ảnh chân dung|	Là ảnh chụp khuôn mặt người dùng.|
|4|	Ảnh GTTT|	Là ảnh chụp giấy tờ tùy thân của người dùng (Mặt trước, mặt sau hoặc cả hai mặt trong cùng một bức ảnh)|

# Mô tả module eKYC

## Tổng quan

**Module EKYC do Techainer cung cấp** cho phép người dùng đăng tải ảnh/video chân dung khuôn mặt và ảnh giấy tờ tùy thân rồi dùng các module AI để trích xuất thông tin trên giấy tờ và so khớp khuôn mặt trên giấy tờ tùy thân và ảnh/video chân dung khuôn mặt hiện tại để xác nhận đây là cùng một người.

Các loại GTTT mà API hỗ trợ:

    - Chứng minh nhân dân 9 số
    - Chứng minh nhân dân 12 số
    - Căn cước công dân
    - Căn cước công dân gắn chip
    - Hộ chiếu

## Các API sử dụng

|STT | Tên API | Chức năng | URL|
|--- | --- | --- | ---|
|1 | Đăng ký người dùng bằng eKYC với ảnh | Hệ thống cung cấp API nhận và so sánh ảnh chân dung với   ảnh GTTT | <IP>/call/register_ekyc_front_back_face|
|2 | Đăng ký người dùng bằng eKYC với video | Hệ thống cung cấp API nhận và so sánh video chân dung   với ảnh GTTT | <IP>/call/register_ekyc_front_back_face_video|
|3 | Tạo mới thông tin trên hệ thống dữ liệu có sẵn | Hệ thống cung cấp API để đăng ký hoặc thêm mới ảnh vân   tay và ảnh chân dung | <IP>/call/register_user_face|
|4 | So sánh ảnh chân dung với ảnh GTTT | Hệ thống cung cấp API nhận và so sánh ảnh chân dung với   ảnh GTTT | <IP>/call/check_match_image_card_image_general|
|5 | So sánh ảnh chân dung với ảnh chân chung đã lưu trong   hệ thống | Hệ thống cung cấp API nhận và so sánh ảnh chân dung với   dữ liệu có sẵn | <IP>/call/verify_user_face|
|6 | Khởi tạo/cập nhật ảnh chân dung trong cơ sở dữ liệu bên   thứ 3 | Hệ thống cung cấp API khởi tạo/cập nhật ảnh chân dung   trong cơ sở dữ liệu bên thứ 3 | <IP>/call/register_user_face_third_party|
|7 | Truy vấn người dùng bằng ảnh chân dung | Hệ thống cung cấp API để truy vấn người dùng bằng ảnh   chân dung. | <IP>/call/search_face/|
|8 | Truy vấn ảnh chân dung và ảnh vân tay của khách hàng | Hệ thống cung cấp API để truy vấn ảnh chân dung và ảnh   vân tay của khách hàng. | <IP>/call/get_all_face_of_user|
|9 | Xóa ảnh chân dung và ảnh vân tay | Hệ thống cung cấp API để xóa ảnh chân   dung của khách hàng. | <IP>/call/delete_user_face/|
|10 | Trích xuất thông tin giấy tờ tùy thân | Trả về các trường thông tin trên hình ảnh của giấy tờ   tùy thân | <IP>/call/predict|


# Request, response format

You should use a `Content-Type: application/json` header with all PUT and POST
requests except when uploading documents or live photos. For these requests,
use a `Content-Type: multipart/form-data` header.

Responses return JSON with a consistent structure, except downloads.

You must make all your requests to the API over HTTPS and TLS 1.2, with
Server Name Indication enabled. Any requests made over HTTP will fail.

## API Token

Các header sau là bắt buộc để call được API thành công, x-api-key được Techainer cung cấp để kiểm thử API:

|Key | Value|
|--- | ---|
|Accept | */*|
|Accept-Encoding | gzip, deflate, br|
|Connection | keep-alive|
|x-api-key | feda33e3-6c9e-4807-bee9-ba84015ed07a|


## Response format

Đầu ra của API là dữ liệu theo định dạng JSON với cấu trúc được mô tả dưới đây:

|STT | Tên | Loại dữ liệu | Mô tả|
|--- | --- | --- | ---|
|1 | output | Dictionary | Chi tiết mô tả bên dưới|
|2 | time | Float | Thời gian xử lý của API|
|3 | api_version | String | Version của API đang chạy. Dùng để debug|
|4 | mlchain_version | String | Version sử dụng MLChain hiện tại. Dùng để debug|
|5 | request_id | String | Mã ID được tạo ra cho yêu cầu tương ứng|
|6 | error | String | Lỗi API trả về (lỗi hệ thống được mô tả ở bảng d)|
|7 | code | String | Mã code trả về|


# Postman Collection

(Cho cái nút bấm cái là chạy được Postman collection)

# Mô tả các API sử dụng

## **Đăng ký người dùng bằng eKYC với ảnh**

```python
import request
response = request.request()
```

`POST | <IP>/call/register_ekyc_front_back_face`

### Thông tin tổng quan

|Tên | Đăng ký người dùng bằng EKYC với ảnh|
|--- | ---|
|Mô tả | Hệ thống cung cấp API nhận và so sánh ảnh chân dung với ảnh GTTT|
|Tác nhân | API Client|
|Trigger | API được gọi|
|Điều kiện trước | Đầu vào theo đúng quy ước cho từng API.|
|Điều kiện sau | Kết quả trả về bao gồm khớp/không khớp, phần trăm giống nhau và độ tự tin|

### Thông tin kết nối

|URL | <IP>/call/register_ekyc_front_back_face|
|--- | ---|
|Method | POST|
|Request Content-type | multipart/form-data|
|Response Content-type | JSON|
|Remark | Đăng ký người dùng bằng eKYC|

### Đầu vào

|STT | Tham số | Ý nghĩa | Mô tả | Bắt buộc|
|--- | --- | --- | --- | ---|
|1 | image_card1 | Ảnh mặt trước GTTT mặt chứa ảnh chân dung (khuôn mặt) | Định dạng:Image: JPG, PNG, JPEG, Base64URL: HTTP, HTTPS của các loại trên | Có|
|2 | image_card2 | Ảnh mặt sau GTTT mặt chứa ảnh chân dung (khuôn mặt) | Định dạng:Image: JPG, PNG, JPEG, Base64URL: HTTP, HTTPS của các loại trên | Có|
|3 | user_id | ID của người dùng | Kiểu dữ liệu: String | Có|
|4 | image_general | Ảnh chân dung | Định dạng:Image: JPG, PNG, JPEGBase64URL: HTTP, HTTPS của các loại trên. | Có|
|5 | check_rotate | Check_rotate sẽ kiểm tra xem đầu vào có quay sai hướng (góc 90, 180, 270 độ). thì quay trở lại góc 0 độ | Mặc định: True=> False: Không thực hiện chức năng Kiểu dữ liệu: Boolean | Không|
|6 | threshold | Ngưỡng cho phép việc khớp độ giống nhau giữa ảnh chân dung và ảnh chân dung trên GTTT | Dịnh dạng: FloatMặc định: 0.5. Có giá trị từ 0 đến 1. | Không|


### Đầu ra

Đầu ra là các phần tử bao gồm:

|STT | Tên | Loại dữ liệu | Mô tả|
|--- | --- | --- | ---|
|1 | output | Dictionary | Chi tiết mô tả bên dưới|
|2 | time | Float | Thời gian xử lý của API|
|3 | api_version | String | Version của API đang chạy. Dùng để debug|
|4 | mlchain_version | String | Version sử dụng MLChain hiện tại. Dùng để debug|
|5 | request_id | String | Mã ID được tạo ra cho yêu cầu tương ứng|
|6 | error | String | Lỗi API trả về (lỗi hệ thống được mô tả ở bảng d)|
|7 | code | String | Mã code trả về|



**Các thuộc tính của giá trị “output”**

Tùy vào loại GTTT sử dụng, các trường thông tin được trích xuất được mô tả như sau:


**Chứng minh nhân dân mặt trước**

|Tên trường | Kiểu dữ liệu | Mô tả|
|--- | --- | ---|
|class_name | String | Loại GTTT được trích xuất|
|liveness | String | Độ thật của GTTT(Liveness không được bật - Auto return True)|
|id | String | ID của thẻ GTTT|
|ho_ten | String | Họ tên được trích xuất|
|ngay_sinh | String | Ngày sinh được trích xuất|
|nguyen_quan | String | Nguyên quán|
|ho_khau_thuong_tru | String | HKTT được trích xuất|


### 3. Các trường thông tin chung trả về

|Tên trường | Kiểu dữ liệu | Mô tả|
|--- | --- | ---|
|value | String | • value: Giá trị nhận dạng được trên đầu vào, trả về N/A nếu không phát   hiện được thông tin.|
|confidence | String | • confidence: Độ tự tin trong dự đoán của model AI, giá trị từ 0-> 1   biểu thị độ tự tin tăng dần.|
|value_unidecode | String | • value_unidecode: Giá trị dưới dạng unidecode|
|normalized | String | • normalized: Đưa giá trị về dạng thống nhất gồm các trường thông tin   tương ứng|
| |  | |
|similarity | String | • similarity: Kết quả so sánh phần trăm giống nhau, giá trị từ 0->1   biểu thị độ tương đồng tăng dần.|
|code | String | • code: Chuẩn hóa trường thông tin theo dạng mã số|
|validate | String | • validate: Xác thực thẻ GTTT|
|is_valid | Boolean | • is_valid: Giá trị hợp lệ  true: Hợp lệfalse: Không hợp lệ|
|liveness | String | • liveness: Độ thật của GTTT(Liveness không được bật - Auto return True)   true: Hợp lệfalse: Không hợp lệ|


### **3.1. Đầu ra “validate” của các trường thông tin tương ứng**

### **3.2. Đầu ra “normalized” của các trường thông tin tương ứng**

### **Phần tử 2 - So sánh khuôn mặt**
### **Phần tử 3 - Mã lỗi “error”**

|Error Code | Thông báo | Ý nghĩa|
|--- | --- | ---|
|0 | There's no face on capture and card image | Lỗi không tìm thấy mặt trong ảnh chân dung khuôn mặt và ảnh giấy tờ tùy   thân|
|1 | There's no face on capture image | Lỗi không tìm thấy mặt trong ảnh chân dung khuôn mặt|
|2 | There's no face on card image | Lỗi không tìm thấy mặt trong ảnh giấy tờ tùy thân|
|4 | Matching fail | Chỉ số so khớp dưới ngưỡng (Similarity<Threshold)|
|E850 | User face is already existing, can not registered | Ảnh đầu vào (ảnh chân dung/ảnh trên GTTT) match trên 95% với khuôn mặt có   trên hệ thống. Trong trường hợp xóa khuôn mặt trong hệ thống|
|E855 | Face id is not exists | Không tồn tại ảnh cần xóa|


Đầu ra của API là dữ liệu theo định dạng JSON với cấu trúc được mô tả dưới đây:

```json
"output": [
{
"id": {
    "value": "00130003",
    "confidence": 1.0,
    "validate": {
        "id_check": "FAKE",
        "id_logic": 1,
        "id_logic_message": "ID LENGTH IS NOT VALID",
        "idconf": [
                    0.8,
                    0.8,
                    0.8,
                    0.8,
                    0.8,
                    0.8,
                    0.8,
                    0.8]
                },
    "value_unidecode": "00130003"
    },
    "ho_ten": {
        "value": "NGUYỄN PHƯƠNG",
        "confidence": 1.0,
        "value_unidecode": "NGUYEN PHUONG"
        },
    "ngay_sinh": {
        "value": "N/A",
        "normalized": {
            "value": "N/A",
            "year": {
                "value": -1
                },
        "month": {
                "value": -1
                },
        "day": {
            "value": -1
            },
        "value_unidecode": "N/A"
    },
"confidence": 1.0,
"value_unidecode": "N/A"
},
"gioi_tinh": {
    "value": "NỮ",
    "normalized": {
        "value": 1
        },
"confidence": 1.0,
"value_unidecode": "NU"
},
"quoc_tich": {
"value": "N/A",
"normalized": {
    "value": "N/A",
    "code": -1,
    "code2": -1,
    "value_unidecode": "N/A"
    },

"confidence": 0.5,
"value_unidecode": "N/A"
},
"nguyen_quan": 
{
    "value": "XUÂN LA, TÂY HỒ, HÀ NỘI",
    "normalized": {
        "value": "PHƯỜNG XUÂN LA, QUẬN TÂY HỒ, TP HÀ NỘI",
        "tinh": {
            "value": "TP HÀ NỘI",
            "code": 59,
            "value_unidecode": "TP HA NOI"
            },
        "huyen": {
            "value": "QUẬN TÂY HỒ",
            "code": 20613,
            "value_unidecode": "QUAN TAY HO"
            },
        "xa": {
            "value": "PHƯỜNG XUÂN LA",
            "code": -1,
            "value_unidecode": "PHUONG XUAN LA"
            },
    "value_unidecode": "PHUONG XUAN LA, QUAN TAY HO, TP HA NOI"
    },
"confidence": 1.0,
"value_unidecode": "XUAN LA, TAY HO, HA NOI"
},

"ho_khau_thuong_tru": {
    "value": "N/A",
    "normalized": {
        "value": "N/A",
        "tinh": {
            "value": "N/A",
            "code": -1,
            "value_unidecode": "N/A"
            },
        "huyen": {
            "value": "N/A",
            "code": -1,
            "value_unidecode": "N/A"
            },
        "xa": {
            "value": "N/A",
            "code": -1,
            "value_unidecode": "N/A"
            },
        "value_unidecode": "N/A"
    },
"confidence": 0.5,
"value_unidecode": "N/A"
},

"ngay_het_han": {
    "value": "N/A",
    "normalized": {
        "value": "N/A",
        "year": {
            "value": -1
            },
        "month": {
            "value": -1
            },
        "day": {
            "value": -1
            },
    "value_unidecode": "N/A"
    },
"confidence": 0.8,
"value_unidecode": "N/A"
},

"class_name": {
    "value": "CĂN CƯỚC CÔNG DÂN GẮN CHIP - MẶT TRƯỚC",
    "confidence": 1.0,
        "normalized": {
            "value": 4,
            "code": "CCCD_CHIP"
            }
        },

"liveness": {
    "liveness": "True"
    }
},
{
"di_hinh": {
    "value": "NỐT RUỒI C:LEM BÊN TRƯỚC ĐUÔI LÔNG MÀY PHẢI",
    "confidence": 1.0,
    "value_unidecode": "NOT RUOI C:LEM BEN TRUOC DUOI LONG MAY PHAI"
    },
"ngay_cap": {
    "value": "25/04/2021",
    "normalized": {
    "value": "25/04/2021",
    "year": {
        "value": 2021
        },
    "month": {
        "value": 4
        },
    "day": {
        "value": 25
        },
    "value_unidecode": "25/04/2021"
    },
    "confidence": 1.0,
    "value_unidecode": "25/04/2021"
    },

    "noi_cap": {
        "value": "CỤC CẢNH SÁT QUẢN LÝ HÀNH CHÍNH VỀ TRẬT TỰ XÃ HỘI",
        "confidence": 0.0,
        "value_unidecode": "CUC CANH SAT QUAN LY HANH CHINH VE TRAT TU XA HOI"
        },

    "ho_ten": {
        "value": "LE QUOC DUNG",
        "confidence": 0.8,
        "value_unidecode": "LE QUOC DUNG"
        },
    "ngay_sinh": {
        "value": "25/08/1990",
        "normalized": {
            "value": "25/08/1990",
            "year": {
                "value": 1990
                },
            "month": {
                "value": 8
                },

            "day": {
                "value": 25
                },
            "value_unidecode": "25/08/1990"
            },
    "confidence": 0.8,
    "value_unidecode": "25/08/1990"
    },

    "gioi_tinh": {
        "value": "NAM",
        "normalized": {
            "value": 0
            },
    "confidence": 0.5,
    "value_unidecode": "NAM"
    },
    "ngay_het_han": {
    "value": "25/08/2030",
    "normalized": {
        "value": "25/08/2030",
        "year": {
            "value": 2030
            },
        "month": {
            "value": 8
            },
        "day": {
            "value": 25
            },
        "value_unidecode": "25/08/2030"
        },
    "confidence": 0.8,
    "is_valid": true,
    "value_unidecode": "25/08/2030"
    },
    "id": {
        "value": "035090001704",
        "confidence": 0.8,
        "value_unidecode": "035090001704"
        },
    "class_name": {
    "value": "CĂN CƯỚC CÔNG DÂN GẮN CHIP - MẶT SAU",
    "confidence": 1.0,
    "normalized": {
        "value": 5,
        "code": "CCCD_CHIP"
        }
    },
    "liveness": {
        "liveness": "True"
        }
    },
{
"is_matched": {
    "value": "False",
    "similarity": 0.0,
    "confidence": 0.9801,
    "liveness": "True"
    },
"error": {
    "value": "Matching fail",
    "confidence": 0.8,
    "code": 4
    }
},
null,
null
],
"time": 17.914251804351807,
"api_version": "0.2",
"mlchain_version": "0.2.8",
"request_id": "d7e51de2-e075-4e9c-976d-bf82b8246e6f"
}
```

# Khả năng cam kết (CCU)

Khả năng xử lý đồng thời (CCU) cho nghiệp vụ eKYC (Bao gồm so với khớp khuôn mặt, trích xuất thông tin và các nghiệp vụ khác) là 5. Thời gian xử lý cho mỗi request là 3s
