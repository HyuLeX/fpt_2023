# JSON?

[JSON document](https://developer.mozilla.org/en-US/docs/Learn/JavaScript/Objects/JSON)

- Javascript Object Notation

# JSON structure
- Có thể cho các dạng dữ liệu vào trong JSON file như `strings, numbers, arrays, booleans, and other object literals`
- JSON cho phép xây dựng cây data hierarchy trong JSON file

Ví dụ:

```
{
  "squadName": "Super hero squad",
  "homeTown": "Metro City",
  "formed": 2016,
  "secretBase": "Super tower",
  "active": true,
  "members": [
    {
      "name": "Molecule Man",
      "age": 29,
      "secretIdentity": "Dan Jukes",
      "powers": ["Radiation resistance", "Turning tiny", "Radiation blast"]
    },
    {
      "name": "Madame Uppercut",
      "age": 39,
      "secretIdentity": "Jane Wilson",
      "powers": [
        "Million tonne punch",
        "Damage resistance",
        "Superhuman reflexes"
      ]
    },
    {
      "name": "Eternal Flame",
      "age": 1000000,
      "secretIdentity": "Unknown",
      "powers": [
        "Immortality",
        "Heat Immunity",
        "Inferno",
        "Teleportation",
        "Interdimensional travel"
      ]
    }
  ]
}
```
- Có thể đặt tên cho JSON này là superheroes. Ví dụ về sử dụng object superheroes trong JS program:
```
superHeroes.homeTown;
superHeroes["active"];
```
- Và để truy cập sâu hơn vào data hierarchy, Ví dụ:
```
superHeroes["members"][1]["powers"][2]; // member#1 là Molecule Man và power#2 là Radiation blast
```
# JSON syntax
> Data is in name/value pairs

> Data is separated by commas

> Curly braces hold objects

> Square brackets hold arrays