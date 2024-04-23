# Test ur ELK
- Test command ELK

```
curl -X GET "localhost:9200"
```
# 1. Sử dụng elasticsearch với kibana
### manage index trong elasticsearch
- Syntax tạo index:
```
PUT Name-of-the-Index
```
- Ví dụ:
```
PUT book_index
```
> Trong trường hợp muốn thay đổi như tên index thì tạo index mới và match index cũ vào index mới

- Ví dụ thay đổi tên index:
```
PUT new_index //tạo index mới

POST _reindex
{
  "source": {
    "index": "your_old_index"
  },
  "dest": {
    "index": "new_index"
  }
}//map index cũ vào index mới
```
- Syntax tạo index cùng với các thông tin liên quan (shard number?, replicas number?):
```
PUT /name_of_index
{
  "settings": {
    "index": {
      "number_of_shards": 3,  
      "number_of_replicas": 2 
    }
  }
}
```

### manage document trong elasticsearch
- Syntax tạo document:

```
PUT Name-of-the-Index/_doc/id-you-want-to-assign-to-this-document
{
  "field": "value"
}
```
- Ví dụ:
```
PUT book_index/_book_author/1
{
  "first_name": "John",
  "last_name": "sussy baka"
}
```
- Syntax cập nhật doc trong index
```
POST Name-of-the-Index/_doc/id-you-want-to-assign-to-this-document
{
  "field": "value"
}
```
- Ví dụ:
```
POST book_index/_book_author/1
{
  "first_name": "John",
  "last_name": "sussy baka"
}
```