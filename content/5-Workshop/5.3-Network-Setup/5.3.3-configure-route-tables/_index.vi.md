---
title : "Cấu hình Route Table"
date : 2024-01-01
weight : 3
chapter : false
pre : " <b> 5.3.3 </b> "
---

Trong phần này, bạn sẽ tạo 2 route table riêng biệt: một cho public subnet (cho phép truy cập Internet) và một cho private subnet (chỉ cho phép giao tiếp nội bộ trong VPC).

#### Bước 1: Tạo Route Table cho Public Subnet

1. Trong thanh điều hướng, chọn **Route Tables**, click **Create route table**.
2. Cấu hình:
   - **Name**: `public-rt`
   - **VPC**: `vpc-0686bd0330b6b622f (library-vpc)`
3. Click **Create route table**.

![create-public-rt](/images/5-Workshop/5.3-Network-Setup/5.3.3-configure-route-tables/create-public-rt.png)

4. Sau khi tạo thành công, chọn `public-rt`, vào tab **Routes** → click **Edit routes**.

![public-rt-created](/images/5-Workshop/5.3-Network-Setup/5.3.3-configure-route-tables/public-rt-created.png)

5. Click **Add route**, nhập:
   - **Destination**: `0.0.0.0/0`
   - **Target**: chọn **Internet Gateway** đã làm lúc nãy.
6. Click **Save changes**.

![edit-public-route](/images/5-Workshop/5.3-Network-Setup/5.3.3-configure-route-tables/edit-public-route.png)

{{% notice note %}}
Route `10.0.0.0/16 → local` được tạo mặc định, cho phép các subnet trong VPC giao tiếp nội bộ với nhau. Route `0.0.0.0/0 → Internet Gateway` mới thêm sẽ cho phép public subnet truy cập ra Internet.
{{% /notice %}}

7. Chuyển sang tab **Subnet associations**, click **Edit subnet associations**.

![public-rt-subnet-tab](/images/5-Workshop/5.3-Network-Setup/5.3.3-configure-route-tables/public-rt-subnet-tab.png)

8. Tick chọn `public-subnet`, click **Save associations**.

![associate-public-subnet](/images/5-Workshop/5.3-Network-Setup/5.3.3-configure-route-tables/associate-public-subnet.png)

---

#### Bước 2: Tạo Route Table cho Private Subnet

9. Click **Create route table**, cấu hình:
   - **Name**: `private-rt`
   - **VPC**: `vpc-0686bd0330b6b622f (library-vpc)`
10. Click **Create route table**.

![create-private-rt](/images/5-Workshop/5.3-Network-Setup/5.3.3-configure-route-tables/create-private-rt.png)

{{% notice note %}}
Route table cho private subnet **không** cần thêm route `0.0.0.0/0`. Mặc định nó chỉ chứa route nội bộ: `10.0.0.0/16 → local`, nghĩa là các subnet chỉ giao tiếp được với nhau trong VPC, không thể truy cập/được truy cập từ Internet.
{{% /notice %}}

11. Sau khi tạo xong, chuyển sang tab **Subnet associations**, click **Edit subnet associations**.

![private-rt-subnet-tab](/images/5-Workshop/5.3-Network-Setup/5.3.3-configure-route-tables/private-rt-subnet-tab.png)

12. Tick chọn cả `private-subnet-1` và `private-subnet-2`, click **Save associations**.

![associate-private-subnet](/images/5-Workshop/5.3-Network-Setup/5.3.3-configure-route-tables/associate-private-subnet.png)