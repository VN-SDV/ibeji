# Dự án Eclipse Ibeji

- [Giới thiệu](#giới thiệu)
- [Thiết kế cấp cao](#thiết kế cấp cao)
- [Điều kiện tiên quyết](#điều kiện tiên quyết)
   - [Cài đặt gcc](#install-gcc)
   - [Cài đặt Rust](#install-rust)
   - [Cài đặt trình biên dịch Protobuf](#install-protobuf-compiler)
- [Nhân bản Repo](#cloning-the-repo)
- [Ghi chú của nhà phát triển](#developer-notes)
   - [JSON-LD Crate](#json-ld-crate)
   - [Trình phân tích DTDL](#dtdl-parser)
- [Tòa nhà](#tòa nhà)
- [Chạy thử nghiệm](#running-the-tests)
- [Chạy Demo](#running-the-demo)
- [Nhãn hiệu](#trademarks)

## <a name="introduction">Giới thiệu</a>

Eclipse Ibeji nhằm mục đích cung cấp khả năng thể hiện một biểu diễn kỹ thuật số về trạng thái phương tiện và các khả năng của nó
thông qua một kiến trúc có thể mở rộng, cởi mở và năng động, cung cấp quyền truy cập vào phần cứng, cảm biến và khả năng của xe.

## <a name="high-level-design">Thiết kế cấp cao</a>

Kiến trúc của Ibeji có Dịch vụ song sinh kỹ thuật số trong xe làm cốt lõi. Dịch vụ bản sao kỹ thuật số trong xe nắm bắt tất cả các khả năng chính của xe
và cung cấp chúng cho người tiêu dùng Ibeji. Một thành phần khác trong kiến trúc của Ibeji là Nhà cung cấp. Một phương tiện có thể có một hoặc nhiều nhà cung cấp.
Nhà cung cấp hiển thị một tập hợp con các khả năng chính của phương tiện bằng cách đăng ký chúng với Dịch vụ bản sao kỹ thuật số trong xe. Sau khi đã đăng ký với
Đến lượt mình, Dịch vụ Bản sao Kỹ thuật số Trong Xe có thể được cung cấp cho người tiêu dùng Ibeji. Mỗi khả năng bao gồm siêu dữ liệu cho phép người tiêu dùng Ibeji hiểu
bản chất của khả năng, cách làm việc với nó và cách truy cập từ xa.

## <a name="prerequisites">Điều kiện tiên quyết</a>

### <a name="install-gcc">Cài đặt gcc</a>

Rust cần trình liên kết của gcc, vì vậy bạn sẽ cần cài đặt nó. Để cài đặt gcc, hãy làm như sau:

vỏ ```
Sudo apt cài đặt gcc
```

### <a name="install-rust">Cài đặt Rust</a>

Tại thời điểm này, bạn sẽ cần sử dụng bản phát hành Rust hàng đêm. Mặc dù không lý tưởng nếu dựa vào bản phát hành hàng đêm, nhưng chúng ta có thể dựa vào
bản phát hành ổn định của Rust vào một thời điểm nào đó trong tương lai không xa khi một số thùng Rust mà chúng tôi sử dụng cũng có thể dựa vào nó. Để cài đặt Rust, hãy làm như sau:

vỏ ```
cập nhật sudo apt
sudo apt cài đặt -y snapd
Sudo snap cài đặt Rustup --classic
cài đặt chuỗi công cụ rỉ sét hàng đêm-2022-08-11
Rustup mặc định hàng đêm-2022-08-11
```

Nếu bạn đã cài đặt Rust nhưng đang sử dụng một bản phát hành khác thì bạn có thể chuyển sang bản phát hành nightly-2022-08-11 bằng cách chạy các lệnh sau:

vỏ ```
cài đặt chuỗi công cụ rỉ sét hàng đêm-2022-08-11
Rustup mặc định hàng đêm-2022-08-11
```

### <a name="install-protobuf-compiler">Cài đặt trình biên dịch Protobuf</a>

Bạn sẽ cần cài đặt Trình biên dịch Protobuf. Điều này có thể được thực hiện bằng cách thực hiện:

`sudo apt install -y trình biên dịch protobuf`

## <a name="cloning-the-repo">Nhân bản Repo</a>

Repo có hai mô-đun con [opendigitaltwins-dtdl](https://github.com/Azure/opendigitaltwins-dtdl) và [iot-plugandplay-models](https://github.com/Azure/iot-plugandplay-models) cung cấp các tệp ngữ cảnh DTDL
và tệp mẫu DTDL. Để đảm bảo rằng những thứ này được bao gồm, vui lòng sử dụng lệnh sau khi nhân bản repo github của Ibeji:

`git clone --recurse-submodules https://github.com/eclipse-ibeji/ibeji`

## <a name="developer-notes">Ghi chú của nhà phát triển</a>

### <a name="json-ld-crate">Thùng JSON-LD</a>

Tốt nhất là chúng ta nên sử dụng thùng json_ld 0.6.1 lấy nguồn từ [tại đây](https://github.com/timothee-haudebourg/json-ld).
Tuy nhiên, nó hiện có vấn đề về bản dựng được thảo luận [tại đây](https://github.com/timothee-haudebourg/json-ld/issues/40).
Để khắc phục sự cố này, bạn sẽ cần sử dụng git clone để lấy nguồn từ [tại đây](https://github.com/blast-hardcheese/json-ld)
và kiểm tra nhánh "resolve-issue-40" của nó. Nó sẽ được sao chép vào một thư mục là anh chị em với ibeji.

### <a name="dtdl-parser">Trình phân tích cú pháp DTDL</a>

Hiện không có Trình phân tích cú pháp DTDL cho Rust, vì vậy chúng tôi đã cung cấp một trình phân tích cú pháp tối giản cho DTDL v2 dựa trên [Trình phân tích cú pháp DTDL JavaScript](https://github.com/Azure/azure-sdk-for-js/tree/ %40azure/dtdl-parser_1.0.0-beta.2/sdk/digitaltwins/dtdl-parser).

## <a name="building">Tòa nhà</a>

Khi bạn đã cài đặt các điều kiện tiên quyết, hãy chuyển đến thư mục gốc của phần đăng ký của bạn và chạy:

`xây dựng hàng hóa`

Điều này sẽ xây dựng tất cả các thư viện và tệp thực thi.

## <a name="running-the-tests">Chạy thử nghiệm</a>

Sau khi xây dựng thành công Ibeji, bạn có thể chạy tất cả các bài kiểm tra đơn vị. Để thực hiện việc này, hãy chuyển đến thư mục gốc của người đăng ký và chạy:

`kiểm tra hàng hóa`

Hiện tại, chúng tôi không có thử nghiệm tích hợp hoặc thử nghiệm đầu cuối.

## <a name="running-the-demo">Chạy Demo</a>

Hiện tại có ba bản minh họa: một minh họa việc sử dụng thuộc tính, một minh họa việc sử dụng lệnh và một minh họa
thể hiện việc sử dụng hỗn hợp các thuộc tính và lệnh.

Các bản trình diễn sử dụng tệp cấu hình và chúng tôi đã cung cấp phiên bản mẫu của từng tệp cấu hình. Những mẫu này có thể được tìm thấy trong:

- {repo-root-dir}/core/invehicle_digital_twin/mẫu
- {repo-root-dir}/samples/common/template

Các hướng dẫn sau đây dành cho bản demo để sử dụng thuộc tính.

Các bước:

1. Cách tốt nhất để chạy bản trình diễn là sử dụng ba cửa sổ: một cửa sổ chạy Bản sao kỹ thuật số trong xe, một cửa sổ chạy Nhà cung cấp và một cửa sổ chạy Người tiêu dùng.
Định hướng ba cửa sổ để chúng được xếp thành một cột. Cửa sổ trên cùng có thể được sử dụng cho Twin kỹ thuật số trong xe.
Cửa sổ ở giữa có thể được sử dụng cho Nhà cung cấp. Cửa sổ dưới cùng có thể được sử dụng cho Người tiêu dùng.<br>
1. Trong mỗi cửa sổ, hãy thay đổi thư mục thành thư mục chứa các tạo phẩm xây dựng.
Đảm bảo rằng bạn thay thế "{repo-root-dir}" bằng thư mục gốc của kho lưu trữ trên máy mà bạn đang chạy bản trình diễn.<br><br>
`cd {repo-root-dir}/đích/gỡ lỗi`<br>
1. Tạo ba tệp cấu hình có nội dung sau, nếu chưa có:<br><br>
---- Consumer_settings.yaml ----<br>
`consumer_authority: "0.0.0.0:6010"`<br>
`invehicle_digital_twin_url: "http://0.0.0.0:5010"`<br><br>
---- invehicle_digital_twin_settings.yaml ----<br>
`invehicle_digital_twin_authority: "0.0.0.0:5010"`<br><br>
---- nhà cung cấp_settings.yaml ----<br>
`provider_authority: "0.0.0.0:4010"`<br>
`invehicle_digital_twin_url: "http://0.0.0.0:5010"`<br><br>
1. Trong cửa sổ trên cùng, hãy chạy:<br><br>
`./in-vehicle-digital-twin`<br>
1. Trong cửa sổ ở giữa, hãy chạy:<br><br>
`./property-provider`<br>
1. Trong cửa sổ dưới cùng, hãy chạy:<br><br>
`./property-consumer`<br>
1. Sử dụng control-c trong mỗi cửa sổ khi bạn muốn dừng bản trình diễn.

Các hướng dẫn sau đây dành cho bản demo để sử dụng lệnh.

Các bước:

1. Cách tốt nhất để chạy bản trình diễn là sử dụng ba cửa sổ: một cửa sổ chạy Bản sao kỹ thuật số trong xe, một cửa sổ chạy Nhà cung cấp và một cửa sổ chạy Người tiêu dùng.
Định hướng ba cửa sổ để chúng được xếp thành một cột. Cửa sổ trên cùng có thể được sử dụng cho Twin kỹ thuật số trong xe.
Cửa sổ ở giữa có thể được sử dụng cho Nhà cung cấp. Cửa sổ dưới cùng có thể được sử dụng cho Người tiêu dùng.<br>
1. Trong mỗi cửa sổ, hãy thay đổi thư mục thành thư mục chứa các tạo phẩm xây dựng.
Đảm bảo rằng bạn thay thế "{repo-root-dir}" bằng thư mục gốc của kho lưu trữ trên máy mà bạn đang chạy bản trình diễn.<br><br>
`cd {repo-root-dir}/đích/gỡ lỗi`<br>
1. Tạo ba tệp cấu hình có nội dung sau, nếu chưa có:<br><br>
---- Consumer_settings.yaml ----<br>
`consumer_authority: "0.0.0.0:6010"`<br>
`invehicle_digital_twin_url: "http://0.0.0.0:5010"`<br><br>
---- invehicle_digital_twin_settings.yaml ----<br>
`invehicle_digital_twin_authority: "0.0.0.0:5010"`<br><br>
---- nhà cung cấp_settings.yaml ----<br>
`provider_authority: "0.0.0.0:4010"`<br>
`invehicle_digital_twin_url: "http://0.0.0.0:5010"`<br><br>
1. Trong cửa sổ trên cùng, hãy chạy:<br><br>
`./in-vehicle-digital-twin`<br>
1. Trong cửa sổ ở giữa, hãy chạy:<br><br>
`./command-provider`<br>
1. Trong cửa sổ dưới cùng, hãy chạy:<br><br>
`./command-consumer`<br>
1. Sử dụng control-c trong mỗi cửa sổ khi bạn muốn dừng bản trình diễn.

Các hướng dẫn sau đây dành cho bản trình diễn để sử dụng hỗn hợp các lệnh và thuộc tính.

Các bước:

1. Cách tốt nhất để chạy bản trình diễn là sử dụng ba cửa sổ: một cửa sổ chạy Bản sao kỹ thuật số trong xe, một cửa sổ chạy Nhà cung cấp và một cửa sổ chạy Người tiêu dùng.
Định hướng ba cửa sổ để chúng được xếp thành một cột. Cửa sổ trên cùng có thể được sử dụng cho Twin kỹ thuật số trong xe.
Cửa sổ ở giữa có thể được sử dụng cho Nhà cung cấp. Cửa sổ dưới cùng có thể được sử dụng cho Người tiêu dùng.<br>
1. Trong mỗi cửa sổ, hãy thay đổi thư mục thành thư mục chứa các tạo phẩm xây dựng.
Đảm bảo rằng bạn thay thế "{repo-root-dir}" bằng thư mục gốc của kho lưu trữ trên máy mà bạn đang chạy bản trình diễn.<br><br>
`cd {repo-root-dir}/đích/gỡ lỗi`<br>
1. Tạo ba tệp cấu hình có nội dung sau, nếu chưa có:<br><br>
---- Consumer_settings.yaml ----<br>
`consumer_authority: "0.0.0.0:6010"`<br>
`invehicle_digital_twin_url: "http://0.0.0.0:5010"`<br><br>
---- invehicle_digital_twin_settings.yaml ----<br>
`invehicle_digital_twin_authority: "0.0.0.0:5010"`<br><br>
---- nhà cung cấp_settings.yaml ----<br>
`provider_authority: "0.0.0.0:4010"`<br>
`invehicle_digital_twin_url: "http://0.0.0.0:5010"`<br><br>
1. Trong cửa sổ trên cùng, hãy chạy:<br><br>
`./in-vehicle-digital-twin`<br>
1. Trong cửa sổ ở giữa, hãy chạy:<br><br>
`./mixed-provider`<br>
1. Trong cửa sổ dưới cùng, hãy chạy:<br><br>
`./mixed-consumer`<br>
1. Sử dụng control-c trong mỗi cửa sổ khi bạn muốn dừng bản trình diễn.

Nếu bạn muốn người tiêu dùng và nhà cung cấp cho mỗi bản demo sử dụng Chariott để khám phá URL cho Dịch vụ bản sao kỹ thuật số trong xe, thay vì
có nó được cung cấp tĩnh trong tệp cấu hình tương ứng của chúng, sau đó thực hiện các thao tác sau trước khi bắt đầu mỗi bản trình diễn:

1. Sao chép một bản Chariott từ GitHub (`https://github.com/eclipse-chariott/chariott`).
1. Xây dựng Chariott
1. Đặt biến môi trường CHARIOTT_REGISTRY_TTL_SECS của Chariott thành một số cao (chúng tôi đề xuất 86400 giây), vì Ibeji không dựa vào Chariot
