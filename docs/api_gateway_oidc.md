---
typora-copy-images-to: ./images

---

## 创建 lambda 函数

打开 https://console.amazonaws.cn/lambda/home ，点击 **Create function** 按钮。

![image-20220408102649531](images/image-20220408102649531.png)

填入函数名称 helloWorld，点击按钮 **Create function**

![image-20220408102807639](images/image-20220408102807639.png)

## 创建 API

打开 api gateway https://console.amazonaws.cn/apigateway/main/apis ， 点击 **Create API**



![image-20220408103058423](images/image-20220408103058423.png)

选择 HTTP API ，点击 **Build**

![image-20220408103127644](images/image-20220408103127644.png)

输入 API name，点击 **Next**

![image-20220408103252451](images/image-20220408103252451.png)

先不设置 路由，点击 **Next**

![image-20220408103401431](images/image-20220408103401431.png)

先不设置 stage，点击 **Next**

![image-20220408103440513](images/image-20220408103440513.png)

最后点击 **Create**

![image-20220408103543143](images/image-20220408103543143.png)

在左侧菜单栏点击 `Routes`，然后点击 **Create**

![image-20220408103646015](images/image-20220408103646015.png)

method 选择 `GET`，路径输入 `/oidc-test`（路径名可以随便写，这里仅仅是示例）,点击 **Create** 按钮

![image-20220408103804310](images/image-20220408103804310.png)

点击 `GET` 方法，然后点击 **Attach integration**，

![image-20220408104122671](images/image-20220408104122671.png)

点击 **Create and attach an integration**

![image-20220408104139834](images/image-20220408104139834.png)

在 `Integration type` 中选择`Lambda function`

![image-20220408104243448](images/image-20220408104243448.png)

在 弹出的 **Integration details** 选项卡中点击 `Lambda function` 输入框，然后选择在第一节创建的 `helloWorld` 函数，然后点击 **Create** 按钮。

![image-20220408104445469](images/image-20220408104445469.png)

点击左侧菜单 API:myoidc 区域，复制出来图中 Invoke URL

![image-20220408104810235](images/image-20220408104810235.png)

然后拼接上 `oidc-test` 路径，用浏览器打开，正常情况下显示 "Hello from Lambda" 输出

![image-20220408104917694](images/image-20220408104917694.png)

点击左侧菜单 `Authorization`，然后点击 **Create and attach authorizer**

![image-20220408130318902](images/image-20220408130318902.png)

输入表单项 `Name`，`Issuer URL` , `Audience`，其中 `Audience` 是 authing 中的应用 ID，然后点击**Create and attach**

![image-20220408133223447](images/image-20220408133223447.png)

## 配置 API 跨域

点击 `CORS`，然后点击 **Configure** 按钮

![image-20220408134029746](images/image-20220408134029746.png)

allow-origin 和 allow-headers 设置为 `*`， allow-methods 设置为 GET 和 OPTIONS，点击 **Save** 按钮。

![image-20220408134800466](images/image-20220408134800466.png)

## 使用 curl 测试

```shell
curl -H "Authorization: Bearer eyJhbGciOiJSUzI1NiIsInR5cCI6IkpXVCIsImtpZCI6ImJIWWxKMFlZX1A2UWxUNzV3alVPUXlnMzV4ZGoyUi1qN2VNOEV4VS1XZW8ifQ.eyJuYmYiOjE2NDkzMzMxMDgsImp0aSI6IlhlTVFiUWczTWtMQXE2T2RCMXllZyIsInN1YiI6IjYyNDE4MDM2NDgzMjc5N2JkOTBlNjcwYiIsImlhdCI6MTY0OTMzNTEwOCwiZXhwIjoxNjUwNTQ0NzA4LCJzY29wZSI6Im9wZW5pZCBwcm9maWxlIiwiaXNzIjoiaHR0cHM6Ly9hd3MtZGVtby15dW5ueXN1bm55LmF1dGhpbmcuY24vb2lkYyIsImF1ZCI6IjYyNDNlNjE0NThiM2M2MGFhMWVjMGU3ZCJ9.vCUo6dqOT-TFgUKlI7M6q6kfIJt_U4s4QRF4pMEp0yx68_cW3jkECC79dk88gulUNw7KH7SVsUkAC73RGcnxdJyiSf36obHu0jydpCaZOSrHEeegRaQEt4by3Kt-nVENpDj-mXj59_s5KTkA3G6PZAyPKuc81qp2gEynTzcCcX5jdbPtjN_L2wY-7104aJKg_ZqXI2Q7Z-jCZ_H2IKR1trNGmL77NYEjs5wpE3wplFZgleQ0YDfV3NTPpG_1YE23VGqN3nkeLSEPCNQU5PEuaPoERY504F03vS49VtkxMby19HCdvONyenLH8H7gFmEEtrFsIb-PegzsZitPW0pgAQ" https://58li4spdvj.execute-api.cn-north-1.amazonaws.com.cn/oidc-test
```

将链接中的 api id 换成刚才新建的 ID 。