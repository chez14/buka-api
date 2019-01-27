---
title: Bukalapak API Reference

language_tabs: # must be one of https://git.io/vQNgJ
  - shell

toc_footers:
  - <a href='#'>Sign Up for a Developer Key</a>
  - <a href='https://github.com/lord/slate'>Documentation Powered by Slate</a>

includes:
  - errors

search: true
---

# Introduction

Welcome to the Bukalapak API! You can use our API to access Bukalapak API endpoints, which can get information on products, transactions, and users, etc.

# Authentication

Bukalapak uses combination of `user_id` and API `token` to allow access for **required authentication’s resources**. Bukalapak expects for the `user_id` and API `token` to be included in all API requests to the server in request that looks like the following:

```shell
curl -u user_id:token
```



You must replace `user_id:token` with your user_id and API token.



## Get API token

> Sample Request

```shell
curl "https://api.bukalapak.com/v2/authenticate.json"
  -u "username:password"
  -X "POST"
```

> Success Response

```json
{
  "status"    : "OK",
  "user_id"   : "157324",
  "user_name" : "Sayur Kangkung",
  "confirmed" : true,
  "token"     : "U8Ch2LigkVhdI3XwYRA",
  "email"     : "sayur@kangkung.com",
  "omnikey"   : "a15d3e8835c69f1c4fd6b38fe9098b4b",
  "message"   : null
}
```

> Failure Response

```json
{
  "status"    : "ERROR",
  "user_id"   : null,
  "user_name" : null,
  "confirmed" : false,
  "token"     : null,
  "email"     : null,
  "omnikey"   : null,
  "message"   : "Username atau password tidak valid"
}
```

This endpoint used to retrieve API `token`.

Use Bukalapak `username` and `password` to obtain `user_id` and API `token`. You can register for a new Bukalapak user at our [website](https://web.archive.org/web/20170912234943/https://www.bukalapak.com/register).

### HTTP Request

`POST https://api.bukalapak.com/v2/authenticate.json`

### Parameters

## Facebook Login

> Sample Request

```shell
curl "https://api.bukalapak.com/v2/facebook_loginv2.json"
  -X "POST"
  -d "facebook_id=something&facebook_token=somethingelse"
```

> Success Response

```json
{
  "status": "OK",
  "user_id": "157324",
  "user_name": "Sayur Kangkung",
  "token": "U8Ch2LigkVhdI3XwYRA",
  "message": null
}
```

> Failure Response

```json
{
    "status": "ERROR",
    "message": "User tidak ditemukan"
}
```

This endpoint used to retrieve API `token`.

Use Facebook OAuth to get linked account. You can register for a new Bukalapak user at our [website](https://web.archive.org/web/20170912234943/https://www.bukalapak.com/register) and then linked your Facebook account with your Bukalapak account

### HTTP Request

`POST https://api.bukalapak.com/v2/facebook_loginv2.json`

### Parameters

| Parameter        |          | Description          |
| ---------------- | -------- | -------------------- |
| `facebook_id`    | required | id from fb accounr=t |
| `facebook_token` | required | token from fb api    |

## Google Login

> Sample Request

```shell
curl "https://api.bukalapak.com/v2/google_login.json"
  -X "POST"
  -d "email=user@bukalapak.com&google_token=something"
```

> Success Response

```json
{
  "status": "OK",
  "user_id": "157324",
  "user_name": "Sayur Kangkung",
  "token": "U8Ch2LigkVhdI3XwYRA",
  "message": null
}
```

> Failure Response

```json
{
    "status": "ERROR",
    "message": "User tidak ditemukan"
}
```

This endpoint used to retrieve API `token`.

Use Google OAuth to get linked account. You can register for a new Bukalapak user at our [website](https://web.archive.org/web/20170912234943/https://www.bukalapak.com/register) and then linked your google account with your Bukalapak account.

### HTTP Request

`POST https://api.bukalapak.com/v2/google_login.json`

### Parameters

| Parameter      |          | Description             |
| -------------- | -------- | ----------------------- |
| `email`        | required | email of google account |
| `google_token` | required | token from google api   |

# Categories

## Get All Categories

```shell
curl "https://api.bukalapak.com/v2/categories.json"
  -H "If-None-Match: '1984705864'"
  -u "99999999:t0k3nt0k3n"

curl "https://api.bukalapak.com/v2/categories.json"
  -u "99999999:t0k3nt0k3n"
```

> Sample response:

```json
{
  "status": "OK",
  "categories": [
    {
      "id": 64,
      "name": "Sepeda",
      "url": "/c/sepeda",
      "children": [
        {
          "id": 242,
          "name": "Fullbike",
          "url": "/c/sepeda/fullbike",
          "children": [
            {
              "id": 370,
              "name": "MTB",
              "url": "/c/sepeda/fullbike/mtb"
            },
            {
              "id": 371,
              "name": "Roadbike",
              "url": "/c/sepeda/fullbike/roadbike"
            }
          ]
        },
        {
          "id": 85,
          "name": "Frame",
          "url": "/c/sepeda/frame",
          "children": [
            {
              "id": 372,
              "name": "MTB",
              "url": "/c/sepeda/frame/mtb"
            },
            {
              "id": 373,
              "name": "Roadbike",
              "url": "/c/sepeda/frame/mtb"
            }
          ]
        }
      ]
    },
    {
      "id": 10,
      "name": "Kamera",
      "url": "/c/kamera",
      "children": [
        {
          "id": 186,
          "name": "Kamera Digital",
          "url": "/c/kamera/kamera-digital"
        },
        {
          "id": 350,
          "name": "Kamera Analog",
          "url": "/c/kamera/kamera-analog"
        }
      ]
    },
  ],
  "message": null
}
```

This endpoint retrieves all categories.

You can optionally set `If-None-Match` header or `Etag` header. If request `Etag` match, server will send `304 Not Modified` response without body. Server will set `Etag` header to every request to this resource.

### HTTP Reuest

`GET https://api.bukalapak.com/v2/categories.json`

### Parameters

None

## Get Attributes For a Category

```shell
curl "https://api.bukalapak.com/v2/categories/8/attributes.json"
  -H "If-None-Match: '1984705864'"
  -u "99999999:t0k3nt0k3n"

curl "https://api.bukalapak.com/v2/categories/8/attributes.json"
  -u "99999999:t0k3nt0k3n"
```

> Sample response:

```json
{
  "status": "OK",
  "attributes": [
    {
      "fieldName": "brand",
      "displayName": "Merek",
      "inputType": "select",
      "options": [
        "Oppo",
        "Andromax",
        "iPhone",
        "Acer",
        "Advan",
        "Nokia",
        "Samsung",
        "Sony Ericsson",
        "TiPhone",
        "Lain-lain"
      ],
      "required": true
    },
    {
      "fieldName": "operating_system",
      "displayName": "Operating System",
      "inputType": "select",
      "options": [
        "Blackberry",
        "Android",
        "iOS",
        "Windows Phone",
        "Symbian",
        "Linux",
        "Non Smartphone"
      ],
      "required": true
    },
    {
      "fieldName": "features",
      "displayName": "Features",
      "inputType": "check_boxes",
      "options": [
        "Touchscreen",
        "Wifi",
        "Bluetooth",
        "3G",
        "GPS Navigation",
        "Video Player",
        "Front Camera",
        "QWERT Keyboard",
        "Dual Sim Card"
      ],
      "required": true
    },
    {
      "fieldName": "bentuk",
      "displayName": "Bentuk",
      "inputType": "select",
      "options": [
        "Klasik (Bar)",
        "Sliding",
        "Flip"
      ],
      "required": true
    },
    {
      "fieldName": "display_size",
      "displayName": "Display Size",
      "inputType": "select",
      "options": [
        "1.8\"",
        "4.5\"",
        "5.0\"",
        "7.0\""
      ],
      "required": false
    },
    {
      "fieldName": "camera",
      "displayName": "Camera",
      "inputType": "select",
      "options": [
        "Camera",
        "No Camera"
      ],
      "required": true
    },
    {
      "fieldName": "garansi",
      "displayName": "Garansi",
      "inputType": "select",
      "options": [
        "Tidak bergaransi",
        "1-12 bulan",
        "2 tahun"
      ],
      "required": true
    },
    {
      "fieldName": "network",
      "displayName": "Network",
      "inputType": "select",
      "options": [
        "CDMA",
        "GSM",
        "Dual GSM-CDMA",
        "Dual GSM-GSM"
      ],
      "required": true
    },
    {
      "fieldName": "body_color",
      "displayName": "Body Color",
      "inputType": "check_boxes",
      "options": [
        "Hitam",
        "Putih",
        "Silver",
        "Emas kuning",
        "Hijau",
        "Ungu"
      ],
      "required": true
    }
  ],
  "message": null
}
```

You can optionally set `If-None-Match` header or `Etag` header. If request `Etag` match, server will send `304 Not Modified` response without body. Server will set `Etag` header to every request to this resource.

### HTTP Request

`GET htps://api.bukalapak.com/v2/categories/:id/attributes.json`

### Parameters

None

### Dictionary

Possible values for `inputType`:

| inputType                | Description                                   |
| ------------------------ | --------------------------------------------- |
| `string`                 | equivalent to `input` type `text` tag in html |
| `text`                   | equivalent to `textarea`                      |
| `select`, `combo_select` | equivalent to `select`                        |
| `boolean`, `check_boxes` | equivalent to `input` type `checkbox`         |
| `radio_buttons`          | equivalent to `input` type `radio`            |

# Carts

## View Cart

> Sample Request

```shell
curl  "https://api.bukalapak.com/v2/carts.json"
  -u  "66:tok3ntok3n"

curl  "https://api.bukalapak.com/v2/carts.json?identity=tokenkeyiskmzwa8awaa"
```

> Success Response

```json
{
  "status": "OK",
  "cart_id": 3,
  "cart": [
    {
      "seller": {
        "id": 4,
        "username": "meow",
        "name": "Kucing",
        "gender": null,
        "avatar": "https://www.bukalapak.com/images/default_avatar/medium/default.jpg",
        "level": "",
        "level_badge_url": "",
        "lapak_name": null,
        "lapak_desc": "",
        "lapak_header": "https://www.bukalapak.com/images/header-lapak-default.jpg",
        "last_login": "2016-01-07T18:01:37.000+07:00",
        "joined_at": "2015-10-21T17:47:25.000+07:00",
        "verified_user": false,
        "official": false,
        "store_closed": false,
        "schedule_close_store": null,
        "close_date": null,
        "reopen_date": null,
        "close_reason": null,
        "rejection": {
          "rejected": 0,
          "recent_trans": 0
        },
        "feedbacks": {
          "positive": 0,
          "negative": 0
        },
        "address": {
          "province": "Nanggroe Aceh Darussalam",
          "city": "Aceh Jaya"
        }
      },
      "items": [
        {
          "id": 152,
          "name": "Bantal Sofa Ekspor Geometrik Leaf Gray Flat Woven 40x40",
          "quantity": 1,
          "price": 70000,
          "stock": 11,
          "message": null,
          "product": {
            "deal_info": {},
            "deal_request_state": "cannot request",
            "price": 70000,
            "courier": [
              "JNE REG"
            ],
            "seller_username": "meow",
            "seller_name": "Kucing",
            "seller_id": 4,
            "seller_avatar": "https://www.bukalapak.com/images/default_avatar/medium/default.jpg",
            "seller_level": "",
            "seller_level_badge_url": "",
            "seller_positive_feedback": 0,
            "seller_negative_feedback": 0,
            "seller_term_condition": "",
            "seller_alert": null,
            "for_sale": true,
            "state_description": [],
            "last_relist_at": "2015-12-04T16:02:13.000+07:00",
            "specs": {},
            "force_insurance": null,
            "free_shipping_coverage": [],
            "id": "1m",
            "url": "https://www.bukalapak.com/p/fashion/baby-kids/sleepwear/1m-jual-bantal-sofa-ekspor-geometrik-leaf-gray-flat-woven-40x40",
            "name": "Bantal Sofa Ekspor Geometrik Leaf Gray Flat Woven 40x40",
            "active": true,
            "city": "Aceh Jaya",
            "province": "Nanggroe Aceh Darussalam",
            "weight": 750,
            "image_ids": [
              61
            ],
            "images": [
              "https://www.bukalapak.com/system4/images/6/1/large/2015-12-04T16%253A02%253A12%252B07%253A00.jpg"
            ],
            "small_images": [
              "https://www.bukalapak.com/system4/images/6/1/small/2015-12-04T16%253A02%253A12%252B07%253A00.jpg"
            ],
            "desc": "Bantal Sofa Kualitas Ekspor, harga terjangkau<br/>Bahan : Flat Woven Fabric<br/>Motif 2 sisi (depan - belakang sama)<br/>Isi bantal : Silicon Premium<br/>Sarung bantal dilengkapi restleting.<br/>Dapat dicuci<br/>Cocok untuk menghiasi rumah, cafe, hotel ataupun mobil Anda<br/>Size : 40x40<br/>Harga Normal : Rp. 125.000/Bantal<br/><br/>Fast respon<br/>WA/Sms no call: <br/>Call Us :  (Fitri)<br/>YM : fazha_interior.com",
            "condition": "new",
            "nego": false,
            "stock": 11,
            "minimum_negotiable": null,
            "view_count": 12,
            "sold_count": 0,
            "waiting_payment": 0,
            "favorited": false,
            "created_at": "2015-12-04T16:02:13.000+07:00",
            "product_sin": [],
            "category_id": 169,
            "category": "Sleepwear",
            "category_structure": [
              "Fashion",
              "Baby & Kids",
              "Sleepwear"
            ],
            "interest_count": 5
          },
          "original_price": 70000,
          "discount_price": null
        }
      ]
    }
  ],
  "message": null
}
```

### HTP Request

`GET https://api.bukalapak.com/v2/carts.json`

### Parameters

| Parameter  |          | Description                                                  |
| ---------- | -------- | ------------------------------------------------------------ |
| `identity` | optional | Is not required when logged in as a BL user, but required to identify the cart belonging to a non-logged-in user. The identity of each non-logged-in user must be unique. |

## Add Product to Cart

> Sample Request

```shell
curl  "https://api.bukalapak.com/v2/carts/add_product/my5q.json"
  -u  "66:tok3ntok3n"
  -X  "POST"
  -d  "quantity=2"

curl  "https://api.bukalapak.com/v2/carts/add_product/my5q.json"
  -X  "POST"
  -d  "identity=tokenkeyiskmzwa8awaa&quantity=2"
```

> Success Response

```json
{
  "status": "OK",
  "cart_id": 3,
  "cart": [
    {
      "seller": {
        "id": 2,
        "username": "meow",
        "name": "Kucing",
        "gender": null,
        "avatar": "https://www.bukalapak.com/images/default_avatar/medium/default.jpg",
        "level": "BL User",
        "level_badge_url": "https://www.bukalapak.com/images/badge/seller/xhdpi/level-1.png",
        "lapak_name": null,
        "lapak_desc": "alakazam",
        "lapak_header": "https://www.bukalapak.com/images/header-lapak-default.jpg",
        "last_login": "2016-01-15T18:29:53.000+07:00",
        "joined_at": "2015-09-21T19:24:09.000+07:00",
        "verified_user": false,
        "official": false,
        "store_closed": false,
        "schedule_close_store": null,
        "close_date": null,
        "reopen_date": null,
        "close_reason": null,
        "rejection": {
          "rejected": 0,
          "recent_trans": 0
        },
        "feedbacks": {
          "positive": 7,
          "negative": 10
        },
        "address": {
          "province": "Jawa Timur",
          "city": "Kab. Pasuruan"
        }
      },
      "items": [
        {
          "id": 156,
          "name": "The Untololgy",
          "quantity": 1,
          "price": 34400,
          "stock": 130,
          "message": null,
          "product": {
            "deal_info": {},
            "deal_request_state": "cannot request",
            "price": 34400,
            "courier": [
              "JNE REG"
            ],
            "seller_username": "meow",
            "seller_name": "Kucing",
            "seller_id": 2,
            "seller_avatar": "https://www.bukalapak.com/images/default_avatar/medium/default.jpg",
            "seller_level": "BL User",
            "seller_level_badge_url": "https://www.bukalapak.com/images/badge/seller/xhdpi/level-1.png",
            "seller_positive_feedback": 7,
            "seller_negative_feedback": 10,
            "seller_term_condition": "<p>ini catatanku, mana catatanmu?</p>\n",
            "seller_alert": null,
            "for_sale": true,
            "state_description": [],
            "last_relist_at": "2015-12-04T16:02:13.000+07:00",
            "specs": {},
            "force_insurance": null,
            "free_shipping_coverage": [],
            "id": "al",
            "url": "https://www.bukalapak.com/p/buku-233/fiksi/al-jual-buku-the-untololgy",
            "name": "The Untololgy",
            "active": true,
            "city": "Kab. Pasuruan",
            "province": "Jawa Timur",
            "weight": 250,
            "image_ids": [
              411
            ],
            "images": [
              "https://www.bukalapak.com/system4/images/4/1/1/large/2016-01-06T11%253A41%253A49%252B07%253A00.jpg"
            ],
            "small_images": [
              "https://www.bukalapak.com/system4/images/4/1/1/small/2016-01-06T11%253A41%253A49%252B07%253A00.jpg"
            ],
            "desc": "\"Assalammu'alaikum mas dzikri, ikhlas agak susah ya mas.<br/>Saya harus ikhlas nggak melanjutkan hubungan karena<br/>kami beda agama\".<br/><br/>Wa'alaikum Salam. Iya, kalau ikhlas itu mudah, ikhlas nggak akan jadi sifat yg istimewa di hidup ini kan?<br/><br/>\"Saya nggak bisa bayangin kalau jodoh dia bukan saya, nggak tahu saya akan seperti apa nantinya <img title='sedih' src='https://www.bukalapak.com/images/emoji/sad.gif'> <br/><br/>Masalah kita putus itu sebenarnya hanya sepele. Bahwa saya bukan seorang mahasiswi kedokteran dan saya mempunyai darah sunda <img title='sedih' src='https://www.bukalapak.com/images/emoji/sad.gif'><br/><br/>Hal yang saya sesalkan buat apa 2,5 tahun bersama kalau memang rules dikeluarga dia itu satu alasan yang bisa menghentikan saya <img title='sedih' src='https://www.bukalapak.com/images/emoji/sad.gif'>\"<br/><br/>Bukan menghentikanmu,tapi menghentikan kalian. Karena hubungan ini bukan tentang kamu aja, tapi juga tentang dia yang tidak boleh melawan orang tua, karena nanti durhaka.<br/><br/>Buku ini memuat obrolan tentang segala macam masalah, termasuk cinta, persahabatan, orang tua, sekolah dan kesuksesan. Juga percakapan imajiner dengan Tuhan, cangkir, keyboard, komputer dan diri penulis sendiri. Tidak mencoba memberi jawaban, tapi mengajak pembaca menyelami dan menemukan jawaban mereka sendiri.",
            "condition": "new",
            "nego": false,
            "stock": 130,
            "minimum_negotiable": null,
            "view_count": 2,
            "sold_count": 0,
            "waiting_payment": 0,
            "favorited": false,
            "created_at": "2016-01-06T11:41:49.000+07:00",
            "product_sin": [],
            "category_id": 245,
            "category": "Fiksi",
            "category_structure": [
              "Buku",
              "Fiksi"
            ],
            "interest_count": 1
          },
          "original_price": 34400,
          "discount_price": null
        }
      ]
    }
  ],
  "message": "The Untololgy telah ditambahkan ke Keranjang Belanja"
}
```

> Failure Response

```json
{
  "status": "ERROR",
  "cart_id": null,
  "cart": null,
  "message": "Stok tidak mencukupi"
}
```

### HTTP Request

`POST https://api.bukalapak.com/v2/carts/add_product/:id.json`

### Parameters

| Parameter  |          | Description                                                  |
| ---------- | -------- | ------------------------------------------------------------ |
| `id`       | required | ID of the product to add.                                    |
| `identity` | optional | Is not required when logged in as a BL user, but required to identify the cart belonging to a non-logged-in user. The identity of each non-logged-in user must be unique. |
| `quantity` | optional | Quantity of product added to cart. Defaults to `1`.          |

## Add Offer to Cart (not used anymore)

> Sample Request

```shell
curl -u 15:tokenkeyiskmzwa8awaa https://api.bukalapak.com/v2/carts/add_offer/3452.json -X POST -d ''
curl https://api.bukalapak.com/v2/carts/add_offer/3452.json -X POST -d 'identity=tokenkeyiskmzwa8awaa'
```

> Success Response

```json
{
  "status": "OK",
  "cart_id": 12,
  "cart": [
    {
      "seller": {
        "id": 66,
        "username": "tmasa",
        "name": "tmasa",
        "avatar": "https://www.bukalapak.com/images/default_avatar/medium/default.jpg",
        "lapak_name": "",
        "lapak_desc": "",
        "lapak_header": "https://www.bukalapak.com/images/header-lapak-default.jpg",
        "feedbacks": {
          "positive": 1,
          "negative": 0
        },
        "address": {
          "province": "DKI Jakarta",
          "city": "Jakarta Timur"
        }
      },
      "items": [
        {
          "id": 115,
          "name": "LG D821 Google Nexus 5 - 16GB White",
          "quantity": 1,
          "price": 5500000,
          "stock": 1,
          "message": null,
          "product": {
            "id": "my5x",
            "category": "Server",
            "category_id": 157,
            "category_structure": ["Komputer","Server"],
            "name": "LG D821 Google Nexus 5 - 16GB Black",
            "active": true,
            "city": "Jakarta Timur",
            "province": "DKI Jakarta",
            "price": 5500000,
            "weight": "1000",
            "courier": ["JNE"],
            "force_insurance": null,
            "image_ids": [2603544],
            "images": [
              "https://www.bukalapak.com/system/images/2/6/0/3/5/4/4/large/2014-07-07T13_15_02_07_00.jpg"
            ],
            "small_images": [
              "https://www.bukalapak.com/system/images/2/6/0/3/5/4/4/small/2014-07-07T13_15_02_07_00.jpg"
            ],
            "url": "https://www.bukalapak.com/p/komputer/server/my5q-jual-lg-d821-google-nexus-5-16gb-black",
            "desc": "Operating System : Android\u003cbr/\u003eFeatures : Touchscreen, Wifi, Bluetooth, 3G, GPS Navigation, MP3, Message, e-mail, Video Player, Front Camera\u003cbr/\u003eDisplay Size : 5.0\"\u003cbr/\u003e\u003cbr/\u003eDESKRIPSI BARANG :\u003cbr/\u003eGoogle bersama LG kembali berkolaborasi untuk meluncurkan smartphone seri Nexus mereka, yakni Google Nexus 5. Sistem operasi Android 4.4 KitKat terbaru adalah daya tarik utama dari Google Nexus 5. Dipersenjatai dengan chipset tercepat Qualcomm MSM8974 Snapdragon 800 dengan prosesor Quad-core 2.3 GHz Krait 400 dan GPU Adreno 330, pengalaman Anda dalam menjelajahi Android 4.4 akan semakin menyenangkan di Google Nexus 5. Belum lagi seri Nexus terkenal akan update sistem operasi yang cepat, tidak terkecuali Google Nexus 5.\u003cbr/\u003e\u003cbr/\u003eBaru \u0026amp; Bersegel",
            "condition": "new",
            "nego": true,
            "seller_username": "tmasa",
            "seller_name": "tmasa",
            "seller_id": 66,
            "seller_avatar": "https://www.bukalapak.com/images/default_avatar/medium/default.jpg",
            "seller_level": "BL User",
            "seller_positive_feedback": 1,
            "seller_negative_feedback": 0,
            "payment_ready": true,
            "stock": 1,
            "specs": {
              "brand": null,
              "processor": null,
              "type": null
            },
            "state_description": []
          }
        }
      ],
  "message": "Item telah ditambahkan ke Keranjang Belanja"
}
```

> Failure Response

```json
{
  "status": "ERROR",
  "cart_id": 12,
  "cart": [],
  "message": "Stok barang tidak mencukupi atau barang sudah terjual ke pembeli lain dengan harga pas"
}
```

### HTTP Request

`POST https://api.bukalapak.com/v2/carts/add_offer/:id.json`

### Parameters

| Parameter  |          | Description                                                  |
| ---------- | -------- | ------------------------------------------------------------ |
| `id`       | required | ID of the offer to add.                                      |
| `identity` | optional | Is not required when logged in as a BL user, but required to identify the cart belonging to a non-logged-in user. The identity of each non-logged-in user must be unique. |

## Update Item in Cart

Update cart item quantity.

> Sample Request

```shell
curl  "https://api.bukalapak.com/v2/carts/item/2908.json"
  -u  "66:tok3ntok3n"
  -X  "PATCH"
  -d  'quantity=3'
curl  "https://api.bukalapak.com/v2/carts/item/2908.json"
  -X  "PATCH"
  -d  "identity=tokenkeyiskmzwa8awaa&quantity=3"
```

> Success Response

```json
{
  "status": "OK",
  "message": "Jumlah pembelian berhasil diubah",
  "info": {
    "price": 34400,
    "quantity": 3
  }
}
```

> Failure Response

```json
{
  "status": "ERROR",
  "message": "Gagal mengubah jumlah pembelian",
  "info": null
}
```

### HTTP Request

`PATCH https://api.bukalapak.com/v2/carts/item/:id.json`

### Parameters

| Parameter  |          | Description                                                  |
| ---------- | -------- | ------------------------------------------------------------ |
| `id`       | required | ID of the offer to add.                                      |
| `identity` | optional | Is not required when logged in as a BL user, but required to identify the cart belonging to a non-logged-in user. The identity of each non-logged-in user must be unique. |
| `quantity` | optional | Quantity of product added to cart. Defaults to `1`.          |

## Remove Item from Cart

> Sample Request

```shell
curl  "https://api.bukalapak.com/v2/carts/item/2908.json"
  -u  "15:tokenkeyiskmzwa8awaa"
  -X  "DELETE"

curl  "https://api.bukalapak.com/v2/carts/item/2908.json"
  -X  "DELETE"
  -d  "identity=tokenkeyiskmzwa8awaa"
```

> Success Response

```json
{
  "status": "OK",
  "message": "The Untololgy telah dihapus dari Keranjang Belanja"
}
```

### HTTP Request

`DELETE https://api.bukalapak.com/v2/carts/item/:id.json`

### Parameters

| Parameter  |          | Description                                                  |
| ---------- | -------- | ------------------------------------------------------------ |
| `id`       | required | ID of the offer to add.                                      |
| `identity` | optional | Is not required when logged in as a BL user, but required to identify the cart belonging to a non-logged-in user. The identity of each non-logged-in user must be unique. |

## Get Shipping Estimation

> Sample Request

```shell
curl  "https://api.bukalapak.com/v2/carts/1/shipping_estimation.json"
  -u  "66:tokenkeyiskmzwa8awaa"
  -d  "seller_id=14&to=Jakarta Selatan&to_area=Pasar Minggu"
```

> Success Response

```json
{
  "status": "OK",
  "shipping_fees": [
    {
      "courier": "tiki",
      "service": "TIKI Reg",
      "price": 153000
    },
    {
      "courier": "rpx",
      "service": "RPX Economy Package",
      "price": 120000
    }
  ],
  "message": null
}
```

### HTTP Request

`GET https:/api.bukalapak.com/v2/carts/:id/shipping_estimation.json`

### Parameters

| Parameter   |          | Description                     |
| ----------- | -------- | ------------------------------- |
| `id`        | required | ID of the cart to be estimated. |
| `seller_id` | required | ID of seller.                   |
| `to`        | required | Shipping destination city.      |
| `to_area`   | required | Shipping destination district.  |

# Deals

## Get Deal Common Information

> Sample Request

```shell
curl https://api.bukalapak.com/v2/deals/info.json
```

> Sample Response

```json
{
  "status":"OK",
  "min_date":"2015-02-25",
  "max_date":"2015-03-02",
  "fee_percentage":0.0,
  "message":null
}
```

Gets deal common information

### HTTP Reuest

`GET https://api.bukalapak.com/v2/deals/info.json`

### Parameters

None

## Request New or Edit Existing Deal

> Sample Request

```shell
curl -u 6:s7uggBrVrEkckEgqRc -d '{ "reduced_price": "9000", "percentage": "10" , "year": "2015", "month": "2", "day": "27"}' "http://api.bukalapak.com/v2/deals/new/50994.json" -H "Content-Type: application/json" -X POST
```

> Success Response

```json
{
  "status":"OK",
  "id":"13ci",
  "product_detail": {
    "id":"13ci",
    "category":"Minuman",
    "category_id":123,
    "category_structure":["Food","Minuman"],
    "name":"Kaos Jersey England UK XL",
    "active":true,
    "city":"Jakarta Selatan",
    "province":"DKI Jakarta",
    "price":10000,
    "weight":1000,
    "courier":["JNE","RPX","Wahana"],
    "force_insurance":false,
    "image_ids": [80227],
    "images": [
      "https://www.bukalapak.com/system/images/8/0/2/2/7/large/index3.jpeg"
    ],
    "small_images": [
      "https://www.bukalapak.com/system/images/8/0/2/2/7/small/index3.jpeg"
    ],
    "url":"https://www.bukalapak.com/p/food/minuman/13ci-jual-kaos-jersey-england-uk-xl",
    "desc":"dcsavcsafdrv",
    "condition":"new",
    "nego":false,
    "seller_username":"admins",
    "seller_name":"aaddmmiin",
    "seller_id":6,
    "seller_avatar":"https://www.bukalapak.com/images/default_avatar/medium/default.jpg",
    "seller_level":"Pedagang",
    "seller_positive_feedback":12,
    "seller_negative_feedback":1,
    "payment_ready":true,
    "stock":1,
    "specs":{},
    "state_description":[],
    "minimum_negotiable":null,
    "for_sale":true,
    "view_count":0,
    "favorited":false,
    "interest_count":0,
    "free_shipping_coverage":[],
    "deal_info": {
      "original_price":10000,
      "discount_price":9000,
      "discount_percentage":10,
      "state":"edited"
    },
    "deal_request_state":"can edit"
  },
  "message":"Diskon berhasil diajukan!"
}
```

> Failure Response

```json
{
  "status":"ERROR",
  "id":null,
  "product_detail":null,
  "message":"Diskon gagal diajukan! Harga setelah diskon tidak sesuai dengan persentase!"
}
```

Request new or update existing deal on selected product.

### HTTP Request

`POST https://api.bukalapak.com/v2/deals/new/:product_id.json`

### Parameters

| Parameter            |          | Description                                                  |
| -------------------- | -------- | ------------------------------------------------------------ |
| `percentage`         | required | Discount percentage number.                                  |
| `reduced_price`      | required | Price after discount percentage is applied to product price. |
| `day` `month` `year` | optional | Date when the discount will be applied, default to `min_date`. |

## Get Campaign info

> Sample Request

```shell
curl https://api.bukalapak.com/v2/deals/campaigns.json?page=1
```

> Sample Response

```json
{
  "status":"OK",
  "campaigns":[
  {
    "id":1,
    "title":"Lebaran Oke",
    "description":"Bukalapak",
    "promotion_url":"http://www.bukalapak.com/promo/lebaran",
    "banner_url":"http://www.bukalapak.com/system4/uploads/1/960x190.jpg"
  },
  {
    "id":2,
    "title":"Puasa Shaum",
    "description":"ayuk puasa",
    "promotion_url":"http://www.bukalapak.com/promo/puasa-shaum",
    "banner_url":"http://www.bukalapak.com/system4/uploads/2/Cover.jpg"
  }
  ],
  "message":null
}
```

Gets list of available campaigns.

### HTTP Request
`GET https://api.bukalapak.com/v2/deals/campaigns.json`

### Parameters

`page` | optional | Page to display. `per_page` | optional | Number to display per page.

## Get Special Promo Info

> Sample Request

```shell
curl https://api.bukalapak.com/v2/deals/special_promo/1.json
```

> Sample Success Response

```json
{
  "status": "OK",
  "message": null,
  "special_promo": {
    "title": "Promo Spesial November",
    "description": "Promo Spesial November dari Bukalapak",
    "content": "Bulan november adalah bulan romantis, karena itu Bukalapak..",
    "terms_and_condition": "Syarat dan ketentuan Promo Spesial November",
    "banner_redirect_url": "",
    "start_date": "2015-05-02T00:00:00.000+07:00",
    "end_date": "2015-05-03T23:59:00.000+07:00",
    "image": "https://s2.bukalapak.com/uploads/special_promo/37/%28PROMO%29-Bedug-Berkah_BL_LANDINGPAGE.jpg"
  },
  "flash_banners": [
    {
      "image": "https://s4.bukalapak.com/uploads/flash_banner/5284/mobile/rsz_kosmetik_favorit_diskon_hingga_60__480x195.jpg",
      "description": "Tentukan brand kosmetik pilihanmu diskon hingga 60%",
      "info": {
        "type": "campaign",
        "id": 4195,
        "url": "https://www.bukalapak.com/promo/tentukan-brand-kosmetik-pilihanmu-diskon-hingga-60",
        "promo_due": "2016-05-28T23:59:00.000+07:00"
      }
    }
  ],
  "promo_banners": [
    {
      "image": "https://s2.bukalapak.com/uploads/flash_banner/5302/original/rsz_sales_mobil_impian_diskon_hingga_5__178x178.jpg",
      "description": "mobil impian ada dibukalapak diskon hingga 5%",
      "info": {
        "type": "campaign",
        "id": 4390,
        "url": "https://www.bukalapak.com/promo/ragam-iphone-harga-mulai-1-jutaan",
        "promo_due": "2016-06-03T23:59:00.000+07:00"
      }
    },
  ]
}
```

> Sample Failure Response

```json
{
  "status": "ERROR",
  "message": "Promo tidak ditemukan",
  "special_promo": null
}
```

Get content of special promo on specified id.

### HTTP Request

`GET ttps://api.bukalapak.com/v2/deals/special_promo/:id.json`

### Parameters

| Parameter |          | Description          |
| --------- | -------- | -------------------- |
| `id`      | required | Id of special promo. |

# Dompet

## BukaDompet History

> Sample Request

```shell
curl -u "66:tok3ntok3n" "https://api.bukalapak.com/v2/dompet/history.json?page=1&per_page=2"
```

> Success Response

```json
{
  "status": "OK",
  "balance": 53840976,
  "topup_history": [],
  "withdrawal_history": [],
  "mutation_history": [
    {
      "id": 102,
      "type": "Deposit::Debit",
      "action": "payment",
      "amount": 48000,
      "initial_balance": 53888976,
      "final_balance": 53840976,
      "transaction_id": 92,
      "transaction_no": "160000000092",
      "note": "Pembayaran untuk transaksi <font color='#a31844'>#160000000092<\font>",
      "created_at": "2016-01-08T11:34:18.000+07:00",
      "updated_at": "2016-01-08T11:34:18.000+07:00"
    },
    {
      "id": 101,
      "type": "Deposit::Debit",
      "action": "payment",
      "amount": 315800,
      "initial_balance": 54204776,
      "final_balance": 53888976,
      "transaction_id": 90,
      "transaction_no": "151228020090",
      "note": "Pembayaran untuk transaksi <font color='#a31844'>#151228020090<\font>",
      "created_at": "2015-12-28T02:35:30.000+07:00",
      "updated_at": "2015-12-28T02:35:30.000+07:00"
    }
  ],
  "message": null
}
```

Get current user’s BukaDompet history.



<aside class="warning">Requires authentication</aside>



### HTTP Reques

`GET https://api.bukalapak.com/v2/dompet/history.json`

### Parameters

| Parameter  |          | Description                                                  |
| ---------- | -------- | ------------------------------------------------------------ |
| `page`     | optional | Page number to display. Default value is `1`.                |
| `per_page` | optional | Number of record to display per page. Default value is `10`. |

### Dictionary

| Name     | Description                                                  |
| -------- | ------------------------------------------------------------ |
| `type`   | Type of mutation. Possible values are `Deposit::Credit` and `Deposit::Debit` |
| `action` | Action that trigger mutation. Possible values are `remit`, `topup`, `payment`, `refund`, `withdrawal`, and `restore`. |

## Mutation History

> Sample Request

```shell
curl -u "66:tok3ntok3n" "https://api.bukalapak.com/v2/dompet/history/mutations.json?page=1&per_page=2"
```

> Sample Response

```json
{
  "status": "OK",
  "balance": 53840976,
  "history": [
    {
      "id": 102,
      "type": "Deposit::Debit",
      "action": "payment",
      "amount": 48000,
      "initial_balance": 53888976,
      "final_balance": 53840976,
      "transaction_id": 92,
      "transaction_no": "160000000092",
      "note": "Pembayaran untuk transaksi <font color='#a31844'>#160000000092<\font>",
      "created_at": "2016-01-08T11:34:18.000+07:00",
      "updated_at": "2016-01-08T11:34:18.000+07:00"
    },
    {
      "id": 101,
      "type": "Deposit::Debit",
      "action": "payment",
      "amount": 315800,
      "initial_balance": 54204776,
      "final_balance": 53888976,
      "transaction_id": 90,
      "transaction_no": "151228020090",
      "note": "Pembayaran untuk transaksi <font color='#a31844'>#151228020090<\font>",
      "created_at": "2015-12-28T02:35:30.000+07:00",
      "updated_at": "2015-12-28T02:35:30.000+07:00"
    }
  ],
  "message": null
}
```

Get current user’s mutation history.



<aside class="warning">Requires authentication</aside>



### HTTP Request

`GET htps://api.bukalapak.com/v2/dompet/history/mutations.json`

### Parameters

| Parameter  |          | Description                                                  |
| ---------- | -------- | ------------------------------------------------------------ |
| `page`     | optional | Page number to display. Default value is `1`.                |
| `per_page` | optional | Number of record to display per page. Default value is `10`. |

### Dictionary

| Name     | Description                                                  |
| -------- | ------------------------------------------------------------ |
| `type`   | Type of mutation. Possible values are `Deposit::Credit` and `Deposit::Debit` |
| `action` | Action that trigger mutation. Possible values are `remit`, `topup`, `payment`, `refund`, `withdrawal`, and `restore`. |

## Withdrawal History

> Sample Request

```shell
curl -u "66:tok3ntok3n" "https://api.bukalapak.com/v2/dompet/history/withdrawals.json?page=1&per_page=2"
```

> Success Response

```json
{
  "status": "OK",
  "balance": 24758981,
  "history": [
    {
      "amount": 29081995,
      "bank_account_id": 1,
      "cancelled_at": null,
      "created_at": "2016-01-16T00:03:25.000+07:00",
      "deposit_id": 1,
      "id": 1,
      "processed_at": null,
      "state": "pending",
      "updated_at": "2016-01-16T00:03:25.000+07:00"
    }
  ],
  "message": null
}
```

Get current user’s withdrawal history.



<aside class="warning">Requires authentication</aside>



### HTTP Request

`GET htts://api.bukalapak.com/v2/dompet/history/withdrawals.json`

### Parameters

| Parameter  |          | Description                                                  |
| ---------- | -------- | ------------------------------------------------------------ |
| `page`     | optional | Page number to display. Default value is `1`.                |
| `per_page` | optional | Number of record to display per page. Default value is `10`. |

## Withdrawal Request

> Sample Request

```shell
curl -u "66:tok3ntok3n" -X "POST" "https://api.bukalapak.com/v2/dompet/withdraw.json" -d '{"deposit_withdrawal": {"amount": "25000", "bank_account_id": "41812", "password": "testing1234"}}' -H "Content-Type: application/json"
```

> Success Response

```json
{
  "status": "OK",
  "withdrawal_id": 4,
  "message": "Pencairan dengan nomor tiket #C2 akan diproses oleh tim Bukalapak. Dana akan ditransfer ke rekening Anda dalam waktu 2x24 jam"
}
```

> Failure Response
>
> #### Invalid account ID

```json
{
  "status": "ERROR",
  "withdrawal_id": null,
  "message": "Rekening pencairan harus milik Anda."
}
```

> #### Invalid email:

```json
{
  "status": "ERROR",
  "withdrawal_id": null,
  "message": "Email tidak valid."
}
```

> #### Invalid password:

```json
{
  "status": "ERROR",
  "withdrawal_id": null,
  "message": "Password tidak valid."
}
```

> #### More than one withdrawal request in a day:

```json
{
  "status": "ERROR",
  "withdrawal_id": null,
  "message": "Pencairan hanya bisa dilakukan satu kali sehari."
}
```

> #### Amount exceeds balance

```json
{
  "status": "ERROR",
  "withdrawal_id": null,
  "message": "Pencairan dana maksimal sejumlah saldo yang dimiliki."
}
```

> #### Amount + transfer fee exceeds balance

```json
{
  "status": "ERROR",
  "withdrawal_id": null,
  "message": "Jumlah pencairan dan biaya transfer lebih besar dari saldo."
}
```

> #### More than one withdrawal request in a day and invalid password:

```json
{
  "status": "ERROR",
  "withdrawal_id": null,
  "message": "Pencairan hanya bisa dilakukan satu kali sehari., Password tidak valid."
}
```

Make withdrawal request for current user.



<aside class="warning">Requires authentication</aside>



### HTTP Request

`POST https://api.bukalapak.com/v2/dompet/withdraw.json`

### Parameters

`deposit_withdrawal` Attributes for withdrawal, constructed by the following fields:

| Parameter         |          | Description                                        |
| ----------------- | -------- | -------------------------------------------------- |
| `amount`          | required | Amount to withdraw.                                |
| `bank_account_id` | required | Bank account id for current user’s target account. |
| `password`        | required | Current user’s password.                           |

## Topup Request

> Sample Request

```shell
curl -u "66:tok3ntok3n" -X "POST" "https://api.bukalapak.com/v2/dompet/topup.json" -d '{"amount": "25000", "bank_account_id": "41812", "bca": "1", "mandiri": "2", "bni": "3", "bri": "4"}'
```

> Success Response

```json
{
  "status": "OK",
  "unique_code": 213,
  "message": "Topup berhasil di-request"
}
```

> Failure Response
>
> #### Invalid topup amount:

```json
{
  "status": "ERROR",
  "unique_code": null,
  "message": "Minimal Top Up adalah Rp. 10.000,- dan Maksimal Rp. 100.000.000,-"
}
```

> #### Invalid bank account id:

```json
{
  "status": "ERROR",
  "unique_code": null,
  "message": "Id rekening bank tidak terdaftar"
}
```

Make topup request for current user.



<aside class="warning">Requires authentication</aside>



### HTTP Request

`POST https://api.bukalapak.com/v2/dompet/topup.json`

### Parameters

| Parameter         |          | Description                                        |
| ----------------- | -------- | -------------------------------------------------- |
| `amount`          | required | Amount to topup.                                   |
| `bank_account_id` | required | Bank account id for current user’s target account. |
| `bca`             | optional | account id displayed for bank BCA.                 |
| `bni`             | optional | account id displayed for bank BNI.                 |
| `bri`             | optional | account id displayed for bank BRI.                 |
| `mandiri`         | optional | account id displayed for bank Mandiri.             |

## QuickBuy Info

> Sample Request

```shell
curl -X "GET" "https://api.bukalapak.com/v2/dompet/quick_buy/info.json?token=000051HF&transaction_id=93"
```

> Success Response

```json
{
  "status": "OK",
  "balance": 0,
  "message": "Anda sudah melakukan request pencairan atau sudah terdaftar di Bukalapak"
}
```

> Failure Response
>
> #### Invalid data:

```json
{
  "status": "ERROR",
  "balance": null,
  "message": "Kode Pembeli atau Nomor Transaksi yang Anda Masukkan Salah"
}
```

> #### No data sent:

```json
{
  "status": "ERROR",
  "balance": null,
  "message": "Kode Pembeli dan Nomor Transaksi tidak boleh kosong"
}
```

Get transaction info for QuickBuy.

### HTTP Request

`GET https://api.bukalapak.com/v2/dompet/quick_buy/info.json`

### Parameters

| Parameter        |          | Description                          |
| ---------------- | -------- | ------------------------------------ |
| `token`          | required | QuickBuy token.                      |
| `transaction_id` | required | Transaction id for current QuickBuy. |

## QuickBuy Withdraw

> Sample Request

```shell
curl -X "POST" "https://api.bukalapak.com/v2/dompet/quick_buy/withdraw.json?token=000051HF&transaction_id=93"
```

> Success Response

```json
{
  "status": "OK",
  "withdrawal_id": 130,
  "message": "Pencairan dengan nomor tiket #C130 akan diproses oleh tim Bukalapak. Dana akan ditransfer ke rekening Anda dalam waktu 2x24 jam."
}
```

> Failure Response
>
> #### No refund found:

```json
{
  "status": "ERROR",
  "withdrawal_id": null,
  "message": "Anda sudah melakukan request pencairan atau sudah terdaftar di Bukalapak"
}
```

> #### No data sent:

```json
{
  "status": "ERROR",
  "withdrawal_id": null,
  "message": "Kode Pembeli dan Nomor Transaksi tidak boleh kosong"
}
```

Ask withdrawal for QuickBuy.

### HTTP Request

`POST https://api.bukalapak.com/v2/dompet/quick_buy/withdraw.json`

### Parameters

| Parameter        |          | Description                          |
| ---------------- | -------- | ------------------------------------ |
| `token`          | required | QuickBuy token.                      |
| `transaction_id` | required | Transaction id for current QuickBuy. |

# Errors

Bukalapak API uses the following error codes:

| Error Code | Meaning                                                      |
| ---------- | ------------------------------------------------------------ |
| 410        | Gone – Consider updating your client application.            |
| 500        | Internal Server Error – We had a problem with our server. Try again later. |

# Favorites

## Get Favorites

> Sample Request

```shell
curl -u "66:tokenkeyiskmzwa8awaa" "https://api.bukalapak.com/v2/favorites.json"
```

> Success Response

```json
{
  "status": "OK",
  "products": [
    {
      "deal_info": {},
      "deal_request_state": "can request",
      "price": 130000,
      "courier": [
        "JNE REG"
      ],
      "seller_username": "meow",
      "seller_name": "Kucing Kurus Mandi di Papan",
      "seller_id": 2,
      "seller_avatar": "https://www.bukalapak.com/images/default_avatar/medium/default.jpg",
      "seller_level": "BL User",
      "seller_level_badge_url": "https://www.bukalapak.com/images/badge/seller/xhdpi/level-1.png",
      "seller_delivery_time": "< 1 jam",
      "seller_positive_feedback": 10,
      "seller_negative_feedback": 10,
      "seller_term_condition": "<p>ini catatanku, mana catatanmu?</p>\n",
      "seller_alert": null,
      "for_sale": true,
      "state_description": [],
      "last_relist_at": "2015-10-16T13:39:14.000+07:00",
      "specs": {
        "brand": "Nokia",
        "operating_system": "Symbian",
        "features": "Tahan Banting",
        "bentuk": "Klasik (Bar)",
        "display_size": "1.8\"",
        "camera": "No Camera",
        "garansi": "2 tahun",
        "network": "GSM",
        "body_color": "hitam"
      },
      "force_insurance": false,
      "free_shipping_coverage": [],
      "id": "17",
      "url": "https://www.bukalapak.com/p/hp-elektronik/handphone-hp/17-jual-nokia-3310",
      "name": "nokia 3310",
      "active": true,
      "city": "Kab. Pasuruan",
      "province": "Jawa Timur",
      "weight": 1000,
      "image_ids": [
        44
      ],
      "images": [
        "https://www.bukalapak.com/system4/images/4/4/large/nokia3310.jpg"
      ],
      "small_images": [
        "https://www.bukalapak.com/system4/images/4/4/small/nokia3310.jpg"
      ],
      "desc": "THOR HANDPHONE!!!",
      "condition": "used",
      "nego": false,
      "stock": 130,
      "minimum_negotiable": null,
      "view_count": 12,
      "sold_count": 0,
      "waiting_payment": 0,
      "favorited": false,
      "created_at": "2015-10-16T13:39:14.000+07:00",
      "product_sin": [],
      "category_id": 2,
      "category": "Handphone (HP)",
      "category_structure": [
        "HP & Elektronik",
        "Handphone (HP)"
      ],
      "interest_count": 1
    }
  ],
  "message": null
}
```

Get favorite product list for the logged in user.



<aside class="warning">Requires authentication</aside>



### HTTP Rquest

`GET https://api.bukalapak.com/v2/favorites.json`

### Parameters

| Parameter  |          | Description                                                  |
| ---------- | -------- | ------------------------------------------------------------ |
| `page`     | optional | Page number to display. Default value is `1`.                |
| `per_page` | optional | Number of favorite products to display per page. Default value is `18`. |
| `sort_by`  | optional | Possible values are `terbaru`, `termurah`, and `termahal`. Default value is `terbaru`. |

## Get User Favorites

> Sample Request

```shell
curl -X "GET" "https://api.bukalapak.com/v2/favorites/sayurkangkung.json"
```

> Success Response

```json
{
  "status": "OK",
  "products": [
    {
      "deal_info": {},
      "deal_request_state": "can request",
      "price": 170000,
      "courier": [
        "JNE REG"
      ],
      "seller_username": "meow",
      "seller_name": "Kucing Kurus Mandi di Papan",
      "seller_id": 2,
      "seller_avatar": "https://www.bukalapak.com/images/default_avatar/medium/default.jpg",
      "seller_level": "BL User",
      "seller_level_badge_url": "https://www.bukalapak.com/images/badge/seller/xhdpi/level-1.png",
      "seller_delivery_time": "< 1 jam",
      "seller_positive_feedback": 10,
      "seller_negative_feedback": 10,
      "seller_term_condition": "<p>ini catatanku, mana catatanmu?</p>\n",
      "seller_alert": null,
      "for_sale": true,
      "state_description": [],
      "last_relist_at": "2015-09-22T10:48:23.000+07:00",
      "specs": {
        "type": null,
        "brand": null,
        "ukuran": null,
        "bahan": null
      },
      "force_insurance": null,
      "free_shipping_coverage": [],
      "id": "16",
      "url": "https://www.bukalapak.com/p/hobi-hiburan/mainan/static-figure/16-jual-starly-evolution-pack-pokemon-figure-takara-tomy",
      "name": "Starly Evolution Pack - Pokemon Figure Takara Tomy",
      "active": true,
      "city": "Kab. Pasuruan",
      "province": "Jawa Timur",
      "weight": 1000,
      "image_ids": [
        43
      ],
      "images": [
        "https://www.bukalapak.com/system4/images/4/3/large/2015-09-28T16%253A24%253A23%252B07%253A00.jpg"
      ],
      "small_images": [
        "https://www.bukalapak.com/system4/images/4/3/small/2015-09-28T16%253A24%253A23%252B07%253A00.jpg"
      ],
      "desc": "Pokemon Figure Takara Tomy Starly-Staravia-Staraptor Evolution Set<br/>Kondisi : Starly &amp; Staraptor Baru (MISB), Staravia Loose 90% masih bagus<br/>Merk : Takara Tomy<br/>Ukuran : +- 4cm Normal Size<br/>Karakter : Starly, Staravia, Staraptor<br/>Harga Nett",
      "condition": "new",
      "nego": false,
      "stock": 14,
      "minimum_negotiable": null,
      "view_count": 4,
      "sold_count": 1,
      "waiting_payment": 0,
      "favorited": false,
      "created_at": "2015-09-28T16:24:23.000+07:00",
      "product_sin": [],
      "category_id": 216,
      "category": "Static Figure",
      "category_structure": [
        "Hobi & Hiburan",
        "Mainan",
        "Static Figure"
      ],
      "interest_count": 15
    }
  ],
  "message": null
}
```

> Failure Response

```json
{
  "status": "ERROR"
  "products": null
  "message": "User tidak ditemukan"
}
```

Get favorite product list for the requested user.

### HTTP Request

`GET https://api.bukalapak.com/v2/favorites/:username.json`

### Parameters

| Parameter  |          | Description                                                  |
| ---------- | -------- | ------------------------------------------------------------ |
| `username` | required | The username of the requested user.                          |
| `page`     | optional | Page number to display. Default value is `1`.                |
| `per_page` | optional | Number of favorite products to display per page. Default value is `18`. |
| `sort_by`  | optional | Possible values are `terbaru`, `termurah`, and `termahal`. Default value is `terbaru`. |

## Add to Favorites

> Sample Request

```shell
curl -u "66:tokenkeyiskmzwa8awaa" -X "POST" "https://api.bukalapak.com/v2/favorites/mx5q/add.json"
```

> Success Response

```json
{
  "status": "OK",
  "message": "Produk telah ditambahkan ke daftar favorit kamu"
}
```

Add product to logged in user’s favorite list.



<aside class="warning">Requires authentication</aside>



### HTTP Request

`POST https://api.bukalapak.com/v2/favorites/:id/add.json`

### Parameters

| Parameter |          | Description          |
| --------- | -------- | -------------------- |
| `id`      | required | Target product’s ID. |

## Bulk Add to Favorites

> Sample Request

```shell
curl -u "66:tokenkeyiskmzwa8awaa" -X "POST" "https://api.bukalapak.com/v2/favorites/bulk_add.json" -d '{"products_id":["g","z","s","q","b"]}' -H "Content-Type: application/json"
```

> Success Response

```json
{
  "status":"OK",
  "message":"5 barang berhasil di-set favorite",
  "success":["g","z","s","q","b"],
  "fail":[]
}
```

Add many products to logged in user’s favorite list.



<aside class="warning">Requires authentication</aside>



### HTTP Request

`POST https://api.bukalapak.com/v2/favorites/bulk_add.json`

### Parameters

| Parameter     |          | Description          |
| ------------- | -------- | -------------------- |
| `products_id` | required | Target products' ID. |

## Remove from Favorites

> Sample Request

```shell
curl -u "66:tok3ntok3n" "https://api.bukalapak.com/v2/favorites/mx5q/remove.json"
```

> Success Response

```json
{
  "status": "OK",
  "message": "Produk telah dihapus dari daftar favorit kamu"
}
```

Remove product from logged in user’s favorite list.



<aside class="warning">Requires authentication</aside>



### HTTP Request

`DELETE https://api.bukalapak.com/v2/favorites/:id/remove.json`

### Parameters

| Parameter |          | Description          |
| --------- | -------- | -------------------- |
| `id`      | required | Target product’s ID. |

## Bulk Remove from Favorites

> Sample Request

```shell
curl -u "66:tok3ntok3n" -X "PATCH" "https://api.bukalapak.com/v2/favorites/bulk_remove.json" -d '{"products_id":["g","z","s","q","b"]}' -H "Content-Type: application/json"
```

> Success Response

```json
{
  "status":"OK",
  "message":"5 barang berhasil di-unset favorite",
  "success":["g","z","s","q","b"],
  "fail":[]
}
```

Remove many products from logged in user’s favorite list.



<aside class="warning">Requires authentication</aside>



### HTTP Request

`PATCH https://api.bukalapak.com/v2/favorites/bulk_remove.json`

### Parameters

| Parameter     |          | Description          |
| ------------- | -------- | -------------------- |
| `products_id` | required | Target products' ID. |

# Images

## Create Product Image

> Sample Request

```shell
curl -u 15:tokenkeyiskmzwa8awaa https://api.bukalapak.com/v2/images.json -F file=@product-image.png -X POST
```

> Success Response

```json
{
  "status": "OK",
  "id": "157324",
  "message": null
}
```

> Failure Response
>
> #### No file uploaded

```json
{
  "status": "ERROR",
  "id": "null",
  "message": "Harus ada file gambar"
}
```

> #### Invalid file type:

```json
{
  "status": "ERROR",
  "id": "null",
  "message": "Harus berupa file gambar"
}
```

> #### Invalid image dimension:

```json
{
  "status": "ERROR",
  "id": "null",
  "message": "Ukuran gambar Anda 200x200, ukuran minimal adalah 300x300"
}
```



Uploaded image must have a minimum resolution of 300x300.



### HTTP Request

`POST https://api.bukalapak.com/v2/images.json`

### Parameters

None

### POST request data

None

## Check Image Status

Check image status whether it has been assigned to a product or not.

> Sample Request

```shell
curl -u 15:tokenkeyiskmzwa8awaa https://api.bukalapak.com/v2/images/status/181244.json
```

> Success Response
>
> #### Response for image without product

```json
{
  "status": "OK",
  "id": 1838301,
  "message": "Orphaned"
}
```

> #### Response for image that has been assigned to product

```json
{
  "status": "ERROR",
  "id": 1838301,
  "message": "Assigned"
}
```

> Failure Response

```json
{
  "status": "ERROR",
  "id": 1838301,
  "message": "Gambar tidak ditemukan"
}
```

### HTTP Request


GET https://api.bukalapak.com/v2/images/status/:id.json`

### Parameters

| Parameter |          | Description       |
| --------- | -------- | ----------------- |
| `id`      | required | Image identifier. |

## Delete Product Image

> Sample Request

```shell
curl -u 15:tokenkeyiskmzwa8awaa -X DELETE https://api.bukalapak.com/v2/images/181244.json
```

> Success Response

```json
{
  "status": "OK",
  "id": 1838301,
  "message": "Gambar dihapus"
}
```

> Failure Response
>
> #### Response for nonexistent image

```json
{
  "status": "ERROR",
  "user_id": 1838301,
  "message": "Gagal menghapus gambar"
}
```

> #### Response when trying to delete another user’s image

```json
{
  "status": "ERROR",
  "user_id": 1838301,
  "message": "Tidak dapat menghapus gambar milik pengguna lain"
}
```

### HTTP Request

`DELETE https://api.bukalapak.com/v2/images/:id.json`

### Parameters

| Parameter |          | Description       |
| --------- | -------- | ----------------- |
| `id`      | required | Image identifier. |

## Set Image as Primary

> Sample Request

```shell
curl -u 15:tokenkeyiskmzwa8awaa -X PATCH https://api.bukalapak.com/v2/images/181244/primary.json
```

> Success Response

```json
{
  "status": "OK",
  "id": 1838301,
  "message": "Gambar utama telah dipilih"
}
```

> Failure Response
>
> #### Response for nonexistent image

```json
{
  "status": "ERROR",
  "id": null,
  "message": "Gagal mengganti gambar"
}
```

> #### Response when trying to delete another user’s image

```json
{
  "status": "ERROR",
  "id": null,
  "message": "Tidak dapat mengganti gambar utama"
}
```

### HTTP Request

`PATCH https://api.bukalapak.com/v2/images/:id/primary.json`

### Parameters

| Parameter |          | Description       |
| --------- | -------- | ----------------- |
| `id`      | required | Image identifier. |

# Additional Informations

## Get Supported Banks List

> Sample Request

```shell
curl https://api.bukalapak.com/v2/banks.json
```

> Success Response

```json
{
  "status":"OK",
  "banks": [
    "Bank Central Asia (BCA)",
    "Bank Mandiri",
    "Bank Negara Indonesia (BNI)",
    "Bank Rakyat Indonesia (BRI)",
    ...
    "Bank Perkreditan Rakyat (BPR KS)"
    ],
  "message":null
}
```

Gets list of supported banks

### HTP Request

`GET https://api.bukalapak.com/v2/banks.json`

### Parameters

None

## Get Active Bank Account List

> Sample Request

```shell
curl https://api.bukalapak.com/v2/bank_accounts.json
```

> Success Response

```json
{
    "status": "OK",
    "accounts": [
        {
            "id": 1,
            "bank": "bca",
            "branch": "Bank BCA, Jakarta",
            "name": "PT Bukalapak",
            "number": "XXX XXX 2527",
            "payment": true,
            "topup": true
        },
        ...
        {
            "id": 4,
            "bank": "bri",
            "branch": "Bank BRI, Jakarta",
            "name": "PT Bukalapak",
            "number": "XXX XXX XXX 743 303",
            "payment": true,
            "topup": true
        }
    ],
    "message": null
}
```

Gets list of active banks

### HTP Request

`GET https://api.bukalapak.com/v2/banks.json`

### Parameters

None

## Get Address List

> Sample Request

```shell
curl https://api.bukalapak.com/v2/address.json
```

> Success Response

```json
{
  "status":"OK",
  "address": {
    "Bali": {
      "Badung": [
        "Abiansemal",
        "Jimbaran",
        "Kuta",
        "Legian",
        "Menguwi",
        "Ngurah Rai",
        "Nusa Dua",
        "Petang",
        "Sanur"
      ],
      ...
      "Toba Samosir": [
        "Ajibata",
        "Balige",
        "Bor Bor",
        "Habinsaran",
        "Lagu Boti",
        "Lumban Julu",
        "Nassau",
        "Pintu Pohan Meranti",
        "Porsea",
        "Siantar Narumonda",
        "Sigumpar",
        "Silaen",
        "Tampahan",
        "Uluan"
      ]
    }
  },
  "message":null
}
```

Gets list of all provinces, cities, and districts

### HTTPRequest

`GET https://api.bukalapak.com/v2/address.json`

### Parameters

None

## Get Provinces List

> Sample Request

```shell
curl https://api.bukalapak.com/v2/address/provinces.json
```

> Success Response

```json
{
  "status":"OK",
  "provinces": [
    "Bali",
    "Banten",
    ...
    "Sumatera Utara"
    ],
  "message":null
}
```

Gets list of provinces

### HTTP Request


GET https://api.bukalapak.com/v2/address/provinces.json`

### Parameters

None

## Get Cities List

> Sample Request

```shell
curl https://api.bukalapak.com/v2/address/cities.json?province=DKI+Jakarta
```

> Success Response

```json
{
  "status":"OK",
  "cities": [
    "Jakarta Barat",
    "Jakarta Pusat",
    "Jakarta Selatan",
    "Jakarta Timur",
    "Jakarta Utara",
    "Kepulauan Seribu"
    ],
  "message":null
}
```

Gets list of cities

### HTTP Reques

`GET https://api.bukalapak.com/v2/address/cities.json`

### Parameters

| Property   |          | Description                                |
| ---------- | -------- | ------------------------------------------ |
| `province` | required | Name of the province to get city list for. |

## Get Districts List

> Sample Request

```shell
curl "https://api.bukalapak.com/v2/address/districts.json?province=DKI+Jakarta&city=Jakarta+Utara"
```

> Success Response

```json
{
  "status":"OK",
  "districts": [
    "Cilincing",
    "Kelapa Gading",
    "Koja",
    "Pademangan",
    "Penjaringan",
    "Tanjung Priok"
    ],
  "message":null
}
```

Gets list of districts

### HTTP Request


GET https://api.bukalapak.com/v2/address/districts.json`

### Parameters

| Property   |          | Description                                    |
| ---------- | -------- | ---------------------------------------------- |
| `province` | required | Name of the province to get district list for. |
| `city`     | required | Name of the city to get district list for.     |

## Get District Detail

> Sample Request

```shell
curl "https://api.bukalapak.com/v2/address/district_detail.json?district=Mampang+Prapatan"
```

> Success Response

```json
{
  "status":"OK",
  "district":"Mampang Prapatan",
  "city":"Jakarta Selatan",
  "province":"DKI Jakarta".
  "message":null
}
```

Gets list of districts

### HTTP Request

`GET ttps://api.bukalapak.com/v2/address/district_detail.json`

### Parameters

| Property   |          | Description                           |
| ---------- | -------- | ------------------------------------- |
| `district` | required | Name of the district to get info for. |

## Get Available Couriers

> Sample Request

```shell
curl "https://api.bukalapak.com/v2/available_couriers.json"
```

> Success Response

```json
{
  "status": "OK",
  "message": null,
  "available_couriers": [
    {
      "courier": "JNE REG",
      "is_express": false,
      "is_required": true,
      "info": "Jasa pengiriman JNE REG merupakan kurir wajib karena memiliki jangkauan pengiriman terluas. Jika Anda menggunakan kurir selain JNE REG sebagai kurir utama Anda, silakan tambahkan keterangan tersebut pada <strong>Catatan Pelapak</strong>."
    },
    {
      "courier": "JNE YES",
      "is_express": true,
      "is_required": false,
      "info": ""
    },
    {
      "courier": "TIKI Reg",
      "is_express": false,
      "is_required": false,
      "info": ""
    },
    {
      "courier": "TIKI ONS",
      "is_express": true,
      "is_required": false,
      "info": ""
    },
    {
      "courier": "Pos Kilat Khusus",
      "is_express": false,
      "is_required": false,
      "info": ""
    },
    {
      "courier": "RPX Economy Package",
      "is_express": false,
      "is_required": false,
      "info": ""
    },
    {
      "courier": "RPX Next Day Package",
      "is_express": true,
      "is_required": false,
      "info": ""
    },
    {
      "courier": "Wahana Tarif Normal",
      "is_express": false,
      "is_required": false,
      "info": ""
    },
    {
      "courier": "SiCepat REG",
      "is_express": false,
      "is_required": false,
      "info": ""
    },
    {
      "courier": "SiCepat BEST",
      "is_express": true,
      "is_required": false,
      "info": ""
    }
  ]
}
```

Gets list of available couriers

### HTTP Request

`GET https://api.bukalapak.com/v2/available_couriers.json`

### Parameters

None

## Get Flash Banners

> Sample Request

```shell
curl https://api.bukalapak.com/v2/flash_banners.json
```

> Sample Response

```json
{
  "status": "OK",
  "banners": [
    {
      "image": "https://s0.bukalapak.com/system4/flash_banners/3010/mobile/rsz_bedcover_480x195.jpg",
      "description": "Bed cover Cantik Harga mulai 150 Ribuan",
      "info": {
        "type": "campaign",
        "id": 2155,
        "url": "https://www.bukalapak.com/promo/bed-cover-cantik-harga-mulai-150-ribuan",
        "promo_due": "2016-01-19T23:59:00.000+07:00"
      }
    },
    {
      "image": "https://s2.bukalapak.com/uploads/flash_banner/5167/mobile/%28PROMO%29-Bedug-Berkah_BL_SALES_480X195.jpg",
      "description": "promo diskon belanja ramadhan",
      "info": {
        "type": "special_promo",
        "id": 37,
        "url": "https://www.bukalapak.com/promo-diskon-belanja-ramadhan-lebaran"
      }
    },
  ],
  "message": null
}
```

Gets current flash banners' informations. Flash banners are the topmost banners on Bukalapak homepage. There are 3 main type of flash banner, that is: campaign, special_promo, and url. The type of flash banner described on field “type” in “info”. When a flash banner has “special_promo” type, you can get special promo information by calling end point “Get Special Promo” from Deals section.

### HTTP Requet

`GET https://api.bukalapak.com/v2/flash_banners.json`

### Parameters

None

# Labels

## Get User Labels

> Sample Request

```shell
curl -u "66:tokenkeyiskmzwa8awaa" "https://api.bukalapak.com/v2/labels/index.json"
```

> Success Response

```json
{
  "status": "OK",
  "labels": [
    {
      "id": 24,
      "name": "Buku",
      "slug": "buku",
      "description": null
    },
    {
      "id": 27,
      "name": "Busana",
      "slug": "busana",
      "description": null
    },
    {
      "id": 30,
      "name": "Makanan",
      "slug": "makanan",
      "description": null
    },
    {
      "id": 33,
      "name": "Peralatan Kantor",
      "slug": "peralatan-kantor",
      "description": "deskripsi memotivasi"
    }
  ],
  "message": null,
  "max_label": 10
}
```

Get label list for the logged in user.



<aside class="warning">Requires authentication</aside>



### HTTP Requst

`GET https://api.bukalapak.com/v2/labels/index.json`

### Parameters

None

## Add Label

> Sample Request

```shell
curl -u "66:tokenkeyiskmzwa8awaa" -X "POST" "https://api.bukalapak.com/v2/labels/create.json" -d "labels_label[name]=Music&labels_label[description]=all about music"
```

> Success Response

```json
{
  "status": "OK",
  "label": {
    "id": 130,
    "name": "Mainan",
    "slug": "mainan",
    "description": "tentang mainan"
  },
  "message": "Pembuatan label berhasil"
}
```

> Failure Response

```json
{
  "status": "ERROR",
  "label": {
    "id": null,
    "name": "",
    "slug": null,
    "description": ""
  },
  "message": "Nama label wajib diisi"
}
```

Add label for logged user.



<aside class="warning">Requires authentication</aside>



### HTTP Request

`POST https://api.bukalapak.com/v2/labels/create.json`

### Parameters

| Parameter     |          | Description               |
| ------------- | -------- | ------------------------- |
| `name`        | required | The name of label.        |
| `description` | required | The description of label. |

## Edit Label

> Sample Request

```shell
curl -u "66:tokenkeyiskmzwa8awaa" -X "PUT" "https://api.bukalapak.com/v2/labels/update/:id.json" -d "labels_label[name]=Toys&labels_label[description]=all about toys"
```

> Success Response

```json
{
  "status": "OK",
  "label": {
    "id": 130,
    "name": "Toys",
    "slug": "toys",
    "description": "all about toys"
  },
  "message": "Label berhasil disimpan"
}
```

> Failure Response

```json
{
  "status": "ERROR",
  "label": {
    "id": 130,
    "name": "",
    "slug": "mainan",
    "description": ""
  },
  "message": "Label gagal disimpan"
}
```

Edit label for logged user.



<aside class="warning">Requires authentication</aside>



### HTTP Request

```
PUT https://api.bukalapak.com/v2/labels/update/:id.json
```

### Parameters

| Parameter     |          | Description               |
| ------------- | -------- | ------------------------- |
| `name`        | required | The name of label.        |
| `description` | required | The description of label. |

## Delete Label

> Sample Request

```shell
curl -u "66:tokenkeyiskmzwa8awaa" -X "DELETE" "https://api.bukalapak.com/v2/labels/delete/:id.json"
```

> Success Response

```json
{
  "status": "OK",
  "label": {
    "id": 130,
    "name": "Toys",
    "slug": "toys",
    "description": "tentang mainan"
  },
  "message": "Label berhasil dihapus"
}
```

Delete label for logged user.



<aside class="warning">Requires authentication</aside>



### HTTP Request

`DELETE https://api.bukalapak.com/v2/labels/delete/:id.json`

### Parameters

None

# Messages

## Get Inbox

> Sample Request
>
> #### Get specific page

```shell
curl -u 67287:lXymG93y83m6RHzZV5FY https://api.bukalapak.com/v2/messages.json?page=1
```

> #### Get only inboxes with unread messages

```shell
curl -u 67287:lXymG93y83m6RHzZV5FY https://api.bukalapak.com/v2/messages.json?filter=unread
```

> #### Get only inboxes containing specific words

```shell
curl -u 67287:lXymG93y83m6RHzZV5FY https://api.bukalapak.com/v2/messages.json?search="nanya+om"
```

> Success Response

```json
{
  "status": "OK",
  "unread": 0,
  "inbox": [
    {
      "id": "520e0474e42b5658ab00001c",
      "updated_at": "2013-12-03T08:54:49+07:00",
      "partner_id": "155905",
      "partner_name": "Zakka Fauzan Muhammad",
      "partner_avatar": "https://s0.bukalapak.com/system/avatars/055/f87/412/9cf/0ec/36837/thumb/IMG1.png?1387424302",
      "user_id": "62817",
      "user_name": "Sayur Kangkung",
      "last_message": "sip diterima san...",
      "last_message_read": false,
      "last_message_sent": "2014-02-04T12:34:37+07:00"
    },
    {
      "id": "5125950c948f5c1a05000662",
      "updated_at": "2013-12-02T21:50:51+07:00",
      "partner_id": "39435",
      "partner_name": "Cecep",
      "partner_avatar": "https://s1.bukalapak.com/system/avatars/055/f87/412/9cf/0ec/36837/thumb/IMG2.png?1387424302",
      "user_id": "62817",
      "user_name": "Sayur Kangkung",
      "last_message": "ok",
      "last_message_read": true,
      "last_message_sent": "2014-02-04T12:34:37+07:00"
    },
    {
      "id": "516ffb155ff21f7b53000178",
      "updated_at": "2013-12-02T11:26:03+07:00",
      "partner_id": "78285",
      "partner_name": "Khairul",
      "partner_avatar":"https://s1.bukalapak.com/system/avatars/055/f87/412/9cf/0ec/36837/thumb/IMG3.png?1387424302",
      "user_id": "62817",
      "user_name": "Sayur Kangkung",
      "last_message": "kung",
      "last_message_read": true,
      "last_message_sent": "2014-02-04T12:34:37+07:00"
    },
    {
      "id": "4ffab90e5ff21f447e000004",
      "updated_at": "2013-07-28T17:05:40+07:00",
      "partner_id": "57451",
      "partner_name": "Renjay Shop",
      "partner_avatar":"https://s0.bukalapak.com/system/avatars/055/f87/412/9cf/0ec/36837/thumb/IMG4.png?1387424302",
      "user_id": "62817",
      "user_name": "Sayur Kangkung",
      "last_message": "testing...",
      "last_message_read": true,
      "last_message_sent": "2014-02-04T12:34:37+07:00"
    }
  ]
}
```

Get current user’s inbox

### HTTP equest

`GET https://api.bukalapak.com/v2/messages.json`

### Parameters

| Parameter  |          | Description                                                  |
| ---------- | -------- | ------------------------------------------------------------ |
| `page`     | optional | Page number to display. Default value is `1`.                |
| `per_page` | optional | Number of record to display per page. Default value is `10`. |
| `filter`   | optional | If defined with `unread`, return only inboxes with unread messages. Return all inbox if undefined or defined with other values. |
| `search`   | optional | Words to be searched on messages.                            |

## Get Emoticons

> Sample Request

```shell
curl -u 67287:lXymG93y83m6RHzZV5FY https://api.bukalapak.com/v2/messages/emoticons.json
```

> Success Response

```json
{
  "status": "OK",
  "emoticon_set": [
    [" :) ","https://www.bukalapak.com/images/emoji/smile.gif"],
    [" [marah] ","https://www.bukalapak.com/images/emoji/anger.gif"],
    [" [tai] ","https://www.bukalapak.com/images/emoji/bad.gif"],
    [" [ngopi] ","https://www.bukalapak.com/images/emoji/coffee.gif"],
    [" [gaya] ","https://www.bukalapak.com/images/emoji/cool.gif"],
    [" [nangis] ","https://www.bukalapak.com/images/emoji/cry.gif"],
    [" [kecoa] ","https://www.bukalapak.com/images/emoji/dog.gif"],
    [" [ngiler] ","https://www.bukalapak.com/images/emoji/envy.gif"],
    [" [takut] ","https://www.bukalapak.com/images/emoji/fear.gif"],
    [" :D ","https://www.bukalapak.com/images/emoji/grin.gif"],
    [" [bunuh] ","https://www.bukalapak.com/images/emoji/kill.gif"],
    [" [suka] ","https://www.bukalapak.com/images/emoji/love.gif"],
    [" [ok] ","https://www.bukalapak.com/images/emoji/ok.gif"],
    [" [babi] ","https://www.bukalapak.com/images/emoji/pig.gif"],
    [" [muntah] ","https://www.bukalapak.com/images/emoji/puke.gif"],
    [" [masa si] ","https://www.bukalapak.com/images/emoji/question.gif"],
    [" :( ","https://www.bukalapak.com/images/emoji/sad.gif"],
    [" :o ","https://www.bukalapak.com/images/emoji/shock.gif"],
    [" [wow] ","https://www.bukalapak.com/images/emoji/shuai.gif"],
    [" [ngantuk] ","https://www.bukalapak.com/images/emoji/sleepy.gif"],
    [" [ngrokok] ","https://www.bukalapak.com/images/emoji/smoke.gif"],
    [" [ngupil] ","https://www.bukalapak.com/images/emoji/stupid.gif"],
    [" [cape de] ","https://www.bukalapak.com/images/emoji/sweat.gif"],
    [" [jelek] ","https://www.bukalapak.com/images/emoji/thumbdown.gif"],
    [" :P ","https://www.bukalapak.com/images/emoji/tongue.gif"],
    [" [mikir] ","https://www.bukalapak.com/images/emoji/uplook.gif"],
    [" [ketawa] ","https://www.bukalapak.com/images/emoji/wink.gif"],
    [" [jempol] ","https://www.bukalapak.com/images/emoji/zan.gif"]
  ]
}
```

### HTTP Request

`GET https://api.bukalapak.com/v2/messages/emoticons.json`

### Parameters

None

## Get Conversation

> Sample Request

```shell
curl -u 67287:lXymG93y83m6RHzZV5FY https://api.bukalapak.com/v2/messages/516d3299425762188f000011.json?per_page=5&keep_unread=1
```

> Success Response

```json
{
  "status": "OK",
  "instant_messages": [
    {
      "id": "529c0bdb521fb0dc4500025e",
      "body": "kung",
      "created_at": "2013-12-02T11:26:03+07:00",
      "inbox_id": "516ffb155ff21f7b53000178",
      "read": true,
      "receiver_id": "78285",
      "receiver_name": "Khairul",
      "receiver_avatar": "https://s0.bukalapak.com/system/avatars/055/f87/412/9cf/0ec/36837/thumb/xkcd.png?1387424302",
      "sender_id": "62817",
      "sender_name": "Sayur Kangkung",
      "sender_avatar": "https://s1.bukalapak.com/system/avatars/055/f87/412/9cf/0ec/36837/thumb/sayur.png?1387424302",
      "updated_at": "2013-12-02T11:26:03+07:00"
    },
    {
      "id": "529c0b01e42b565bfb00047a",
      "body": "kung",
      "created_at": "2013-12-02T11:22:25+07:00",
      "inbox_id": "516ffb155ff21f7b53000178",
      "read": true,
      "receiver_id": "78285",
      "receiver_name": "Khairul",
      "receiver_avatar": "https://s0.bukalapak.com/system/avatars/055/f87/412/9cf/0ec/36837/thumb/xkcd.png?1387424302",
      "sender_id": "62817",
      "sender_name": "Sayur Kangkung",
      "sender_avatar": "https://s1.bukalapak.com/system/avatars/055/f87/412/9cf/0ec/36837/thumb/sayur.png?1387424302",
      "updated_at": "2013-12-02T11:22:25+07:00"
    }
  ],
  "message": null
}
```

> Failure Response
>
> #### Response when trying to get other user’s conversation

```json
{
  "status": "ERROR",
  "instant_messages": null,
  "message": "Gagal membaca message, hanya bisa membuka inbox milik masing-masing"
}
```

Get current user’s selected conversation

### HTTP Requst

`GET https://api.bukalapak.com/v2/messages/:id.json`

### Parameters

| Parameter     |          | Description                                                  |
| ------------- | -------- | ------------------------------------------------------------ |
| `page`        | optional | Page number to display. Default value is `1`.                |
| `per_page`    | optional | Number of record to display per page. Default value is `10`. |
| `keep_unread` | optional | If defined with `1`, don’t flag the inbox as read.           |

## Get Message

> Sample Request

```shell
curl -u 67287:lXymG93y83m6RHzZV5FY https://api.bukalapak.com/v2/messages/im/516e2565177961034c000002.json
```

> Success Response

```json
{
  "status": "OK",
  "instant_message": {
    "id": "524673ca318b27602f00000a",
    "body": "Halo Sayur Kangkung,\n\nKami telah memblokir lapakmu untuk barang:\n<strong>[DT] WIMCYCLE ADRENALINE DH TEAM 2012 - SIZE M</strong>\nSeharga: Rp 125.000\nKondisi barang: Bekas\n\nBarang diblokir karena alasan berikut ini:\n- Harga tidak sesuai\n\nJika kamu ingin mengaktifkan kembali lapakmu, kami minta kerjasama kamu untuk memperbaikinya. Kamu bisa langsung memperbaiki dengan klik https://www.bukalapak.com/products/ggm8-jual-dt-wimcycle-adrenaline-dh-team-2012-size-m/edit.\n\nTerima kasih atas perhatian & kerjasama Kamu.\n\n",
    "created_at": "2013-09-28T13:14:34+07:00",
    "inbox_id": "524673c9318b27602f000009",
    "read": true,
    "receiver_id": "62817",
    "receiver_name": "Sayur Kangkung",
    "receiver_avatar": "https://s0.bukalapak.com/system/avatars/055/f87/412/9cf/0ec/36837/thumb/xkcd.png?1387424302",
    "sender_id": "225448",
    "sender_name": "roni hafid",
    "sender_avatar": "https://s1.bukalapak.com/system/avatars/055/f87/412/9cf/0ec/36837/thumb/sayur.png?1387424302",
    "updated_at": "2013-12-03T18:39:41+07:00"
  },      
  "message": null
}
```

> Failure Response
>
> #### Response when trying to get other user’s message

```json
{
  "status": "ERROR",
  "instant_messages": null,
  "message": "Gagal membaca message, hanya bisa membuka inbox milik masing-masing"
}
```

Get current user’s selected message



Note that calling this will also flag the selected message as read.



### HTTP Request
`GET https://api.bukalapak.com/v2/messages/im/:id.json`

### Parameters

None

## Create Message

> Sample Request

```shell
curl -u 110677:JheQQS0OKApu3hGJwkRH -d '{ "instant_message": {"receiver_id": "110675", "category": "0", "body_bb": "tesssss", "client_id": "1223b8c30a347321299611f873b449ad"}, "product_id": "mwza" }' https://api.bukalapak.com/v2/messages.json -H "Content-Type: application/json" -X POST
```

> Success Response

```json
{
  "status": "OK",
  "id": "516d303c425762188f000007",
  "client_id": "1223b8c30a347321299611f873b449ad",
  "conversation_id": "5252262184eab00c8300000c",
  "message": "Pesan terkirim"
}
```

> Failure Response
>
> #### Required parameters not supplied

```json
{
  "status": "ERROR",
  "id": null,
  "client_id": "1223b8c30a347321299611f873b449ad",
  "conversation_id": "5252262184eab00c8300000c",
  "message": "Gagal mengirim pesan: harap menggunakan format yang seharusnya"
}
```

> #### Invalid receiver id

```json
{
  "status": "ERROR",
  "id": null,
  "client_id": "1223b8c30a347321299611f873b449ad",
  "conversation_id": "5252262184eab00c8300000c",
  "message": "Tidak dapat mengirim pesan kepada pembeli"
}
```

> #### Wrong category used for non-admin receiver

```json
{
  "status": "ERROR",
  "id": null,
  "client_id": "1223b8c30a347321299611f873b449ad",
  "conversation_id": "5252262184eab00c8300000c",
  "message": "Pengiriman pesan untuk kategori ini hanya dapat ditujukan kepada admin"
}
```

> #### Other failures response

```json
{
  "status": "ERROR",
  "id": null,
  "client_id": "1223b8c30a347321299611f873b449ad",
  "conversation_id": "5252262184eab00c8300000c",
  "message": "Gagal mengirim pesan"
}
```



<aside class="warning">Requires authentication</aside>



### HTTP Request

`POST https://api.bukalapak.com/v2/messages.json`

### Parameters

None

### POST Request Data

| Property          |          | Description                                      |
| ----------------- | -------- | ------------------------------------------------ |
| `instant_message` | required | New message to be sent                           |
| `product_id`      | optional | ID of the product the sender wants to ask about. |

The `instant_message` parameter contains these properties:

| Property      |          | Description                                                  |
| ------------- | -------- | ------------------------------------------------------------ |
| `receiver_id` | required | Message receiver’s user ID                                   |
| `category`    | required | Message category:0 = normal message1 = transaction2 = BukaDompet (withdrawal, topup)3 = feature & error4 = suggestion5 = question6 = partnershipNote that category > 0 must be addressed to admin only. |
| `body_bb`     | required | Message’s content                                            |
| `client_id`   | optional | Client generated id, a unique string to identify the message |



Note : if `client_id` is not supplied on request, the response will also contain `client_id` with `null` value.



## Delete Conversation

> Sample Request

```shell
curl -u 110677:JheQQS0OKApu3hGJwkRH https://api.bukalapak.com/v2/messages/516d3299425762188f000011.json -H "Content-Type: application/json" -X DELETE
```

> Success Response

```json
{
  "status": "OK",
  "id": "516d3299425762188f000011",
  "message": "Conversation berhasil dihapus"
}
```

> Failure response:

```json
{
  "status": "ERROR",
  "id": "516d3299425762188f000011",
  "message": "Conversation gagal dihapus"
}
```

Delete existing conversation



<aside class="warning">Requires authentication</aside>



### HTTP Request

`DELETE https://api.bukalapak.com/v2/messages/:id.json`

### Parameters

| Parameter |          | Description                             |
| --------- | -------- | --------------------------------------- |
| `id`      | required | Identifier for message being destroyed. |

## Delete Message

> Sample Request

```shell
curl -u 110677:JheQQS0OKApu3hGJwkRH https://api.bukalapak.com/v2/messages/516d3299425762188f000015.json -H "Content-Type: application/json" -X DELETE
```

> Success Response

```json
{
  "status": "OK",
  "id": "516d3299425762188f000015",
  "message": "Pesan berhasil dihapus"
}
```

> Failure response:

```json
{
  "status": "ERROR",
  "id": "516d3299425762188f000015",
  "message": "Pesan gagal dihapus"
}
```

Delete existing message



<aside class="warning">Requires authentication</aside>



### HTTP Request

`DELETE https://api.bukalapak.com/v2/messages/im/:id.json`

### Parameters

| Parameter |          | Description                             |
| --------- | -------- | --------------------------------------- |
| `id`      | required | Identifier for message being destroyed. |

# Notifications

## Add Android Device

> Getting the device’s properties

```
//for parameter: manufacturer
String  MANUFACTURER    =   android.os.Build.MANUFACTURER;
//for parameter: model
String  MODEL           =   android.os.Build.MODEL;
//for parameter: product_name
String  PRODUCT         =   android.os.Build.PRODUCT;
```

> Sample Request

```shell
curl -u 66:tok3ntok3n "https://api.bukalapak.com/v2/notifications/android.json" -X POST --data "reg_id=ASD223SDA&model=GG-P4124H&manufacturer=Nokia&name=Lumpia"
```

> Success Response

```json
{
  "status": "OK",
  "message": "Device ditambahkan"
}
```

> Failure Response

```json
{
  "status": "ERROR",
  "message": "Gagal menambahkan device"
}
```

Add user’s Android device to receive notifications.



<aside class="warning">Requires authentication</aside>



### HTTP Request

`POST https://api.bukalapak.com/v2/notifications/android.json`

### Parameters

| Parameter      |          | Description                    |
| -------------- | -------- | ------------------------------ |
| `reg_id`       | required | Registration ID of the device. |
| `model`        | optional | Device model.                  |
| `manufacturer` | optional | Device manufacturer.           |
| `product_name` | optional | Device product name.           |
| `apps_version` | optional | Apps version.                  |

## Update Android Device

Update user’s Android device for receiving notifications.



<aside class="warning">Requires authentication</aside>



> Sample Request

```shell
curl -u 66:tok3ntok3n "https://api.bukalapak.com/v2/notifications/android.json" -X PATCH --data "old_reg_id=ASD223SDA&new_reg_id=RAG2314EN"
```

> Success Response

```json
{
  "status": "OK",
  "message": "Device diupdate"
}
```

> Failure Response

```json
{
  "status": "ERROR",
  "message": "Gagal mengupdate device"
}
```

### HTTP Request

`PATCH https://api.bukalapak.com/v2/notifications/android.json`

### Parameters

| Parameter    |          | Description                         |
| ------------ | -------- | ----------------------------------- |
| `old_reg_id` | required | Registered ID of the device.        |
| `new_reg_id` | required | New registration ID for the device. |

## Remove Android Device

> Sample Request

```shell
curl -u 66:tok3ntok3n "https://api.bukalapak.com/v2/notifications/android.json" -X DELETE --data "reg_id=ASD223SDA"
```

> Success Response

```json
{
  "status": "OK",
  "message": "Device telah dihapus dari daftar"
}
```

> Failure Response

```json
{
  "status": "ERROR",
  "message": "Device dimiliki oleh pengguna lain"
}
```

Remove user’s Android device from receiver devices list.



<aside class="warning">Requires authentication</aside>



### HTTP Request

`DELETE https://api.bukalapak.com/v2/notifications/android.json`

### Parameters

| Parameter |          | Description                    |
| --------- | -------- | ------------------------------ |
| `reg_id`  | required | Registration ID of the device. |

## Add IOS Device

> Sample Request

```shell
curl -u 66:tok3ntok3n "https://api.bukalapak.com/v2/notifications/ios.json" -X POST --data "token=ASD223SDA&model=Iphone 5s&operating_system=IOS7&app_version=1.0"
```

> Success Response

```json
{
  "status": "OK",
  "message": "Device ditambahkan"
}
```

> Failure Response

```json
{
  "status": "ERROR",
  "message": "Gagal menambahkan device"
}
```

Add user’s IOS device to receive notifications.



<aside class="warning">Requires authentication</aside>



### HTTP Request

`POST https://api.bukalapak.com/v2/notifications/ios.json`

### Parameters

| Parameter          |          | Description          |
| ------------------ | -------- | -------------------- |
| `token`            | required | The device token.    |
| `model`            | optional | Device model.        |
| `operating_system` | optional | Device manufacturer. |
| `apps_version`     | optional | Apps version.        |

## Update IOS Device

Update user’s IOS device for receiving notifications.



<aside class="warning">Requires authentication</aside>



> Sample Request

```shell
curl -u 66:tok3ntok3n "https://api.bukalapak.com/v2/notifications/ios.json" -X PATCH --data "old_token=ASD223SDA&new_token=RAG2314EN"
```

> Success Response

```json
{
  "status": "OK",
  "message": "Device diupdate"
}
```

> Failure Response

```json
{
  "status": "ERROR",
  "message": "Gagal mengupdate device"
}
```

### HTTP Request

`PATCH https://api.bukalapak.com/v2/notifications/ios.json`

### Parameters

| Parameter   |          | Description               |
| ----------- | -------- | ------------------------- |
| `old_token` | required | Token of the device.      |
| `new_token` | required | New tokeb for the device. |

## Remove IOS Device

> Sample Request

```shell
curl -u 66:tok3ntok3n "https://api.bukalapak.com/v2/notifications/ios.json" -X DELETE --data "token=ASD223SDA"
```

> Success Response

```json
{
  "status": "OK",
  "message": "Device telah dihapus dari daftar"
}
```

> Failure Response

```json
{
  "status": "ERROR",
  "message": "Device dimiliki oleh pengguna lain"
}
```

Remove user’s IOS device from receiver devices list.



<aside class="warning">Requires authentication</aside>



### HTTP Request

`DELETE https://api.bukalapak.com/v2/notifications/ios.json`

### Parameters

| Parameter |          | Description          |
| --------- | -------- | -------------------- |
| `token`   | required | Token of the device. |

## Logout Device

> Sample Request

```shell
curl -u 66:tok3ntok3n "https://api.bukalapak.com/v2/notifications/logout.json" -X DELETE --data "reg_id=ASD223SDA"
```

> Success Response

```json
{
  "status": "OK",
  "message": "Device telah log out"
}
{
  "status": "OK",
  "message": "Device not found"
}
```

> Failure Response

```json
{
  "status": "ERROR",
  "message": "Gagal log out"
}
```

Logout current user from current device.



<aside class="warning">Requires authentication</aside>



### HTTP Request

`DELETE https://api.bukalapak.com/v2/notifications/logout.json`

### Parameters

| Parameter |          | Description                    |
| --------- | -------- | ------------------------------ |
| `reg_id`  | required | Registration ID of the device. |
| `token`   | required | Token of ios device.           |

Only one of above parameters is required.

## Get Unread Notifications

> Sample Request

```shell
curl -u 66:tok3ntok3n "https://api.bukalapak.com/v2/notifications/unreads.json"
```

> Sample Response

```json
{
  "messages": 0,
  "transactions_need_action_as_seller": 0,
  "transactions_as_buyer": 0,
  "unread_notifications": 0,
  "transactions_need_action_as_buyer": 4,
  "cart_items": 4
}
```

Get numbers of unread messages and transactions.



<aside class="warning">Requires authentication</aside>



### HTTP Request

`GET https://api.bukalapak.com/v2/notifications/unreads.json`

### Parameters

| Parameter |          | Description                    |
| --------- | -------- | ------------------------------ |
| `reg_id`  | required | Registration ID of the device. |

## Set Notifications as Read

> Sample Request

```shell
curl -u 66:tok3ntok3n -X PATCH "https://api.bukalapak.com/v2/notifications.json" --data ""
```

> Sample Response

```json
{
  "status": "OK",
  "message": null
}
```



<aside class="warning">Requires authentication</aside>



### HTTP Request

`PATCH https://api.bukalapak.com/v2/notifications.json`

## Set a Notification as Read

> Sample Request

```shell
curl -u 66:tok3ntok3n -X PATCH "https://api.bukalapak.com/v2/notifications/52a6e5e284eab03aa200013a.json"
```

> Success Response

```json
{
  "status": "OK",
  "unread": 0,
  "message": "Notifikasi ditandai sebagai terbaca"
}
```

> Failure Response

```json
{
  "status": "ERROR",
  "unread": 1,
  "message": "Notifikasi tersebut tidak dapat ditandai"
}
```



<aside class="warning">Requires authentication</aside>



### HTTP Request

`PATCH https://api.bukalapak.com/v2/notifications/:notification_transaction_id.json`

### Parameters

| Parameter                     |          | Description                         |
| ----------------------------- | -------- | ----------------------------------- |
| `notification_transaction_id` | required | Notification ID of the transaction. |

## Get List of Notifications

> Sample Request

```shell
curl -u 66:tok3ntok3n "https://api.bukalapak.com/v2/notifications/list.json?type[]=discount&type[]=campaign"
```

> Sample Response

```json
{
  "status": "OK",
  "data": [
    {
      "id": "569346de6976613129050000",
      "created_at": "2016-01-11T13:08:30.768+07:00",
      "read_state": false,
      "type": "discount",
      "title": "contoh diskon kategori",
      "message": "ada diskon gede-gedean untuk kategori ...",
      "details": {
        "image_url": null,
        "id": "3",
        "category_name": "Mobile Phones Accessories",
        "unread_items": null
      }
    },
    {
      "id": "569346de6976613129040000",
      "created_at": "2016-01-11T13:08:30.668+07:00",
      "read_state": false,
      "type": "discount",
      "title": "contoh diskon",
      "message": "ayo cek diskon apa aja yang ada di Bukalapak.com",
      "details": {
        "image_url": null,
        "unread_items": null
      }
    },
    {
      "id": "569332df69766106f2000000",
      "created_at": "2016-01-11T11:43:11.256+07:00",
      "read_state": false,
      "type": "campaign",
      "title": "Contoh campaign",
      "message": "ayo buruan beli ...",
      "details": {
        "image_url": null,
        "id": "1",
        "unread_items": null
      }
    }
  ]
}
```



<aside class="warning">Requires authentication</aside>



### HTTP Request

`GET https://api.bukalapak.com/v2/notifications/list.json`

### Parameters

| Parameter  |          | Description                                                  |
| ---------- | -------- | ------------------------------------------------------------ |
| `page`     | optional | Page number to display. Default value is `1`.                |
| `per_page` | optional | Number of record to display per page. Default value is `10`. |
| `type[]`   | optional | Type of notifications to display in container. Default value is all of Promo Types. |

## Android Notifications Data Samples

> Transaction Notification

```json
{
  "type": "transaction",
  "receiver_id": 66,
  "message": "Transaksi baru dari Liem Lie Wie",
  "details":
  {
    "id": 52001,
    "transaction": {
      "id": 52001,
      "state": "paid",
      "updated_at": "2014-01-23T13:48:51+07:00",
      "quick_trans": false
      "transaction_id": "140123102001",
      "amount": 25000,
      "quantity": 1,
      "courier": "JNE REG",
      "buyer_notes": "",
      "shipping_fee": 9000,
      "shipping_id": null,
      "shipping_code": null,
      "shipping_service": null,
      "insurance_cost": 0,
      "total_amount": 34000,
      "products": [
        {
          "id": "3fbd9",
          "name": "Bantal bibir pink Impor",
          "price": 70000
          "small_images": [
            "https://s2.bukalapak.com/system3/images/1/2/8/5/4/9/8/2/large/20141013_171248.jpg"
          ]
          "order_quantity" : 2
        }
      ],
      "consignee": {
        "name": "Liem Lie Wie",
        "phone": "021-56953410",
        "address": "Roxy Square Building lantai LG blok B2 no.8\r\nJalan Kyai Tapa no.1 (seberang KFC)",
        "area": "Grogol",
        "city": "Jakarta Barat",
        "province": "DKI Jakarta",
        "post_code": "11440"
      },
      "buyer": {
        "id": 52357,
        "name": "Liem Lie Wie",
        "username": "ebenhaezernet"
      },
      "seller": {
        "id": 66,
        "name": "Testing Account",
        "username": "testingaccount"
      },
      "actions": ["deliver", "reject"],
      "created_at": "2014-01-23T10:48:51+07:00",
    },
    "unread_items": {
      "unread_notifications": 92,
      "messages": 1,
      "transactions_need_action_as_seller": 5,
      "transactions_need_action_as_buyer": 2,
      "offers_need_action_as_seller": 0,
      "offers_need_action_as_buyer": 0
    }
  }
}
```

> Offer Notification

```json
{
  "data": {
    "type": "nego",
    "receiver_id": 66,
    "message": "Anda mendapatkan tawaran nego dari Me Ow",
    "details": {
      "id": 51588,
      "state": "waiting",
      "nego_price": 100,
      "quantity": 1,
      "product": {
        "id": "mx5n",
        "name": "Bantal bibir pink Impor",
        "normal_price": 70000,
        "stock": 2,
        "small_images": [
          "https://s2.bukalapak.com/system3/images/1/2/8/5/4/9/8/2/large/20141013_171248.jpg"
        ]
      },
      "actions": ["accept", "reject"],
      "buyer": {
        "id": 15,
        "name": "Me Ow",
        "username": "meow"
      },
      "seller": {
        "id": 66,
        "name": "Testing Account",
        "username": "testingaccount"
      },
      "unread_items": {
        "messages": 0,
        "transactions_need_action_as_seller": 12,
        "transactions_need_action_as_buyer": 3,
        "offers_need_action_as_seller": 1,
        "offers_need_action_as_buyer": 0
      }
    }
  }
}
```

> Message Notification

```json
{
  "data": {
    "type": "message",
    "receiver_id": 66,
    "message": "Anda mendapatkan pesan dari Me Ow"
    "details": {
      "id": "56be34322",
      "inbox_id": "56be34",
      "sender_id": 15,
      "message": "mantab gan",
      "unread_items": {
        "messages": 0,
        "transactions_need_action_as_seller": 12,
        "transactions_need_action_as_buyer": 3,
        "offers_need_action_as_seller": 1,
        "offers_need_action_as_buyer": 0
      }
    }
  }
}
```

> Dompet Withdrawal Notification

```json
{
  "data": {
    "type": "dompet",
    "receiver_id": 66,
    "message": "Dana sebesar 25000 telah dicairkan"
    "details": {
      "id": "5",
      "amount": 25000,
      "unread_items": {
        "messages": 0,
        "transactions_need_action_as_seller": 12,
        "transactions_need_action_as_buyer": 3,
        "offers_need_action_as_seller": 1,
        "offers_need_action_as_buyer": 0
      }
    }
  }
}
```

> Report Notification

```json
{
  "data": {
    "type": "report",
    "receiver_id": 66,
    "message": "g.kunci sinchan telah dilaporkan",
    "details": {
      "product": {
        id: 1,
        ...
      },
      "unread_items": {
        "messages": 0,
        "transactions_need_action_as_selleroffer_": 12,
        "transactions_need_action_as_buyer": 3,
        "offers_need_action_as_seller": 1,
        "offers_need_action_as_buyer": 0
      }
    }
  }
}
```

> Reminder (only received right after logging in via app)

```json
{
  "data": {
    "type": "reminder",
    "receiver_id": 66,
    "unread_notifications": 17,
    "messages": 0,
    "details": {
      "unread_items": {
        "messages": 0,
        "transactions_need_action_as_seller": 12,
        "transactions_need_action_as_buyer": 3,
        "offers_need_action_as_seller": 1,
        "offers_need_action_as_buyer": 0
      }
    }
  }
}
```

> Discount Category Notification (Discount for specific category)

```json
{
  "data": {
    "id": "569346de6976613129050000",
    "created_at": "2016-01-11T13:08:30.768+07:00",
    "read_state": false,
    "type": "discount",
    "title": "contoh diskon kategori",
    "message": "ada diskon gede-gedean untuk kategori ...",
    "details": {
      "image_url": null,
      "id": "3",
      "category_name": "Mobile Phones Accessories",
      "unread_items": null
    }
  }
}
```

> Discount Notification

```json
{
  "data": {
    "id": "569346de6976613129040000",
    "created_at": "2016-01-11T13:08:30.668+07:00",
    "read_state": false,
    "type": "discount",
    "title": "contoh diskon",
    "message": "ayo cek diskon apa aja yang ada di Bukalapak.com",
    "details": {
      "image_url": null,
      "unread_items": null
    }
  }
}
```

> Category Notification

```json
{
  "data": {
    "id": "569346de6976613129030000",
    "created_at": "2016-01-11T13:08:30.570+07:00",
    "read_state": false,
    "type": "category",
    "title": "contoh kategori",
    "message": "ayo coba lihat kategori ...",
    "details": {
      "image_url": null,
      "id": "1",
      "category_name": "HP & Elektronik",
      "unread_items": null
    }
  }
}
```

> Profile Notification

```json
{
  "data": {
    "id": "569346de6976613129020000",
    "created_at": "2016-01-11T13:08:30.467+07:00",
    "read_state": false,
    "type": "profile",
    "title": "contoh profile",
    "message": "contoh message profile",
    "details": {
      "image_url": null,
      "user": {
        "id": 9,
        "username": "andi89",
        "name": "andi",
        "gender": "Laki-Laki",
        "avatar": "https://s2.bukalapak.com/images/default_avatar/medium/default.jpg",
        "level": "",
        "level_badge_url": "",
        "lapak_name": null,
        "lapak_desc": "dsvasdvasdv",
        "lapak_header": "https://s2.bukalapak.com/images/header-lapak-default.jpg",
        "last_login": "2016-01-07T22:32:04.000+07:00",
        "joined_at": "2015-09-06T13:22:12.000+07:00",
        "verified_user": false,
        "official": false,
        "store_closed": false,
        "reopen_date": null,
        "close_reason": null,
        "rejection": {
          "rejected": 0,
          "recent_trans": 0
        },
        "feedbacks": {
          "positive": 0,
          "negative": 0
        },
        "address": {
          "province": "Bali",
          "city": "Badung"
        }
      },
      "unread_items": null
    }
  }
}
```

> Profile Notification

```json
{
  "data": {
    "id": "569346de6976613129010000",
    "created_at": "2016-01-11T13:08:30.402+07:00",
    "read_state": false,
    "type": "product",
    "title": "contoh produk notifikasi",
    "message": "contoh message produk",
    "details": {
      "image_url": null,
      "product": {
        "deal_info": {},
        "deal_request_state": "can request",
        "price": 1765000,
        "courier": [
          "JNE REG"
        ],
        "seller_username": "testes",
        "seller_name": "tes",
        "seller_id": 7,
        "seller_avatar": "https://s2.bukalapak.com/images/default_avatar/medium/default.jpg",
        "seller_level": "BL User",
        "seller_level_badge_url": "https://s2.bukalapak.com/images/badge/seller/xhdpi/level-1.png",
        "seller_positive_feedback": 2,
        "seller_negative_feedback": 0,
        "seller_term_condition": "",
        "seller_alert": null,
        "for_sale": true,
        "state_description": [],
        "last_relist_at": "2015-09-02T13:44:23.000+07:00",
        "specs": {},
        "force_insurance": null,
        "free_shipping_coverage": [],
        "id": "h",
        "url": "https://s2.bukalapak.com/p/hp-elektronik/handphone-hp/h-jual-sony-xperia-e4-dual",
        "name": "Sony Xperia E4 Dual",
        "active": true,
        "city": "Ketapang",
        "province": "Kalimantan Barat",
        "weight": 400,
        "image_ids": [
          20
        ],
        "images": [
          "https://s2.bukalapak.com/system4/images/2/0/large/2015-09-02T13:42:56%2B07:00.jpg"
        ],
        "small_images": [
          "https://s2.bukalapak.com/system4/images/2/0/small/2015-09-02T13:42:56%2B07:00.jpg"
        ],
        "desc": "",
        "condition": "new",
        "nego": null,
        "stock": 5,
        "minimum_negotiable": null,
        "view_count": 7,
        "sold_count": 0,
        "waiting_payment": 0,
        "favorited": false,
        "created_at": "2015-09-02T13:42:56.000+07:00",
        "product_sin": [],
        "category_id": 2,
        "category": "Handphone (HP)",
        "category_structure": [
          "HP & Elektronik",
          "Handphone (HP)"
        ],
        "interest_count": 0
      },
      "unread_items": null
    }
  }
}
```

> Announcement Notification

```json
{
  "data": {
    "id": "569346de6976613129000000",
    "created_at": "2016-01-11T13:08:30.322+07:00",
    "read_state": false,
    "type": "announcement",
    "title": "Ayo update apps bukalapak kamu",
    "message": "Segera update apps bukalapak kamu",
    "details": {
      "image_url": null,
      "unread_items": null,
      "link_to": "/promo/1"
    }
  }
}
```

> Campaign Notification

```json
{
  "data": {
    "id": "569332df69766106f2000000",
    "created_at": "2016-01-11T11:43:11.256+07:00",
    "read_state": false,
    "type": "campaign",
    "title": "Contoh campaign",
    "message": "ayo buruan beli ...",
    "details": {
      "image_url": null,
      "id": "1",
      "unread_items": null
    }
  }
}
```

# Products

## Product Dictionary

| Property            | Description                                                  |
| ------------------- | ------------------------------------------------------------ |
| `condition`         | Denotes whether a product is a used item or new. Possible values **new**, **used**. |
| `payment_ready`     | Denotes whether a product can be purchase or not. Possible values **true**, **false**. |
| `state_description` | Explains why a product cannot be purchased. Possible values are **Lapak Tutup**, **Stok Habis**, **Melanggar**, **Penjual Tidak Aktif**. |
| `nego`              | Denotes whether buyer can negotiate the product price. Possible values are **true**, **false**. |
| `free_shipping`     | can be filled with codes of the area where the shipping fee will be made free. |

Available values for free shipping:

| Code | Area                       |
| ---- | -------------------------- |
| `0`  | Seluruh Indonesia          |
| `1`  | Pulau Jawa                 |
| `2`  | Jabodetabek                |
| `3`  | Bali                       |
| `4`  | Banten                     |
| `5`  | Bengkulu                   |
| `6`  | Daerah Istimewa Yogyakarta |
| `7`  | DKI Jakarta                |
| `8`  | Gorontalo                  |
| `9`  | Jambi                      |
| `10` | Jawa Barat                 |
| `11` | Jawa Tengah                |
| `12` | Jawa Timur                 |
| `13` | Kalimantan Barat           |
| `14` | Kalimantan Selatan         |
| `15` | Kalimantan Tengah          |
| `16` | Kalimantan Timur           |
| `17` | Kalimantan Utara           |
| `18` | Kepulauan Bangka Belitung  |
| `19` | Kepulauan Riau             |
| `20` | Lampung                    |
| `21` | Maluku                     |
| `22` | Maluku Utara               |
| `23` | Nanggroe Aceh Darussalam   |
| `24` | Nusa Tenggara Barat        |
| `25` | Nusa Tenggara Timur        |
| `26` | Papua                      |
| `27` | Papua Barat                |
| `28` | Riau                       |
| `29` | Sulawesi Barat             |
| `30` | Sulawesi Selatan           |
| `31` | Sulawesi Tengah            |
| `32` | Sulawesi Tenggara          |
| `33` | Sulawesi Utara             |
| `34` | Sumatera Barat             |
| `35` | Sumatera Selatan           |
| `36` | Sumatera Utara             |

## Product List

> Sample Request
>
> #### Sample request by keywords

```shell
curl -u 67287:lXymG93y83m6RHzZV5FY "https://api.bukalapak.com/v2/products.json?keywords=fixie&page=2&per_page=20"

curl -u 67287:lXymG93y83m6RHzZV5FY -H 'If-None-Match: "9c17139c006bd5e543028b12b978967b"' "https://api.bukalapak.com/v2/products.json"
```

> #### Sample request with favorited products

```shell
curl -u 67287:lXymG93y83m6RHzZV5FY "https://api.bukalapak.com/v2/products.json?favorited=true"
```

> #### Sample request by keywords, minimum price and maximum price

```shell
curl -u 67287:lXymG93y83m6RHzZV5FY "https://api.bukalapak.com/v2/products.json?keywords=galaxy+tab&price_range=on&price_min=3300000&price_max=3500000"
```

> #### Sample request by brand

```shell
curl -u 67287:lXymG93y83m6RHzZV5FY "https://api.bukalapak.com/v2/products.json?brand=Polygon"
```

> #### Sample request by nego

```shell
curl -u 67287:lXymG93y83m6RHzZV5FY "https://api.bukalapak.com/v2/products.json?nego=1"
```

> #### Sample request by keywords and price range

```shell
curl -u 67287:lXymG93y83m6RHzZV5FY "https://api.bukalapak.com/v2/products.json?keywords=blackberry&price_range=5000000-10000000"
```

> #### Sample request by keywords and new conditions

```shell
curl -u 67287:lXymG93y83m6RHzZV5FY "https://api.bukalapak.com/v2/products.json?keywords=nikon&conditions\[\]=new"
```

> #### Sample request by keywords and used conditions

```shell
curl -u 67287:lXymG93y83m6RHzZV5FY "https://api.bukalapak.com/v2/products.json?keywords=canon&conditions\[\]=used"
```

> #### Sample request deal conditions

```shell
curl -u 67287:lXymG93y83m6RHzZV5FY "https://api.bukalapak.com/v2/products.json?todays_deal=1&tomorrows_deal=0"
```

> Success Response
>
> #### Sample response by keywords

```json
{
  "status": "OK",
  "products": [{
    "id": "mtvk",
    "category": "Fixie",
    "category_id": 24,
    "category_structure": ["Sepeda", "Frame", "Fixie"],
    "name": "Frameset BRAIN Atales (NEW) Pink Sz 52 On SALE!!!",
    "active": true,
    "city": "Jakarta Timur",
    "province": "DKI Jakarta",
    "price": 850000,
    "weight": 1000,
    "courier": "JNE REG",
    "force_insurance": false,
    "image_ids": [2591424]
    "images": [
      "https://s4.bukalapak.com/system/images/2/5/9/1/4/2/4/large/image.jpg?1372228356"
    ],
    "small_images": [
      "https://s4.bukalapak.com/system/images/2/5/9/1/4/2/4/small/image.jpg?1372228356"
    ],
    "url": "https://www.bukalapak.com/p/sepeda/frame/fixie-376/mtvk_-frameset-brain-atales-new-pink-sz-52-on-sale",
    "desc": "Frameset BRAIN Atales (NEW) Pink Sz 52 SALE!!!\r\n\r\nIncld:\r\n- frame\r\n- fork\r\n- headset",
    "condition": "new",
    "nego": false,
    "seller_username": "ssbike",
    "seller_name": "S S",
    "seller_id": 3423,
    "seller_avatar": "https://www.bukalapak.com/system/avatars/055/f87/412/9cf/0ec/36837/medium/xkcd.png?1387424302",
    "seller_level": "Pedagang Besar",
    "seller_level_badge_url": "https://www.bukalapak.com/images/badge/seller/xhdpi/level-5.png",
    "seller_positive_feedback": 46,
    "seller_negative_feedback": 31,
    "seller_term_condition": "Barang yang di beli tidak dapat dikembalikan.",
    "seller_alert": null,
    "payment_ready": true,
    "stock": 1,
    "specs": {
      "brand": "Lain-lain",
      "type": "Track",
      "bahan": "Alloy",
      "ukuran": "52",
      "ukuran_seat_tube": "27,2",
      "ukuran_headtube": "1 1/8 inch (Over Size)"
    },
    "state_description": [],
    "minimum_negotiable": null,
    "for_sale": true,
    "favorited": false,
    "free_shipping_coverage": [],
    "deal_info": {
      "original_price": 850000,
      "discount_price": 765000,
      "discount_percentage": 10,
      "state": "pending"
    },
    "deal_request_state": "can edit",
    "product_sin":  ["Deskripsi tidak tepat", "Spesifikasi tidak tepat"]
  }],
  "categories": [{
      "id": 1,
      "name": "Handphone",
      "url": "/c/handphone",
      "children": [{
          "id": 2,
          "name": "HP & Smartphone",
          "url": "/c/handphone/hp-smartphone",
          "count": 19
        },
        {
          "id": 3,
          "name": "Casing",
          "url": "/c/handphone/casing",
          "count": 4
        }
      ],
      "count": 23
  }],
  "message": null
}
```

> #### Sample response with favorited

```json
{
  "status": "OK",
  "products": [{
    "id": "mtvk",
    "category": "Fixie",
    "category_id": 24,
    "category_structure": ["Sepeda", "Frame", "Fixie"],
    "name": "Frameset BRAIN Atales (NEW) Pink Sz 52 On SALE!!!",
    "active": true,
    "city": "Jakarta Timur",
    "province": "DKI Jakarta",
    "price": 850000,
    "weight": 1000,
    "courier": "JNE REG",
    "force_insurance": false,
    "image_ids": [2591424]
    "images": [
      "https://s4.bukalapak.com/system/images/2/5/9/1/4/2/4/large/image.jpg?1372228356"
    ],
    "small_images": [
      "https://s4.bukalapak.com/system/images/2/5/9/1/4/2/4/small/image.jpg?1372228356"
    ],
    "url": "https://www.bukalapak.com/p/sepeda/frame/fixie-376/mtvk_-frameset-brain-atales-new-pink-sz-52-on-sale",
    "desc": "Frameset BRAIN Atales (NEW) Pink Sz 52 SALE!!!\r\n\r\nIncld:\r\n- frame\r\n- fork\r\n- headset",
    "condition": "new",
    "nego": false,
    "seller_username": "ssbike",
    "seller_name": "S S",
    "seller_id": 3423,
    "seller_avatar": "https://www.bukalapak.com/system/avatars/055/f87/412/9cf/0ec/36837/medium/xkcd.png?1387424302",
    "seller_level": "Pedagang Besar",
    "seller_level_badge_url": "https://www.bukalapak.com/images/badge/seller/xhdpi/level-5.png",
    "seller_positive_feedback": 46,
    "seller_negative_feedback": 31,
    "seller_term_condition": "Barang yang di beli tidak dapat dikembalikan.",
    "seller_alert": null,
    "payment_ready": true,
    "stock": 1,
    "specs": {
      "brand": "Lain-lain",
      "type": "Track",
      "bahan": "Alloy",
      "ukuran": "52",
      "ukuran_seat_tube": "27,2",
      "ukuran_headtube": "1 1/8 inch (Over Size)"
    },
    "state_description": [],
    "minimum_negotiable": null,
    "for_sale": true,
    "favorited": false,
    "free_shipping_coverage": [],
    "deal_info": {
      "original_price": 850000,
      "discount_price": 765000,
      "discount_percentage": 10,
      "state": "pending"
    },
    "deal_request_state": "can edit",
    "product_sin":  ["Deskripsi tidak tepat", "Spesifikasi tidak tepat"]
  }],
  "message": null,
  "favorited": ["mtvk"]

}
```

> #### Sample response by keywords, minimum price and maximum price

```json
{
  "status": "OK",
  "products": [{
    "id": "ix45",
    "category": "Handphone (HP)",
    "category_id": 40,
    "category_structure": ["HP & Elektronik", "Handphone (HP)"],
    "name": "Dijual Galaxy Tab 2, 7inch",
    "active": true,
    "city": "Jakarta Utara",
    "province": "DKI Jakarta",
    "price": 3350000,
    "weight": 800,
    "courier": "JNE REG",
    "force_insurance": false,
    "image_ids": [2129322],
    "images": [
      "https://s2.bukalapak.com/system/images/2/1/2/9/3/2/2/large/20130211_143503.jpg?1362242270"
    ],
    "small_images": [
      "https://s2.bukalapak.com/system/images/2/1/2/9/3/2/2/small/20130211_143503.jpg?1362242270"
    ],
    "url": "https://www.bukalapak.com/p/hp-elektronik/handphone-hp/ix45_-dijual-galaxy-tab-2-7inch",
    "desc": "barang lengkap, mulus, pembelian, jadi masi garansi :)",
    "condition": "used",
    "nego": true,
    "seller_username": "hendrikpoltak31194",
    "seller_name": "hendrik poltak",
    "seller_id": 112345,
    "seller_avatar": "https://www.bukalapak.com/system/avatars/055/f87/412/9cf/0ec/36837/medium/xkcd.png?1387424302",
    "seller_level": "Pedagang Besar",
    "seller_level_badge_url": "https://www.bukalapak.com/images/badge/seller/xhdpi/level-5.png",
    "seller_positive_feedback": 46,
    "seller_negative_feedback": 31,
    "seller_term_condition": "Barang yang di beli tidak dapat dikembalikan.",
    "seller_alert": "Pelapak dari produk ini sudah tidak login lebih dari 2 minggu, namun produk masih tersedia.",
    "payment_ready": true,
    "stock": 1,
    "specs": {
      "brand": "Samsung",
      "operating_system": "Android",
      "features": [
        "Touchscreen",
        "Wifi",
        "Bluetooth",
        "3G",
        "GPS Navigation",
        "Memory Card Slots",
        "MP3",
        "Message",
        "e-mail",
        "Video Player",
        "Front Camera",
        "QWERT Keyboard",
        ""
      ],
      "bentuk": "Klasik (Bar)",
      "display_size": "7.0\"",
      "camera": "Camera",
      "garansi": "1-12 bulan",
      "network": "GSM",
      "body_color": "PATCHih"
    },
    "state_description": [],
    "minimum_negotiable": null,
    "for_sale": true,
    "favorited": false,
    "free_shipping_coverage": [],
    "deal_info": {
      "original_price": 850000,
      "discount_price": 765000,
      "discount_percentage": 10,
      "state": "pending"
    },
    "deal_request_state": "can edit",
    "product_sin":  ["Deskripsi tidak tepat", "Spesifikasi tidak tepat"]
  }],
  "message": null
}
```

> #### Sample response by brand

```json
{
  "status": "OK",
  "products": [{
    "id": "n2fc",
    "category": "MTB",
    "category_id": 81,
    "category_structure": ["Sepeda", "Fullbike", "MTB"],
    "name": "Polygon Cozmic RXX Carbon size:16\" kondisi Baru Groupset XTR",
    "active": true,
    "city": "Cilacap",
    "province": "Jawa Tengah",
    "price": 21000000,
    "weight": "8000",
    "courier": ["JNE REG"],
    "force_insurance": false,
    "image_ids": [2616081],
    "images": [
      "https://s1.bukalapak.com/system2/images/2/6/1/6/0/8/1/large/DSCN6379a.JPG?1372661546"
    ],
    "small_images": [
      "https://s1.bukalapak.com/system2/images/2/6/1/6/0/8/1/small/DSCN6379a.JPG?1372661546"
    ],
    "url": "https://www.bukalapak.com/p/sepeda/fullbike/mtb/n2fc_-polygon-cozmic-rxx-carbon-size16-kondisi-baru-groupset-xtr--3",
    "desc": "Polygon Cozmic RXX Carbon size:16 kondisi Baru Groupset XTR + Fork Mosso...",
    "condition": "new",
    "nego": true,
    "seller_username": "ghober168",
    "seller_name": "Bernadus Hariyanto (Ghober168)",
    "seller_id": 34562,
    "seller_avatar": "https://www.bukalapak.com/system/avatars/055/f87/412/9cf/0ec/36837/medium/xkcd.png?1387424302",
    "seller_level": "Pedagang Besar",
    "seller_level_badge_url": "https://www.bukalapak.com/images/badge/seller/xhdpi/level-5.png",
    "seller_positive_feedback": 46,
    "seller_negative_feedback": 31,
    "seller_term_condition": "Barang yang di beli tidak dapat dikembalikan.",
    "seller_alert": null,
    "payment_ready": true,
    "stock": 1,
    "specs": {
      "brand": "Polygon",
      "type": "XC (Cross Country)",
      "bahan": null,
      "ukuran": null
    },
    "state_description": [],
    "minimum_negotiable": null,
    "for_sale": true,
    "favorited": false,
    "free_shipping_coverage": [],
    "deal_info": {
      "original_price": 850000,
      "discount_price": 765000,
      "discount_percentage": 10,
      "state": "pending"
    },
    "deal_request_state": "can edit",
    "product_sin":  ["Deskripsi tidak tepat", "Spesifikasi tidak tepat"]
  }],
  "message": null
}
```

> #### Sample response by nego

```json
{
  "status": "OK",
  "products": [{
    "id": "n2he",
    "category": "MTB",
    "category_id": 81,
    "category_structure": ["Sepeda", "Frame", "MTB"],
    "name": "frame dartmoor hornet 2013",
    "active": true,
    "city": "Tangerang Selatan",
    "province": "Banten",
    "price": 2600000,
    "weight": "7000",
    "courier": ["JNE REG"],
    "force_insurance": false,
    "image_ids": [2616275],
    "images": [
      "https://s0.bukalapak.com/system2/images/2/6/1/6/2/7/5/large/20130528_103510.jpg?1372663040"
    ],
    "small_images": [
      "https://s0.bukalapak.com/system2/images/2/6/1/6/2/7/5/small/20130528_103510.jpg?1372663040"
    ],
    "url": "https://www.bukalapak.com/p/sepeda/frame/mtb-372/n2he_-frame-dartmoor-hornet-2013--2",
    "desc": "frame dartmoor hornet 2013..kondisi mulus..pemakaian  bln mei 2013..",
    "condition": "used",
    "nego": true,
    "seller_username": "kandim",
    "seller_name": "denny irenk",
    "seller_id": 5643298,
    "seller_avatar": "https://www.bukalapak.com/system/avatars/055/f87/412/9cf/0ec/36837/medium/xkcd.png?1387424302",
    "seller_level": "Pedagang Besar",
    "seller_level_badge_url": "https://www.bukalapak.com/images/badge/seller/xhdpi/level-5.png",
    "seller_positive_feedback": 46,
    "seller_negative_feedback": 31,
    "seller_term_condition": "Barang yang di beli tidak dapat dikembalikan.",
    "seller_alert": null,
    "payment_ready": true,
    "stock": 1,
    "specs": {
      "brand": "Dartmoor",
      "type": "All Mountain",
      "bahan": "Alloy",
      "ukuran": "14.5",
      "Spacing": null,
      "ukuran_seat_tube": "",
      "ukuran_headtube": "1 1/8 inch (Over Size)"
    },
    "state_description": [],
    "minimum_negotiable": null,
    "for_sale": true,
    "favorited": false,
    "free_shipping_coverage": [],
    "deal_info": {
      "original_price": 850000,
      "discount_price": 765000,
      "discount_percentage": 10,
      "state": "pending"
    },
    "deal_request_state": "can edit",
    "product_sin":  ["Deskripsi tidak tepat", "Spesifikasi tidak tepat"]
  }],
  "message": null
}
```

> #### Sample response by keywords and price range

```json
{
  "status": "OK",
  "products":[
    {
      "id": "n2hf",
      "category": "Handphone (HP)",
      "category_id": 41,
      "category_structure": ["HP & Elektronik", "Handphone (HP)"],
      "name": "BLACKBERRY Q10 GARANSI RESMI SCM (Authorised Distributor)",
      "active": true,
      "city": "Jakarta Selatan",
      "province": "DKI Jakarta",
      "price": 6999000,
      "weight": "700",
      "courier": ["JNE REG"],
      "force_insurance": false,
      "image_ids": [2616274],
      "images": [
        "https://s4.bukalapak.com/system/images/2/6/1/6/2/7/4/large/q10_scm.jpg?1372662756"
      ],
      "small_images": [
        "https://s4.bukalapak.com/system/images/2/6/1/6/2/7/4/small/q10_scm.jpg?1372662756"
      ],
      "url": "https://www.bukalapak.com/p/hp-elektronik/handphone-hp/n2hf_-blackberry-q10-garansi-resmi-scm-authorised-distributor",
      "desc": "BLACKBERRY Q10\r\nKondisi: BRAND NEW IN BOX (BNIB).\r\nGARANSI: 2 TAHUN dari SCM ...",
      "condition": "new",
      "nego": false,
      "seller_username": "superx07",
      "seller_name": "superx07",
      "seller_id": 234231,
      "seller_avatar": "https://www.bukalapak.com/system/avatars/055/f87/412/9cf/0ec/36837/medium/xkcd.png?1387424302",
      "seller_level": "Pedagang Besar",
      "seller_level_badge_url": "https://www.bukalapak.com/images/badge/seller/xhdpi/level-5.png",
      "seller_positive_feedback": 46,
      "seller_negative_feedback": 31,
      "seller_term_condition": "Barang yang di beli tidak dapat dikembalikan.",
      "seller_alert": null,
      "payment_ready": true,
      "stock": 10,
      "specs": {
        "brand": "Blackberry",
        "operating_system": "Blackberry",
        "features": [""],
        "bentuk": "Klasik (Bar)",
        "display_size": "3.2\"",
        "camera": "Camera",
        "garansi": "1-12 bulan",
        "network": "GSM",
        "body_color": "PATCHih"
      },
      "state_description": [],
      "minimum_negotiable": null,
      "for_sale": true,
      "favorited": false,
      "free_shipping_coverage": [],
      "deal_info": {
        "original_price": 850000,
        "discount_price": 765000,
        "discount_percentage": 10,
        "state": "pending"
      },
      "deal_request_state": "can edit",
      "product_sin":  ["Deskripsi tidak tepat", "Spesifikasi tidak tepat"]
    }],
  "message": null
}
```

> #### Sample response by keywords and new conditions

```json
{
  "status": "OK",
  "products": [{
    "id": "n1vh",
    "category": "Digital Camera",
    "category_id": 35,
    "category_structure": ["Kamera", "Digital Camera"],
    "name": "Nikon D7000 KIT",
    "active": true,
    "city": "Surabaya",
    "province": "Jawa Timur",
    "price": 2250000,
     "weight": "1400",
    "courier": ["JNE REG"],
    "force_insurance": false,
    "image_ids": [2614505],
    "images": [
      "https://s0.bukalapak.com/system2/images/2/6/1/4/5/0/5/large/950.jpg?1372648607"
    ],
    "small_images": [
      "https://s0.bukalapak.com/system2/images/2/6/1/4/5/0/5/small/950.jpg?1372648607"
    ],
    "url": "https://www.bukalapak.com/p/kamera/digital-camera/n1vh_-nikon-d7000-kit--39",
    "desc": "Barang 100% asli original\r\nNikon D7000 ...",
    "condition": "new",
    "nego": false,
    "seller_username": "mitra_kamera72",
    "seller_name": "mitra_kamera72",
    "seller_id": 3498,
    "seller_avatar": "https://www.bukalapak.com/system/avatars/055/f87/412/9cf/0ec/36837/medium/xkcd.png?1387424302",
    "seller_level": "Pedagang Besar",
    "seller_level_badge_url": "https://www.bukalapak.com/images/badge/seller/xhdpi/level-5.png",
    "seller_positive_feedback": 46,
    "seller_negative_feedback": 31,
    "seller_term_condition": "Barang yang di beli tidak dapat dikembalikan.",
    "seller_alert": null,
    "payment_ready": true,
    "stock": 1,
    "specs": {
      "type": "D-SLR",
      "brand": "Nikon",
      "megapixel": "<5.00MP",
      "optical_zoom": "0",
      "screen_size": "",
      "garansi": "1-12 bulan",
      "memory_card_type": "MicroSD",
      "body_color": "hitam",
      "video": "Yes",
      "image_stabilization": ""
    },
    "state_description": [],
    "minimum_negotiable": null,
    "for_sale": true,
    "favorited": false,
    "free_shipping_coverage": [],
    "deal_info": {
      "original_price": 850000,
      "discount_price": 765000,
      "discount_percentage": 10,
      "state": "pending"
    },
    "deal_request_state": "can edit",
    "product_sin":  ["Deskripsi tidak tepat", "Spesifikasi tidak tepat"]
  }],
  "message": null
}
```

> #### Sample response by keywords and used conditions

```json
{
  "status": "OK",
  "products": [{
    "id": "n2gn",
    "category": "Digital Camera",
    "category_id": 35,
    "category_structure": ["Kamera", "Digital Camera"],
    "name": "Canon EOS 650D, Sigma 30mm f1.4 EX DC HSM, Canon Speedlite 320EX",
    "active": true,
    "city": "Jakarta Selatan",
    "province": "DKI Jakarta",
    "price": 11000000,
    "weight": "1000",
    "courier": ["JNE REG"],
    "force_insurance": false,
    "image_ids": [2616195],
    "images": [
      "https://s0.bukalapak.com/system2/images/2/6/1/6/1/9/5/large/Objektiv.jpg?1372662175"
    ],
    "small_images": [
      "https://s0.bukalapak.com/system2/images/2/6/1/6/1/9/5/small/Objektiv.jpg?1372662175"
    ],
    "url": "https://www.bukalapak.com/p/kamera/digital-camera/n2gn_-canon-eos-650d-sigma-30mm-f14-ex-dc-hsm-canon-speedlite-320ex",
    "desc": "Dijual paketan ataupun ketengan:\r\n\r\nBody Canon EOS 650D (dus kit) beserta perlengkapannya Rp ensa Sigma 30mm f/1.4 EX DC HSM Rp 5.000.000\r\n\r\nSpeedlite Canon 320EX Rp 1.500.000\r\n\r\nSemuanya beli awal 2013 di JPC, masih bergaransi, mulus.\r\n\r\nBoleh beli paketan komplit  atau dimutilasi dengan harga seperti yang udah ditulis.\r\n\r\nFoto yang ada sementara masih ambil dari internet karena barang di rumah, nanti akan diupdate :)",
    "condition": "used",
    "nego": true,
    "seller_username": "lifebehindbars",
    "seller_name": "Kevin Oei",
    "seller_id": 11239,
    "seller_avatar": "https://www.bukalapak.com/system/avatars/055/f87/412/9cf/0ec/36837/medium/xkcd.png?1387424302",
    "seller_level": "Pedagang Besar",
    "seller_level_badge_url": "https://www.bukalapak.com/images/badge/seller/xhdpi/level-5.png",
    "seller_positive_feedback": 46,
    "seller_negative_feedback": 31,
    "seller_term_condition": "Barang yang di beli tidak dapat dikembalikan.",
    "seller_alert": null,
    "payment_ready": true,
    "stock": 1,
    "specs": {
      "type": "D-SLR",
      "brand": "Canon",
      "megapixel": "10.0 - 20.0MP",
      "optical_zoom": "0",
      "screen_size": "",
      "garansi": "1-12 bulan",
      "memory_card_type": "MicroSD",
      "body_color": "hitam",
      "video": "Yes",
      "image_stabilization": ""
    },
    "state_description": [],
    "minimum_negotiable": null,
    "for_sale": true,
    "favorited": false,
    "free_shipping_coverage": [],
    "deal_info": {
      "original_price": 850000,
      "discount_price": 765000,
      "discount_percentage": 10,
      "state": "pending"
    },
    "deal_request_state": "can edit",
    "product_sin":  ["Deskripsi tidak tepat", "Spesifikasi tidak tepat"]
  }],
  "message": null
}
```

> #### Sample response by deal conditions

```json
{
  "status": "OK",
  "products": [{
    "id": "n2gn",
    "category": "Digital Camera",
    "category_id": 35,
    "category_structure": ["Kamera", "Digital Camera"],
    "name": "Canon EOS 650D, Sigma 30mm f1.4 EX DC HSM, Canon Speedlite 320EX",
    "active": true,
    "city": "Jakarta Selatan",
    "province": "DKI Jakarta",
    "price": 11000000,
    "weight": "1000",
    "courier": ["JNE REG"],
    "force_insurance": false,
    "image_ids": [2616195],
    "images": [
      "https://s0.bukalapak.com/system2/images/2/6/1/6/1/9/5/large/Objektiv.jpg?1372662175"
    ],
    "small_images": [
      "https://s0.bukalapak.com/system2/images/2/6/1/6/1/9/5/small/Objektiv.jpg?1372662175"
    ],
    "url": "https://www.bukalapak.com/p/kamera/digital-camera/n2gn_-canon-eos-650d-sigma-30mm-f14-ex-dc-hsm-canon-speedlite-320ex",
    "desc": "Dijual paketan ataupun ketengan:\r\n\r\nBody Canon EOS 650D (dus kit) beserta perlengkapannya Rp ensa Sigma 30mm f/1.4 EX DC HSM Rp 5.000.000\r\n\r\nSpeedlite Canon 320EX Rp 1.500.000\r\n\r\nSemuanya beli awal 2013 di JPC, masih bergaransi, mulus.\r\n\r\nBoleh beli paketan komplit  atau dimutilasi dengan harga seperti yang udah ditulis.\r\n\r\nFoto yang ada sementara masih ambil dari internet karena barang di rumah, nanti akan diupdate :)",
    "condition": "used",
    "nego": true,
    "seller_username": "lifebehindbars",
    "seller_name": "Kevin Oei",
    "seller_id": 11239,
    "seller_avatar": "https://www.bukalapak.com/system/avatars/055/f87/412/9cf/0ec/36837/medium/xkcd.png?1387424302",
    "seller_level": "Pedagang Besar",
    "seller_level_badge_url": "https://www.bukalapak.com/images/badge/seller/xhdpi/level-5.png",
    "seller_positive_feedback": 46,
    "seller_negative_feedback": 31,
    "seller_term_condition": "Barang yang di beli tidak dapat dikembalikan.",
    "seller_alert": null,
    "payment_ready": true,
    "stock": 1,
    "specs": {
      "type": "D-SLR",
      "brand": "Canon",
      "megapixel": "10.0 - 20.0MP",
      "optical_zoom": "0",
      "screen_size": "",
      "garansi": "1-12 bulan",
      "memory_card_type": "MicroSD",
      "body_color": "hitam",
      "video": "Yes",
      "image_stabilization": ""
    },
    "state_description": [],
    "minimum_negotiable": null,
    "for_sale": true,
    "favorited": false,
    "free_shipping_coverage": [],
    "deal_info": {
      "original_price": 850000,
      "discount_price": 765000,
      "discount_percentage": 10,
      "state": "applied"
    },
    "deal_request_state": "cannot edit",
    "product_sin":  ["Deskripsi tidak tepat", "Spesifikasi tidak tepat"]
  }],
  "message": null
}
```

Get a list of products. If parameter `keywords` exist, this will give a number of products matching with keywords `keywords`.

You can optionally set `If-None-Match` header or `Etag` header. If request `Etag` match, server will send `304 Not Modified` response without body. Server will set `Etag` header to every request to this resource.

### HTTP Request

- `GET https://api.bukalapak.com/v2/products.json`
- `GET https://api.bukalapak.com/v2/products.json?keywords=mtb`. Show products that matches with keywords `mtb`.
- `GET https://api.bukalapak.com/v2/products.json?page=1&per_page=10`. First ten products.

### Parameters

| Parameter                |          | Description                                                  |
| ------------------------ | -------- | ------------------------------------------------------------ |
| `keywords`               | optional | Keywords use to search products.                             |
| `category_id`            | optional | Only search for items in a certain category.                 |
| `page`                   | optional | Pagination page, default to `0`.                             |
| `per_page`               | optional | Number results per_page, default to `20`. Allowed values `6, 18, 24, 48, 96`. |
| `nego` & `harga_pas`     | optional | If searching for negotiable products, set `nego` to `1` and `harga_pas` to `0`. If searching for non-negotiable products, set `nego` to `0` and `harga_pas` to `1`. If given the same values, search result returns both negotiable and non-negotiable products. |
| `top_seller`             | optional | If searching for products from top sellers only, set value to `1`. Allowed values are `1` and `0`. |
| `conditions`             | optional | Allowed values are `new` and `used`.                         |
| `favorited`              | optional | Returns array of product ids favorited by the `current_user`. |
| `free_shipping_coverage` | optional | Fill with the code of the free shipping area.                |
| `province`               | optional | Name of the seller’s province.                               |
| `city`                   | optional | Name of the seller’s city.                                   |
| `price_min`              | optional | Minimum price.                                               |
| `price_max`              | optional | Maximum price.                                               |
| `sort_by`                | optional | Allowed values are `Terbaru`, `Termurah`, `Termahal`, and `Acak`. |
| `user_id`                | optional | Seller’s id.                                                 |
| `todays_deal`            | optional | Denotes whether a product is on deal or not. Allowed values are `1` and `0`. |
| `tomorrows_deal`         | optional | Denotes whether a product is tomorrow’s deal or not. Allowed values are `1` and `0`. |
| `campaign_ids`           | optional | Search product on specific campaign. Allowed values are id of campaign |

## Get Popular Products

> Sample Request

```shell
curl https://api.bukalapak.com/v2/products/populars.json
```

> Sample Response

```json
{
  "status": "OK",
  "hobby": [
    {
      "id": "mx0k",
      "category": "Consoles",
      "category_id": 221,
      "category_structure": ["HP \u0026 Elektronik", "Video Game", "Consoles"],
      "name": "xbox",
      "active": true,
      "city": "Surabaya",
      "province": "Jawa Timur",
      "price": 120000,
      "weight": "3000",
      "courier": ["JNE REG"],
      "force_insurance": false,
      "image_ids": [2601430],
      "images": [
        "http://www.bukalapak.com/system/images/2/6/0/1/4/3/0/large/paket_push_mylapak.png"
      ],
      "small_images": [
        "http://www.bukalapak.com/system/images/2/6/0/1/4/3/0/small/paket_push_mylapak.png"
      ],
      "url": "http://www.bukalapak.com/p/hp-elektronik/video-game/consoles/mx0k-jual-xbox",
      "desc": "ssdsfsdf",
      "condition": "used",
      "nego": false,
      "seller_username": "testingaccount",
      "seller_name": "Testing Account",
      "seller_id": 204253,
      "seller_avatar": "http://www.bukalapak.com/images/default_avatar/medium/default.jpg",
      "seller_level": "Pedagang",
      "seller_level_badge_url": "https://www.bukalapak.com/images/badge/seller/xhdpi/level-5.png",
      "seller_positive_feedback": 46,
      "seller_negative_feedback": 31,
      "seller_term_condition": "Barang yang di beli tidak dapat dikembalikan.",
      "seller_alert": null,
      "payment_ready": true,
      "stock": 1,
      "specs": {"platform": "Microsoft Xbox 360"},
      "state_description": [],
      "minimum_negotiable": null,
      "for_sale": true,
      "favorited": false,
      "free_shipping_coverage": [],
      "deal_info": {
        "original_price": 850000,
        "discount_price": 765000,
        "discount_percentage": 10,
        "state": "pending"
      },
      "deal_request_state": "can edit",
      "product_sin":  ["Deskripsi tidak tepat", "Spesifikasi tidak tepat"]
    },
    /* ... */
  ],
  "fashion": [
   {
      "id": "mx0k",
      "category": "Consoles",
      "category_id": 221,
      "category_structure": ["HP \u0026 Elektronik", "Video Game", "Consoles"],
      "name": "xbox",
      "active": true,
      "city": "Surabaya",
      "province": "Jawa Timur",
      "price": 120000,
      "weight": "3000",
      "courier": ["JNE REG"],
      "force_insurance": false,
      "image_ids": [2601430],
      "images": [
        "http://www.bukalapak.com/system/images/2/6/0/1/4/3/0/large/paket_push_mylapak.png"
      ],
      "small_images": [
        "http://www.bukalapak.com/system/images/2/6/0/1/4/3/0/small/paket_push_mylapak.png"
      ],
      "url": "http://www.bukalapak.com/p/hp-elektronik/video-game/consoles/mx0k-jual-xbox",
      "desc": "ssdsfsdf",
      "condition": "used",
      "nego": false,
      "seller_username": "testingaccount",
      "seller_name": "Testing Account",
      "seller_id": 204253,
      "seller_avatar": "http://www.bukalapak.com/images/default_avatar/medium/default.jpg",
      "seller_level": "Pedagang",
      "seller_level_badge_url": "https://www.bukalapak.com/images/badge/seller/xhdpi/level-5.png",
      "seller_positive_feedback": 46,
      "seller_negative_feedback": 31,
      "seller_term_condition": "Barang yang di beli tidak dapat dikembalikan.",
      "seller_alert": null,
      "payment_ready": true,
      "stock": 1,
      "specs": {"platform": "Microsoft Xbox 360"},
      "state_description": [],
      "minimum_negotiable": null,
      "for_sale": true,
      "favorited": false,
      "free_shipping_coverage": [],
      "deal_info": {
        "original_price": 850000,
        "discount_price": 765000,
        "discount_percentage": 10,
        "state": "pending"
      },
      "deal_request_state": "can edit",
      "product_sin":  ["Deskripsi tidak tepat", "Spesifikasi tidak tepat"]
    },
    /* ... */
    ],
  "electronic":[
    {
      "id": "mx0k",
      "category": "Consoles",
      "category_id": 221,
      "category_structure": ["HP \u0026 Elektronik", "Video Game", "Consoles"],
      "name": "xbox",
      "active": true,
      "city": "Surabaya",
      "province": "Jawa Timur",
      "price": 120000,
      "weight": "3000",
      "courier": ["JNE REG"],
      "force_insurance": false,
      "image_ids": [2601430],
      "images": [
        "http://www.bukalapak.com/system/images/2/6/0/1/4/3/0/large/paket_push_mylapak.png"
      ],
      "small_images": [
        "http://www.bukalapak.com/system/images/2/6/0/1/4/3/0/small/paket_push_mylapak.png"
      ],
      "url": "http://www.bukalapak.com/p/hp-elektronik/video-game/consoles/mx0k-jual-xbox",
      "desc": "ssdsfsdf",
      "condition": "used",
      "nego": false,
      "seller_username": "testingaccount",
      "seller_name": "Testing Account",
      "seller_id": 204253,
      "seller_avatar": "http://www.bukalapak.com/images/default_avatar/medium/default.jpg",
      "seller_level": "Pedagang",
      "seller_level_badge_url": "https://www.bukalapak.com/images/badge/seller/xhdpi/level-5.png",
      "seller_positive_feedback": 46,
      "seller_negative_feedback": 31,
      "seller_term_condition": "Barang yang di beli tidak dapat dikembalikan.",
      "seller_alert": null,
      "payment_ready": true,
      "stock": 1,
      "specs": {"platform": "Microsoft Xbox 360"},
      "state_description": [],
      "minimum_negotiable": null,
      "for_sale": true,
      "favorited": false,
      "free_shipping_coverage": [],
      "deal_info": {
        "original_price": 850000,
        "discount_price": 765000,
        "discount_percentage": 10,
        "state": "pending"
      },
      "deal_request_state": "can edit",
      "product_sin":  ["Deskripsi tidak tepat", "Spesifikasi tidak tepat"]
    },
    /* ... */
    ],
  "recommendation":[
   {
      "id": "mx0k",
      "category": "Consoles",
      "category_id": 221,
      "category_structure": ["HP \u0026 Elektronik", "Video Game", "Consoles"],
      "name": "xbox",
      "active": true,
      "city": "Surabaya",
      "province": "Jawa Timur",
      "price": 120000,
      "weight": "3000",
      "courier": ["JNE REG"],
      "force_insurance": false,
      "image_ids": [2601430],
      "images": [
        "http://www.bukalapak.com/system/images/2/6/0/1/4/3/0/large/paket_push_mylapak.png"
      ],
      "small_images": [
        "http://www.bukalapak.com/system/images/2/6/0/1/4/3/0/small/paket_push_mylapak.png"
      ],
      "url": "http://www.bukalapak.com/p/hp-elektronik/video-game/consoles/mx0k-jual-xbox",
      "desc": "ssdsfsdf",
      "condition": "used",
      "nego": false,
      "seller_username": "testingaccount",
      "seller_name": "Testing Account",
      "seller_id": 204253,
      "seller_avatar": "http://www.bukalapak.com/images/default_avatar/medium/default.jpg",
      "seller_level": "Pedagang",
      "seller_level_badge_url": "https://www.bukalapak.com/images/badge/seller/xhdpi/level-5.png",
      "seller_positive_feedback": 46,
      "seller_negative_feedback": 31,
      "seller_term_condition": "Barang yang di beli tidak dapat dikembalikan.",
      "seller_alert": null,
      "payment_ready": true,
      "stock": 1,
      "specs": {"platform": "Microsoft Xbox 360"},
      "state_description": [],
      "minimum_negotiable": null,
      "for_sale": true,
      "favorited": false,
      "free_shipping_coverage": [],
      "deal_info": {
        "original_price": 850000,
        "discount_price": 765000,
        "discount_percentage": 10,
        "state": "pending"
      },
      "deal_request_state": "can edit",
      "product_sin":  ["Deskripsi tidak tepat", "Spesifikasi tidak tepat"]
    },
    /* ... */
  ],
  "message": null
}
```

### HTTP Request


`GET https://api.bukalapak.com/v2/products/populars.json`

### Parameters

None

## Get My Lapak

> Sample Request

```shell
curl -u 67287:lXymG93y83m6RHzZV5FY "https://api.bukalapak.com/v2/products/mylapak.json"
```

> Sample Response

```json
{
  "status": "OK",
  "products": [
    {
      "id": "mab5",
      "category": "Suspension",
      "category_id": 78
      "category_structure": ["Sepeda", "Fork & Suspension", "Suspension"],
      "name": "Testing BL App",
      "active": true,
      "city": "Jakarta Selatan",
      "province": "DKI Jakarta",
      "price": 1250000,
      "weight": "1000",
      "courier": ["JNE REG"],
      "force_insurance": false,
      "image_ids": [2532736],
      "images": [
        "https://s1.bukalapak.com/system/images/2/5/3/2/7/3/6/large/IMG_0205.JPG?1371219033"
      ],
      "small_images": [
        "https://s1.bukalapak.com/system/images/2/5/3/2/7/3/6/small/IMG_0205.JPG?1371219033"
      ],
      "url": "https://www.bukalapak.com/p/sepeda/fork-suspension/suspension/mab5_-testing-bl-app",
      "desc": "Test upload from BL App, please ignore",
      "condition": "new",
      "nego": true,
      "seller_username": "meow",
      "seller_name": "Me Oww",
      "seller_id": 15,
      "seller_avatar": "https://www.bukalapak.com/system/avatars/055/f87/412/9cf/0ec/36837/medium/xkcd.png?1387424302",
      "seller_level": "Pedagang",
      "seller_level_badge_url": "https://www.bukalapak.com/images/badge/seller/xhdpi/level-5.png",
      "seller_positive_feedback": 46,
      "seller_negative_feedback": 31,
      "seller_term_condition": "Barang yang di beli tidak dapat dikembalikan.",
      "seller_alert": null,
      "payment_ready": true,
      "specs": {
        "merk_shock": null,
        "size_shock": null,
        "spring": null
      },
      "state_description": [],
      "minimum_negotiable": null,
      "for_sale": true,
      "favorited": false,
      "free_shipping_coverage": [],
      "deal_info": {
        "original_price": 850000,
        "discount_price": 765000,
        "discount_percentage": 10,
        "state": "pending"
      },
      "deal_request_state": "can edit",
      "product_sin":  ["Deskripsi tidak tepat", "Spesifikasi tidak tepat"]
    }
    /* ... */
  ],
  "can_push": true,
  "remaining_push": 22,
  "message": null
}
```

Get current user’s store (lapak). Products returned for this request are those which can be purchased.

You can optionally set `If-None-Match` header or `Etag` header. If request `Etag` match, server will send `304 Not Modified` response without body. Server will set `Etag` header to every request to this resource.

### HTTP Request

- `GET https://api.bukalapak.com/v2/products/mylapak.json`. No search parameter available. Get products which **can be purchased**.
- `GET https://api.bukalapak.com/v2/products/mylapak.json?not_for_sale_only=1`. Get products which **can not be purchased**.

### Parameters

| Parameter                |          | Description                                                  |
| ------------------------ | -------- | ------------------------------------------------------------ |
| `page`                   | optional | Page number to display. Default value is `1`.                |
| `keywords`               | optional | Keywords use to search products.                             |
| `not_for_sale_only`      | optional | Ask to return products which can not be purchased if set to `1` |
| `category_id`            | optional | Only search for items in a certain category.                 |
| `conditions`             | optional | Allowed values are `new` and `used`.                         |
| `price_min`              | optional | Minimum price.                                               |
| `price_max`              | optional | Maximum price.                                               |
| `sort_by`                | optional | Allowed values are `Terbaru`, `Termurah`, and `Termahal`.    |
| `deal_filter`            | optional | Allowed values are `applied`, `tomorrows_deal`, `pending`, `edited`, `canceled`. Values joined with `:` (e.g.: `pending:edited:canceled`) will return all products with selected deal states |
| `free_shipping_coverage` | optional | Fill with the code of the free shipping area.                |

## Create Product

> Sample Request

```shell
curl -u 67287:lXymG93y83m6RHzZV5FY \
-d '{
      "product": {
        "category_id": "242",
        "name": "Polygon Helios 200",
        "new": "true",
        "price": "2700000",
        "negotiable": "true",
        "weight": "5000",
        "stock": "2",
        "description_bb": "Sepeda roadbike polygon series helios 200",
        "free_shipping": [2, 3, 4],
        "product_detail_attributes": {
          "type": "Roadbike",
          "brand": "Polygon",
          "bahan": "Cromoly",
          "referer": "bukalapak_app"
        }
      },
      "images": "10820, 10822, 10283",
      "force_insurance": "on"
    }' \
"https://api.bukalapak.com/v2/products.json" -H "Content-Type: application/json" -X POST
```

> Success Response

```json
{
  "status": "OK",
  "id": "kxvi",
  "product_detail": {
    "id": "kxvi",
    "category": "BMX",
    "category_id": 380,
    "category_structure": ["Fashion", "Men", "Coat & Jacket"],
    "name": "Jaket Kulit Sapi",
    "active": true,
    "city": "Gorontalo",
    "province": "Gorontalo",
    "price": 5000000,
    "weight": "15000",
    "courier":["JNE REG"],
    "force_insurance": true,
    "image_ids": [],
    "images": [],
    "small_images": [],
    "url": "https://www.bukalapak.com/p/sepeda/fullbike/bmx-380/mx5p-jual-jaket-kulit-sapi",
    "desc": "Jaket kulit sapi asli, bisa dibuat kerupuk kulit dalam keadaan darurat",
    "condition": "used",
    "nego": false,
    "seller_username": "testingaccount",
    "seller_name": "Testing Account",
    "seller_id": 66,
    "seller_avatar": "https://www.bukalapak.com/system/avatars/055/f87/412/9cf/0ec/36837/medium/xkcd.png?1387424302",
    "seller_level": "Pedagang",
    "seller_level_badge_url": "https://www.bukalapak.com/images/badge/seller/xhdpi/level-5.png",
    "seller_positive_feedback": 46,
    "seller_negative_feedback": 31,
    "seller_term_condition": "Barang yang di beli tidak dapat dikembalikan.",
    "seller_alert": null,
    "payment_ready": true,
    "stock": 1,
    "specs": {
      "brand": null,
      "bahan": null,
      "ukuran": null
    },
    "state_description": [],
    "minimum_negotiable": null,
    "for_sale": true,
    "favorited": false,
    "free_shipping_coverage": [],
    "deal_info": {},
    "deal_request_state": "can request",
    "product_sin":  ["Deskripsi tidak tepat", "Spesifikasi tidak tepat"]
  }
  "message": "Produk ditambahkan"
}
```

> Failure Response
>
> #### No image supplied

```json
{
  "status": "ERROR",
  "id": null,
  "product_detail": null,
  "message": "Image dari produk dibutuhkan untuk menjual"
}
```

> #### Seller address not filled

```json
{
  "status": "ERROR",
  "id": null,
  "product_detail": null,
  "message": "Isilah alamat Anda sebelum mulai menjual"
}
```



<aside class="warning">Requires authentication</aside>



### HTTP Request

`POST https://api.bukalapak.com/v2/products.json`

### Parameters

None

### POST Request Data

| Property          |          | Description                                                  |
| ----------------- | -------- | ------------------------------------------------------------ |
| `product`         | required | Attributes of new product in JSON.                           |
| `images`          | required | List of images identifier for new product. Required between 1-5 images. Multiple images should be separated by comma. Image should be created first and one image can be used only for one product. More on [images](https://web.archive.org/web/20170912234943/bukalapak.github.io/api/#create-product-image) |
| `force_insurance` | optional | If value is defined, force insurance on product.             |

Attributes for `product` is constructed by following fields:

| Property                    |          | Description                                                  |
| --------------------------- | -------- | ------------------------------------------------------------ |
| `category_id`               | required | Category of new product. [Check this page for valid categories](https://web.archive.org/web/20170912234943/bukalapak.github.io/api/#get-all-categories). |
| `name`                      | required | Product name.                                                |
| `price`                     | required | Product price.                                               |
| `weight`                    | required | Product weight in grams.                                     |
| `stock`                     | required | Number new product in stock.                                 |
| `description_bb`            | required | Description for new product. You can use BBCode format.      |
| `new`                       | optional | Product condition as in *new* or *used*. Possible value are *true* for *new* and *false* for *used* product. |
| `negotiable`                | optional | This field indicate whether new product price is negotiable or not. Possible value are *false* for fixed price and *true* for negotiable price. Default value is *false*. |
| `free_shipping`             | optional | Fill with codes of the area where the shipping free will be made free. |
| `product_detail_attributes` | optional | Details attributes for product in JSON. [Attributes vary based on category of product](https://web.archive.org/web/20170912234943/bukalapak.github.io/api/#get-attributes-for-a-category). |

Example fields for `product_detail_attributes`:

| Property  |          | Description                                                  |
| --------- | -------- | ------------------------------------------------------------ |
| `type`    | optional | Type of product. For product categorized as *fullbike* type can be *MTB*, *Roadbike*, etc. |
| `brand`   | optional | For *Fullbike*, brand can be *United*, *Polygon*, etc.       |
| `ukuran`  | optional |                                                              |
| `bahan`   | optional |                                                              |
| `referer` | optional | Fill this if the product is uploaded from a mobile app or something else that’s not Bukalapak’s website. |

## Update Product

> Sample Request

```shell
curl -u 67287:lXymG93y83m6RHzZV5FY \
-d '{
      "product": {
        "price": "2700000",
        "stock": "2"
      },
      "images": "623525, 4552235",
    }' \
"https://api.bukalapak.com/v2/products/f3vi.json" -H "Content-Type: application/json" -X PATCH
```

> Success Response

```json
{
  "status": "OK",
  "product": {
    "id": "f3vi",
    "category": "Handphone (HP)",
    "category_id": 40,
    "category_structure": ["HP & Elektronik", "Handphone (HP)"],
    "name": "Gemini PALING MAHAL (made in mexico)",
    "active": true,
    "city": "Jakarta Selatan",
    "province": "DKI Jakarta",
    "price": 2700000,
    "weight": "1000",
    "courier": ["JNE REG"],
    "force_insurance": false,
    "image_ids": [4],
    "images": [
      "https://s0.bukalapak.com/system/images/1/6/7/6/6/8/0/large/IMG00475-20121105-1431.jpg?1352105447"
    ],
    "small_images": [
      "https://s0.bukalapak.com/system/images/1/6/7/6/6/8/0/small/IMG00475-20121105-1431.jpg?1352105447"
    ],
    "url": "https://www.bukalapak.com/p/hp-elektronik/handphone-hp/f3vi_-dijual-blackberry-8520-ori",
    "desc": "blackberry 8520 original\r\nnot fake / KW / grade ori\r\njudge by pic\r\nmade in mexico\r\nmemory card and battery not included\r\nberrindo\r\nbought it 2009 september\r\nbox, charger, etc included",
    "condition": "new",
    "nego": true,
    "payment_ready": true,
    "specs": {
      "brand": "Blackberry",
      "operating_system": "Blackberry",
      "features": [
        "Wifi", "Bluetooth", "Memory Card Slots", "MP3", "Message","e-mail", "Video Player", "QWERT Keyboard",""
      ],
      "bentuk": "Klasik (Bar)",
      "display_size": "",
      "camera": "Camera",
      "garansi": "Tidak bergaransi",
      "network": "GSM",
      "body_color": "hitam"
    },
    "state_description": [],
    "minimum_negotiable": null,
    "for_sale": true,
    "favorited": false,
    "free_shipping_coverage": [],
    "deal_info": {},
    "deal_request_state": "can request",
    "product_sin":  ["Deskripsi tidak tepat", "Spesifikasi tidak tepat"]
  },
  "message": "Produk diupdate"
}
```

> Failure Response
>
> #### Product not found by given id

```json
{
  "status": "ERROR",
  "product": null,
  "message": "Produk tidak ditemukan"
}
```

> #### Using more than 5 images

```json
{
  "status": "ERROR",
  "product": null,
  "message": "Image tidak boleh lebih dari 5"
}
```

> #### Invalid price supplied

```json
{
  "status": "ERROR",
  "product": null,
  "message": "Harga yang Anda masukkan tidak valid"
}
```



<aside class="warning">Requires authentication</aside>



### HTTP Request

`PATCH https://api.bukalapak.com/v2/products/:id.json`

### Parameters

| Parameter |          | Description                           |
| --------- | -------- | ------------------------------------- |
| `id`      | required | Identifier for product being updated. |

### PATCH Request Data

| Parameter         |          | Description                                                  |
| ----------------- | -------- | ------------------------------------------------------------ |
| `product`         | optional | Attributes of existing product in JSON                       |
| `force_insurance` | optional | If value is defined, force insurance on product.             |
| `images`          | optional | List of images identifier for existing product. There should be between 1-5 images after adding new images . Multiple images should be separated by comma. Image should be created first and image can be used only for one product. More on [images](https://web.archive.org/web/20170912234943/bukalapak.github.io/api/#create-product-image) |

Attributes for `product` is constructed by following fields:

| Property                    |          | Description                                                  |
| --------------------------- | -------- | ------------------------------------------------------------ |
| `category_id`               | required | Category of new product. [Check this page for valid categories](https://web.archive.org/web/20170912234943/bukalapak.github.io/api/#get-all-categories). |
| `name`                      | required | Product name.                                                |
| `price`                     | required | Product price.                                               |
| `weight`                    | required | Product weight in grams.                                     |
| `stock`                     | required | Number new product in stock.                                 |
| `description_bb`            | required | Description for new product. You can use BBCode format.      |
| `new`                       | optional | Product condition as in *new* or *used*. Possible value are *true* for *new* and *false* for *used* product. |
| `negotiable`                | optional | This field indicate whether new product price is negotiable or not. Possible value are *false* for fixed price and *true* for negotiable price. Default value is *false*. |
| `free_shipping`             | optional | Fill with codes of the area where the shipping free will be made free. |
| `product_detail_attributes` | optional | Details attributes for product in JSON. [Attributes vary based on category of product](https://web.archive.org/web/20170912234943/bukalapak.github.io/api/#get-attributes-for-a-category). |

Example fields for `product_detail_attributes`:

| Property |          | Description                                                  |
| -------- | -------- | ------------------------------------------------------------ |
| `type`   | optional | Type of product. For product categorized as *fullbike* type can be *MTB*, *Roadbike*, etc. |
| `brand`  | optional | For *Fullbike*, brand can be *United*, *Polygon*, etc.       |
| `ukuran` | optional |                                                              |
| `bahan`  | optional |                                                              |

## Read Product

> Sample Request

```shell
curl -u 67287:lXymG93y83m6RHzZV5FY "https://api.bukalapak.com/v2/products/kxvi.json" -H "Content-Type: application/json" -X GET
```

> Success Response

```json
{
  "status": "OK",
  "product":
  {
    "id": "kxvi",
    "category": "Handphone (HP)",
    "category_id": 40,
    "category_structure": ["HP & Elektronik", "Handphone (HP)"],
    "name": "NOKIA 5200- Black",
    "active": true,
    "city": "Jakarta Selatan",
    "province": "DKI Jakarta",
    "price": 2700000,
    "weight": 800,
    "courier": "JNE REG",
    "force_insurance": false,
    "image_ids": [1676680],
    "images": [
      "https://s0.bukalapak.com/system/images/1/6/7/6/6/8/0/large/IMG00475-20121105-1431.jpg?1352105447"],
    "small_images": [
      "https://s0.bukalapak.com/system/images/1/6/7/6/6/8/0/small/IMG00475-20121105-1431.jpg?1352105447"
    ],
    "url": "https://www.bukalapak.com/p/hp-elektronik/handphone-hp/kxvi_-dijual-bb-8520-ori-not-fake",
    "desc": "blackberry 8520 original\r\nnot fake / KW / grade ori\r\njudge by pic\r\nmade in mexico\r\nmemory card and battery not included\r\nberrindo\r\nbought it 2009 september\r\nbox, charger, etc included",
    "condition": "new",
    "nego": true
    "payment_ready": false
    "specs": {
      "brand": "Blackberry",
      "operating_system": "Blackberry",
      "features": [
        "Wifi","Bluetooth","Memory Card Slots","MP3","Message","e-mail","Video Player","QWERT Keyboard",""
      ],
      "bentuk": "Klasik (Bar)",
      "display_size": "",
      "camera": "Camera",
      "garansi": "Tidak bergaransi",
      "network": "GSM",
      "body_color": "hitam"
    },
    "state_description": ["Stok Habis", "Melanggar"],
    "minimum_negotiable": null,
    "for_sale": true,
    "favorited": false,
    "free_shipping_coverage": [],
    "tag_pages": [
      {
        "id": 3919,
        "name": "Smartphone",
        "has_landing_page": true
      },
      {
        "id": 778,
        "name": "Nokia 5200",
        "has_landing_page": false
      }
    ],
    "deal_info": {},
    "deal_request_state": "can request",
    "product_sin":  ["Deskripsi tidak tepat", "Spesifikasi tidak tepat"],
    "installment":  [
      {
        "bank_issuer": "bca",
        "terms": ["3", "6", "12"]
      }
    ]
  },
  "message": null
}
```

> Failure Response

```json
{
   "status": "ERROR",
   "product": null,
   "message": "Produk tidak ditemukan"
}
```

You can optionally set `If-None-Match` header or `Etag` header. If request `Etag` match, server will send `304 Not Modified` response without body. Server will set `Etag` header to every request to this resource.

### HTTP Requst

`GET https://api.bukalapak.com/v2/products/:id.json`

### Parameters

| Parameter |          | Description                        |
| --------- | -------- | ---------------------------------- |
| `id`      | required | Identifier for product being read. |

## Read Product

> Sample Request

```shell
curl -u 67287:lXymG93y83m6RHzZV5FY "https://api.bukalapak.com/v2/products/ar6/snapshot/342.json" -H "Content-Type: application/json" -X GET
```

> Success Response

```json
{
  "status": "OK",
  "product_snapshot": {
    "product_detail_history": {
      "id": 9,
      "transaction_id": 342,
      "product_id": 13938,
      "created_at": "2016-09-05T15:49:22.000+07:00",
      "updated_at": "2016-09-05T15:49:22.000+07:00",
      "primary_image_url": "http://www.local.host:5000/system4/images/82042/original/2015-04-23T16:07:17%2B07:00.jpg",
      "image_url": [],
      "name": "Sillybandz Radbandz Sky Scene-S",
      "price": 45000,
      "discount_percentage": null,
      "category": "Lain-lain",
      "new": true,
      "size": null,
      "weight": "400",
      "detail_category_attributes": {},
      "description": "Tidak ada deskripsi",
      "user_term_condition": null,
      "last_changed": "2015-12-30T11:26:43.000+07:00",
      "seller_name": "BL tes",
      "seller_avatar_url": "http://www.local.host:5000/images/default_avatar/small/default.jpg",
      "seller_level": 1,
      "seller_level_string": "BL User",
      "seller_feedback": "26% (19 feedback)",
      "seller_city": "Jakarta Selatan"
    }
  },
  "message": null
}
```

### HTTP Request

`GET https://api.bukalapak.om/v2/products/:product_id/snapshot/:transaction_id.json`

### Parameters

| Parameter        |          | Description                                          |
| ---------------- | -------- | ---------------------------------------------------- |
| `product_id`     | required | Identifier for product being read.                   |
| `transaction_id` | required | Identifier for transaction where the product bought. |

## Remove Product

> Sample Request

```shell
curl -u 67287:lXymG93y83m6RHzZV5FY "https://api.bukalapak.com/v2/products/kxvi/remove.json" -H "Content-Type: application/json" -X PATCH
```

> Success Response

```json
{
  "status": "OK",
  "product_id": "kxvi",
  "message": "Produk telah dihapus"
}
```

> Failure Response

```json
{
   "status": "ERROR",
   "product_id": "kxvi",
   "message": "Produk tidak ditemukan"
}
```

### HTTP Request

`PATCH https://api.bukalapak.com/v2/products/:id/remove.json`

### Parameters

| Parameter |          | Description                        |
| --------- | -------- | ---------------------------------- |
| `id`      | required | Identifier for product being read. |

## Set Product as Sold

> Sample Request

```shell
curl -u 67287:lXymG93y83m6RHzZV5FY "https://api.bukalapak.com/v2/products/kxvi/sold.json" -H "Content-Type: application/json" -X PATCH
```

> Success Response

```json
{
  "status": "OK",
  "id": "kxvi",
  "message": "Produk telah diset menjadi terjual"
}
```

> Failure Response

```json
{
  "status": "ERROR",
  "product_id": null,
  "message": "Produk tidak ditemukan"
}
```



<aside class="warning">Requires authentication</aside>



### HTTP Request

`PATCH https://api.bukalapak.com/v2/products/:id/sold.json`

### Parameters

| Parameter |          | Description                        |
| --------- | -------- | ---------------------------------- |
| `id`      | required | Identifier for product being sold. |

## Push Product

> Sample Request

```shell
curl -u 67287:lXymG93y83m6RHzZV5FY "https://api.bukalapak.com/v2/products/kxvi/push.json" -d '{"force": "0"}' -H "Content-Type: application/json" -X PATCH
```

> Success Response

```json
{
  "status": "OK",
  "can_push": true,
  "remaining_push": 20,
  "deposit":0,
  "push_price":500,
  "message": "Barang telah berhasil di-push"
}
```

> Failure Response

```json
{
  "status": "ERROR",
  "can_push": false,
  "remaining_push": 0,
  "deposit":0,
  "push_price":500,
  "message": "Barang gagal di-push"
}
```



<aside class="warning">Requires authentication</aside>



### HTTP Request

`PATCH https://api.bukalapak.com/v2/products/:id/push.json`

### Parameters

| Parameter |          | Description                                                  |
| --------- | -------- | ------------------------------------------------------------ |
| `id`      | required | Identifier for product being pushed.                         |
| `force`   | optional | If set to `1`, will reduce Bukadompet balance when Push Package is not enough. If set to `0`, will not reduce Bukadompet balance when Push Package is not enough. |

## Push Many Product

> Sample Request

```shell
curl -u 7:tok3ntok3n "https://api.bukalapak.com/v2/products/bulk_push.json"
    -X PATCH
    -d '{"products_id":["s","u","t","a","b","c"], "force":"0"}'
    -H "Content-Type: application/json"
```

> Success Response

```json
{
    "status":"OK",
    "can_push":true,
    "remaining_push":0,
    "message":"Semua barang berhasil di-push",
    "deposit":0,
    "push_price":500,
    "success":["s","u","t","a","b","c"],
    "fail":[]
}
```

> Failure Response

```json
{
    "status":"ERROR",
    "can_push":false,
    "remaining_push":0,
    "message":"Barang gagal di-push!",
    "deposit":0,
    "push_price":500,
    "success":[],
    "fail":["s","u","t","a","b","c"]
}
```



<aside class="warning">Requires authentication</aside>



### HTTP Request

`PATCH https://api.bukalapak.com/v2/products/bulk_push.json`

### Parameters

| Parameter     |          | Description                                                  |
| ------------- | -------- | ------------------------------------------------------------ |
| `products_id` | required | Identifier for products being pushed in array.               |
| `force`       | optional | If set to `1`, will reduce Bukadompet balance when Push Package is not enough. If set to `0`, will not reduce Bukadompet balance when Push Package is not enough. |

## Set Product as Available

> Sample Request

```shell
curl -u 67287:lXymG93y83m6RHzZV5FY "https://api.bukalapak.com/v2/products/kxvi/relist.json" -H "Content-Type: application/json" -X PATCH
```

> Success Response

```json
{
  "status": "OK",
  "id": "kxvi",
  "message": "Produk telah diset untuk dijual"
}
```

> Failure Response

```json
{
  "status": "ERROR",
  "product": null,
  "message": "Produk tidak ditemukan"
}
```



<aside class="warning">Requires authentication</aside>



### HTTP Request

`PATCH https://api.bukalapak.com/v2/products/:id/relist.json`

### Parameters

| Parameter |          | Description                          |
| --------- | -------- | ------------------------------------ |
| `id`      | required | Identifier for product being relist. |

## Set Many Product as Available

> Sample Request

```shell
curl -u 7:tok3ntok3n "https://api.bukalapak.com/v2/products/bulk_set_available.json" -X PATCH -d '{"products_id":["s","u","t","a","b","c"]}' -H "Content-Type: application/json"
```

> Success Response

```json
{
  "status":"OK",
  "message":"Status semua barang akan menjadi tersedia dalam beberapa saat",
  "success":["s","u","t","a","b","c"],
  "fail":[]
}
```

> Failure Response

```json
{
  "status":"ERROR",
  "message":"Gagal mengubah status barang menjadi tersedia!",
  "success":[],
  "fail":["s","u","t","a","b","c"]
}
```



<aside class="warning">Requires authentication</aside>



### HTTP Request

`PATCH https://api.bukalapak.com/v2/products/bulk_set_available.json`

### Parameters

| Parameter     |          | Description                                 |
| ------------- | -------- | ------------------------------------------- |
| `products_id` | required | Identifier for products to relist in array. |

## Set Many Product as Unavailable

> Sample Request

```shell
curl -u 7:tok3ntok3n "https://api.bukalapak.com/v2/products/bulk_set_unavailable.json" -X PATCH -d '{"products_id":["s","u","t","a","b","c"]}' -H "Content-Type: application/json"
```

> Success Response

```json
{
  "status":"OK",
  "message":"Status semua barang akan menjadi tidak tersedia dalam beberapa saat",
  "success":["s","u","t","a","b","c"],
  "fail":[]
}
```

> Failure Response

```json
{
  "status":"ERROR",
  "message":"Gagal mengubah status barang menjadi tidak tersedia!",
  "success":[],
  "fail":["s","u","t","a","b","c"]
}
```



<aside class="warning">Requires authentication</aside>



### HTTP Request

`PATCH https://api.bukalapak.com/v2/products/bulk_set_unavailable.json`

### Parameters

| Parameter     |          | Description                                 |
| ------------- | -------- | ------------------------------------------- |
| `products_id` | required | Identifier for products to unlist in array. |

## Read Product Review

> Sample Request

```shell
curl -u 67287:lXymG93y83m6RHzZV5FY "https://api.bukalapak.com/v2/products/kxvi/reviews.json" -H "Content-Type: application/json" -X GET
```

> Success Response

```json
{
  "status": "OK",
  "message": null,
  "rating": {
    "average_rate": "4.0",
    "user_count": 1
  }
  "reviews": [
    {
      "id": 28,
      "sender_id": 4,
      "sender_name": "Avril Lavigne",
      "sender_type": "User",
      "rate": 5,
      "body": "I like this cap, its really comfortable",
      "updated_at": "2016-02-02T16:31:31.000+07:00",
      "product": null
    }
  ]
}
```

Get Review from Product

### HTTP Request

`GET https://api.bukalapak.com/v2/products/:id/reviews.json`

### Parameters

| Parameter  |          | Description                                                |
| ---------- | -------- | ---------------------------------------------------------- |
| `id`       | required | Identifier for product.                                    |
| `page`     | optional | Page number to display.                                    |
| `per_page` | optional | Number of records to display per page. Default value is 5. |

## Get Shipping List

> Sample Request

```shell
curl "https://api.bukalapak.com/v2/products/kxvi/shipping_list.json?to=Ambon&to_area=Ambon" -H "Content-Type: application/json"
```

> Success Response

```json
{
  "status":"OK",
  "fee_list":[
    {
      "courier_name":"tiki",
      "couriers":[
        {
          "service":"TIKI Reg",
          "price":84500,
          "eta":1
        }
      ]
    },
    {
      "courier_name":"rpx",
      "couriers":[
        {
          "service":"RPX Economy Package",
          "price":60000,
          "eta":"4"
        }
      ]
    }
  ],
  "message":null
}
```

### HTTP Request

`GET htts://api.bukalapak.com/v2/products/:id/shipping_list.json`

### Parameters

| Parameter  |          | Description                             |
| ---------- | -------- | --------------------------------------- |
| `id`       | required | Identifier for product.                 |
| `to`       | required | Shipping destination city.              |
| `to_area`  | required | Shipping destination district.          |
| `quantity` | optional | Product quantity, default value is `1`. |

## Get Related Products

> Sample Request

```shell
curl -u 67287:lXymG93y83m6RHzZV5FY "https://api.bukalapak.com/v2/products/3/related.json" -H "Content-Type: application/json"
```

> Success Response

```json
{
  "status": "OK",
  "products": [
    {
      "id": "m",
      "category": "Hardware \u0026 Accessories",
      "category_id":66,
      "category_structure" : ["Komputer", "Hardware \u0026 Accessories"],
      "name": "(507284-001) HP 300GB 2.5\" SFF 6G Dual Port SAS 10K RPM Hot Plug Hard Drive",
      "active": true,
      "city": "Bengkulu Selatan",
      "province": "Bengkulu",
      "price": 2500000,
      "weight": "1",
      "courier": ["JNE REG"],
      "force_insurance": null,
      "image_ids": [93],
      "images": [
        "http://www.bukalapak.com/system3/images/9/3/large/2014-09-10T21_52_41_07_00.jpg"
      ],
      "small_images": [
        "http://www.bukalapak.com/system3/images/9/3/small/2014-09-10T21_52_41_07_00.jpg"
      ],
      "url": "http://www.bukalapak.com/p/komputer/hardware-accessories/m-jual-507284-001-hp-300gb-2-5-sff-6g-dual-port-sas-10k-rpm-hot-plug-hard-drive",
      "desc": "Technical Specifications :\u003cbr/\u003eHard Drive Capacity : 300GB\u003cbr/\u003eGeneration : SAS\u003cbr/\u003eExternal Data Transfer Rate : 6.0 GB/sec",
      "condition": "new",
      "nego": false,
      "seller_username": "ragen",
      "seller_name": "Ragen",
      "seller_id": 1,
      "seller_avatar": "http://www.bukalapak.com/images/default_avatar/medium/default.jpg",
      "seller_level": "BL User",
      "seller_level_badge_url": "https://www.bukalapak.com/images/badge/seller/xhdpi/level-5.png",
      "seller_positive_feedback": 5,
      "seller_negative_feedback": 1,
      "seller_term_condition": "Barang yang di beli tidak dapat dikembalikan.",
      "seller_alert": null,
      "payment_ready": true,
      "stock": 1,
      "specs": {},
      "state_description": [],
      "minimum_negotiable": null,
      "for_sale": true,
      "favorited": false,
      "free_shipping_coverage": [],
      "deal_info": {},
      "deal_request_state": "can request",
      "product_sin":  ["Deskripsi tidak tepat", "Spesifikasi tidak tepat"]
    },
    ...
  ],
  "message": null
  }
}
```

### HTTP Request

`GET https://api.bukalapak.com/v2/products/:id/related.json`

### Parameters

| Parameter |          | Description              |
| --------- | -------- | ------------------------ |
| `id`      | required | Identifier for product . |

## Edit Product’s Label

> Sample Request

```shell
curl -u "66:tokenkeyiskmzwa8awaa" -X "PATCH" "https://api.bukalapak.com/v2/products/update_label.json" -d '{"product": {"product_id": "5h", "labels": [64,65]}}' -H "Content-Type: application/json"
```

> Success Response

```json
{
  "status": "OK",
  "product": {
    "product": {
      "id": 197,
      "type": null,
      "name": "Tas Selempang SUPREME",
      "price": 130000,
      "description": "Tas Selempang SUPREME<br /><br />Meskipun merupakan tas olahraga, Tas selempang SUPREME dapat digunakan untuk kebutuhan lainnya seperti tempat untuk meletakkan barang bawaan seperti handphone, buku dan aksesoris lainnya, saat hangout bersama teman.<br /><br />- Ukuran (Tinggi x Lebar x Tebal) : 35cm x 18cm x 9cm<br />- Pilihan Warna: Merah, Pink, dan Biru dengan Motif Air<br />- Tali selempang dapat dipindah ke kanan atai kiri tas. (ada pengaitnya di sisi kanan dan kiri tas.)<br />- Kompartemen/Bagian:<br />> 1 kompatemen depan dengan resleting<br />> 1 kompartemen utama dengan resleting, di dalamnya terdapat tambahan 1 saku kecil.<br />- Apa yang anda lihat di foto, itulah yang Anda dapatkan<br />============================================================<br />Contact:<br />LINE: onionmonkey.shop<br />INSTAGRAM: onionmonkey.shop<br />FACEBOOK: https://www.facebook.com/",
      "city": "Jakarta Selatan",
      "province": "DKI Jakarta",
      "user_id": 5,
      "category_id": 163,
      "available": true,
      "categories_string": null,
      "primary_imageid": null,
      "new": true,
      "size": null,
      "rent_or_sell": "Dijual",
      "year": null,
      "car_model_id": null,
      "motor_model_id": null,
      "car_type": null,
      "kilometer": null,
      "transmition": null,
      "delta": true,
      "comments_count": 0,
      "images_count": 0,
      "pilihan": false,
      "cached_slug": null,
      "created_at": "2016-01-05T13:49:58.000+07:00",
      "updated_at": "2016-01-20T02:13:48.033+07:00",
      "description_bb": "Tas Selempang SUPREME<br /><br />Meskipun merupakan tas olahraga, Tas selempang SUPREME dapat digunakan untuk kebutuhan lainnya seperti tempat untuk meletakkan barang bawaan seperti handphone, buku dan aksesoris lainnya, saat hangout bersama teman.<br /><br />- Ukuran (Tinggi x Lebar x Tebal) : 35cm x 18cm x 9cm<br />- Pilihan Warna: Merah, Pink, dan Biru dengan Motif Air<br />- Tali selempang dapat dipindah ke kanan atai kiri tas. (ada pengaitnya di sisi kanan dan kiri tas.)<br />- Kompartemen/Bagian:<br />> 1 kompatemen depan dengan resleting<br />> 1 kompartemen utama dengan resleting, di dalamnya terdapat tambahan 1 saku kecil.<br />- Apa yang anda lihat di foto, itulah yang Anda dapatkan<br />============================================================<br />Contact:<br />LINE: onionmonkey.shop<br />INSTAGRAM: onionmonkey.shop<br />FACEBOOK: https://www.facebook.com/",
      "active": true,
      "contact_name": null,
      "contact_phone": null,
      "contact_fb": null,
      "sold_at": null,
      "stock": 61,
      "state": "available",
      "state_changed_at": {},
      "stat_changed_at": null,
      "shippping_method": null,
      "minimum_negotiable": null,
      "negotiable": false,
      "weight": "100"
    }
  },
  "message": "Pengaturan label berhasil"
}
```



<aside class="warning">Requires authentication</aside>



### HTTP Request

`PATCH https://api.bukalapak.com/v2/products/update_label.json`

### Parameters

None

## Bulk Edit Product’s Label

> Sample Request

```shell
curl -u "66:tokenkeyiskmzwa8awaa" -X "PATCH" "https://api.bukalapak.com/v2/products/bulk_update_label.json" -d '{"products": [{"product_id": "5h", "labels": [64,65]}, {"product_id": "5v", "labels": [64]}]}' -H "Content-Type: application/json"
```

> Success Response

```json
{
  "status": "OK",
  "product": {
    "product": {
      "id": 211,
      "type": null,
      "name": "Tas Olahraga T90",
      "price": 120000,
      "description": "Tas Olahraga T90\r\n\r\n- Ukuran (P x L x T):40cm x 20cm x 22cm\r\n- Warna yang tersedia: Merah. (Biru Stock Habis)\r\n- Kompartemen utama.\r\n- Ada tali panjang\r\n\r\n============================================================\r\nContact:\r\nLINE: onionmonkey.shop\r\nINSTAGRAM: onionmonkey.shop\r\nFACEBOOK: https://www.facebook.com/onionmonkey.shop",
      "city": "Jakarta Selatan",
      "province": "DKI Jakarta",
      "user_id": 5,
      "category_id": 224,
      "available": true,
      "categories_string": null,
      "primary_imageid": null,
      "new": true,
      "size": null,
      "rent_or_sell": "Dijual",
      "year": null,
      "car_model_id": null,
      "motor_model_id": null,
      "car_type": null,
      "kilometer": null,
      "transmition": null,
      "delta": true,
      "comments_count": 0,
      "images_count": 0,
      "pilihan": false,
      "cached_slug": null,
      "created_at": "2016-01-05T13:53:21.000+07:00",
      "updated_at": "2016-01-20T02:19:33.920+07:00",
      "description_bb": "Tas Olahraga T90\r\n\r\n- Ukuran (P x L x T):40cm x 20cm x 22cm\r\n- Warna yang tersedia: Merah. (Biru Stock Habis)\r\n- Kompartemen utama.\r\n- Ada tali panjang\r\n\r\n============================================================\r\nContact:\r\nLINE: onionmonkey.shop\r\nINSTAGRAM: onionmonkey.shop\r\nFACEBOOK: https://www.facebook.com/onionmonkey.shop",
      "active": true,
      "contact_name": null,
      "contact_phone": null,
      "contact_fb": null,
      "sold_at": null,
      "stock": 61,
      "state": "available",
      "state_changed_at": {},
      "stat_changed_at": null,
      "shippping_method": null,
      "minimum_negotiable": null,
      "negotiable": false,
      "weight": "500"
    }
  },
  "message": "Pengaturan label berhasil"
}
```



<aside class="warning">Requires authentication</aside>



### HTTP Request

`PATCH https://api.bukalapak.com/v2/products/bulk_update_label.json`

### Parameters

None

## Get Promo Banners

> Sample Request

```shell
curl https://api.bukalapak.com/v2/products/promo_banners.json?version=2
```

> Sample Response

```json
{
  "status": "OK",
  "promo_banners": [
    {
      "image": "https://s0.bukalapak.com/system4/flash_banners/2980/original/rsz_rok_wanita_178x178.jpg",
      "description": "Promo Rok Wanita Harga mulai 20.000-an",
      "info": {
        "type": "campaign",
        "id": 2347,
        "url": "https://www.bukalapak.com/promo/promo-rok-wanita-harga-mulai-20-000-an",
        "promo_due": "2016-01-19T23:59:00.000+07:00"
      }
    },
    {
      "image": "https://s0.bukalapak.com/system4/flash_banners/2965/original/178x178_%281%29.jpg",
      "description": "Botol Minum Sepeda Ekonomis Dan Praktis Mulai 30 Ribu",
      "info": {
        "type": "url",
        "id": null,
        "url": "https://www.bukalapak.com/promo/botol-minum-sepeda-ekonomis-dan-praktis-harga-mulai-30-ribuan?campaign_ids=1236&page=2&search%5Bkeywords%5D=&view_mode=grid",
        "promo_due": null
      }
    }
  ],
  "message": null
}
```

Gets current promo banners' informations. Promo banners are banners titled `promo hari ini` on Bukalapak homepage.

### HTTP Request

`GET https://api.bukalapak.com/v2/products/promo_banners.json`

### Parameters

| Parameter |          | Description                                                  |
| --------- | -------- | ------------------------------------------------------------ |
| `version` | optional | JSON formatting version to display. Setting this to `2` will give you the new format. The old format is yet to be deprecated. |

### Dictionary

Possible values of `type` for `version=2` :

| inputType  | Description                                            |
| ---------- | ------------------------------------------------------ |
| `campaign` | A campaign promo. With `id` and, usually, `promo_due`. |
| `url`      | Just a url. Has no `id` or `promo_due`.                |

## Get Product Bidding Info

> Sample Request

```shell
curl -u 67287:lXymG93y83m6RHzZV5FY "https://api.bukalapak.com/v2/products/3/bid.json"
```

> Success Response

```json
{
  "status": "OK",
  "bid_setting": {
    "on_sem": true,
    "bid_value": 1000,
    "sem_start": "2017-05-09T00:00:00.000+07:00",
    "sem_end": "2017-05-16T23:59:59.999+07:00",
    "sem_keyword": "",
    "min_bid": 200,
    "max_bid": 9999
  },
  "recommended_bid_value": 200,
  "message": null
}
```

> Failure Response

```json
{
  "status": "ERROR",
  "bid_setting": null,
  "message": "Gagal mengakses konfigurasi Promoted Push"
}
```

Get product bidding information.



<aside class="warning">Requires authentication</aside>



### HTTP Request
`GET https://api.bukalapak.com/v2/products/:id/bid.json`

### Parameters

| Parameter |          | Description             |
| --------- | -------- | ----------------------- |
| `id`      | required | Identifier for product. |

## Promote Push Product

> Sample Request

```shell
curl -u 67287:lXymG93y83m6RHzZV5FY "https://api.bukalapak.com/v2/products/3/bid.json"
    -X PATCH
    -d '{"start_year":"2017", "start_month":"5", "start_day":"10", "end_year":"2017", "end_month":"6", "end_day":"5", "bid_value":"500", "on_sem":"1"}'
    -H "Content-Type: application/json"
```

> Success Response

```json
{
  "status": "OK",
  "message": "Promoted Push barang LCD Monitor berhasil disimpan dan diaktifkan"
}
```

> Sample Failure Response

```json
{
  "status": "ERROR",
  "message": "Gagal mengubah konfigurasi Promoted Push produk"
}
```



<aside class="warning">Requires authentication</aside>



### HTTP Request

`PATCH https://api.bukalapak.com/v2/products/:id/bid.json`

### Parameters

| Parameter     |          | Description                                                  |
| ------------- | -------- | ------------------------------------------------------------ |
| `start_year`  | required | Start year of promoted push.                                 |
| `start_month` | required | Start month of promoted push.                                |
| `start_day`   | required | Start date of promoted push.                                 |
| `end_year`    | required | End year of promoted push.                                   |
| `end_month`   | required | End month of promoted push.                                  |
| `end_day`     | required | End date of promoted push.                                   |
| `bid_value`   | required | Amount to bid.                                               |
| `on_sem`      | optional | Promoted push activation, set value to `1` to activate promoted push. |

# Product Reviews

## Create Product Review

> Sample Request

```shell
curl -u 67287:lXymG93y83m6RHzZV5FY "https://api.bukalapak.com/v2/product_review.json" -X "POST" -d "body=I really love this stuff. Thank u.&rate=2&transaction_id=82&product_id=13"
```

> Success Response

```json
{
  "status": "OK",
  "message": "Ulasan berhasil diperbarui",
  "review": {
    "id": 28,
    "sender_id": 4,
    "sender_name": "Name of Sender",
    "sender_type": "User",
    "rate": 3,
    "body": "What a cool Batman Action Figure",
    "updated_at": "2016-02-18T17:50:28.000+07:00",
    "product": {
      "deal_info": {},
      "deal_request_state": "can request",
      "price": 700000,
      "And all the other product attributes": "",
    }
  }
}
```

Create a review for given product in transaction.



<aside class="warning">Requires authentication</aside>



### HTTP Request

`POST https://api.bukalapak.com/v2/product_review.json`

### Parameters

| Parameter        | required | Description                                |
| ---------------- | -------- | ------------------------------------------ |
| `rate`           | required | Rate for product being reviewed            |
| `body`           | required | Review for product                         |
| `transaction_id` | required | Transaction id for product being reviewed. |
| `product_id`     | required | Id for product being reviewed.             |

## Update Product Review

> Sample Request

```shell
curl -u 67287:lXymG93y83m6RHzZV5FY "https://api.bukalapak.com/v2/product_review/102.json" -X "PATCH" -d "body=Barangnya bagus, terima kasih&rate=5"
```

> Success Response

```json
{
  "status": "OK",
  "message": "Ulasan berhasil diperbarui",
  "review": {
    "id": 28,
    "sender_id": 4,
    "sender_name": "Name of Sender",
    "sender_type": "User",
    "rate": 3,
    "body": "What a cool Batman Action Figure",
    "updated_at": "2016-02-18T17:50:28.000+07:00",
    "product": {
      "deal_info": {},
      "deal_request_state": "can request",
      "price": 700000,
      "And all the other product attributes": "",
    }
  }
}
```

Update review for given product review id.



<aside class="warning">Requires authentication</aside>



### HTTP Request

`PATCH https://api.bukalapak.com/v2/product_review/:id.json`

### Parameters

| Parameter | required | Description                         |
| --------- | -------- | ----------------------------------- |
| `id`      | required | Identifier for review being updated |
| `rate`    | required | Rate for product being reviewed     |
| `body`    | required | Review for product                  |

## Create Product Review Quick Buyer

> Sample Request

```shell
curl -u 67287:lXymG93y83m6RHzZV5FY "https://api.bukalapak.com/v2/product_review/quick_buy.json" -X "POST" -d "body=I really love this stuff. Thank u.&rate=2&transaction_id=82&product_id=13&token=0002PN0z"
```

> Success Response

```json
{
  "status": "OK",
  "message": "Ulasan berhasil diperbarui",
  "review": {
    "id": 28,
    "sender_id": 4,
    "sender_name": "Name of Sender",
    "sender_type": "QuickBuyer",
    "rate": 3,
    "body": "What a cool Batman Action Figure",
    "updated_at": "2016-02-18T17:50:28.000+07:00",
    "product": {
      "deal_info": {},
      "deal_request_state": "can request",
      "price": 700000,
      "And all the other product attributes": "",
    }
  }
}
```

Create a review for given product in transaction.



<aside class="warning">Requires authentication</aside>



### HTTP Request

`POST https://api.bukalapak.com/v2/product_review/quick_buy.json`

### Parameters

| Parameter        | required | Description                                |
| ---------------- | -------- | ------------------------------------------ |
| `rate`           | required | Rate for product being reviewed            |
| `body`           | required | Review for product                         |
| `transaction_id` | required | Transaction id for product being reviewed. |
| `product_id`     | required | Id for product being reviewed.             |
| `token`          | required | Access token of Quick Buyer                |

## Update Product Review Quick Buyer

> Sample Request

```shell
curl -u 67287:lXymG93y83m6RHzZV5FY "https://api.bukalapak.com/v2/product_review/quick_buy/102.json" -X "PATCH" -d "body=Barangnya bagus, terima kasih&rate=5&token=0002PN0z"
```

> Success Response

```json
{
  "status": "OK",
  "message": "Ulasan berhasil diperbarui",
  "review": {
    "id": 28,
    "sender_id": 4,
    "sender_name": "Name of Sender",
    "sender_type": "QuickBuyer",
    "rate": 3,
    "body": "What a cool Batman Action Figure",
    "updated_at": "2016-02-18T17:50:28.000+07:00",
    "product": {
      "deal_info": {},
      "deal_request_state": "can request",
      "price": 700000,
      "And all the other product attributes": "",
    }
  }
}
```

Update review for given product review id.



<aside class="warning">Requires authentication</aside>



### HTTP Request

`PATCH https://api.bukalapak.com/v2/product_review/quick_buy/:id.json`

### Parameters

| Parameter | required | Description                         |
| --------- | -------- | ----------------------------------- |
| `id`      | required | Identifier for review being updated |
| `rate`    | required | Rate for product being reviewed     |
| `body`    | required | Review for product                  |
| `token`   | required | Access token of Quick Buyer         |

# Promoted Pushes

## Get Promoted Push Info

> Sample Request

```shell
curl -u 67287:lXymG93y83m6RHzZV5FY "https://api.bukalapak.com/v2/budget.json"
```

> Success Response

```json
{
  "status": "OK",
  "budget": 10000,
  "message": null,
  "balance": 50000,
  "loan_info": {
    "eligible": true,
    "limit": 100000,
    "remaining": 100000
  },
  "loan_banner_image": "https://s3.bukalapak.com/uploads/banner/promotion_feature/c2c22420d309154d80449b85/mobile/loan_banner_m.jpg_1488536584",
  "loan_banner_link": "https://www.bukalapak.com/bantuan/category/fitur-bukalapak/pinjaman-saldo?utm_medium=banner_promotion"
}
```

Get information for current user’s promoted push budget



<aside class="warning">Requires authentication</aside>



### HTT Request

`GET https://api.bukalapak.com/v2/budget.json`

### Parameters

None

## Topup Promoted Push

> Sample Request

```shell
curl -u 67287:lXymG93y83m6RHzZV5FY -X "POST" "https://api.bukalapak.com/v2/budget.json" -d '{"amount": "10000"}' -H 'Content-Type: application/json'
```

> Success Response

```json
{
  "status": "OK",
  "budget": 10000,
  "message": "Penambahan Budget Promoted Push berhasil. Gunakan Promoted Push barang pilihanmu di halaman Barang Dijual",
  "balance": 50000,
  "loan_info": {
    "eligible": true,
    "limit": 100000,
    "remaining": 100000
  }
}
```

> Failure Response
>
> #### Frozen BukaDompet

```json
{
  "status": "ERROR",
  "budget": 10000,
  "message": "Saldo BukaDompet Anda dibekukan, Anda tidak dapat melakukan topup Budget Promoted Push",
  "balance": 50000,
  "loan_info": {
    "eligible": true,
    "limit": 100000,
    "remaining": 100000
  }
}
```

> #### Invalid topup amount

```json
{
  "status": "ERROR",
  "budget": 10000,
  "message": "Minimal Penambahan Budget Promoted Push adalah 200",
  "balance": 50000,
  "loan_info": {
    "eligible": true,
    "limit": 100000,
    "remaining": 100000
  }
}
```

> #### Failed to topup

```json
{
  "status": "ERROR",
  "budget": 10000,
  "message": "Gagal melakukan topup Budget Promoted Push",
  "balance": 50000,
  "loan_info": {
    "eligible": true,
    "limit": 100000,
    "remaining": 100000
  }
}
```

Topup current user’s promoted push budget



<aside class="warning">Requires authentication</aside>



### HTTP Request

`POST https://api.bukalapak.com/v2/budget.json`

### Parameters

| Parameter |          | Description                     |
| --------- | -------- | ------------------------------- |
| `amount`  | required | Amount of promoted push budget. |

## Get Promoted Push Click History

> Sample Request

```shell
curl -u 67287:lXymG93y83m6RHzZV5FY "https://api.bukalapak.com/v2/budget/click_history.json?page=1&per_page=2"
```

> Success Response

```json
{
  "status": "OK",
  "events": [
    {
      "time": "2017-05-09T06:37:55.018+07:00",
      "cost": 3820,
      "product": {
        "deal_info": {},
        "deal_request_state": "can request",
        "price": 100000000,
        "courier": [
          "JNE REG",
          "JNE YES"
        ],
        "seller_username": "sayurkangkung",
        "seller_name": "Sayur Kangkung",
        "seller_id": 67287,
        "seller_avatar": "https://www.bukalapak.com/images/default_avatar/medium/default.jpg",
        "seller_level": "Pedagang",
        "seller_level_badge_url": "https://www.bukalapak.com/images/badge/seller/xhdpi/level-2.png",
        "seller_delivery_time": "3 jam",
        "seller_positive_feedback": 20,
        "seller_negative_feedback": 5,
        "seller_term_condition": "",
        "seller_alert": null,
        "for_sale": true,
        "state_description": [],
        "premium_account": true,
        "top_merchant": false,
        "last_order_schedule": null,
        "seller_voucher": {},
        "waiting_payment": 0,
        "sold_count": 0,
        "specs": {},
        "force_insurance": true,
        "free_shipping_coverage": [],
        "id": "7rdty6",
        "url": "https://www.bukalapak.com/p/food/makanan/7rdty6-jual-cireng-salju",
        "name": "Cireng Salju",
        "active": true,
        "city": "Jakarta Selatan",
        "province": "DKI Jakarta",
        "weight": 100,
        "image_ids": [
          1125718536
        ],
        "images": [
          "https://s1.bukalapak.com/img/6358175211/large/Cireng_Salju.jpg"
        ],
        "small_images": [
          "https://s1.bukalapak.com/img/6358175211/small/Cireng_Salju.jpg"
        ],
        "desc": "Cireng salju enak",
        "condition": "new",
        "stock": 1,
        "favorited": false,
        "created_at": "2017-03-23T14:58:29.000+07:00",
        "updated_at": "2017-04-25T12:46:10.000+07:00",
        "product_sin": [],
        "rating": {
          "average_rate": 0,
          "user_count": 0
        },
        "current_variant_name": "",
        "current_product_sku_id": 461372866,
        "product_sku": [],
        "options": [],
        "category_id": 2389,
        "category": "Makanan",
        "category_structure": [
          "Food"
        ],
        "interest_count": 2,
        "last_relist_at": "2017-04-21T09:31:16.000+07:00",
        "view_count": 303
      }
    },
    {
      "time": "2017-05-09T05:59:01.689+07:00",
      "cost": 540,
      "product": {
        "deal_info": {},
        "deal_request_state": "can request",
        "price": 500000,
        "courier": [
          "JNE REG",
          "JNE YES"
        ],
        "seller_username": "sayurkangkung",
        "seller_name": "Sayur Kangkung",
        "seller_id": 20528363,
        "seller_avatar": "https://www.bukalapak.com/images/default_avatar/medium/default.jpg",
        "seller_level": "Pedagang",
        "seller_level_badge_url": "https://www.bukalapak.com/images/badge/seller/xhdpi/level-2.png",
        "seller_delivery_time": "3 jam",
        "seller_positive_feedback": 20,
        "seller_negative_feedback": 5,
        "seller_term_condition": "",
        "seller_alert": null,
        "for_sale": true,
        "state_description": [],
        "premium_account": true,
        "top_merchant": false,
        "last_order_schedule": null,
        "seller_voucher": {},
        "waiting_payment": -6,
        "sold_count": 2,
        "specs": {},
        "force_insurance": false,
        "free_shipping_coverage": [],
        "id": "5828th",
        "url": "https://www.bukalapak.com/p/food/makanan/5828th-jual-bakso-goreng",
        "name": "Bakso goreng",
        "active": true,
        "city": "Jakarta Selatan",
        "province": "DKI Jakarta",
        "weight": 100,
        "image_ids": [
          723924830
        ],
        "images": [
          "https://s0.bukalapak.com/img/038429327/large/Bakso_Goreng.jpg"
        ],
        "small_images": [
          "https://s0.bukalapak.com/img/038429327/small/Bakso_Goreng.jpg"
        ],
        "desc": "Bakso goreng pedas manis",
        "condition": "new",
        "stock": 1,
        "favorited": false,
        "created_at": "2016-12-06T18:32:15.000+07:00",
        "updated_at": "2017-04-25T12:46:15.000+07:00",
        "product_sin": [],
        "rating": {
          "average_rate": 0,
          "user_count": 0
        },
        "current_variant_name": "",
        "current_product_sku_id": 269078168,
        "product_sku": [],
        "options": [],
        "category_id": 558,
        "category": "Makanan",
        "category_structure": [
          "Food"
        ],
        "interest_count": 49,
        "last_relist_at": "2017-04-06T13:30:52.000+07:00",
        "view_count": 416
      }
    }
  ],
  "message": null
}
```

Get current user’s promoted push click history



<aside class="warning">Requires authentication</aside>



### HTTP Request

`GET https://api.bukalapak.com/v2/budget/click_history.json`

### Parameters

| Property   |          | Description                                  |
| ---------- | -------- | -------------------------------------------- |
| `page`     | required | Page number to display.                      |
| `per_page` | required | Number of click history to display per page. |

# Pushes

## Get Push Package List

> Sample Request

```shell
curl -u 67287:lXymG93y83m6RHzZV5FY https://api.bukalapak.com/v2/pushes/push_package.json
```

> Sample Response

```json
{
  "status": "OK",
  "available_packages": [
    {
      "name": "100",
      "push_amount": 100,
      "price": 20000,
      "validity_day": 30,
      "recommendation": true,
      "description": "Diskon 20%",
      "normal_price": 20000,
      "discount": 0
    },
    {
      "name": "Super Big",
      "push_amount": 10000,
      "price": 500000,
      "validity_day": 90,
      "recommendation": false,
      "description": null,
      "normal_price": 500000,
      "discount": 0
    }
  ],
  "balance": 550000,
  "push_balance": {
    "balance": 0,
    "grace": false,
    "date": "2016-09-01T23:59:59.000+07:00"
  },
  "discount_for_premium_user": 5,
  "premium_user": true,
  "message": null
}
```

### HTTP Request

`GET https://api.bukalapak.com/v2/pushes/push_package.json`

### Parameters

None

## Buy Push Package

### HTTP Request

`POST https://api.bukalapak.com/v2/pushes/push_package.json`

### Parameters

| Parameter  |          | Description               |
| ---------- | -------- | ------------------------- |
| `name`     | required | Name of the push package. |
| `password` | required | User’s password.          |

> Sample Request

```shell
curl -u 67287:lXymG93y83m6RHzZV5FY https://api.bukalapak.com/v2/pushes/push_package.json -X POST --data "name=Super Big&password=testing1234"
```

> Success Response

```json
{
  "status": "OK",
  "balance": 100000,
  "message": "Pembelian Paket Super Big Berhasil"
}
```

> Failure Response
>
> #### Password doesn’t match

```json
{
  "status": "ERROR",
  "balance": null,
  "message": "Verifikasi Password Gagal"
}
```

> #### No packet chosen

```json
{
  "status": "ERROR",
  "balance": null,
  "message": "Anda Belum Memilih Paket"
}
```

> #### Invalid packet name

```json
{
  "status": "ERROR",
  "balance": null,
  "message": "Tidak Ada Paket Cicilan"
}
```

> #### Other failures

```json
{
  "status": "ERROR",
  "balance": null,
  "message": "Paket Gagal Ditambahkan"
}
```

# SEO Pages

## Brand Page

> Sample Request

```shell
curl https://api.bukalapak.com/v2/c/handphone/aksesoris-handphone/screen-guard/merk/hugu.json
```

> Sample Response

```json
{
  "status": "OK",
  "message": null,
  "title": "Screen Protector Handphone Hugu Murah",
  "banner": "https://s4.bukalapak.com/banners/original/missing.png",
  "products": [
    {
      "deal_info": {},
      "deal_request_state": "can request",
      "price": 28000,
      "courier": [
        "JNE REG",
        "Pos Kilat Khusus"
      ],
      "seller_username": "onriwan",
      "seller_name": "Onriwan Store",
      "seller_id": 1885764,
      "seller_avatar": "https://s4.bukalapak.com/avt/480644/medium/Logo-Instagram%281%29.png",
      "seller_level": "Pedagang Besar",
      "seller_level_badge_url": "https://www.bukalapak.com/images/badge/seller/xhdpi/level-3.png",
      "seller_delivery_time": "21 jam",
      "seller_positive_feedback": 325,
      "seller_negative_feedback": 1,
      "seller_term_condition": "<p><strong>[ PROMO Tempered Glass ]</strong>",
      "seller_alert": null,
      "for_sale": true,
      "state_description": [],
      "premium_account": false,
      "waiting_payment": 0,
      "sold_count": 0,
      "specs": {
        "brand": "Hugu"
      },
      "force_insurance": false,
      "free_shipping_coverage": [],
      "labels": [
        {
          "id": 47982,
          "name": "Aksesoris",
          "slug": "aksesoris",
          "description": null
        }
      ],
      "id": "1nkmca",
      "url": "https://www.bukalapak.com/p/handphone/aksesoris-handphone/screen-guard/1nkmca-jual-lenovo-s850-tempered-glass-my-user",
      "name": "Lenovo S850 - Tempered Glass My User",
      "active": true,
      "city": "Bengkalis",
      "province": "Riau",
      "weight": 30,
      "image_ids": [
        245009548,
        245009773
      ],
      "images": [
        "https://s3.bukalapak.com/img/845900542/large/20160410_111239.jpg",
        "https://s3.bukalapak.com/img/377900542/large/20160410_115741.jpg"
      ],
      "small_images": [
        "https://s3.bukalapak.com/img/845900542/small/20160410_111239.jpg",
        "https://s3.bukalapak.com/img/377900542/small/20160410_115741.jpg"
      ],
      "desc": "* Diharapkan sebelum order menanyakan terlebih dahulu stock dan ketersediaan warna kepada kami.<br/>",
      "condition": "new",
      "stock": 10,
      "favorited": false,
      "created_at": "2016-05-27T15:27:33.000+07:00",
      "product_sin": [],
      "rating": {
        "average_rate": 0,
        "user_count": 0
      },
      "category_id": 181,
      "category": "Screen Guard",
      "category_structure": [
        "Handphone",
        "Aksesoris Handphone",
        "Screen Guard"
      ],
      "interest_count": 0,
      "last_relist_at": "2016-07-29T14:13:57.000+07:00",
      "view_count": 29
    }
  ]
}
```

Get Brand Page information and product list from requested category and brand name.

### HTTP Request

`GET htps://api.bukalapak.com/v2/c/*category_slugs/merk/:brand`

### Parameters

None

# Shipping Fees

## List Shipping Fees

> Sample Request

```shell
curl -u 2:BoqDS9Kkif3EplbHN6ca "https://api.bukalapak.com/v2/shipping_fee.json?courier=TIKI&weight=1000&to=Bima&from=Mataram"
```

> Success Response

```json
{
  "result": [
    {
      "service": "TIKI Reg",
      "harga": 10000
    }
  ],
  "message":null
}
```

> Failure Response
>
> #### No courier supplied

```json
{
  "result": null,
  "message": "Parameter kurir kosong"
}
```

> #### Invalid courier supplied

```json
{
  "result": null,
  "message": "Kurir tidak terdaftar"
}
```

### HTTP Requst

`GET https://api.bukalapak.com/v2/shipping_fee.json`

### Parameters

| Parameter       |          | Description                          |
| --------------- | -------- | ------------------------------------ |
| `courier`       | required | Chosen courier for shipping.         |
| `weight`        | required | Total weight of items to be shipped. |
| `from`          | required | Shipping origin city.                |
| `to`            | required | Shipping destination city.           |
| `from_district` | optional | Shipping origin district.            |
| `to_district`   | optional | Shipping destination district.       |
| `volume`        | optional | Volume of items to be shipped.       |

## Add New Shipping Fee

> Sample Request

```shell
curl -u 2:BoqDS9Kkif3EplbHN6ca "https://api.bukalapak.com/v2/shipping_fee/new/JNE.json" -X POST -d '{"from":"Depok", "to":"Badung", "correction":"30000"}'
```

> Success Response

```json
{
  "status": "OK"
  "message": "Permintaan penambahan ekspedisi pengiriman telah berhasil terkirim dan menunggu persetujuan moderator"
}
```

> Failure Response
>
> #### Not enough parameters supplied

```json
{
  "status": "ERROR",
  "message": "Informasi asal, tujuan, dan biaya kirim wajib diisi!"
}
```

> #### Invalid cities supplied

```json
{
  "status": "ERROR",
  "message": "Kota asal dan tujuan tidak valid"
}
```

> #### Invalid courier supplied

```json
{
  "status": "ERROR",
  "message": "Kurir harus salah satu dari JNE, RPX, atau Wahana (case-sensitive)"
}
```



Requires moderation from admin



### HTTP Request

`POST https://api.bukalapak.com/v2/shipping_fee/new/:courier_name.json`

### Parameters

| Parameter      |          | Description                                                  |
| -------------- | -------- | ------------------------------------------------------------ |
| `courier_name` | required | Chosen courier for shipping. Valid values are only `JNE`, `RPX`, or `Wahana` (case-sensitive). |
| `from`         | required | Shipping origin city.                                        |
| `to`           | required | Shipping destination city.                                   |
| `correction`   | required | Shipping fee.                                                |
| `to_district`  | optional | Shipping destination district.                               |

## Shipping Fee Correction

> Sample Request

```shell
curl -u 2:BoqDS9Kkif3EplbHN6ca "https://api.bukalapak.com/v2/shipping_fee/correction/JNE/330.json" -X PATCH -d '{"price_correction":"30000"}'
```

> Success Response

```json
{
  "status": "OK"
  "message": "Permintaan perubahan tarif pengiriman telah terkirim dan menunggu persetujuan moderator"
}
```

> Failure Response
>
> #### Not enough parameters supplied

```json
{
  "status": "ERROR",
  "message": "Data kurir dan tarif baru harus diisi!"
}
```

> #### Same tariff supplied

```json
{
  "status": "ERROR",
  "message": "Mohon berikan tarif yang berbeda dengan tarif yang sudah ada"
}
```

> #### Similar request existed

```json
{
  "status": "ERROR",
  "message": "Maaf, permintaan serupa sudah diajukan oleh pengguna lain dan sedang menunggu persetujuan."
}
```



Requires moderation from admin



### HTTP Request

`PATCH https://api.bukalapak.com/v2/shipping_fee/correction/:courier_name/:id.json`

### Parameters

| Parameter          |          | Description                                                  |
| ------------------ | -------- | ------------------------------------------------------------ |
| `courier_name`     | required | Chosen courier for shipping. Valid values are only `JNE`, `RPX`, or `Wahana` (case-sensitive). |
| `id`               | required | Shipping fee id.                                             |
| `price_correction` | required | Shipping fee.                                                |

# Subscriptions

## Get Subscription Feeds

> Sample Request

```shell
curl https://api.bukalapak.com/v2/subscriptions.json
```

> Success Response

```json
{
  "status": "OK",
  "message": null,
  "feed_subscriptions": [
    {
      "user": {
        "id": 2,
        "username": "indrasaputra",
        "name": "Indra Saputra",
        "gender": "Laki-laki",
        "avatar": "https://www.bukalapak.com/images/default_avatar/medium/default.jpg",
        "level": "",
        "level_badge_url": "",
        "lapak_name": null,
        "lapak_desc": "lapak hape",
        "lapak_header": "https://www.bukalapak.com/images/header-lapak-default.jpg",
        "last_login": "2015-12-23T21:46:30.000+07:00",
        "joined_at": "2015-08-31T14:53:47.000+07:00",
        "verified_user": true,
        "official": false,
        "store_closed": false,
        "reopen_date": null,
        "close_reason": null,
        "rejection": {
          "rejected": 4,
          "recent_trans": 10
        },
        "feedbacks": {
          "positive": 0,
          "negative": 1
        },
        "address": {
          "province": "DKI Jakarta",
          "city": "Jakarta Selatan"
        }
      },
      "last_activity_at": "2015-12-15T15:48:29.235+07:00",
      "products": [
        {
          "deal_info": {},
          "deal_request_state": "cannot request",
          "price": 5000000,
          "courier": [
            "JNE REG",
            "JNE YES",
            "TIKI Reg",
            "TIKI ONS",
            "Pos Kilat Khusus",
            "RPX Economy Package",
            "RPX Next Day Package",
            "Wahana Tarif Normal"
          ],
          "seller_username": "indrasaputra",
          "seller_name": "Indra Saputra",
          "seller_id": 2,
          "seller_avatar": "https://www.bukalapak.com/images/default_avatar/medium/default.jpg",
          "seller_level": "",
          "seller_level_badge_url": "",
          "seller_positive_feedback": 0,
          "seller_negative_feedback": 1,
          "seller_term_condition": "",
          "seller_alert": null,
          "for_sale": true,
          "state_description": [],
          "last_relist_at": "2015-12-15T15:48:29.000+07:00",
          "specs": {
            "platform": "Sony PS3"
          },
          "force_insurance": false,
          "free_shipping_coverage": [],
          "id": "27",
          "url": "https://www.bukalapak.com/p/hp-elektronik/video-game/consoles/27-jual-barang-bagus-coy",
          "name": "Play Station 3",
          "active": true,
          "city": "Jakarta Selatan",
          "province": "DKI Jakarta",
          "weight": 500,
          "image_ids": [
            114
          ],
          "images": [
            "https://www.bukalapak.com/system4/images/1/1/4/large/1.jpg"
          ],
          "small_images": [
            "https://www.bukalapak.com/system4/images/1/1/4/small/1.jpg"
          ],
          "desc": "barang bagus sekali",
          "condition": "new",
          "nego": false,
          "stock": 95,
          "minimum_negotiable": null,
          "view_count": 17,
          "sold_count": 0,
          "waiting_payment": 11,
          "favorited": false,
          "created_at": "2015-12-15T15:48:29.000+07:00",
          "product_sin": [],
          "category_id": 55,
          "category": "Consoles",
          "category_structure": [
            "HP & Elektronik",
            "Video Game",
            "Consoles"
          ],
          "interest_count": 13
        },
        /* ... */
      ]
    },
    /* ... */
  ]
}
```

Get subscriptions feed owned by current user.

### HTTP Requet

`GET https://api.bukalapak.com/v2/subscriptions.json`

### Parameters

| Parameter  |          | Description                         |
| ---------- | -------- | ----------------------------------- |
| `page`     | optional | Page number, default to `1`.        |
| `per_page` | required | Number of feed to display per page. |
| `keywords` | optional | Seller name                         |

## Get Subscribers

> Sample Request

```shell
curl https://api.bukalapak.com/v2/subscriptions/1/subscribers.json
```

> Success Response

```json
{
  "status": "OK",
  "message": null,
  "subscribers": [
    {
      "user": {
        "id": 3,
        "username": "myunusbahari",
        "name": "M yunus Bahari",
        "gender": null,
        "avatar": "https://www.bukalapak.com/images/default_avatar/medium/default.jpg",
        "level": "",
        "level_badge_url": "",
        "lapak_name": null,
        "lapak_desc": "Lapak laptop",
        "lapak_header": "https://www.bukalapak.com/images/header-lapak-default.jpg",
        "last_login": "2015-12-22T11:55:38.000+07:00",
        "joined_at": "2015-08-31T14:54:48.000+07:00",
        "verified_user": true,
        "official": false,
        "store_closed": false,
        "reopen_date": null,
        "close_reason": null,
        "rejection": {
          "rejected": 1,
          "recent_trans": 1
        },
        "feedbacks": {
          "positive": 0,
          "negative": 0
        },
        "address": {
          "province": "Jawa Timur",
          "city": "Kab. Blitar"
        }
      },
      "subscribed_at": "2015-12-18T10:01:06.000+07:00",
      "total_transaction": 0
    },
    /* ... */
  ]
}
```

Get subscribers from spesific user.

### HTTP Request

`GET https:/api.bukalapak.com/v2/subscriptions/:id/subscribers.json`

### Parameters

| Parameter  |          | Description                               |
| ---------- | -------- | ----------------------------------------- |
| `id`       | required | User ID                                   |
| `page`     | optional | Page number, default to `1`.              |
| `per_page` | required | Number of subscriber to display per page. |
| `keywords` | optional | Subscriber name                           |

## Check Subscribe Status

> Sample Request

```shell
curl https://api.bukalapak.com/v2/subscriptions/1/check.json
```

> Success Response

```json
{
  "status": "OK",
  "message": null,
  "subscribed": false
}
```

Get subscribe status current user to spesific user.

### HTTP Request

`GET ttps://api.bukalapak.com/v2/subscriptions/:id/check.json`

### Parameters

| Parameter |          | Description |
| --------- | -------- | ----------- |
| `id`      | required | User ID     |

## Toggle Subscribe

> Sample Request

```shell
curl https://api.bukalapak.com/v2/subscriptions/toggle_subscribe.json
```

> Success Response

```json
{
  "status": "OK",
  "message": "Berhenti Langganan sukses",
  "subscribed": null
}
```

> Failure Response

```json
{
  "status": "ERROR",
  "message": "Tidak bisa berlangganan akun sendiri",
  "subscribed": null
}
```

Add seller to subscription list

### HTTP Request

`POST https://api.bukalapak.com/v2/subscriptions/toggle_subscribe.json`

### Parameters

| Parameter |          | Description |
| --------- | -------- | ----------- |
| `id`      | required | User ID     |

## Number of Subscribers

> Sample Request

```shell
curl https://api.bukalapak.com/v2/subscriptions/1/number_of_subscribers.json
```

> Success Response

```json
{
  "status": "OK",
  "message": null,
  "amount": 2
}
```

Get number of subscribers spesific user.

### HTTP Request

`GET https://api.bukaapak.com/v2/subscriptions/:id/number_of_subscribers.json`

### Parameters

| Parameter |          | Description |
| --------- | -------- | ----------- |
| `id`      | required | User ID     |

# Supports

## Contact Us Bukalapak

`user_id` and `token` are required if email being used is User email.

> Sample Request

```shell
curl -u 2:dt9bM8rmcgNvNNGffjbk https://api.bukalapak.com/v2/supports/contact_us_to_cs.json -X POST -d'{
  "mail_from_non_user":{
    "name": "Kanzaki Urumi",
    "email": "urumi@gmail.com",
    "title": "Error Fatal",
    "category": "3",
    "ticket_id": "",
    "transaction_id": "",
    "body": "Error ketika transaksi melalui ATM"
    "attachment_1": "http://38.media.tumblr.com/fd5126f38310925e038bcdc8508ea359/tumblr_inline_n19bmr8Xtu1qamhyd.jpg",
    "attachment_2": "",
    "attachment_3": ""
  }
}' -H 'Content-Type: application/json'
```

> Success Response

```json
{
  "status": "OK",
  "message": "Laporan Anda telah dikirim dan sedang diproses. Cek balasan pesan tim Bukalapak di e-mail Anda."
}
```

> Failure Response
>
> #### Lack of required data input

```json
{
  "status": "ERROR",
  "message": "Isikan informasi dengan lengkap!"
}
```

### HTTP Request

`POST https://api.bukalapak.com/v2/supports/contact_us_to_cs.json`

### Parameters

| Parameter        |          | Description                                                  |
| ---------------- | -------- | ------------------------------------------------------------ |
| `name`           | required | Name of the reporter.                                        |
| `email`          | required | Email of the reporter.                                       |
| `title`          | required | Title of the report item.                                    |
| `category`       | required | Category of the report item as Integer (1-6).                |
| `body`           | required | Description of the problem.                                  |
| `ticket_id`      |          | Identifier of the ticket. Required if category is number 2   |
| `transaction_id` | optional | Identifier of the transaction. Related to category number 3  |
| `attachment_1`   | optional | URL/Link picture describes about reported item. The link/url must have valid image format path. |
| `attachment_2`   | optional | URL/Link picture describes about reported item. The link/url must have valid image format path. |
| `attachment_3`   | optional | URL/Link picture describes about reported item. The link/url must have valid image format path. |

Available values for Category:

| Code | Description          |
| ---- | -------------------- |
| `1`  | Transaction.         |
| `2`  | BukaDompet.          |
| `3`  | Error & Feature.     |
| `4`  | Critic & Suggestion. |
| `5`  | Question.            |
| `6`  | Partnership          |

## Report Product

Report Suspected Product to CS



<aside class="warning">Requires authentication</aside>



> Sample Request

```shell
curl -u 15:gFIVsQCcDtrFgUgHXdg1 https://api.bukalapak.com/v2/supports/report_product -X POST -d '{ "id": "cskbm", "bad_description": "1", "bad_category": "1", "lapak_duplicated": "1", "other": "Barang ini berbahaya min"}' -H "Content-Type: application/json"
```

> Success Response

```json
{
    "status":"OK",
    "reasons":
        ["Deskripsi tidak tepat","Penempatan kategori barang tidak sesuai","Barang yang identik sama sudah ada di lapak tersebut","Barang ini berbahaya min"],
    "message":"Laporan telah berhasil dikirim"
}
```

### HTTP Request

`POST https://api.bukalapak.com/v2/supports/report_product.json`

### Parameters

| Parameter          |          | Description                                                  |
| ------------------ | -------- | ------------------------------------------------------------ |
| `id`               | required | Product’s id to report.                                      |
| `bad_description`  | optional | If set to `1`,will report a product with reason `Deskripsi tidak tepat`. |
| `bad_price`        | optional | If set to `1`,will report a product with reason `Harga tidak sesuai`. |
| `bad_title`        | optional | If set to `1`,will report a product with reason `Judul tidak sesuai pada Aturan Penggunaan`. |
| `use_phone_number` | optional | If set to `1`,will report a product with reason `Mencantumkan alamat, nomor kontak, atau ID/PIN/username social media`. |
| `lapak_multi`      | optional | If set to `1`,will report a product with reason `Menjual berbagai barang di satu halaman`. |
| `bad_image`        | optional | If set to `1`,will report a product with reason `Pelanggaran pada foto`. |
| `bad_category`     | optional | If set to `1`,will report a product with reason `Penempatan kategori barang tidak sesuai`. |
| `bad_spec`         | optional | If set to `1`,will report a product with reason `Spesifikasi tidak tepat`. |
| `lapak_duplicated` | optional | If set to `1`,will report a product with reason `Barang yang identik sama sudah ada di lapakmu`. |
| `lapak_illegal`    | optional | If set to `1`,will report a product with reason `Menjual barang yang dilarang oleh BL`. |
| `sold_service`     | optional | If set to `1`,will report a product with reason `Menjual jasa`. |
| `other`            | optional | Contain report product `Lain-lain`.                          |

## Report Product Items

Get list of items that are used to report suspected products.

> Sample Request

```shell
curl https://api.bukalapak.com/v2/supports/report_items.json
```

> Success Response

```json
{
  "status": "OK",
  "report_items": {
    "bad_description": "Deskripsi tidak tepat",
    "use_phone_number": "Mencantumkan alamat, nomor kontak, atau ID/PIN/username social media",
    /* ... */
    "pirated": "Permintaan pemilik merek",
    "irrelevant": "Barang tidak relevan di Bukalapak"
  },
  "message": null
}
```

### HTTP Request

`GET https://api.bukalapak.com/v2/supports/report_items.json`

### Parameters

None

# Transactions

## Transaction Dictionary

- `state` State of a Transaction. Possible values are:

| Name              | Description                                                  |
| ----------------- | ------------------------------------------------------------ |
| `pending`         | initial state                                                |
| `addressed`       | transaction shipping address filled                          |
| `payment_chosen`  | payment method has been chosen                               |
| `confirm_payment` | transaction has been paid by buyer but not verified yet by Bukalapak |
| `paid`            | transaction has been paid and payment has been verified Bukalapak |
| `delivered`       | order has been shipped by seller but not received by buyer yet |
| `received`        | order has been received by buyer                             |
| `remitted`        | transaction has been finished and seller has been paid by Bukalapak |
| `rejected`        | transaction has been rejected by seller                      |
| `cancelled`       | transaction has been canceled                                |
| `expired`         | transaction expired                                          |
| `refunded`        | transaction has been refunded                                |
| `actions`         | Actions that can be performed by current user. Possible values are |
| `deliver`         | Can be performed by seller at [Confirm Shipping for Transaction](https://web.archive.org/web/20170912234943/bukalapak.github.io/api/#confirm-shipping) endpoint |
| `reject`          | Can be performed by seller at [Reject Transaction](https://web.archive.org/web/20170912234943/bukalapak.github.io/api/#reject-transaction) endpoint |

- `unread` Possible values are `true` and `false`. User is required to take action as in `actions` if this field set to `true`.

## Get Transactions List

> Sample Request

```shell
curl -u 2:BoqDS9Kkif3EplbHN6ca "https://api.bukalapak.com/v2/transactions.json?page=2"
```

> Sample Response

```json
{
  "status": "OK",
  "transactions": [
    {
      "id": 10,
      "state": "remitted",
      "updated_at": "2014-08-13T14:49:10.000+07:00",
      "unread": false,
      "quick_trans": false,
      "transaction_id": "140813140010",
      "amount": 10000,
      "quantity": 1,
      "courier": "JNE REG",
      "buyer_notes": "",
      "shipping_fee": 0,
      "shipping_id": 0,
      "shipping_code": "",
      "shipping_history": [],
      "shipping_service": "",
      "shipping_cost": 0,
      "insurance_cost": 0,
      "subtotal_amount": 10000,
      "total_amount": 10000,
      "coded_amount": 10361,
      "uniq_code": 361,
      "payment_method": "atm",
    "feedback": {
      "for_seller":{
        "positive":true,
        "body":"Feedback untuk transaksi 141204101965 untuk pembelian 1 buah Refill Lightening Two Way Cake Light Feel wardah1210.",
        "is_editable":false
      },
      "for_buyer": null
    },
      "products": [
        {
          "id": "9",
          "category": "Laptop",
          "category_id": 59,
          "category_structure": ["Komputer", "Laptop"],
          "name": "kompi",
          "active": true,
          "city": "Bogor",
          "province": "Jawa Barat",
          "price": 10000,
          "weight": "1",
          "courier": ["JNE"],
          "force_insurance": false,
          "image_ids": [9],
          "images": [
            "http://www.bukalapak.com/system/images/9/large/black.jpeg"
          ],
          "small_images": [
            "http://www.bukalapak.com/system/images/9/small/black.jpeg"
          ],
          "url": "http://www.bukalapak.com/p/komputer/laptop/9-jual-kompi",
          "desc": "a",
          "condition": "new",
          "nego": false,
          "seller_username": "ragen",
          "seller_name": "Ragen",
          "seller_id": 1,
          "seller_avatar": "http://www.bukalapak.com/images/default_avatar/medium/default.jpg",
          "seller_level": "BL User",
          "seller_positive_feedback": 5,
          "seller_negative_feedback": 1,
          "payment_ready": false,
          "stock": 0,
          "specs": {
            "brand": "Acer",
            "screen_size": "<12 inches",
            "kapasitas_memory": "",
            "kapasitas_hardisk": ""
          },
          "state_description": ["Stok Habis"],
          "minimum_negotiable": null,
          "for_sale": false,
          "favorited": false,
          "free_shipping_coverage": [],
          "order_quantity": 1,
          "accepted_price": 10000
        }
      ],
      "consignee": {
        "name": "Serge",
        "phone": "13212312",
        "address": "Jl. Mampang",
        "area": "Mampang Prapatan",
        "city": "Jakarta Selatan",
        "province": "DKI Jakarta",
        "post_code": "15116"
      },
      "buyer": {
        "id": 2,
        "name": "Serge",
        "username": "serge",
        "email": "pedorov@gmail.com"
      },
      "seller": {
        "id": 1,
        "name": "Ragen",
        "username": "ragen"
      },
      "actions": [
        "receive"
      ],
      "created_at": "2014-08-13T14:46:02.000+07:00",
      "deliver_before": "2014-08-17T14:49:10.465+07:00",
      "pay_before": "2014-08-14T02:46:07.273+07:00",
      "reject_reason": null,
      "state_changes": {
        "addressed_at": "2014-08-13T14:46:03.002+07:00",
        "payment_chosen_at": "2014-08-13T14:46:07.273+07:00",
        "confirm_payment_at": "2014-08-13T14:49:10.081+07:00",
        "paid_at": "2014-08-13T14:49:10.465+07:00",
        "delivered_at": "2014-08-13T16:56:11.465+07:00",
        "received_at": "2014-08-15T12:51:11.342+07:00",
        "remitted_at": "2014-08-15T12:51:11.342+07:00"
      },
      "has_deal_product": false
    },
    /* ... */
  ],
  "message": null
}
```

Get transactions list owned by current user.

You can optionally set `If-None-Match` header or `Etag` header. If request `Etag` match, server will send `304 Not Modified` response without body. Server will set `Etag` header to every request to this resource.

### HTTP Request

`GET https://api.bukalapak.com/v2/transactions.json` `GET https://api.bukalapak.com/v2/transactions.json?page=2&per_page=10`. `page` and `per_page` provided.

### Parameters

| Parameter       |          | Description                                                  |
| --------------- | -------- | ------------------------------------------------------------ |
| `page`          | optional | Page number, default to `1`.                                 |
| `per_page`      | optional | Number of transactions `per_page`, default to `18`.          |
| `seller`        | optional | If undefined return both transactions as seller and buyer. If value is `1`. return transactions as seller. Else, return transactions as buyer. |
| `keywords`      | optional | Search keywords.                                             |
| `status`        | optional | Returns transaction with states as defined by this parameter. Possible values are `1` to `6`. Value `1` returns transactions with `pending`, `addressed`, `payment_chosen`, or `confirm_payment`state (web counterpart is ‘Menunggu’). Value `2` returns transactions with `paid` state (web counterpart is ‘Dibayar’). Value `3` returns transactions with `delivered` state (web counterpart is ‘Dikirim’). Value `4` returns transactions with `received` state (web counterpart is ‘Diterima’). Value `5` returns transactions with `remitted`, `expired`, `cancelled`, or `rejected` state (web counterpart is ‘Selesai’). Value `6` returns transactions with `refunded` state (web counterpart is ‘Dikembalikan’). Leave it undefined to return all transactions. |
| `actionable`    | optional | Value `1` returns transactions that need action. Any other value returns transactions that doesn’t need action. Leave it undefined to return all transactions. |
| `created_since` | optional | Returns transaction created since the date given in this parameter, e.g.: 2015-07-10. Leave empty to return all transactions (not constrained by time). |

## Get Transaction

> Sample Request

```shell
curl -u 2:BoqDS9Kkif3EplbHN6ca "https://api.bukalapak.com/v2/transactions/5.json"
```

> Success Response

```json
{
  "status": "OK",
  "transaction": {
    "id": 5,
    "state": "delivered",
    "updated_at": "2014-08-13T13:26:58.000+07:00",
    "unread": true,
    "quick_trans": false,
    "transaction_id": "140812170005",
    "amount": 30000,
    "quantity": 1,
    "courier": "JNE REG",
    "buyer_notes": "",
    "shipping_fee": 0,
    "shipping_id": 4,
    "shipping_code": "123123",
    "shipping_service": "JNE REG",
    "shipping_cost": 0,
    "insurance_cost": 0,
    "total_amount": 30000,
    "coded_amount": 30000,
    "uniq_code": 489,
    "payment_method": "deposit",
    "feedback": {
      "for_seller": null,
      "for_buyer": null
    },
    "products": [
      {
        "id": "4",
        "category": "Fullbike",
        "category_id": 83,
        "category_structure": [
          "Sepeda",
          "Fullbike"
        ],
        "name": "Sepeda Laki",
        "active": true,
        "city": "Bogor",
        "province": "Jawa Barat",
        "price": 30000,
        "weight": "1000",
        "courier": ["JNE"],
        "force_insurance": false,
        "image_ids": [4],
        "images": [
          "http://www.bukalapak.com/system/images/4/large/10345757_674146519287652_826860618165918327_n.jpg"
        ],
        "small_images": [
          "http://www.bukalapak.com/system/images/4/small/10345757_674146519287652_826860618165918327_n.jpg"
        ],
        "url": "http://www.bukalapak.com/p/sepeda/fullbike/4-jual-haha",
        "desc": "yey",
        "condition": "new",
        "nego": false,
        "seller_username": "ragen",
        "seller_name": "Ragen",
        "seller_id": 1,
        "seller_avatar": "http://www.bukalapak.com/images/default_avatar/medium/default.jpg",
        "seller_level": "BL User",
        "seller_positive_feedback": 5,
        "seller_negative_feedback": 1,
        "payment_ready": false,
        "stock": 0,
        "specs": {
          "type": "MTB",
          "brand": "Biyanchi",
          "ukuran": "",
          "bahan": ""
        },
        "state_description": ["Stok Habis"],
        "minimum_negotiable": null,
        "for_sale": false,
        "favorited": false,
        "free_shipping_coverage": [],
        "order_quantity": 1,
        "accepted_price": 30000
      }
    ],
    "consignee": {
      "name": "Serge",
      "phone": "9787686768",
      "address": "Jl. Mampang",
      "area": "Mampang Prapatan",
      "city": "Jakarta Selatan",
      "province": "DKI Jakarta",
      "post_code": "15116"
    },
    "buyer": {
      "id": 2,
      "name": "Serge",
      "username": "serge",
      "email": "pedorov@gmail.com"
    },
    "seller": {
      "id": 1,
      "name": "Ragen",
      "username": "ragen"
    },
    "actions": [
      "receive"
    ],
    "created_at": "2014-08-12T17:18:50.000+07:00",
    "deliver_before": "2014-08-17T13:26:24.018+07:00",
    "pay_before": "2014-08-12T17:18:50.882+07:00",
    "reject_reason": null,
    "state_changes": {
      "addressed_at": "2014-08-12T17:18:50.882+07:00",
      "payment_chosen_at": "2014-08-12T17:18:56.268+07:00",
      "confirm_payment_at": "2014-08-13T13:24:47.257+07:00",
      "paid_at": "2014-08-13T13:26:24.018+07:00",
      "delivered_at": "2014-08-13T13:26:58.692+07:00"
    },
    "has_deal_product": false,
    "installment": {
      "term": "6",
      "bank_issuer": "bca"
    }
  },
  "message": null
}
```

> Failure Response
>
> #### Cannot see other users' transactions

```json
{
  "status": "ERROR",
  "transaction": null,
  "message": "Hanya dapat melihat detail transaksi diri sendiri"
}
```

> #### Invalid or unregistered transaction id

```json
{
  "status": "ERROR",
  "transaction": null,
  "message": "Transaksi tidak terdaftar atau tidak valid"
}
```

Get transaction details owned by current user.

You can optionally set `If-None-Match` header or `Etag` header. If request `Etag` match, server will send `304 Not Modified` response without body. Server will set `Etag` header to every request to this resource.

### HTTP Request
`GET https://api.bukalapak.com/v2/transactions/:id.json`

### Parameters

| Parameter |          | Description                            |
| --------- | -------- | -------------------------------------- |
| `id`      | required | Identifier for transaction being read. |

## Confirm Shipping

> Sample Request

```shell
curl -u 2:BoqDS9Kkif3EplbHN6ca -d '{ "payment_shipping": { "transaction_id": "7870", "shipping_code": "1568772840123" } }' https://api.bukalapak.com/v2/transactions/confirm_shipping.json -H "Content-Type: application/json" -X POST
```

> Success Response

```json
{
  "status": "OK",
  "id": "1315",
  "message": "Konfirmasi pengiriman barang berhasil"
}
```

> Failure Response
>
> #### No transaction id supplied

```json
{
  "status": "ERROR",
  "id": null,
  "message": "Harus ada id transaksi"
}
```

> #### No transaction registered with the given id

```json
{
  "status": "ERROR",
  "id": null,
  "message": "Transaksi tidak ditemukan"
}
```

> #### Logged-in user is not the transaction seller

```json
{
  "status": "ERROR",
  "id": null,
  "message": "Hanya dapat dilakukan oleh seller terkait transaksi tersebut"
}
```

> #### Shipping confirmation cannot be done

```json
{
  "status": "ERROR",
  "id": null,
  "message": "Belum ada konfirmasi pembayaran atau konfirmasi pengiriman barang sudah dilakukan"
}
```



<aside class="warning">Requires authentication</aside>



### HTTP Request

`POST https://api.bukalapak.com/v2/transactions/confirm_shipping.json`

### Parameters

None

### POST request data

`payment_shipping` Attributes of transaction shipping confirmation, constructed by following fields:

| Property         |          | Description                                          |
| ---------------- | -------- | ---------------------------------------------------- |
| `transaction_id` | required | Transaction ID                                       |
| `shipping_code`  | required | Shipping receipt code                                |
| `new_courier`    | optional | Used if courier used is other than JNE, TIKI, or POS |

## Confirm Payment

> Sample Request
>
> #### Using registered bank account

```shell
curl -u 2:BoqDS9Kkif3EplbHN6ca https://api.bukalapak.com/v2/transactions/confirm_payment.json -H "Content-Type: application/json" -X POST -d '{
  "destination": "Bank BCA - 731 025 2527",
  "bank_account_id": "7",
  "transaction_id": "30"
}'
```

> #### Using unregistered bank account

```shell
curl -u 2:BoqDS9Kkif3EplbHN6ca https://api.bukalapak.com/v2/transactions/confirm_payment.json -H "Content-Type: application/json" -X POST -d '{
  "destination": "Bank BCA - 731 025 2527",
  "transaction_id": "30",
  "bank_account_attributes": {
    "bank": "Bank Mandiri",
    "number": "123456789",
    "name": "Serge Nikolai"
  }
}'
```

> #### Using cash transfer

```shell
curl -u 2:BoqDS9Kkif3EplbHN6ca https://api.bukalapak.com/v2/transactions/confirm_payment.json -H "Content-Type: application/json" -X POST -d '{
  "destination": "Bank BCA - 731 025 2527",
  "bank_account_id": "tt",
  "transaction_id": "30",
  "bank_account_attributes": {
    "bank": "Bank Mandiri",
    "name": "Serge Nikolai"
  }
}'
```

> Success Response

```json
{
  "status": "OK",
  "id": 30,
  "message": "Konfirmasi berhasil. Admin kami akan melakukan verifikasi pembayaran Anda."
}
```

> Failure Response
>
> #### No transaction id supplied

```json
{
  "status": "ERROR",
  "id": null,
  "message": "Harus ada id transaksi"
}
```

> #### No transaction registered with the given id

```json
{
  "status": "ERROR",
  "id": null,
  "message": "Transaksi tidak ditemukan"
}
```

> #### Logged-in user is not the transaction buyer

```json
{
  "status": "ERROR",
  "id": null,
  "message": "Hanya dapat dilakukan oleh buyer terkait transaksi tersebut"
}
```

> #### Improper bank account attributes supplied in cash transfer

```json
{
  "status": "ERROR",
  "id": null,
  "message": "Transfer tunai harus mengisi nama rekening dan bank"
}
```

> #### Payment has been confirmed or invalid data supplied

```json
{
  "status": "ERROR",
  "id": null,
  "message": "Harap mengisi sesuai dengan ketentuan"
}
```

### HTTP Request

`POST https://api.bukalapak.com/v2/transactions/confirm_payment.json`

### Parameters

None

### POST request data

| Property                  |          | Description                                                  |
| ------------------------- | -------- | ------------------------------------------------------------ |
| `destination`             | required | Bukalapak’s chosen bank account.                             |
| `transaction_id`          | required | Transaction ID.                                              |
| `bank_account_id`         | optional | ID of buyer’s registered bank account used in payment. Use `tt` value to indicate cash transfer. Not required if using another bank account that hasn’t been registered. |
| `bank_account_attributes` | optional | Required if payment is using cash transfer or unregistered bank account. |

`bank_account_attributes` is constructed by the following fields:

| Property |          | Description                                                  |
| -------- | -------- | ------------------------------------------------------------ |
| `bank`   | required | Name of the bank used to pay.                                |
| `name`   | required | Name of the owner of the account used to pay.                |
| `number` | optional | Required if using bank transfer. Empty if using cash transfer. |

## Confirm Arrival

> Sample Request

```shell
  curl -u 2:BoqDS9Kkif3EplbHN6ca http://api.bukalapak.com/v2/transactions/5/confirm_arrival.json -H "Content-Type: application/json" -X POST -d'{
    "positive": "1",
    "body": "Recommended seller nih (y)",
    "retur":"0"
  }'
  curl -u 2:BoqDS9Kkif3EplbHN6ca http://api.bukalapak.com/v2/transactions/5/confirm_arrival.json -H "Content-Type: application/json" -X POST -d'{
    "positive": "0",
    "body": "barang rusak",
    "complain":"1"
  }'
```

> Success Response

```json
{
  "status": "OK",
  "message": "Konfirmasi penerimaan barang berhasil"
}
```

> Failure Response
>
> #### No transaction registered with the given id

```json
{
  "status": "ERROR",
  "message": "Transaksi tidak ditemukan"
}
```

> #### Logged-in user is not the transaction buyer

```json
{
  "status": "ERROR",
  "message": "Hanya dapat dilakukan oleh buyer terkait transaksi tersebut"
}
```

> #### No feedback supplied

```json
{
  "status": "ERROR",
  "message": "Feedback tidak boleh kosong"
}
```

> #### Arrival confirmation has been done before

```json
{
  "status": "ERROR",
  "message": "Konfirmasi penerimaan barang sudah pernah dilakukan"
}
```

### HTTP Request

`POST https://api.bukalapak.com/v2/transactions/:id/confirm_arrival.json`

### Parameters

| Parameter |          | Description                                          |
| --------- | -------- | ---------------------------------------------------- |
| `id`      | required | ID of the transaction which arrival to be confirmed. |

### POST request data

| Property   |          | Description                                                  |
| ---------- | -------- | ------------------------------------------------------------ |
| `positive` | required | Indicating buyer’s satisfaction toward seller of current transaction. Fill with `1` for denoting satisfactory, otherwise denoting unsatisfactory. |
| `body`     | required | Text containing feedback for current transaction             |
| `retur`    | optional | Indicating whether buyer wants to return bought items or not. Fill with `1` for retur, empty or use other values for no retur. |
| `complain` | optional | Indicating whether buyer wants to complain about bought items or not. Fill with `1` for complain, empty or use other values for no complain, after this you must call api for complain_product. |

## Complain Product

> Sample Request

```
  curl -u 2:BoqDS9Kkif3EplbHN6ca http://api.bukalapak.com/v2/transactions/5/complain_product.json -X POST
  "Content-Type: multipart/form-data" -F "retur=1" -F "attachment=@file-image.png" -F "payment_return[return_reason]=Barang rusak/cacat/pecah" -F "payment_return[return_type]=refund"
```

> Success Response

```json
{
  "status": "OK",
  "transaction": {
    "id": 367,
    "state": "received",
    "updated_at": "2016-11-29T16:41:33.000+07:00",
    "unread": true,
    "quick_trans": false,
    "transaction_id": "160000000367",
    "amount": 80000,
    "quantity": 1,
    "courier": "JNE REG",
    "same_day_service_info": null,
    "buyer_notes": null,
    "shipping_fee": 19000,
    "shipping_id": 24,
    "shipping_code": "1234567890",
    "shipping_history": [],
    "shipping_service": "tes",
    "insurance_cost": 0,
    "subtotal_amount": 99000,
    "total_amount": 99000,
    "coded_amount": 99000,
    "uniq_code": null,
    "use_seller_voucher": false,
    "use_voucher": false,
    "voucher_amount": 0,
    "promo_payment_amount": 0,
    "payment_method": "deposit",
    "payment_method_name": "BukaDompet",
    "payment_amount": 99000,
    "remit_amount": 99000,
    "service_fee": 0,
    "feedback": {
      "for_seller": {
        "id": 201,
        "transaction_id": 367,
        "transaction_no": "160000000367",
        "sender_id": 5,
        "sender_name": "buyer",
        "sender_type": "User",
        "user_id": 4,
        "user_name": "BL tes",
        "body": "barang rusak",
        "positive": false,
        "created_at": "2016-11-29T15:54:10.000+07:00",
        "updated_at": "2016-11-29T16:41:32.000+07:00",
        "replies": null,
        "is_editable": true
      },
      "for_buyer": null
    },
    "products": [
      {
        "deal_info": {},
        "deal_request_state": "can request",
        "price": 80000,
        "courier": [
          "JNE REG",
          "JNE YES",
          "TIKI Reg",
          "TIKI ONS"
        ],
        "seller_username": "adminbl",
        "seller_name": "BL tes",
        "seller_id": 4,
        "seller_avatar": "http://www.local.host:5000/images/default_avatar/medium/default.jpg",
        "seller_level": "BL User",
        "seller_level_badge_url": "http://www.local.host:5000/images/badge/seller/xhdpi/level-1.png",
        "seller_delivery_time": "< 1 jam",
        "seller_positive_feedback": 6,
        "seller_negative_feedback": 19,
        "seller_term_condition": "",
        "seller_alert": null,
        "for_sale": true,
        "state_description": [],
        "premium_account": true,
        "last_order_schedule": null,
        "waiting_payment": -1,
        "sold_count": 0,
        "specs": {},
        "force_insurance": null,
        "free_shipping_coverage": [],
        "id": "aqt",
        "url": "http://www.local.host:5000/p/baby-stuff/lain-lain/aqt-jual-sillybandz-radringz-rockstar-7-8",
        "name": "Sillybandz RadRingz RockStar-7-8",
        "active": true,
        "city": "Jakarta Selatan",
        "province": "DKI Jakarta",
        "weight": 400,
        "image_ids": [
          24015
        ],
        "images": [
          "http://www.local.host:5000/system4/images/51042/large/2015-04-23T16:07:10%2B07:00.jpg"
        ],
        "small_images": [
          "http://www.local.host:5000/system4/images/51042/small/2015-04-23T16:07:10%2B07:00.jpg"
        ],
        "desc": "Tidak ada deskripsi",
        "condition": "new",
        "stock": 1,
        "favorited": false,
        "created_at": "2015-04-23T16:07:10.000+07:00",
        "product_sin": [],
        "rating": {
          "average_rate": 0,
          "user_count": 0
        },
        "category_id": 231,
        "category": "Lain-lain",
        "category_structure": [
          "Baby Stuff",
          "Lain-lain"
        ],
        "interest_count": 1,
        "last_relist_at": "2015-04-23T16:07:10.000+07:00",
        "view_count": 0,
        "order_quantity": 1,
        "accepted_price": 80000
      }
    ],
    "pickup_time": null,
    "installment": {
      "term": null,
      "bank_issuer": null
    },
    "consignee": {
      "name": "tes",
      "phone": "08124356789",
      "address": "tes teasaas fdsfa 123",
      "area": "Benowo",
      "city": "Surabaya",
      "province": "Jawa Timur",
      "post_code": "60192"
    },
    "buyer": {
      "id": 5,
      "name": "buyer",
      "username": "buyer",
      "email": "buyer@bl.com"
    },
    "seller": {
      "id": 4,
      "name": "BL tes",
      "username": "adminbl"
    },
    "invoice": {
      "id": 34,
      "invoice_id": "BL161111111ZINV",
      "state": "paid"
    },
    "voucher": null,
    "actions": [
      "edit_feedback"
    ],
    "created_at": "2016-11-29T15:51:32.000+07:00",
    "deliver_before": "2016-12-01T15:51:34.000+07:00",
    "pay_before": "2016-11-29T16:11:32.000+07:00",
    "reject_reason": null,
    "return_reason": [
      "Barang rusak/cacat/pecah"
    ],
    "state_changes": {
      "addressed_at": "2016-11-29T15:51:33.811+07:00",
      "payment_chosen_at": "2016-11-29T15:51:34.071+07:00",
      "paid_at": "2016-11-29T15:51:34.234+07:00",
      "delivered_at": "2016-11-29T15:53:06.325+07:00",
      "received_at": "2016-11-29T15:54:10.709+07:00"
    },
    "has_deal_product": false,
    "return_info": {
      "id": 7,
      "receiver": "",
      "phone": "",
      "address": "",
      "shipping_code": null
    },
    "total_weight": 400,
    "need_action": true,
    "virtual": false,
    "phone_credit": null
  },
  "discussion": {
    "id": 11,
    "transaction_id": 367,
    "return_id": 7,
    "admin_notes": null,
    "closed": null,
    "closed_by": null,
    "comments": [],
    "attachments": [
      {
        "uploader_id": 5,
        "uploader_type": "User",
        "image_url": "http://www.local.host:5000/system4/discussion_attachment/2/transaction_discussion_160000000367_20161129164133.png",
        "created_at": "2016-11-29T16:41:33.000+07:00"
      }
    ],
    "shipping_id": null,
    "shipping_code": "",
    "shipping_service": "",
    "shipping_destination": "",
    "shipping_status": ""
  },
  "message": "Diskusi komplain pesanan berhasil dibuka"
}
```

### HTTP Request

`POST https://api.bukalapak.com/v2/transactions/:id/complain_product.json`

### Parameters

| Parameter |          | Description                                          |
| --------- | -------- | ---------------------------------------------------- |
| `id`      | required | ID of the transaction which arrival to be confirmed. |

### POST request data

| Property                      |          | Description                                                  |
| ----------------------------- | -------- | ------------------------------------------------------------ |
| `retur`                       | required | Indicating whether buyer wants to return bought items or not. Fill with `1` for retur, empty or use other values for no retur. |
| `attachment`                  | required | Upload of product that want to be returned from buyer here as proof |
| `payment_return[reason]`      | required | choose reason why buyer want to return the product           |
| `payment_return[return_type]` | required | choose how buyer want to compensated                         |

## Confirm Shipping Retur

> Sample Request

```shell
curl -u 2:BoqDS9Kkif3EplbHN6ca -d '{ "payment_shipping": { "return_id": "7870", "shipping_code": "1568772840123" } }' https://api.bukalapak.com/v2/transactions/confirm_shipping.json -H "Content-Type: application/json" -X POST
```

> Success Response

```json
{
  "status": "OK",
  "id": 25,
  "message": "Data pengiriman retur berhasil disimpan"
}
```

> Failure Response
>
> #### No transaction registered with the given id

```json
{
  "status": "ERROR",
  "id": null,
  "message": "Transaksi retur tidak ditemukan"
}
```

> #### Shipping confirmation cannot be done

```json
{
  "status": "ERROR",
  "id": null,
  "message": "Kode atau Kurir salah"
}
```



<aside class="warning">Requires authentication</aside>



### HTTP Request

`POST https://api.bukalapak.com/v2/transactions/confirm_shipping.json`

### Parameters

None

### POST request data

`payment_shipping` Attributes of transaction shipping confirmation, constructed by following fields:

| Property        |          | Description                                          |
| --------------- | -------- | ---------------------------------------------------- |
| `return_id`     | required | Return ID                                            |
| `shipping_code` | required | Shipping receipt code                                |
| `new_courier`   | optional | Used if courier used is other than JNE, TIKI, or POS |

## Reject Transaction

> Sample Request

```shell
curl -u 66:tok3ntok3n -X PATCH "https://api.bukalapak.com/v2/transactions/reject.json" --data "id=51943&reason=Stok Habis"
```

> Success Response

```json
{
  "status": "OK",
  "message": "Transaksi telah ditolak"
}
```

> Failure Response
>
> #### No transaction registered with the given id

```json
{
  "status": "ERROR",
  "message": "Transaksi tidak ditemukan"
}
```

> #### Using other reason than allowed ones

```json
{
  "status": "ERROR",
  "message": "Alasan tidak valid"
}
```

> #### Logged-in user is not the transaction seller

```json
{
  "status": "ERROR",
  "message": "Hanya dapat dilakukan oleh seller terkait transaksi tersebut"
}
```

> #### Other failures

```json
{
  "status": "ERROR",
  "message": "Gagal menolak"
}
```



<aside class="warning">Requires authentication</aside>



### HTTP Request

`PATCH https://api.bukalapak.com/v2/transactions/reject.json`

### Parameters

None

### PATCH request data

| Property |          | Description                                                  |
| -------- | -------- | ------------------------------------------------------------ |
| `id`     | required | Transaction ID.                                              |
| `reason` | required | Reason for rejecting transaction. Allowed values (case sensitive):`Stok Habis``Harga barang/biaya kirim tidak sesuai``Ada kesibukan lain yang sifatnya mendadak``Permintaan pembeli tidak dapat dilayani` |

## Update Shipping Info

> Sample Request

```shell
curl -u 66:tok3ntok3n -X PATCH "https://api.bukalapak.com/v2/transactions/shipping/13388/edit.json" --data "shipping_code=HOHOHO00000111123&delivery_service=JNE REG"
```

> Success Response

```json
{
  "status": "OK",
  "message": "Pengiriman berhasil diperbarui"
}
```

> Failure Response
>
> #### Invalid shipping code

```json
{
  "status": "ERROR",
  "message": "Kode pengiriman tidak valid"
}
```

> #### No shipping record found with given code

```json
{
  "status": "ERROR",
  "message": "Pengiriman tidak ditemukan"
}
```



<aside class="warning">Requires authentication</aside>



### HTTP Request

`PATCH https://api.bukalapak.com/v2/transactions/shipping/:id/edit.json`

### Parameters

None

### PATCH request data

| Property           |          | Description                            |
| ------------------ | -------- | -------------------------------------- |
| `id`               | required | Shipping ID.                           |
| `shipping_code`    | optional | New code for the shipping.             |
| `delivery_service` | optional | New delivery service for the shipping. |

## Send/Edit Feedback

> Sample Request

```shell
curl -u 2:BoqDS9Kkif3EplbHN6ca -d '{ "feedback": { "body": "Puas dengan pembeli ini. Tidak rewel dan fast response.", "positive": "true"  } }' https://api.bukalapak.com/v2/transactions/7907/feedbacks.json -H "Content-Type: application/json" -X POST
```

> Success Response

```json
{
  "status": "OK",
  "message": null,
  "feedback": {
    "id": 22033,
    "transaction_id": 7907,
    "sender_id": 62817,
    "sender_name": "Sayur Kangkung",
    "sender_type": "User",
    "user_id": 31432,
    "user_name": "Khairul",
    "body": "Puas dengan pembeli ini. Tidak rewel dan fast response.",
    "positive": true,
    "created_at":"2012-10-11T17:55:34+07:00",
    "updated_at":"2012-10-11T17:55:34+07:00"
  }
}
```

> Failure Response
>
> #### Invalid data request

```json
{
  "status": "ERROR",
  "message": "Data feedback tidak valid",
  "feedback": null
}
```

> #### Logged-in user is not the transaction seller/buyer

```json
{
  "status": "ERROR",
  "message": "Tidak dapat memberikan feedback",
  "feedback": null
}
```

> #### Transaction not found

```json
{
  "status": "ERROR",
  "message": "Transaksi tidak terdaftar",
  "feedback": null
}
```

Sends or edits feedback of a Transaction. Seller or buyer can use this method.



<aside class="warning">Requires authentication</aside>



### HTTP Request

`POST https://api.bukalapak.com/v2/transactions/:id/feedbacks.json`

### Parameters

None

### POST request data

`feedback` Attributes of feedback, constructed by following fields:

| Property   |          | Description                                                  |
| ---------- | -------- | ------------------------------------------------------------ |
| `body`     | required | Text containing feedback for current transaction             |
| `positive` | required | Boolean value indicating seller’s satisfaction toward buyer of current transaction. Possible values are `true` or `false` |

## Get Product Reviews from Transaction

> Sample Request

```shell
curl -u 67287:lXymG93y83m6RHzZV5FY
"https://api.bukalapak.com/v2/transactions/20917524/product_reviews.json"
```

> Success Response

```json
{
  "status": "OK",
  "message": null,
  "reviews": [
    {
      "id": 29,
      "sender_id": 2,
      "sender_name": "George",
      "sender_type": "QuickBuyer",
      "rate": 5,
      "body": "I love this stuff",
      "updated_at": "2016-02-02T17:23:22.000+07:00",
      "product": {
        "deal_info": {},
        "deal_request_state": "cannot request",
        "price": 450000,
        "id": "ntml",
        "# AND ALL OTHER PRODUCT ATTRIBUTES": ""
        }
    },
    {
      "id": null,
      "sender_id": 2,
      "sender_name": null,
      "sender_type": "User",
      "rate": null,
      "body": null,
      "updated_at": null,
      "product": {
        "deal_info": {},
        "deal_request_state": "cannot request",
        "price": 450000,
        "id": "kxzv",
        "# AND ALL OTHER PRODUCT ATTRIBUTES": ""
        }
    }
  ]
}
```

Get list of product review for each products in a transaction. Note that when object in ‘reviews’ have a null value in ‘id’ attribute means that the review has not been created yet.



<aside class="warning">Requires authentication</aside>



### HTTP Request

`GET https://ai.bukalapak.com/v2/transactions/:id/product_reviews.json`

### Parameters

| Parameter |          | Description            |
| --------- | -------- | ---------------------- |
| `id`      | required | ID of the transaction. |

## Get Return Transaction Discussion

> Sample Request

```shell
curl -u 204253:lXymG93y83m6RHzZV5FY https://api.bukalapak.com/v2/transactions/21/return/discussion.json
curl -u 204253:lXymG93y83m6RHzZV5FY https://api.bukalapak.com/v2/transactions/return_discussion/11.json
```

> Success Response

```json
{
  "status": "OK",
  "discussion": {
    "id": 1,
    "transaction_id": 21,
    "admin_notes": null,
    "closed": null,
    "closed_by": null,
    "comments": [
      {
        "sender_id": 4,
        "admin_id": null,
        "sender_type": "User",
        "body": "Kembalikan!",
        "created_at": "2015-02-02T11:23:29.000+07:00"
      },
      {
        "sender_id": 2,
        "admin_id": null,
        "sender_type": "User",
        "body": "OK gan sabar ya",
        "created_at": "2015-02-02T11:26:39.000+07:00"
      }
    ],
    "attachments": [
      {
        "uploader_id": 4,
        "uploader_type": "User",
        "image_url": "/system/discussion_attachments/5/original/374466_4948720042017_1287462475_n.png",
        "created_at": "2015-02-02T13:57:14.000+07:00"
      }
    ]
  },
  "message": null
}
```

> Failure Response
>
> #### User is not authorized to do the action

```json
{
  "status": "ERROR",
  "discussion": null,
  "message": "Hanya dapat melihat diskusi transaksi diri sendiri"
}
```

> #### Transaction not found

```json
{
  "status": "ERROR",
  "discussion": null,
  "message": "Transaksi tidak ditemukan"
}
```

### HTTP Request

`GET https://apibukalapak.com/v2/transactions/:id/return/discussion.json`

### Parameters

| Parameter  |          | Description                     |
| ---------- | -------- | ------------------------------- |
| `id`       | required | ID of the returned transaction. |
| `page`     | optional | Page number to be shown.        |
| `per_page` | optional | Discussion counts per page.     |

### HTTP Request

`GET https://api.bukalapak.om/v2/transactions/return_discussion/:discussion_id.json`

### Parameters

| Parameter       |          | Description                 |
| --------------- | -------- | --------------------------- |
| `discussion_id` | required | ID of the return discussion |
| `page`          | optional | Page number to be shown.    |
| `per_page`      | optional | Discussion counts per page. |

## Confirm Arrival Return Transaction Discussion

> Sample Request

```shell
curl -u 204253:lXymG93y83m6RHzZV5FY https://api.bukalapak.com/v2/transactions/83/return/confirm_arrival.json
```

> Success Response

```json
{
  "status": "OK",
  "message": null
}
```

> Failure Response
>
> #### Confirm arrival service error

```json
{
  "status": "ERROR",
  "message": "Gagal konfirmasi penerimaan barang"
}
```

> #### User cannot confirm arrival

```json
{
  "status": "ERROR",
  "message": "Anda tidak dapat melakukan konfirmasi barang"
}
```

> #### Return transaction not approved by Admin

```json
{
  "status": "ERROR",
  "message": "Permohonan pengembalian untuk transaksi ini belum disetujui oleh Admin"
}
```

> #### Transaction not found

```json
{
  "status": "ERROR",
  "message": "Transaksi tidak ditemukan"
}
```

### HTTP Request

`POST https://api.bukalapak.com/v2/transactions/:id/return/confirm_arrival.json`

### Parameters

| Parameter |          | Description                     |
| --------- | -------- | ------------------------------- |
| `id`      | required | ID of the returned transaction. |

## Call Admin To Return Transaction Discussion

> Sample Request

```shell
curl -u 204253:lXymG93y83m6RHzZV5FY https://api.bukalapak.com/v2/transactions/21/return/call_admin.json
```

> Success Response

```json
{
  "status": "OK",
  "message": null
}
```

> Failure Response
>
> #### User is not authorized to do the action

```json
{
  "status": "ERROR",
  "message": "Hanya dapat melihat diskusi transaksi diri sendiri"
}
```

> #### Transaction not found

```json
{
  "status": "ERROR",
  "message": "Transaksi tidak ditemukan"
}
```

> #### Return Discussion has called Admin

```json
{
  "status": "ERROR",
  "message": "Memanggil Admin telah dilakukan sebelumnya"
}
```

> #### Failuer call Admin

```json
{
  "status": "ERROR",
  "message": "Gagal memanggil Admin"
}
```

### HTTP Request

`POST https://api.bukalapak.com/v2/transactions/:id/return/call_admin.json`

### Parameters

| Parameter |          | Description                                   |
| --------- | -------- | --------------------------------------------- |
| `id`      | required | ID of the returned transaction.               |
| `reason`  | required | reason for call admin to returned discussion. |

## Close Discussion in Return Transaction Discussion

> Sample Request

```shell
curl -u 204253:lXymG93y83m6RHzZV5FY https://api.bukalapak.com/v2/transactions/21/return/close_discussion.json
```

> Success Response

```json
{
  "status": "OK",
  "message": null
}
```

> Failure Response
>
> #### User is not authorized to do the action

```json
{
  "status": "ERROR",
  "message": "Hanya buyer yang dapat menutup diskusi transaksi"
}
```

> #### Transaction not found

```json
{
  "status": "ERROR",
  "message": "Transaksi tidak ditemukan"
}
```

> #### Failuer close discussion

```json
{
  "status": "ERROR",
  "message": "Gagal menutup diskusi"
}
```

### HTTP Request

`POST https://api.bukalapak.com/v2/transactions/:id/return/close_discussion.json`

### Parameters

| Parameter |          | Description                                         |
| --------- | -------- | --------------------------------------------------- |
| `id`      | required | ID of the returned transaction.                     |
| `reason`  | required | reason for close discussion in returned discussion. |

## Add Discussion to Return Page

> Sample Request

```shell
curl -u 204253:lXymG93y83m6RHzZV5FY https://api.bukalapak.com/v2/transactions/21/return/comment_discussion.json?comment_body="tolong ditukar" -F attachment="attachment.png" -X POST
```

> Success Response

```json
{
  "status": "OK",
  "message": "Diskusi berhasil disimpan"
}
```

> Failure Response
>
> #### User is not authorized to do the action

```json
{
  "status": "ERROR",
  "message": "Pengguna tidak diizinkan melakukan ini"
}
```

> #### Missing parameter

```json
{
  "status": "ERROR",
  "message": "Parameter tidak lengkap"
}
```

> #### Transaction not found

```json
{
  "status": "ERROR",
  "message": "Transaksi tidak ditemukan"
}
```

### HTTP Request

`POST https://api.bukalapak.com/v2/transactions/:id/return/comment_discussion.json`

### Parameters

| Parameter |          | Description                     |
| --------- | -------- | ------------------------------- |
| `id`      | required | ID of the returned transaction. |

### POST request data

| Property       |          | Description                                        |
| -------------- | -------- | -------------------------------------------------- |
| `comment_body` | required | The comment to be posted.                          |
| `attachment`   | optional | Attachment for the comment. It has to be an image. |

## Add Return Address Info

> Sample Request

```shell
curl -u 204253:lXymG93y83m6RHzZV5FY https://api.bukalapak.com/v2/transactions/21/return/return_info.json?receiver=Sayur&phone=088800008888&return_address=Here -X PATCH
```

> Success Response

```json
{
  "status": "OK",
  "message": "Alamat retur berhasil diisi"
}
```

> Failure Response
>
> #### User is not authorized to do the action

```json
{
  "status": "ERROR",
  "message": "Pengguna tidak diizinkan melakukan ini"
}
```

> #### Missing parameter

```json
{
  "status": "ERROR",
  "message": "Parameter tidak lengkap"
}
```

> #### Transaction not found

```json
{
  "status": "ERROR",
  "message": "Transaksi tidak ditemukan"
}
```

### HTTP Request

`PATCH https://api.bukalapak.com/v2/transactions/:id/return/return_info.json`

### Parameters

| Parameter |          | Description                     |
| --------- | -------- | ------------------------------- |
| `id`      | required | ID of the returned transaction. |

### PATCH request data

| Property         |          | Description                     |
| ---------------- | -------- | ------------------------------- |
| `receiver`       | required | Seller’s address receiver name. |
| `phone`          | required | Receiver’s phone number.        |
| `return_address` | required | Receiver’s return address.      |

## Edit Return Address Info

> Sample Request

```shell
curl -u 204253:lXymG93y83m6RHzZV5FY https://api.bukalapak.com/v2/transactions/21/return/edit_return_info.json?receiver=Sayur&phone=088800008888&return_address=Here -X PATCH
```

> Success Response

```json
{
  "status": "OK",
  "message": "Alamat retur berhasil diubah"
}
```

> Failure Response
>
> #### User is not authorized to do the action

```json
{
  "status": "ERROR",
  "message": "Anda tidak dapat mengubah alamat pengembalian barang"
}
```

> #### Transaction is not found

```json
{
  "status": "ERROR",
  "message": "Transaksi tidak ditemukan"
}
```

> #### Discussion is not found

```json
{
  "status": "ERROR",
  "message": "Diskusi pengembalian barang Anda tidak ditemukan"
}
```

> #### Discussion is closed

```json
{
  "status": "ERROR",
  "message": "Diskusi pengembalian barang Anda telah ditutup"
}
```

> #### User in this discussion is not authorized

```json
{
  "status": "ERROR",
  "message": "Hanya dapat melihat diskusi transaksi diri sendiri"
}
```

> #### State return is state in after delivered

```json
{
  "status": "ERROR",
  "message": "Status pengembalian barang Anda sudah bukan delivered"
}
```

> #### Missing parameter

```json
{
  "status": "ERROR",
  "message": "Parameter tidak lengkap"
}
```

### HTTP Request

`PATCH https://api.bukalapak.com/v2/transactions/:id/return/edit_return_info.json`

### Parameters

| Parameter |          | Description                     |
| --------- | -------- | ------------------------------- |
| `id`      | required | ID of the returned transaction. |

### PATCH request data

| Property         |          | Description                     |
| ---------------- | -------- | ------------------------------- |
| `receiver`       | required | Seller’s address receiver name. |
| `phone`          | required | Receiver’s phone number.        |
| `return_address` | required | Receiver’s return address.      |

## Get Return Address Info

> Sample Request

```shell
curl -u 204253:lXymG93y83m6RHzZV5FY https://api.bukalapak.com/v2/transactions/21/return/return_info.json
```

> Success Response

```json
{
  "status": "OK",
  "message": "Alamat berhasil didapatkan",
  "receiver": "Sayur Kangkung",
  "phone": "088822221111",
  "return_address": "Bukalapak, Jakarta"
}
```

> Failure Response
>
> #### User is not authorized to do the action

```json
{
  "status": "ERROR",
  "message": "Pengguna tidak diizinkan melakukan ini",
  "receiver": null,
  "phone": null,
  "return_address": null
}
```

> #### Transaction not found

```json
{
  "status": "ERROR",
  "message": "Transaksi tidak ditemukan"
  "receiver": null,
  "phone": null,
  "return_address": null
}
```

### HTTP Request

`GET https://api.ukalapak.com/v2/transactions/:id/return/return_info.json`

### Parameters

| Parameter |          | Description                     |
| --------- | -------- | ------------------------------- |
| `id`      | required | ID of the returned transaction. |

## Pay With Credit Card

> Sample Request

```shell
curl -u 204253:lXymG93y83m6RHzZV5FY -d '{ "token" : "451111-1117-11bfc1cb-c6bd-44ad-acb0-741424eb73f0", "cc_name" : "Billy", "cc_billing_address": "Jl. Kemang Timur no 22", "cc_billing_city": "Jakarta", "cc_billing_post_code": "13770", "cc_bank_issuer": "bni", "cc_installment_term": "12" }' https://api.bukalapak.com/v2/transactions/21/pay_credit_card.json -X POST
```

> Success Response

```json
{
  "status": "OK",
  "status_code": 200,
  "message": "Transaksi berhasil dibayar."
}
```

> Success Response on Confimation

```json
{
  "status": "OK",
  "status_code": 201,
  "message": "Transaksi masih dalam konfirmasi."
}
```

Pay with credit card, you must specify the token in exchange of card information

### HTTP Request

`POST https://api.bukalapak.com/v2/transactions/21/pay_credit_card.json`

### Parameters

| Parameter              |          | Description                          |
| ---------------------- | -------- | ------------------------------------ |
| `token`                | required | Token in exchange of card informatio |
| `cc_name`              | optional | Name on Credit Card                  |
| `cc_billing_address`   | optional | Billing addreee                      |
| `cc_billing_city`      | optional | Billing City                         |
| `cc_billing_post_code` | optional | Billing Post Code                    |
| `cc_bank_issuer`       | optional | Bank Issuer of Installment           |
| `cc_installment_term`  | optional | Term of Installment                  |

## Payment Limit & Fee

fetch limit and fee for each payment in bukalapak

> Sample Request

```shell
curl -X GET "https://api.bukalapak.com/v2/transactions/payment_limit_and_fee.json"
```

> Success Response

```json
{
  "status": "OK",
  "cimb_clicks_service_fee": 5000,
  "cimb_clicks_min_trx": 10000,
  "cimb_clicks_max_trx": 5000000,
  "bca_klikpay_service_fee": 5000,
  "bca_klikpay_service_fee_percentage": 2,
  "bca_klikpay_min_trx": 10000,
  "bca_klikpay_max_trx": 100000000,
  "mandiri_ecash_service_fee_percentage": 1,
  "mandiri_ecash_reg_max_trx": 5000000,
  "mandiri_ecash_unreg_max_trx": 1000000,
  "mandiri_ecash_sms_fee": 550,
  "mandiri_clickpay_service_fee": 5000,
  "credit_card_veritrans_service_fee_percentage": "2.3",
  "credit_card_veritrans_service_transaction_fee": 2200,
  "credit_card_veritrans_min_trx": 10000,
  "credit_card_sprintasia_service_fee_percentage": "99.0",
  "idmart_max_trx": 5000000,
  "idmart_cashier_fee": 7500
}
```

### HTTP Request

`GET https://apibukalapak.com/v2/transactions/payment_limit_and_fee.json`

### Parameters

None

# Invoices

## Invoices Dictionary

- `state` State of a Transaction. Possible values are:

| Name             | Description                                                  |
| ---------------- | ------------------------------------------------------------ |
| `pending`        | initial state                                                |
| `payment_chosen` | payment method has been chosen                               |
| `paid`           | invoice has been paid and payment has been verified Bukalapak |

- `unread` Possible values are `true` and `false`. User is required to take action as in `actions` if this field set to `true`.

## Get Invoices List

> Sample Request

```shell
curl -u 1:BoqDS9Kkif3EplbHN6ca "https://api.bukalapak.com/v2/invoices.json?page=2"
```

> Sample Response

```json
{
  "status": "OK",
  "transactions": [
    {
      "id": 131,
      "state": "paid",
      "updated_at": "2016-09-01T11:13:25.000+07:00",
      "created_at": "2016-04-27T16:43:42.000+07:00",
      "quick_trans": false,
      "invoice_id": "BL161111114R",
      "amount": 20000,
      "shipping_fee": 0,
      "insurance_cost": 5040,
      "total_amount": 25040,
      "subtotal_amount": 25040,
      "voucher_amount": 0,
      "voucher": null,
      "promo_payment_amount": 0,
      "retarget_discount_amount": 0,
      "deposit_reduction_amount": 0,
      "uniq_code": null,
      "coded_amount": 25040,
      "payment_method": "credit_card",
      "payment_method_name": "Kartu Visa/Mastercard/JCB",
      "payment_amount": 25040,
      "service_fee": 0,
      "payment_chosen_at": "2016-05-09T18:11:02.000+07:00",
      "expired_at": null,
      "revived_at": null,
      "paid_at": "2016-05-09T18:11:15.000+07:00",
      "cancelled_at": null,
      "pay_before": "2016-04-27T17:03:42.000+07:00",
      "payment_resumable": false,
      "payment_method_editable": false,
      "pickup_time": null,
      "amount_detail": [
        {
          "name": "Harga barang + jasa pengiriman",
          "amount": 25040
        },
        {
          "name": "Biaya pelayanan",
          "amount": 0
        },
        {
          "name": "Potongan Voucher",
          "amount": 0
        },
        {
          "name": "Diskon Metode Pembayaran",
          "amount": 0
        },
        {
          "name": "Kode Pembayaran",
          "amount": null
        },
        {
          "name": "Saldo BukaDompet",
          "amount": 0
        },
        {
          "name": "TOTAL",
          "amount": 25040
        }
      ],
      "buyer": {
        "id": 1,
        "name": "Serge",
        "username": "serge",
        "email": "serge@mail.com"
      },
      "consignee": {
        "name": "Serge",
        "phone": "085172637222",
        "address": "Jl. Mampang no 57",
        "area": "Mampang Prapatan",
        "city": "Jakarta Selatan",
        "province": "DKI Jakarta",
        "post_code": "15116",
        "latitude": null,
        "longitude": null,
        "formatted_address": null
      },
      "virtual": false,
      "type": "invoice",
      "transactions": [
        {
          "id": 399,
          "transaction_id": "160000000399",
          "seller": {
            "id": 3,
            "name": "Ragen",
            "username": "ragen"
          },
          "total_amount": 25040,
          "agent_commission_amount": 0,
          "state": "paid",
          "phone_credit": null,
          "products": [
            {
              "id": "1z",
              "url": "1z-jual-product-yunus",
              "name": "Product Yunus",
              "image_ids": [
                106
              ],
              "images": [
                "http://www.local.host:3000/system4/images/601/large/2015-11-11T19:08:22%2B07:00.jpg"
              ],
              "small_images": [
                "http://www.local.host:3000/system4/images/601/small/2015-11-11T19:08:22%2B07:00.jpg"
              ],
              "price": 20000,
              "order_quantity": 1
            }
          ]
        }
      ],
      "product_description": "Product Yunus"
    },
    /* ... */
  ],
  "message": null
}
```

Get invoices list owned by current user.

You can optionally set `If-None-Match` header or `Etag` header. If request `Etag` match, server will send `304 Not Modified` response without body. Server will set `Etag` header to every request to this resource.

### HTTP Request

`GET https://api.bukalapak.com/v2/invoices.json` `GET https://api.bukalapak.com/v2/invoices.json?page=2&per_page=10`. `page` and `per_page` provided.

### Parameters

| Parameter    |          | Description                                                  |
| ------------ | -------- | ------------------------------------------------------------ |
| `page`       | optional | Page number, default to `1`.                                 |
| `per_page`   | optional | Number of transactions `per_page`, default to `18`.          |
| `keywords`   | optional | Search keywords.                                             |
| `status`     | optional | Returns transaction with states as defined by this parameter. Possible values are `1` to `2`. Value `1` returns transactions with `pending`, `payment_chosen` (web counterpart is ‘Menunggu’). Value `2` returns transactions with `paid` state (web counterpart is ‘Dibayar’). Leave it undefined to return all invoices. |
| `actionable` | optional | Value `1` returns transactions that need action. Any other value returns transactions that doesn’t need action. Leave it undefined to return all transactions. |

## Create Invoices

> Sample Request

```shell
curl -u 1:BoqDS9Kkif3EplbHN6ca -d '{ "payment_invoice":{ "shipping_name": "Serge", "deposit_reduction_amount": 1000, "dropshipper_name": "dropshipper123", "dropshipper_note": "my dropshipper note", "phone": "085172637222", "address":{ "province": "DKI Jakarta", "city": "Jakarta Selatan", "area": "Mampang Prapatan", "address": "Jl. Mampang no 57", "post_code": "15116" }, "transactions_attributes": [ { "seller_id": 2, "courier": "SiCepat REG", "buyer_notes": "my note", "item_ids": [2, 3] } ] }, "payment_method": "deposit", "deposit_password": "xxxx", "cart_id": 72 }' https://api.bukalapak.com/v2/transactions.json -H "Content-Type: application/json" -X POST

> Success Response

​```json
{
  "status": "OK",
  "transaction": {
    "id": 131,
    "state": "paid",
    "updated_at": "2016-09-01T11:13:25.000+07:00",
    "created_at": "2016-04-27T16:43:42.000+07:00",
    "quick_trans": false,
    "invoice_id": "BL161111114R",
    "amount": 20000,
    "shipping_fee": 0,
    "insurance_cost": 5040,
    "total_amount": 25040,
    "subtotal_amount": 25040,
    "voucher_amount": 0,
    "voucher": null,
    "promo_payment_amount": 0,
    "retarget_discount_amount": 0,
    "deposit_reduction_amount": 0,
    "uniq_code": null,
    "coded_amount": 25040,
    "payment_method": "deposit",
    "payment_method_name": "BukaDompet",
    "payment_amount": 25040,
    "service_fee": 0,
    "payment_chosen_at": "2016-05-09T18:11:02.000+07:00",
    "expired_at": null,
    "revived_at": null,
    "paid_at": "2016-05-09T18:11:15.000+07:00",
    "cancelled_at": null,
    "pay_before": "2016-04-27T17:03:42.000+07:00",
    "payment_resumable": false,
    "payment_method_editable": false,
    "pickup_time": null,
    "amount_detail": [
      {
        "name": "Harga barang + jasa pengiriman",
        "amount": 25040
      },
      {
        "name": "Biaya pelayanan",
        "amount": 0
      },
      {
        "name": "Potongan Voucher",
        "amount": 0
      },
      {
        "name": "Diskon Metode Pembayaran",
        "amount": 0
      },
      {
        "name": "Kode Pembayaran",
        "amount": null
      },
      {
        "name": "Saldo BukaDompet",
        "amount": 0
      },
      {
        "name": "TOTAL",
        "amount": 25040
      }
    ],
    "buyer": {
      "id": 1,
      "name": "Serge",
      "username": "serge",
      "email": "serge@mail.com"
    },
    "consignee": {
      "name": "Serge",
      "phone": "085172637222",
      "address": "Jl. Mampang no 57",
      "area": "Mampang Prapatan",
      "city": "Jakarta Selatan",
      "province": "DKI Jakarta",
      "post_code": "15116",
      "latitude": null,
      "longitude": null,
      "formatted_address": null
    },
    "virtual": false,
    "type": "invoice",
    "transactions": [
      {
        "id": 399,
        "transaction_id": "160000000399",
        "seller": {
          "id": 3,
          "name": "Ragen",
          "username": "ragen"
        },
        "total_amount": 25040,
        "agent_commission_amount": 0,
        "state": "paid",
        "phone_credit": null,
        "products": [
          {
            "id": "1z",
            "url": "1z-jual-product-yunus",
            "name": "Product Yunus",
            "image_ids": [
              106
            ],
            "images": [
              "http://www.local.host:3000/system4/images/601/large/2015-11-11T19:08:22%2B07:00.jpg"
            ],
            "small_images": [
              "http://www.local.host:3000/system4/images/601/small/2015-11-11T19:08:22%2B07:00.jpg"
            ],
            "price": 20000,
            "order_quantity": 1
          }
        ]
      }
    ],
    "product_description": "Product Yunus"
  },
  "message": null
}
```

> Failure Response

```json
{
  "status": "ERROR",
  "transaction": null,
  "message": "Gagal membuat tagihan"
}
```

Create a Invoice record as a logged in user or as a quick buyer.

### HTTP Request

`POST https://api.bukalapak.com/v2/invoices.json`

### Parameters

None

### POST request data

| Property           |          | Description                                                  |
| ------------------ | -------- | ------------------------------------------------------------ |
| `payment_invoice`  | required | Attributes of invoice.                                       |
| `voucher_code`     | optional | The code of the voucher used in the payment.                 |
| `payment_method`   | required | payment method, accepted values are `deposit`, `atm`, `alfamart`, `indomaret`, `credit_card`, `bca_klikpay`, `cimb_clicks`, `mandiri_clickpay`, `mandiri_ecash` |
| `deposit_password` | optional | user password for deposit payment method.                    |
| `cart_id`          | required | ID of the cart where the items for the transaction is stored. |

`payment_invoice` are constructed by following fields:

| Property                  |          | Description                                                  |
| ------------------------- | -------- | ------------------------------------------------------------ |
| `shipping_name`           | required | The name of the person to whom the package should be delivered. |
| `dropshipper_name`        | optional | Dropshipper name (buy as dropshipper).                       |
| `dropshipper_notes`       | optional | Dropshipper notes (buy as dropshipper).                      |
| `phone`                   | required | Phone number for seller to contact the buyer or the person who should receive the package. |
| `address`                 | required | Attributes of the address where the package should be delivered. |
| `transactions_attributes` | required | Attributes of transactions.                                  |

`address_attributes` are constructed by following fields:

| Property    |          | Description              |
| ----------- | -------- | ------------------------ |
| `province`  | required | Destination province.    |
| `city`      | required | Destination city.        |
| `area`      | required | Destination area.        |
| `address`   | required | Destination address.     |
| `post_code` | required | Destination postal code. |
| `latitude`  | optional | Destination latitude.    |
| `longitude` | optional | Destination longitude.   |

# Users

## Get User Info

> Sample Request

```shell
curl -u 15:tokenkeyiskmzwa8awaa https://api.bukalapak.com/v2/users/info.json
```

> Success Response

```json
{
  "status": "OK",
  "user": {
    "name": "Me Ow",
    "email": "meow@domain.com",
    "phone": "022345678901",
    "avatar": "https://secure.gravatar.com/avatar/c8a0457bfc1b881755588e05a6ce55f0?s=50",
    "avatar_id": "38432",
    "bank": {
      "name": "Bank Republik Dummy",
      "number": "234567890"
    }
  },
  "message": null
}
```

Gets information for current user



<aside class="warning">Requires authentication</aside>



### HTTP Reuest

`GET https://api.bukalapak.com/v2/users/info.json`

### Parameters

None

## Register New User

> Sample Request

```shell
curl -X POST -F "user[email]=testing@testing12349.com" -F "user[username]=testingtesting910" -F "user[name]=asadasan" -F "user[birthday_date]=21" -F "user[birthday_month]=12"\
  -F "user[birthday_year]=1999" -F "user[password]=testing1234" -F "user[password_confirmation]=testing1234" -F "user[phone]=081238877" -F "user[address_attributes][province]=Banten"\
  -F "user[address_attributes][city]=Tangerang" -F "user[address_attributes][area]=Batuceper" -F "user[address_attributes][address]=jl xxx" -F "user[address_attributes][post_code]=11111"\
  -F "user[policy]=1" -F "user[avatar_attributes][data]=@/home/sdsdkkk/Desktop/xkcd.png" -F "seller_term_condition=Barang Bagus" -F "referer=bukalapak_app"\
  "https://api.bukalapak.com/v2/users.json"
```

> Success Response

```json
{
  "status": "OK",
  "message": "Pendaftaran berhasil, klik link yang dikirimkan ke alamat e-mail kamu untuk melakukan konfirmasi.",
  "user_id": 153,
  "user_name": "testingtesting910",
  "confirmed": false,
  "token": "8O8ZJNmhIMLYmoQiX7X",
  "email": "testing@testing12349.com",
  "omnikey": "1437375e40b73d04dbe9d9eabe66b0ac"
}
```

> Failure Response
>
> #### Username and email has been registered before

```json
{
  "status": "ERROR",
  "message": "Username sudah digunakan dan Email sudah digunakan"
}
```

> #### Registration via Facebook failed

```json
{
  "status": "ERROR",
  "message": "Gagal mendaftar dengan akun Facebook"
}
```

### HTTP Request

`POST https://api.bukalapak.com/v2/users/register.json`

### Parameters

| Property  |          | Description                                                  |
| --------- | -------- | ------------------------------------------------------------ |
| `user`    | optional | Attributes for new user.                                     |
| `referer` | optional | Fill this if the user is registered via a mobile app or something other than Bukalapak’s website. |

`user` is constructed by the following fields:

| Property                  |          | Description                                                  |
| ------------------------- | -------- | ------------------------------------------------------------ |
| `email_or_phone`          | required | E-mail address or phone number to register.                  |
| `username`                | required | Username to register.                                        |
| `name`                    | required | New user’s name.                                             |
| `birthday_date`           | optional | Date of birth. Use together with `birthday_month` and `birthday_year`. |
| `birthday_month`          | optional | Month of birth. Use together with `birthday_date` and `birthday_year` |
| `birthday_year`           | optional | Year of birth. Use together with `birthday_date` and `birthday_month` |
| `password`                | required | Password.                                                    |
| `password_confirmation`   | required | Password confirmation.                                       |
| `phone`                   | optional | User’s phone number.                                         |
| `gender`                  | optional | User’s gender.                                               |
| `address_attributes`      | optional | Attributes of the user’s address.                            |
| `policy`                  | required | Sign that user has accepted the agreements.                  |
| `avatar_attributes[data]` | optional | Image for the user’s avatar.                                 |

`address_attributes` is constructed by following fields:

| Property    |          | Description         |
| ----------- | -------- | ------------------- |
| `province`  | required | User’s province.    |
| `city`      | required | User’s city.        |
| `area`      | required | User’s area.        |
| `address`   | required | User’s address.     |
| `post_code` | required | User’s postal code. |

## Reset Password

> Sample Request

```shell
curl -X POST --data "email=testingaccount@test.com" "https://api.bukalapak.com/v2/users/password_reset.json"
```

> Success Response

```json
{
  "status": "OK",
  "message": "Email penggantian password telah dikirimkan, silakan ikuti petunjuk yang diberikan"
}
```

> Failure Response

```json
{
  "status": "ERROR",
  "message": "Tidak ada user yang terdaftar dengan email tersebut"
}
```

Sends password reset link and instruction to a registered user’s e-mail address.

### HTTP Request

`POST https://api.bukalapak.com/v2/users/password_reset.json`

### Parameters

| Property |          | Description                                            |
| -------- | -------- | ------------------------------------------------------ |
| `email`  | required | E-mail address for sending password reset instruction. |

## Get User Account Setting

> Sample Request

```shell
curl -u 66:tok3ntok3n https://api.bukalapak.com/v2/users.json
```

> Success Response

```json
{
  "status": "OK",
  "user": {
    "id": 66,
    "email": "testingaccount@test.com",
    "phone": "081238877",
    "name": "Testing Account",
    "birthday": "1999-12-12",
    "avatar": "https://s4.bukalapak.com/system/avatars/055/f87/412/9cf/0ec/36837/thumb/xkcd.png?1387268595",
    "avatar_id": 36837,
    "address": {
      "province": "Banten",
      "city": "Tangerang",
      "area": "Batuceper",
      "address": "jl xxx",
      "postal_code": "11111"
    },
    "seller_term_condition": "Barang yang di beli tidak dapat dikembalikan."
  },
  "message": null
}
```



<aside class="warning">Requires authentication</aside>



### HTP Request

`GET https://api.bukalapak.com/v2/users.json`

### Parameters

None

## Update User Account Setting

> Sample Request

```shell
curl -u 66:tok3ntok3n -X PATCH -F "user[name]=asadasan" -F "user[birthday_date]=21" -F "user[birthday_month]=12" -F "user[birthday_year]=1999"\
  -F "user[address_attributes][province]=Banten" -F "user[address_attributes][city]=Tangerang" -F "user[address_attributes][area]=Batuceper"\
  -F "user[address_attributes][address]=jl xxx" -F "user[address_attributes][post_code]=11111"\
  -F "user[avatar_attributes][data]=@/home/sdsdkkk/Desktop/xkcd.png" -F "user[avatar_attributes][id]=36837"\
  "https://api.bukalapak.com/v2/users.json"
```

> Success Response

```json
{
  "status": "OK",
  "user": {
    "id": 66,
    "email": "testingaccount@test.com",
    "phone": "081238877",
    "name": "asadasan",
    "birthday": "1999-12-12",
    "avatar": "https://s4.bukalapak.com/system/avatars/055/f87/412/9cf/0ec/36837/thumb/xkcd.png?1387268595",
    "avatar_id": 36837,
    "lapak_name": "Lapak Super",
    "lapak_desc": "tidak beli barbel melayang",
    "lapak_header": "https://s2.bukalapak.com/system/lapak/e4d/a3b/7fb/bce/234/5/normal/xkcd.png?1387351083",
    "header_id": 15,
    "address": {
      "province": "Banten",
      "city": "Tangerang",
      "area": "Batuceper",
      "address": "jl xxx",
      "postal_code": "11111"
    },
    "seller_term_condition": "Barang yang di beli tidak dapat dikembalikan."
  },
  "message": "Akun Anda telah diupdate"
}
```

Updates account information for current user.



<aside class="warning">Requires authentication</aside>



### HTTP Request

`PATCH https://api.bukalapak.com/v2/users/:id.json`

### Parameters

| Property       |          | Description                                                  |
| -------------- | -------- | ------------------------------------------------------------ |
| `user`         | optional | New attributes for updated user.                             |
| `lapak_header` | optional | Lapak header image.                                          |
| `header_id`    | optional | Replace header with a certain ID, not needed if user doesn’t have header image yet. If omitted when user has header image, delete current header from record and create new header record (not recommended). |

`user` is constructed by the following fields:

| Property                  |          | Description                                                  |
| ------------------------- | -------- | ------------------------------------------------------------ |
| `email`                   | optional | New email.                                                   |
| `old_password`            | optional | Current password, required for updating email & password.    |
| `password`                | optional | New password.                                                |
| `password_confirmation`   | optional | New password’s confirmation, required for updating password. |
| `name`                    | optional | User’s name.                                                 |
| `birthday_date`           | optional | Date of birth. Use together with `birthday_month` and `birthday_year`. |
| `birthday_month`          | optional | Month of birth. Use together with `birthday_date` and `birthday_year` |
| `birthday_year`           | optional | Year of birth. Use together with `birthday_date` and `birthday_month` |
| `phone`                   | optional | User’s phone number.                                         |
| `gender`                  | optional | User’s gender.                                               |
| `address_attributes`      | optional | Attributes of the user’s address.                            |
| `avatar_attributes[data]` | optional | Image for the user’s avatar.                                 |
| `avatar_attributes[id]`   | optional | User’s avatar ID. Required when updating avatar.             |
| `lapak`                   | optional | Lapak title.                                                 |
| `description`             | optional | Lapak description.                                           |

`address_attributes` is constructed by the following fields:

| Property    |          | Description         |
| ----------- | -------- | ------------------- |
| `province`  | required | User’s province.    |
| `city`      | required | User’s city.        |
| `area`      | required | User’s area.        |
| `address`   | required | User’s address.     |
| `post_code` | required | User’s postal code. |

## Get User Profile

> Sample Request

```shell
curl https://api.bukalapak.com/v2/users/204253/profile.json
curl https://api.bukalapak.com/v2/users/testingaccount.json
```

> Success Response

```json
{
  "status": "OK",
  "user": {
    "id": 204253,
    "username": "testingaccount",
    "name": "Testing Account",
    "avatar": "https://s3.bukalapak.com/images/default_avatar/medium/default.jpg",
    "level": "Pedagang",
    "lapak_name": "Lapak Barbel",
    "lapak_desc": "Tidak Beli Barbel Melayang",
    "lapak_header": "https://s1.bukalapak.com/images/header-lapak-default.jpg",
    "last_login": "2014-10-30T14:18:17.000+07:00",
    "store_closed": false,
    "schedule_close_store": null,
    "close_date": null,
    "close_reason": null,
    "reopen_date": null,
    "joined_at": "2014-04-04T11:03:46.000+07:00",
    "rejection": {
      "rejected": 1,
      "recent_trans": 60
    },
    "feedbacks": {
      "positive": 16,
      "negative": 5
    },
    "address": {
      "province": "Jawa Timur",
      "city": "Surabaya"
    }
  },
  "message": null
}
```

> Failure Response

```json
{
  "status": "ERROR",
  "user": null,
  "message": "Pengguna tidak ditemukan"
}
```

### HTTP Request

`GET https://api.bukalapak.com/v2/users/:id/profile.json` or `GET https://api.bukalapak.com/v2/users/:username.json`

### Parameters

None

## Get User Account Summary

Get summary of user

> Sample Request

```shell
curl -u 15:tokenkeyiskmzwa8awaa https://api.bukalapak.com/v2/users/account_summary.json
```

> Success Response

```json
{
  "status": "OK",
  "summary": {
    "address": "Jl Poltangan no 20, Pasar Minggu, Jakarta Selatan",
    "products_for_sale": 5172,
    "products_not_for_sale": 2470,
    "bookmarks": 2,
    "balance": 2122000,
    "pending_topups": 0,
    "pending_withdrawals": 0,
    "need_action_seller": 3,
    "need_action_buyer": 0,
    "dispute_count": 1,
    "remaining_pushes": 2321,
    "seller_positive": 14041,
    "seller_negative": 0,
    "buyer_positive": 20,
    "buyer_negative": 0,
    "accepted_orders": 100,
    "rejected_orders": 0,
    "couriers": [
      "JNE REG"
    ],
    "facebook": true,
    "twitter": true,
    "newsletter": true,
    "komunitas_email_replies": true,
    "seller_badge": {
      "current_badge": "Recommended Seller",
      "icon": "https://www.bukalapak.com/images/badge/seller/xhdpi/level-7.png",
      "n_feedback": 35960,
      "next_badge": "Trusted Seller"
    }
  }
}
```

> Failure Response

```json
{
  "status": "ERROR",
  "message": "Anda harus login untuk mengakses halaman ini"
}
```



<aside class="warning">Requires authentication</aside>



### HTTP Request

`GET https://api.bukalapak.com/v2/users/account_summary.json`

### Parameters

None

## Get Top Sellers

> Sample Request

```shell
curl https://api.bukalapak.com/v2/users/top_sellers.json
```

> Success Response

```json
{
  "status": "OK",
  "category": "Sepeda"
  "top_sellers": [
    {
      "id": 204253,
      "username": "testingaccount",
      "name": "Testing Account",
      "avatar": "https://s3.bukalapak.com/images/default_avatar/medium/default.jpg",
      "lapak_name": "Lapak Barbel",
      "lapak_desc": "Tidak Beli Barbel Melayang",
      "lapak_header": "https://s1.bukalapak.com/images/header-lapak-default.jpg",
      "feedbacks": {
        "positive": 16,
        "negative": 5
      },
      "address": {
        "province": "Jawa Timur",
        "city": "Surabaya"
      }
    },
    /* ... */
  ],
  "message": null
}
```

### HTTP Request


`GET https://api.bukalapak.com/v2/users/top_sellers.json`

### Parameters

| Property      |          | Description                                           |
| ------------- | -------- | ----------------------------------------------------- |
| `category_id` | optional | Request top sellers list for certain categories only. |

## Get User Feedbacks

> Sample Request

```shell
curl https://api.bukalapak.com/v2/users/62817/feedbacks.json?page=1&per_page=10&feedback_as_seller=1
```

> Success Response

```json
{
  "status": "OK",
  "message": null,
  "redeemable": false,
  "feedbacks": [
    {
      "id": 22032,
      "transaction_id": 7921,
      "transaction_no": "140624187921",
      "sender_id": 1,
      "sender_name": "Nugroho Herucahyono",
      "sender_type": "User",
      "user_id": 62817,
      "user_name": "Sayur Kangkung",
      "body": "Pembeli yang baik. Tidak rewel dan responsive",
      "positive": true,
      "created_at":"2012-10-11T17:55:34+07:00",
      "updated_at":"2012-10-11T17:55:34+07:00"
    },
    {
      "id": 22031,
      "transaction_id": 7907,
      "transaction_no": "140624187907",
      "sender_id": 31432,
      "sender_name": "Khairul",
      "sender_type": "User",
      "user_id": 62817,
      "user_name": "Sayur Kangkung",
      "body": "Recommended buyer. Ga banyak tanya :). Bayar sesuai harga dan cepat tanggap.",
      "positive": true,
      "created_at":"2012-10-11T17:55:34+07:00",
      "updated_at":"2012-10-11T17:55:34+07:00"
    }
  ]
}
```

> Failure Response

```json
{
  "status": "ERROR",
  "message": "Pengguna tidak dapat ditemukan",
  "redeemable": false,
  "feedbacks": []
}
```



<aside class="warning">Requires authentication</aside> to get redeemable status



## Get Single Feedback

> Sample Request

```shell
curl https://api.bukalapak.com/v2/users/feedbacks/62817.json?page=1&per_page=10&feedback_as_seller=1
```

> Success Response

```json
{
  "status": "OK",
  "message": null,
  "redeemable": false,
  "feedback": 
    {
      "id": 22032,
      "transaction_id": 7921,
      "transaction_no": "140624187921",
      "sender_id": 1,
      "sender_name": "Nugroho Herucahyono",
      "sender_type": "User",
      "user_id": 62817,
      "user_name": "Sayur Kangkung",
      "body": "Pembeli yang baik. Tidak rewel dan responsive",
      "positive": true,
      "created_at":"2012-10-11T17:55:34+07:00",
      "updated_at":"2012-10-11T17:55:34+07:00"
    }
}
```

### HTTP Request

`GET https://api.bukalapak.com/v2/users/:id/feedbacks.json`

### Parameters

| Property             |          | Description                                                  |
| -------------------- | -------- | ------------------------------------------------------------ |
| `page`               | optional | Page number to display. Default value is `1`.                |
| `per_page`           | optional | Number of record to display per page. Default value is `10`. |
| `feedback_as_seller` | optional | Field indicating whether to return feedback as seller or as buyer. Possible values are `1` and anything else. If set to `1`, response will return feedbacks as seller. Other values will return feedback as buyer. Leave it empty to get feedbacks both as seller and buyer. |
| `feedback_positive`  | optional | Field indicating whether to return positive or negative feedbacks. Possible values are `1` and anything else. If set to `1`, response will return positive feedbacks only. Other values will return negative feedbacks only. Leave it empty to get all positive and negative feedbacks. |

## Delete User Feedback

> Sample Request

```shell
curl -u 66:tok3ntok3n -X DELETE "https://api.bukalapak.com/v2/users/feedbacks/31/delete.json
```

> Success Response

```json
{
  "status": "OK",
  "message": "Feedback negatif berhasil dihapus"
}
```

> Failure Response
>
> #### User not found

```json
{
  "status": "ERROR",
  "message": "Pengguna tidak dapat ditemukan"
}
```

> #### Negative feedback not found

```json
{
  "status": "ERROR",
  "message": "Feedback negatif tidak dapat ditemukan"
}
```

> #### Not enough positive feedbacks to redeem

```json
{
  "status": "ERROR",
  "message": "Feedback positif tidak cukup untuk menghapus feedback negatif"
}
```



<aside class="warning">Requires authentication</aside>



### HTTP Request

`DELETE https://api.bukalapak.com/v2/users/feedbacks/:feedback_id/delete.json`

### Parameters

None

## Show Bank Accounts

> Sample Request

```shell
curl -u 15:tokenkeyiskmzwa8awaa https://api.bukalapak.com/v2/users/banks.json
```

> Success Response

```json
{
  "status": "OK",
  "accounts": [
    {
      "id": 41829,
      "bank": "Bank Central Asia (BCA)",
      "number": "123 456 789",
      "name": "Me Ow",
      "primary": false
    },
    {
      "id": 41831,
      "bank": "Bank Central Asia (BCA)",
      "number": "987 654 321",
      "name": "Me Ow",
      "primary": false
    }
  ],
  "message": null
}
```

Get bank account list for the current user.



<aside class="warning">Requires authentication</aside>



### HTTP Reqest

`GET https://api.bukalapak.com/v2/users/banks.json`

### Parameters

None

## Add New Bank Account

> Sample Request

```shell
curl -u 66:tok3ntok3n -X POST "https://api.bukalapak.com/v2/users/banks.json" --data "payment_bank_account[name]=Testing Account&payment_bank_account[bank]=Bank Central Asia (BCA)&payment_bank_account[number]=987 654 321&password=testing1234"
```

> Success Response

```json
{
  "status": "OK",
  "bank_account_id": 41835,
  "message": "Rekening bank ditambahkan"
}
```

> Failure Response
>
> #### Wrong password supplied

```json
{
  "status": "ERROR",
  "bank_account_id": null,
  "message": "Password salah"
}
```

> #### Other failures

```json
{
  "status": "ERROR",
  "bank_account_id": null,
  "message": "Gagal menambahkan rekening bank"
}
```

Adds a new bank account for the current user.



<aside class="warning">Requires authentication</aside>



### HTTP Request

`POST https://api.bukalapak.com/v2/users/banks.json`

### Parameters

None

### POST Request Data

| Property               |          | Description                      |
| ---------------------- | -------- | -------------------------------- |
| `payment_bank_account` | required | Attributes for new bank account. |
| `password`             | required | Current user’s password.         |

`payment_bank_account` is constructed by the following fields:

| Property |          | Description                |
| -------- | -------- | -------------------------- |
| `name`   | required | Name of the account owner. |
| `bank`   | required | Name of the bank.          |
| `number` | required | The bank account’s number. |

## Update Bank Account

> Sample Request

```shell
curl -u 66:tok3ntok3n -X PATCH "https://api.bukalapak.com/v2/users/settings/bank/41829/primary.json" --data "payment_bank_account[name]=Bill Gates&payment_bank_account[bank]=Bank Central Asia (BCA)&payment_bank_account[number]=123 456 789&password=testing1234"
```

> Success Response

```json
{
  "status": "OK",
  "message": "Rekening bank telah diupdate"
}
```

> Failure Response
>
> #### Wrong password supplied

```json
{
  "status": "ERROR",
  "message": "Password salah"
}
```

> #### Trying to access other user’s bank account

```json
{
  "status": "ERROR",
  "message": "Anda tidak dapat mengakses rekening ini"
}
```

> #### Other failures

```json
{
  "status": "ERROR",
  "message": "Gagal mengupdate rekening"
}
```

Updates current user’s bank account.



<aside class="warning">Requires authentication</aside>



### HTTP Request

`PATCH https://api.bukalapak.com/v2/users/banks/:bank_account_id.json`

### Parameters

None

### PATCH Request Data

| Property               |          | Description                            |
| ---------------------- | -------- | -------------------------------------- |
| `payment_bank_account` | required | New attributes to update bank account. |
| `password`             | required | Current user’s password.               |

`payment_bank_account` is constructed by the following fields:

| Property |          | Description                |
| -------- | -------- | -------------------------- |
| `name`   | required | Name of the account owner. |
| `bank`   | required | Name of the bank.          |
| `number` | required | The bank account’s number. |

## Set Bank Account to Primary

> Sample Request

```shell
curl -u 66:tok3ntok3n -X PATCH "https://api.bukalapak.com/v2/users/banks/41831/primary.json" --data ""
```

> Success Response

```json
{
  "status": "OK",
  "message": "Set to primary"
}
```

Sets current user’s primary bank account.



<aside class="warning">Requires authentication</aside>



### HTTP Request

`PATCH https://api.bukalapak.com/v2/users/banks/:bank_account_id/primary.json`

### Parameters

None

## Delete Bank Account

> Sample Request

```shell
curl -u 66:tok3ntok3n -X DELETE "https://api.bukalapak.com/v2/users/banks/41832.json" --data ""
```

> Success Response

```json
{
  "status": "OK",
  "message": "Rekening telah dihapus"
}
```

> Failure Response

```json
{
  "status": "ERROR",
  "message": "Anda tidak dapat mengakses rekening ini"
}
```

Deletes one of current user’s bank account.



<aside class="warning">Requires authentication</aside>



### HTTP Request

`DELETE https://api.bukalapak.com/v2/users/banks/:bank_account_id.json`

### Parameters

None

## Retrieve Address Attributes

> Sample Request

```shell
curl "https://api.bukalapak.com/v2/users/address_attributes.json?province=Riau&city=Bengkalis"
```

> Success Response
>
> #### Requesting list of provinces

```json
{
  "status": "OK",
  "type": "province",
  "list": [
    "Bali","Banten","Bengkulu","Daerah Istimewa Yogyakarta","DKI Jakarta","Gorontalo","Jambi","Jawa Barat","Jawa Tengah","Jawa Timur","Kalimantan Barat","Kalimantan Selatan","Kalimantan Tengah","Kalimantan Timur","Kalimantan Utara","Kepulauan Bangka Belitung","Kepulauan Riau","Lampung","Maluku","Maluku Utara","Nanggroe Aceh Darussalam","Nusa Tenggara Barat","Nusa Tenggara Timur","Papua","Papua Barat","Riau","Sulawesi Barat","Sulawesi Selatan","Sulawesi Tengah","Sulawesi Tenggara","Sulawesi Utara","Sumatera Barat","Sumatera Selatan","Sumatera Utara"
  ],
  "message": null
}
```

> #### Requesting list of cities

```json
{
  "status": "OK",
  "type": "city",
  "list": [
    "Bengkalis","Dumai","Indragiri Hilir","Indragiri Hulu","Kampar","Kepulauan Meranti","Kuantan Singingi","Pekanbaru","Pelalawan","Rokan Hilir","Rokan Hulu","Siak"
  ],
  "message": null
}
```

> #### Requesting list of districts:

```json
{
  "status": "OK",
  "type": "district",
  "list": [
    "Bantan","Bengkalis","Bukit Batu","Duri Mandau","Mandau","Pinggir","Rupat","Rupat Utara","Siak Kecil"
  ],
  "message": null
}
```

Retrieve list of registered provinces, cities, or districts depends on the provided parameters. If no parameters provided, return list of registered provinces. If provinces provided, return list of registered cities. If cities provided, return list of registered districts.

### HTTP Request

`GET htps://api.bukalapak.com/v2/users/address_attributes.json`

### Parameters

| Property   |          | Description             |
| ---------- | -------- | ----------------------- |
| `province` | optional | The requested province. |
| `city`     | optional | The requested city.     |

## Retrieve Supported Banks

> Sample Request

```shell
curl "https://api.bukalapak.com/v2/users/bank_names.json"
```

> Success Response

```json
{
  "status": "OK",
  "list": [
    "Bank Central Asia (BCA)","Bank Mandiri","Bank Negara Indonesia (BNI)","Bank Rakyat Indonesia (BRI)","Bank Tabungan Negara (BTN)","Bank Agroniaga","Bank Artha Graha International","Bank Bukopin","Bank Bumi Arta","Bank Capital Indonesia","Bank CIMB Niaga","Bank Danamon Indonesia","Bank Ekonomi Raharja","Bank Ganesha","Bank Hana","Bank ICB BumiPATCHra","Bank ICBC Indonesia","Bank Index Selindo","Bank Maybank Indonesia","Bank Maspion","Bank Mayapada","Bank Mega","Bank Mestika Dharma","Bank Metro Express", ...
  ],
  "message": null
}
```

Retrieve list of supported banks.

### HTTP Request
`GET https://api.bukalapak.com/v2/users/bank_names.json`

### Parameters

None

## Close Store

> Sample Request

```shell
curl -u 204253:8zm2L9lJDXWKc0wTOX6V https://api.bukalapak.com/v2/users/close_store.json -X PATCH --data 'user[store_closed_end_year]=2014&user[store_closed_end_month]=12&user[store_closed_end_date]=14'
```

> Success Response

```json
{
  "status": "OK",
  "message": "Anda berhasil menutup lapak."
}
```

> Failure Response

```json
{
  "status": "ERROR",
  "message": "Tanggal buka tidak boleh kosong."
}
```

Close store for a while.

### HTTP Request

`PATCH https://api.bukalapak.com/v2/users/close_store.json`

### Parameters

None

### PATCH Request Data

`user` Attributes needed to close user’s store, constructed by the following fields:

| Property                   |          | Description                |
| -------------------------- | -------- | -------------------------- |
| `store_closed_end_year`    | required | Year of the reopening.     |
| `store_closed_end_month`   | required | Month of the reopening.    |
| `store_closed_end_date`    | required | Day of the reopening.      |
| `store_closed_start_year`  | optional | Year of the closing.       |
| `store_closed_start_month` | optional | Month of the closing.      |
| `store_closed_start_date`  | optional | Day of the closing.        |
| `store_closed_reason`      | optional | The reason of the closing. |

## Open Store

> Sample Request

```shell
curl -u 204253:8zm2L9lJDXWKc0wTOX6V https://api.bukalapak.com/v2/users/open_store.json -X PATCH --data ''
```

> Success Response

```json
{
  "status": "OK",
  "message": "Anda berhasil membuka lapak."
}
```

Reopen store after closing.

### HTTP Request

`PATCH https://api.bukalapak.com/v2/users/open_store.json`

### Parameters

None

## Get Courier Settings

> Sample Request

```shell
curl -u 204253:8zm2L9lJDXWKc0wTOX6V https://api.bukalapak.com/v2/users/couriers.json
```

> Success Response

```json
{
  "status": "OK",
  "message": null,
  "couriers": ["JNE", "TIKI"]
}
```

Retrieve users' courier settings.

### HTTP Reques

`GET https://api.bukalapak.com/v2/users/couriers.json`

### Parameters

None

## Set Courier Settings

> Sample Request

```shell
curl -u 204253:8zm2L9lJDXWKc0wTOX6V htt[s://api.bukalapak.com/v2/users/couriers.json -X PATCH -d '{"couriers":["JNE", TIKI"]}' -H "Content-Type: application/json"
```

> Success Response

```json
{
  "status": "OK",
  "message": "Kurir telah diset",
  "couriers": ["JNE", "TIKI"]
}
```

> Failure Response

```json
{
  "status": "ERROR",
  "message": "Gagal mengeset kurir",
  "couriers": null
}
```

Set users' courier settings.

### HTTP Request

`PATCH https://api.bukalapak.com/v2/users/couriers.json`

### Parameters

| Property   |          | Description                                                  |
| ---------- | -------- | ------------------------------------------------------------ |
| `couriers` | optional | User’s courier choices, available choices are `JNE`, `Pos Kilat`, `TIKI`, and `ESL`. Case sensitive, if left blank will default to JNE. Must be sent as an array. |

## Get Products

> Sample Request

```shell
curl "https://api.bukalapak.com/v2/users/2/products.json"
```

> Success Response

```json
{
  "status": "OK",
  "products": [
    {
      "id": "1c",
      "category": "Komputer",
      "category_id": 58,
      "category_structure": ["Komputer"],
      "name": "Mediatech Flash Disk FK-014 8 GB / 8GB",
      "active": true,
      "city": "Badung",
      "province": "Bali",
      "price": 63000,
      "weight": "100",
      "courier": ["JNE"],
      "force_insurance": null,
      "image_ids": [126],
      "images": [
        "https://s1.bukalapak.com/system3/images/1/2/6/large/2014-09-12T17_00_29_07_00.jpg"
      ],
      "small_images": [
        "https://s1.bukalapak.com/system3/images/1/2/6/small/2014-09-12T17_00_29_07_00.jpg"
      ],
      "url": "https://www.bukalapak.com/p/komputer/1c-jual-mediatech-flash-disk-fk-014-8-gb-8gb",
      "desc": "Password Keeper<br/>Disk Partition<br/>USB 2.0 DRIVE<br/>Feature:<br/>water resistant, shock resistant, partitions feature, password feature, windows vista booster.<br/>compatuble: windows 7, windows vista, windows XP, Mac OS v.10.5.x +<br/>Linux v.2.6.x +",
      "condition": "new",
      "nego": false,
      "seller_username": "serge",
      "seller_name": "Serge",
      "seller_id": 2,
      "seller_avatar": "https://s2.bukalapak.com/images/default_avatar/medium/default.jpg",
      "seller_level": "",
      "seller_positive_feedback": 0,
      "seller_negative_feedback": 0,
      "payment_ready": true,
      "stock": 1,
      "specs": {},
      "state_description": [],
      "minimum_negotiable": null,
      "for_sale": true,
      "favorited": false,
      "free_shipping_coverage": []
    },
    /* ... */
  ],
  "message": null
}
```

You can optionally set `If-None-Match` header or `Etag` header. If request `Etag` match, server will send `304 Not Modified` response without body. Server will set `Etag` header to every request to this resource.

### HTTP Request

`GET https://api.bukalapak.com/v2/users/:id/products.json`

### Parameters

| Property   |          | Description                                           |
| ---------- | -------- | ----------------------------------------------------- |
| `page`     | optional | Page number to display. Default value is `1`.         |
| `per_page` | optional | Number of products to display. Default value is `24`. |
| `keywords` | optional | Keywords use to search products.                      |

## Report User

> Sample Request

```shell
curl -X POST "https://api.bukalapak.com/v2/users/2/report.json" --data '{"message":"isi laporan"}'
```

> Success Response

```json
{
  "status": "OK",
  "message": "Laporan Anda telah dikirim."
}
```

### HTTP Request

`POST https://api.bukalapak.com/v2/users/:id/report.json`

### Parameters

| Property  |          | Description                                   |
| --------- | -------- | --------------------------------------------- |
| `message` | required | Message to Bukalapak about the reported user. |

## Get Transaction Addresses

> Sample Request

```shell
curl -u 2:BoqDS9Kkif3EplbHN6ca "https://api.bukalapak.com/v2/users/trans_addresses.json"
```

> Success Response

```json
{
  "status": "OK",
  "addresses": [
    {
      "summary": "Serge (Jalan)",
      "name": "Serge",
      "phone": "02123213",
      "province": "Bali",
      "city": "Badung",
      "area": "Abiansemal",
      "address": "Jalan",
      "post_code": "14122"
    },
    {
      "summary": "Serge (Jl. Mampang)",
      "name": "Serge",
      "phone": "9787686768",
      "province": "DKI Jakarta",
      "city": "Jakarta Selatan",
      "area": "Mampang Prapatan",
      "address": "Jl. Mampang",
      "post_code": "15116"
    },
    /* ... */
  ],
  "message": null
}
```

Get current user’s transaction addresses.



<aside class="warning">Requires authentication</aside>



You can optionally set `If-None-Match` header or `Etag` header. If request `Etag` match, server will send `304 Not Modified` response without body. Server will set `Etag` header to every request to this resource.

### HTTP Request

`GET https://api.bukalapak.com/v2/users/trans_addresses.json`

### Parameters

None

## Confirm User

> Sample Request

```shell
curl "https://api.bukalapak.com/v2/users/confirmation/G0vWlKSzd0GkP6ZJs399.json"
```

> Success Response

```json
{
  "status": "OK",
  "results": {
    "user_id": "157324",
    "user_name": "Sayur Kangkung",
    "token": "U8Ch2LigkVhdI3XwYRA"
  }
}
```

> Failure Response

```json
{
  "status": "ERROR",
  "results" : {
    "user_id": null,
    "user_name": null,
    "token": null
  }
}
```

### HTTP Request

`GET https://api.bukalapak.com/v2/confirmation/:token.json`

### Parameters

| Property |          | Description         |
| -------- | -------- | ------------------- |
| `token`  | required | Confirmation token. |

## Get Instagram Authentication URL

> Sample Request

```shell
curl -u 2:BoqDS9Kkif3EplbHN6ca "https://api.bukalapak.com/v2/users/get_ig_code_url.json"
```

> Success Response

```json
{
    "status": "OK",
    "url": "https://api.instagram.com/oauth/authorize/?client_id=00ddc0c264d24c4c883b2ed778af44d0&redirect_uri=https://api.bukalapak.com/v2/users/generate_ig_token.json&response_type=code"
}
```

Get instagram URL for OAuth Authentication. After login to instagram, you can link your instagram account to Bukalapak App. Instagram will redirect the request to bukalapak server and set your instagram token.

### HTTP Request

`GET https://api.bukalapak.com/v2/users/get_ig_code_url.json`

### Parameters

None

## Generate Instagram API Token

> Sample Request

```shell
curl -u 2:BoqDS9Kkif3EplbHN6ca "https://api.bukalapak.com/v2/users/generate_ig_token.json 'code=90967939618f4d01a138206de2335e32'"
```

> Success Response

```json
{
    "status": "OK",
    "instagram_token": "1799529370.00ddc0c.8ed3c431597044f5802b0fbc967bbabd"
}
```

Generate your token so the App can access your Instagram account. This API usually doesn’t called by the apps directly but rather redirected by instagram after OAuth has completed.

### HTTP Request

`GET ttps://api.bukalapak.com/v2/users/generate_ig_token.json`

### Parameters

| Property |          | Description                                           |
| -------- | -------- | ----------------------------------------------------- |
| `code`   | required | Code that generated by Instagram after OAuth process. |

## Set Instagram API Token

> Sample Request

```shell
curl -u 2:BoqDS9Kkif3EplbHN6ca "https://api.bukalapak.com/v2/users/set_instagram_token.json -X POST 'token=1799529370.00ddc0c.8ed3c431597044f5802b0fbc967bbabd'"
```

> Success Response

```json
{
    "status": "OK"
}
```

Set your instagram API token.

### HTTP Request

`POST https://api.bukalapak.com/v2/users/set_instagram_token.json`

### Parameters

| Property |          | Description     |
| -------- | -------- | --------------- |
| `token`  | required | Your new token. |

## Get User Contact List

> Sample Request

```shell
curl -u 2:BoqDS9Kkif3EplbHN6ca https://api.bukalapak.com/v2/users/contact_list.json
```

> Success Response

```json
{
    "status": "OK",
    "body": [
      {
        "partner_type": "seller",
        "partner_id": 11,
        "partner_name": "Hunter X Hunter",
        "partner_avatar_url": "https://s0.bukalapak.com/avt/4/2/7/0/6/4/5/small/image.jpg",
        "items": [
          "Greed Island Book"
        ]
      }
    ],
    "message": null
}
```

Get user’s contact list (other users that the user do transaction with).

### HTTP Request

`GET https://api.bukalapak.com/v2/users/contact_list.json`

### Parameters

None

## Upload Chat Attachment

> Sample Request

```shell
curl https://api.bukalapak.com/v2/chat_attachments.json -F file=@product-image.png -X POST
```

> Success Response

```json
{
  "status": "OK",
  "id": 11,
  "url": "https://s0.bukalapak.com/uploads/chat_attachments/1/1/original/image.jpg",
  "message": null
}
```

> Failure Response
>
> #### Format file tidak terdaftar

```json
{
  "status": "ERROR",
  "id": null,
  "url": null,
  "message": "Format file tidak diijinkan"
}
```

User attach a file to Chat, get url of file attached.

### HTTP Request

`POST https://api.bukalapak.com/v2/users/chat_attachments.json`

### Parameters

None

# User Addresses

## Get all User’s addresses

Get all addresses of current logged in user



<aside class="warning">Requires authentication</aside>



> Sample Request

```shell
curl "https://api.bukalapak.com/v2/user_addresses.json" -u "2:mytoken" -X "GET"
```

### Request UR

`GET https://api.bukalapak.com/v2/user_addresses.json`

### Parameters

`none`

> Success Response

```json
{
  "status": "OK",
  "message": "",
  "user_addresses": [
    {
      "id": 345,
      "primary": false,
      "title": "bukan utama1",
      "name": "tetsdfsdf",
      "phone": "085645262611",
      "address_attributes": {
        "id": 499,
        "address": "bukan utama bali",
        "area": "Abiansemal",
        "city": "Badung",
        "province": "Bali",
        "post_code": "80352"
      }
    },
    {
      "id": 346,
      "primary": true,
      "title": "utama",
      "name": "yunus",
      "phone": "085645272715",
      "address_attributes": {
        "id": 500,
        "address": "alamat utama",
        "area": "Babakan Madang",
        "city": "Kab. Bogor",
        "province": "Jawa Barat",
        "post_code": "16810"
      }
    }
  ]
}
```

## Add address to User’s addresses.

Self explained



<aside class="warning">Requires authentication</aside>



> Sample Request (Success)

```shell
curl "https://api.bukalapak.com/v2/user_addresses" -u "2:JrGYqs4bhAbW1GkRua" -X "POST" -d '{"user_address":{"name":"Haftidulah","phone":"085645272716","title":"Kosan oren","address_attributes":{"province":"DKI Jakarta","city":"Jakarta Selatan","area":"Pasar Minggu","address":"Jl. Kemang Timur no. 2013","post_code":"12560"}}}' -H 'Content-Type: application/json'
```

> Success Response

```json
{
  "status": "OK",
  "message": "Berhasil menambahkan alamat pengiriman baru!",
  "user_addresses": {
    "id": 350,
    "primary": false,
    "title": "Kosan oren",
    "name": "Haftidulah",
    "phone": "085645272716",
    "address_attributes": {
      "id": 509,
      "address": "Jl. Kemang Timur no. 2013",
      "area": "Pasar Minggu",
      "city": "Jakarta Selatan",
      "province": "DKI Jakarta",
      "post_code": "12560"
    }
  }
}
```

> Sample Request (Failed)

```shell
curl "https://api.bukalapak.com/v2/user_addresses" -u "2:JrGYqs4bhAbW1GkRua" -X "POST" -d '{"user_address":{"name":"Haftidulah","phone":"080982035645272716","title":"Kosan oren","address_attributes":{"province":"DKI Jakarta","city":"Jakarta Selatan","area":"Par Minggu","address":"Jl. Kemang Timur no. 2013","post_code":"12560"}}}' -H 'Content-Type: application/json'
```

> Failed Response

```json
{
  "status": "ERROR",
  "message": "Format nomor telepon salah dan Kecamatan harus valid",
  "user_addresses": null
}
```

### Request URL

`POST https://api.bukalapak.com/v2/user_addresses`

### Parameters

| Parameter      |            | Description                                                  |
| -------------- | ---------- | ------------------------------------------------------------ |
| `user_address` | *required* | attributes of user_addresses to be created.                  |
| `set_primary`  | optional   | boolean `true` or `false`. set to `true` if created user address will be set to primary address. |
| `password`     | *optional* | current user password to authorize if `set_primary` value is `true` |

`user_address` Attributes constructed of following fields

| Parameter            |            | Description                     |
| -------------------- | ---------- | ------------------------------- |
| `name`               | *required* | address owner name.             |
| `phone`              | optional   | address owner phone.            |
| `title`              | optional   | address title.                  |
| `address_attributes` | *required* | detailed attributes of address. |

`address_attributes` are constructed by following fields:

| Property    |            | Description                 |
| ----------- | ---------- | --------------------------- |
| `province`  | *required* | province of the address.    |
| `city`      | *required* | city of the address.        |
| `area`      | *required* | area of the address.        |
| `address`   | *required* | street number.              |
| `post_code` | *required* | postal code of the address. |

## Remove User’s address from list

Self explained

<aside class="warning">Requires authentication</aside>



> Sample Request (Success)

```shell
curl "https://api.bukalapak.com/v2/user_addresses/351.json" -u "2:mytoken" -X "DELETE"
```

> Success Response

```json
{
  "status": "OK",
  "message": "Alamat pengiriman berhasil dihapus"
}
```

> Sample Request (Failed) trying to delete last address or primary address

```shell
curl "https://api.bukalapak.com/v2/user_addresses/346.json" -u "2:mytoken" -X "DELETE"
```

> Failed Response

```json
{
  "status": "ERROR",
  "message": "Gagal menghapus alamat!"
}
```

### Request URL

`DELETE https://api.bukalapak.com/v2/user_addresses/:id.json`

### Parameters

| Parameter |            | Description                                     |
| --------- | ---------- | ----------------------------------------------- |
| `id`      | *required* | address id to be deleted from user address list |

## Edit User’s address



<aside class="warning">Requires authentication</aside>


> Sample Request (Success)

```shell
curl "https://api.bukalapak.com/v2/user_addresses/334.json" -u "1:mytoken" -X "PATCH" -H 'Content-Type: application/json' -d '{"user_address": {"title": "testing"}}'
```

> Success Response

```json
{
  "status":"OK",
  "message":"Berhasil memperbarui alamat pengiriman!",
  "user_address": {
    "id":334,"primary":false,
    "title":"testing",
    "name":"tetsdfsdf",
    "phone":"085645262611",
    "address_attributes":{
      "id":499,
      "address":"bukan utama bali",
      "area":"Abiansemal",
      "city":"Badung",
      "province":"Bali",
      "post_code":"80352"
    }
  }
}
```

> Sample Request (Failed) trying to modify primary address without password

```shell
curl "https://api.bukalapak.com/v2/user_addresses/332.json" -u "1:mytoken" -X "PATCH" -H 'Content-Type: application/json' -d '{"set_primary":"true", "user_address": {"title": "testing"}}'
```

> Failed Response

```json
{
  "status": "ERROR",
  "message": "Gagal memperbarui/membuat alamat utama, password yang Anda masukkan salah!",
  "user_address": null
}
```

### Request URL

`PATCH https://api.bukalapak.com/v2/user_addresses/:id.json`

### Parameters

| Parameter      |            | Description                                                  |
| -------------- | ---------- | ------------------------------------------------------------ |
| `user_address` | *required* | attributes of user_addresses to be created.                  |
| `set_primary`  | required   | boolean `true` or `false`. set to `true` if updated user address is primary address. |
| `password`     | optional   | current user password to authorize if `set_primary` value is `true` |

`user_address` Attributes constructed of following fields

| Parameter            |            | Description                     |
| -------------------- | ---------- | ------------------------------- |
| `name`               | *optional* | address owner name.             |
| `phone`              | optional   | address owner phone.            |
| `title`              | optional   | address title.                  |
| `address_attributes` | *required* | detailed attributes of address. |

`address_attributes` are constructed by following fields:

| Property    |          | Description                 |
| ----------- | -------- | --------------------------- |
| `province`  | optional | province of the address.    |
| `city`      | optional | city of the address.        |
| `area`      | optional | area of the address.        |
| `address`   | optional | street number.              |
| `post_code` | optional | postal code of the address. |

## Set an address to become primary address



<aside class="warning">Requires authentication</aside>



> Sample Request

```shell
curl "https://api.bukalapak.com/v2/user_addresses/2/set_primary.json" -u "2:mytoken" -X "PATCH" -d '{"password":"password pintar"}' -H 'Content-Type: application/json'
```

> Success Response

```json
{
  "status": "OK",
  "message": "Sukses mengubah alamat utama ke aszxc!",
  "user_address": {
    "id": 2,
    "primary": true,
    "title": "testestset",
    "name": "Radon",
    "phone": "085645262611",
    "address_attributes": {
      "id": 499,
      "address": "utama bali",
      "area": "Abiansemal",
      "city": "Badung",
      "province": "Bali",
      "post_code": "80352"
    }
  }
}
```

> Failed Response (Wrong password)

```json
{
  "status": "ERROR",
  "message": "Gagal memperbarui/membuat alamat utama, password yang Anda masukkan salah!",
  "user_address": null
}
```

### Request URL

`PATCH https://api.bukalapak.com/v2/user_addresses/:id/set_primary.json`

### Parameters

| Parameter  |            | Description           |
| ---------- | ---------- | --------------------- |
| `password` | *required* | current user password |

## Show an address from user



<aside class="warning">Requires authentication</aside>



> Sample Request

```shell
curl "https://api.bukalapak.com/v2/user_addresses/2.json" -u "2:mytoken" -X "GET"
```

> Success Response

```json
{
  "status": "OK",
  "message": "",
  "user_address": {
    "id": 2,
    "primary": true,
    "title": "show address",
    "name": "Orang Baru",
    "phone": "085645262611",
    "address_attributes": {
      "id": 499,
      "address": "bukan utama",
      "area": "Abiansemal",
      "city": "Badung",
      "province": "Bali",
      "post_code": "80352"
    }
  }
}
```

### Request URL

`GET https://api.bukalapak.com/v2/user_addresses/:id.json`

### Parameters

| Parameter |            | Description                     |
| --------- | ---------- | ------------------------------- |
| `id`      | *required* | user address id to be retrieved |