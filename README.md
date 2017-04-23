## Hướng dẫn cài đặt OMD - Check_MK trên Ubuntu 14.04

#### Menu

[1. Giới thiệu](#1)
[2. Cài đặt trên Server](#2)
[3. Cài đặt Agent trên Host giám sát](#3)
[4. Thêm dịch vụ giám sát Active Checks](#4)

### 1. Giới thiệu  <a name="1"></a>



### 2. Cài đặt trên Server  <a name="2"></a>

- **Bước 1**: Cài đặt Repo cho OMD
    - Thêm key GPG của OMD
    
    ```
    wget -q "https://labs.consol.de/repo/stable/RPM-GPG-KEY" -O - | sudo apt-key add -
    ```
    
    - Khai báo repo của OMD 
    
    ```
    echo "deb http://labs.consol.de/repo/stable/ubuntu $(lsb_release -cs) main" > /etc/apt/sources.list.d/labs-consol-stable.list
    apt-get update
    ```
    
- **Bước 2:** Cài đặt OMD

    - Tìm kiếm phiên bản OMD hiện hành
    
<img src="images/omd-1-search.png" />

    - Cài đặt bản `omd-1.30` bao gồm cả `Nagios`
    
    ```
    apt-get install omd-1.30
    ```
    
    - Trong quá trình cài đặt, phải khai báo mật khẩu cho MySQL
    
<img src="images/2.mysql.png" />

Sau khi khai báo xong, chúng ta chờ cho OMD cài đặt đến khi hoàn tất và thực hiện bước tiếp theo để tạo mới một `site` để monitoring.

- **Bước 3:** Tạo mới một `site`

Trước khi sử dụng, chúng ta phải khai báo một `site`:

```
omd create monitoring
```

<img src="images/3.info.png" />

Như vậy một site có tên là `monitoring` đã được tạo ra và phần thông tin được tô đỏ trong hình. Mặc định, username được cấp là `omdadmin` và password là `omd`.

**Chú ý:** Có thể tạo nhiều `site` và tên được chọn tùy ý.

- **Bước 4:** Kích hoạt `site` vừa tạo

Sau khi tạo xong `site`, chúng ta kích hoạt site đó và đăng nhập thử trên Web UI.

    - Kích hoạt `site`
    
    ```
    omd start monitoring
    ```
    
<img src="images/4.active-site.png" />

    - Truy cập vào Web UI và đăng nhập bằng `omdadmin/omd`
    
    ```
    http://địa-chỉ-ip/monitoring
    ```
    
<img src="images/5.webui1.png" />
    
    - Chọn giao diện `Check_MK`
    
<img src="images/6.webui2-checkmk.png" />

Sau khi chọn xong, chúng ta sẽ thấy một giao diện khá hoàn hảo với đầy đủ những chức năng cần thiết.

<img src="images/7.webui-main.png" />


### 3. Cài đặt Agent trên Host giám sát  <a name="3"></a> 
### 4. Thêm dịch vụ giám sát Active Checks  <a name="4"></a>