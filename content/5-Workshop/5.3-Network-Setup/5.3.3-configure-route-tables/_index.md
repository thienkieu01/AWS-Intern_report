---
title : "Configure Route Tables"
date : 2024-01-01
weight : 3
chapter : false
pre : " <b> 5.3.3 </b> "
---

In this section, you will create 2 separate route tables: one for the public subnet (allowing Internet access) and one for the private subnet (allowing only internal VPC communication).

#### Step 1: Create the Route Table for the Public Subnet

1. In the navigation pane, select **Route Tables**, click **Create route table**.
2. Configure:
   - **Name**: `public-rt`
   - **VPC**: `vpc-0686bd0330b6b622f (library-vpc)`
3. Click **Create route table**.

![create-public-rt](/images/5-Workshop/5.3-Network-setup/5.3.3-configure-route-tables/create-public-rt.png)

4. Once created successfully, select `public-rt`, go to the **Routes** tab → click **Edit routes**.

![public-rt-created](/images/5-Workshop/5.3-Network-setup/5.3.3-configure-route-tables/public-rt-created.png)

5. Click **Add route**, enter:
   - **Destination**: `0.0.0.0/0`
   - **Target**: select the **Internet Gateway** created earlier.
6. Click **Save changes**.

![edit-public-route](/images/5-Workshop/5.3-Network-setup/5.3.3-configure-route-tables/edit-public-route.png)

{{% notice note %}}
The route `10.0.0.0/16 → local` is created by default, allowing subnets within the VPC to communicate with each other internally. The newly added route `0.0.0.0/0 → Internet Gateway` allows the public subnet to reach the Internet.
{{% /notice %}}

7. Switch to the **Subnet associations** tab, click **Edit subnet associations**.

![public-rt-subnet-tab](/images/5-Workshop/5.3-Network-setup/5.3.3-configure-route-tables/public-rt-subnet-tab.png)

8. Check `public-subnet`, click **Save associations**.

![associate-public-subnet](/images/5-Workshop/5.3-Network-setup/5.3.3-configure-route-tables/associate-public-subnet.png)

---

#### Step 2: Create the Route Table for the Private Subnets

9. Click **Create route table**, configure:
   - **Name**: `private-rt`
   - **VPC**: `vpc-0686bd0330b6b622f (library-vpc)`
10. Click **Create route table**.

![create-private-rt](/images/5-Workshop/5.3-Network-setup/5.3.3-configure-route-tables/create-private-rt.png)

{{% notice note %}}
The private subnet's route table does **not** need a `0.0.0.0/0` route added. By default it only contains the internal route: `10.0.0.0/16 → local`, meaning the subnets can only communicate with each other within the VPC, with no access to or from the Internet.
{{% /notice %}}

11. Once created, switch to the **Subnet associations** tab, click **Edit subnet associations**.

![private-rt-subnet-tab](/images/5-Workshop/5.3-Network-setup/5.3.3-configure-route-tables/private-rt-subnet-tab.png)

12. Check both `private-subnet-1` and `private-subnet-2`, click **Save associations**.

![associate-private-subnet](/images/5-Workshop/5.3-Network-setup/5.3.3-configure-route-tables/associate-private-subnet.png)