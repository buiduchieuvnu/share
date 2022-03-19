# Eclipse
```
IDE hỗ trợ lập trình đa ngôn ngữ
```
## Một số lỗi thường gặp
### Lỗi eclipse won't start - no java virtual machine was found
> eclipse won't start - no java virtual machine was found
- Xử lý:
    - Tham khảo: [stackoverflow]( 
https://stackoverflow.com/questions/12426810/eclipse-wont-start-no-java-virtual-machine-was-found)

- Sửa cấu hình java jdk (jre) của eclipse trong file eclipse.ini nằm ở thư mục gốc cài eclipse
- Sửa tham số: `-vm` về đúng đường dẫn thực tế của JDK trên máy
    - VD: `C:\Program Files\Java\jdk1.8.0_221\bin`
- Start lại Eclipse => Done
