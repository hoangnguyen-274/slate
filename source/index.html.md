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
  - 01_register_user_face
  - 02_register_user_video
  - 03_update_info
  - 04_face_matching
  - 05_face_search
  - 06_init_update_portrait
  - 07_querry_customer
  - 08_querry_by_portrait
  - 09_delete_portrait
  - 10_extract_info

search: true

code_clipboard: true

meta:
  - name: description
---

[![Build Status](https://travis-ci.org/joemccann/dillinger.svg?branch=master)](https://travis-ci.org/joemccann/dillinger)

# Sản phẩm Master EKYC

**Module EKYC do Techainer cung cấp** cho phép người dùng đăng tải ảnh/video chân dung khuôn mặt và ảnh giấy tờ tùy thân rồi dùng các module AI để trích xuất thông tin trên giấy tờ và so khớp khuôn mặt trên giấy tờ tùy thân và ảnh/video chân dung khuôn mặt hiện tại để xác nhận đây là cùng một người.

Các loại GTTT mà API hỗ trợ:

- Chứng minh nhân dân 9 số

- Chứng minh nhân dân 12 số

- Căn cước công dân

- Căn cước công dân gắn chip

- Hộ chiếu


# Postman collection
You can run the Master EKYC API version 3.4 collection in Postman:
`Run in Postman` -> Automatically open Postman and import standard collection

The API version 3.4 Postman collection is at version 1.0.

In your Postman environment, you'll need to define the apiToken and baseUrl variables. See region base URLs for baseUrl options.


# Token authentication
- API tokens
- SDK tokens
- Mobile tokens

<aside class="success">
Remember — Request is authenticated!
</aside>

# Rate limits - CCU
Master EKYC's API enforces a maximum volume of requests per minute for all clients. Unless contractually agreed otherwise, the maximum rate is 400 requests per minute.

For sandbox requests, the rate limit is 30 requests per minute.

Any request over the limit will return a `429 Too Many Requests error.`

