# overview

```
global
  # process-level settings go here
defaults
  # default settings go here
frontend listener
  # a frontend that accepts requests from clients
backend webservers
  # servers that fulfill the requests
```
# ACL
> Dùng ACL khi muốn request phải tuân theo các rule nhất định thì mới được tranfer tiếp

- Request phải chính xác theo path
```
frontend www
  bind :80
  acl images_url path_beg -i /images/ /photos/

  #path begin exactly with /image/ or /photo/
```
- Route request này đến một backend cụ thể khi ACL được xem xét xong
```
frontend www
   bind :80
   acl images_url path_beg -i /images/
   use_backend static_assets if images_url
backend static_assets
   server s1 192.168.50.20:80

   # if image_url is evaluated totally, backend with IP ... will recieve that request
```
### AND, OR, negate in if statement

[How to use ACL in HAproxy](https://www.haproxy.com/documentation/haproxy-configuration-tutorials/core-concepts/acls/)

- ACL được đáp ứng cả hai điều kiện đều thỏa mãn (AND logic)
```
frontend www
  bind :80
  acl images_url path_beg /images/
  acl is_get method GET
  
  # The path must begin with /images/ and the method must be GET
  use_backend static_assets if images_url is_get
backend static_assets
  server s1 192.168.50.20:80

  #images-url and is-get are passed at the same time (AND logic)
```
```
frontend www
  bind :80
  use_backend static_assets if { path_beg /images/ } { method POST }
backend static_assets
  server s1 192.168.50.20:80

  #or if statement can be used in this way
```
- Tương tự
  - Với OR: dùng `||`
  - Điều kiện khác: `!`

> Và với khả năng thêm rule khác như: string, ip, domain, regex, range of number, compare
