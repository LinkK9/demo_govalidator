## Validate struct trong golang với asaskevich/govalidator
asaskevich/govalidator là một thư viện giúp lập trình viên validate các input của người dùng một cách thuận tiện mà không cần phải duyệt qua bằng if else, switch....

### Cài đặt
Trong project Golang
vào terminal nhập lệnh: `go get github.com/asaskevich/govalidator`
### Import vào dự án
```go
import "github.com/asaskevich/govalidator"
```
hoặc dùng biến ngắn gọn hơn
```go
import (
  valid "github.com/asaskevich/govalidator"
)
```
### Sử dụng
Để validate struct, govalidator sử dụng các tag trong struct để định nghĩa các kiểu validate. Các tag có tiền tố là `valid:` theo sau là 1 chuỗi các kiểu validate.
```go
type User struct {
	Email string `valid:"required,email"`
	FullName string `valid:"required,alpha"`
	Password string `valid:"required"`
	Phone string `valid:"numeric"`
}
```
Có thể custom các thông báo lỗi bằng cách thêm vào tag các thông báo muốn tùy chỉnh và phân cách với các kiểu validate bằng dấu `~`, vd: `valid:"required~Họ tên không được để trống"`\
Ví dụ cụ thể Validate struct:
```go
type User	struct {
  Name string      `valid:"required,alpha"`
  Age  int         `valid:"numeric"`
}
result, err := govalidator.ValidateStruct(User{"Linh", 28})
if err != nil {
	println("error: " + err.Error())
}
println(result)
```
Ngoài hàm `govalidator.ValidateStruct()` asaskevich/govalidator còn có các hàm: ValidateMap, IsURL, IsJSON... xem thêm tại [https://github.com/asaskevich/govalidator]()
### Chạy thử demo
1. Clone repo về
2. `cd demo_govalidator`
3. `go run main.go`
