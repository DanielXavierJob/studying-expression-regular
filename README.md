# Regular Expression 📝

Here you will see about regular expressions and how they work

## Notes

``\W`` => Anything other than words or numbers

``\w`` => Anything words or numbers


``\d`` => Anything from 0 to 9

``(\w+)`` its a expression to get all numbers or words
- \w matches any word character (equivalent to [a-zA-Z0-9_])
- ``+`` matches the previous token between one and unlimited times, as many times as possible, giving back as needed (greedy)
Global patte

``\s`` matches any whitespace character (equivalent to [\r\n\t\f\v ])

``(<name of group>)`` set name of group in expression


## Beginner 🚀

Here will be exemplified a CPF, and how regular expressions can
to work

### Regex: ``^(\d{3}).(\d{3}).(\d{3})-(\d{2})``

### Date: 123.123.123-12




(most beginner pattern)

### Result: 
```javascript
[
  [
    {
      "content": "122.122.122-12",
      "isParticipating": true,
      "groupNum": 0,
      "startPos": 0,
      "endPos": 14
    },
    {
      "content": "122",
      "isParticipating": true,
      "groupNum": 1,
      "startPos": 0,
      "endPos": 3
    },
    {
      "content": "122",
      "isParticipating": true,
      "groupNum": 2,
      "startPos": 4,
      "endPos": 7
    },
    {
      "content": "122",
      "isParticipating": true,
      "groupNum": 3,
      "startPos": 8,
      "endPos": 11
    },
    {
      "content": "12",
      "isParticipating": true,
      "groupNum": 4,
      "startPos": 12,
      "endPos": 14
    }
  ]
]
```

## CSV 🔥  
Here will be an example of a CSV, where the regular expression will search for all the names

### Regex: 
```Regex 
/^(?<lastName>\w+),\s(?<firstName>\w+)/gm
```

### Data: 
```csv
Xavier, Daniel
Gomes, Laila
Johnson, Jose
 ```

### Result: 
```javascript
[
  [
    {
      "content": "Xavier, Daniel",
      "isParticipating": true,
      "groupNum": 0,
      "startPos": 0,
      "endPos": 14
    },
    {
      "content": "Xavier",
      "isParticipating": true,
      "groupNum": 1,
      "groupName": "lastName",
      "startPos": 0,
      "endPos": 6
    },
    {
      "content": "Daniel",
      "isParticipating": true,
      "groupNum": 2,
      "groupName": "firstName",
      "startPos": 8,
      "endPos": 14
    }
  ],
  [
    {
      "content": "Gomes, Laila",
      "isParticipating": true,
      "groupNum": 0,
      "startPos": 15,
      "endPos": 27
    },
    {
      "content": "Gomes",
      "isParticipating": true,
      "groupNum": 1,
      "groupName": "lastName",
      "startPos": 15,
      "endPos": 20
    },
    {
      "content": "Laila",
      "isParticipating": true,
      "groupNum": 2,
      "groupName": "firstName",
      "startPos": 22,
      "endPos": 27
    }
  ],
  [
    {
      "content": "Johnson, Jose",
      "isParticipating": true,
      "groupNum": 0,
      "startPos": 28,
      "endPos": 41
    },
    {
      "content": "Johnson",
      "isParticipating": true,
      "groupNum": 1,
      "groupName": "lastName",
      "startPos": 28,
      "endPos": 35
    },
    {
      "content": "Jose",
      "isParticipating": true,
      "groupNum": 2,
      "groupName": "firstName",
      "startPos": 37,
      "endPos": 41
    }
  ]
]
```

## SQL To MongoDB 🔥

Here will be exemplified how it would be to transform a SQL to MongoDB


### SQL: 
```SQL
SELECT id, nome, endereco FROM users WHERE id = 1
```

### EXPECTED OUTCOME:
```MongoDB
db.users.find({id: 1}).project({ id: true, nome: true, endereco: true})
```

### Search:
```Regex
select\s(.*?)\sfrom\s(.*?)\swhere\s(.*?)\W{2}\s(.*)
```

### Explanation of groups:

1 - projection

2 - db

3 - where field

4 - where value

#### Configurations:

``/gmi``
- g => Global
- m => Multi line
- i => insensitive case

### Replace:
``
db.$2.find({$3: $4}).project({$1})
``

### Result:

``
db.users.find({id: 1}).project({ id, nome, endereco})
``

But the ``:true`` is missing in the project, how to solve it?

### Solution of SQL to MongoDB:

Get the result of replace, and add ``,`` in last param of project, in case: ``endereco``

#### Configurations:

``/gmi``
- g => Global
- m => Multi line
- i => insensitive case

#### Preview:

``
db.users.find({id: 1}).project({ id, nome, endereco,})
``


#### Regex:
``
(\w+)(?=,)
``

u given the params of project, go to replace it

#### Replace: 

``$1: true``

### Result:
``
db.users.find({id: 1}).project({ id: true, nome: true, endereco: true,})
``