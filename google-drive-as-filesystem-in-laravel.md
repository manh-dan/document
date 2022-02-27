# Setup Laravel Storage Driver sử dụng Google Drive API

Đăng nhập vào Tài khoản Google của bạn và truy cập trang web này:

https://console.developers.google.com/

## Lấy thông tin Client ID và Client Secret

### Khởi tạo Project

Đầu tiên, chúng ta sẽ khởi tạo một dự án mới.

<img width="896" alt="Create a new project" src="https://user-images.githubusercontent.com/43207583/155831219-e493fa02-5556-4639-8a2c-ae634c9148f5.jpg">

Sau đó, Nhập các thông tin được yêu cầu và nhấn nút "Create" để tạo dự án mới như hình bên dưới.

<img width="896" alt="Create a new project" src="https://user-images.githubusercontent.com/43207583/155873075-1c9ec2cd-57c1-4aa2-aeb6-718916e4a723.jpg">

Lúc này, bạn phải mất vài giây trước khi dự án được tạo thành công trên máy chủ.

Đảm bảo rằng bạn đã chọn dự án ở trên cùng.

Sau đó, đi tới Library và tìm kiếm với từ khóa "Google Drive API".

<img width="896" alt="Find Google Drive API" src="https://user-images.githubusercontent.com/43207583/155873085-359f9643-1366-4e24-bde0-dd5654e39055.jpg">

Và sau đó Enable thư viện "Google Drive API".

<img width="896" alt="Enable Google Drive API" src="https://user-images.githubusercontent.com/43207583/155873099-dbbb07cc-c585-4186-9aa8-685680cb18a5.jpg">

### Cài đặt OAuth consent screen

Đầu tiên, bạn chọn mục "OAuth consent screen", sau đó chọn "External" và nhấn nút "Create".

<img width="896" alt="Consent Screen" src="https://user-images.githubusercontent.com/43207583/155873118-6ee33e32-fa5e-4fe8-85dd-9be13cfab189.jpg">

Sau đó, bạn điền các thông tin App name, User support email, Developer contact information và nhấn nút "Save and continue".

<img width="896" alt="Create Credentials" src="https://user-images.githubusercontent.com/43207583/155873127-daf9fac2-bc60-4098-a8c6-29eb08b162d0.png">

Ở màn hình Scopes, bạn có thể đặt phạm vi yêu cầu người dùng thay mặt bạn cấp quyền cho ứng dụng của bạn và cho phép dự án của bạn truy cập vào một số loại dữ liệu người dùng riêng tư nhất định từ Phạm vi tài khoản Google của họ.

Nếu không có gì đăc biệt, bạn có thể nhấn nút "Save and continue" để đến màn hình tiếp theo.

<img width="896" alt="Create Credentials" src="https://user-images.githubusercontent.com/43207583/155873135-d9ad713e-256d-45eb-ae8a-1dac4951a561.png">

Tiếp theo, ở màn hình Test users bạn có thêm các địa chỉ email để thực hiện quá trình kiểm thử trước khi công khai ứng dụng của bạn. Sau khi thêm các địa chỉ email, bạn hãy nhấn nút "Save and continue".

<img width="896" alt="Create Credentials" src="https://user-images.githubusercontent.com/43207583/155873145-f1363421-4c22-435b-9c77-c0ecd48e8b7e.png">

Cuối cùng, ở màn hình Summary sẽ tóm tắt các thông tin mà bạn setting ở các màn hình trước, sau khi các bạn kiểm tra thông tin hãy nhấn nút "Back to dashboard".

<img width="896" alt="Create Credentials" src="https://user-images.githubusercontent.com/43207583/155873154-fa09cb58-aa16-4a8f-8dc2-c016f9d5cd89.png">

### Cài đặt Credentials

Đầu tiên, bạn chọn mục "Credentials" như hình bên dưới

<img width="896" alt="Create Credentials" src="https://user-images.githubusercontent.com/43207583/155873161-e9c31f78-7c86-449b-ad9b-a5c766fc3529.jpg">

Sau đó, bạn hãy nhấn nút "Create credentials" và chọn "OAuth client ID" như hình bên dưới.

<img width="896" alt="Create Credentials" src="https://user-images.githubusercontent.com/43207583/155873171-e985696b-bb94-4738-b3f9-deed6611b7d6.jpg">

Ở màn hình Create OAuth client ID ở mục "Application Type" bạn hãy chọn Web application, sau đó bạn nhập các thông tin Name, Authorized JavaScript origins và Authorized redirect URIs và nhấn nút "Create".

Nếu bạn sử dụng Google Drive, ở mục Authorized redirect URIs bạn thêm URL: https://developers.google.com/oauthplayground

<img width="896" alt="Create Credentials" src="https://user-images.githubusercontent.com/43207583/155873178-42cd5a5f-d5fc-4c9b-ba04-24ac4ef5319b.png">

Cuối cùng, bạn sẽ có thông tin Client ID và Client Secret như hình bên dưới.

<img width="896" alt="Create Credentials" src="https://user-images.githubusercontent.com/43207583/155873187-0a2cfc2b-3e0d-4555-a45d-7bcc1d1d2fc4.jpg">

## Lấy thông tin Refresh Token

Đầu tiên, bạn hãy truy cập vào trang https://developers.google.com/oauthplayground

Ở góc trên cùng bên phải, nhấp vào biểu tượng setting, chọn "Use your own OAuth credentials" và dán client id và client secret của bạn.

<img width="896" alt="Create Credentials" src="https://user-images.githubusercontent.com/43207583/155873197-601c9615-463b-44e8-bbd7-d4a2ef9ad38f.jpg">

In step 1 nằm ở phía bên trái, tìm mục "Drive API v3", mở rộng và kiểm tra từng phạm vi của nó.

<img width="896" alt="Create Credentials" src="https://user-images.githubusercontent.com/43207583/155873202-787e4726-73ad-4083-be9c-1d5dcb7db8a3.jpg">

Nhấp vào "Authorize APIs" và cho phép truy cập vào tài khoản của bạn khi được nhắc nhở.

Khi bạn đến Step 2, bạn chọn mục "Auto-refresh the token before it expires" và nhấp vào "Exchange authorization code for tokens".

<img width="896" alt="Create Credentials" src="https://user-images.githubusercontent.com/43207583/155873216-26b05315-6811-4d13-8fd2-f89005fef272.jpg">





