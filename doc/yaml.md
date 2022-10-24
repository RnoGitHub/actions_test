# gg

## YAML

---
GitHub workflows are written in the YAML format and  format is just a data serialization language which is very simmiler to what JSON is.  
So if you know JSON it's pretty much the sama thing but it's written in a slightly different format.  
GitHub のワークフローは YAML 形式で書かれており、この形式は JSON に非常に似たデータシリアライズ言語である。
JSON を知っている人ならわかると思うが、少し違うフォーマットで書かれている。

prettier configuration. So prettier just in case you don't know, it allows you to format your code and you can set it to also format
If you use VScode, convenience extension is there.  
Extension are Prettier, YAML, YAML to JSON.  

prettierの設定。prettierは知らない人のために言っておくと、コードをフォーマットすることができ、またフォーマットするように設定することができる。

VScodeを使うなら、便利なエクステンションがある。  
拡張機能は、Prettier、YAML、YAML to JSONです。

## `test.yaml`

---
Create a yaml file and it's name "test.yaml".

YAML is just key value pairs.  
YAML is just a bit more readable. So I can have the key here and the value.  

Type as it follows.  

yamlファイルを作成し、名前を "test.yaml "とする。

YAMLは単なるキーと値のペアである。
YAMLはほんの少し読みやすくなっている。だから、ここにキーがあって、値があっても良い。  

以下のように入力する。

```yml
name: "ALi"
age: 28
address: "dwhui:iowdiw"
active: true
```

If you installed extension YAML to JSON to VSCode, type "Ctrl + Shift + P" and search for YAML.
And choice YAML to JSON: selection to JSON or document.
As you can see expected it's just a very simple JSON object.

VSCodeにYAML to JSON拡張機能をインストールした場合は、「Ctrl + Shift + P」をタイプしてYAMLを検索。そして、JSONにYAMLを選択：JSONまたはドキュメントに選択する。
それはちょうど期待していたように非常に単純なJSONオブジェクトとなる。

```JSON
{
  "name": "ALi",
  "age": 28,
  "address": "dwhui:iowdiw",
  "active": true
}
```

## Nested YAML

---
Nested structure of YAML is expressed by 2 spaces.  
YAMLの入れ子構造は、2つのスペースで表現される。

```YML
name: "ALi"
age: 28
address: "dwhui:iowdiw"
active: true
key:
  key: value
  key2: 33
```

Upper example also can convert to JSON.  
上の例もJSONに変換できる。

```JSON
{
  "name": "ALi",
  "age": 28,
  "address": "dwhui:iowdiw",
  "active": true,
  "key": {
    "key": "value",
    "key2": 33
  }
}
```

Indent is important for YAML. If you have a mistake to indent, YAML which is VSCode extension points out your mistake.  
YAMLではインデントが重要でインデントを間違えると、VSCodeの拡張機能であるYAMLはその間違いを指摘する。  

YAML can write like JSON but it is difficult to read.
Recommended expression is no bracket.  
YAMLはJSONのように書けますが、読みにくい。
推奨される表現は、ブラケットを使わないことである。

``` YML
name: "ALi"
age: 28
address: "dwhui:iowdiw"
active: true
key:
  key: value
  key2: 33
  key3: 
    key: value
    key2: value
  jsonObject: { key: value, key2: 33, key3: { key: value, key2: value } }
```

Output is same between `key` and `jsonObject`

```JSON
{
  "name": "ALi",
  "age": 28,
  "address": "dwhui:iowdiw",
  "active": true,
  "key": {
    "key": "value",
    "key2": 33,
    "key3": {
      "key": "value",
      "key2": "value"
    },
    "jsonObject": {
      "key": "value",
      "key2": 33,
      "key3": {
        "key": "value",
        "key2": "value"
      }
    }
  }
}
```

## Array in YAML

---
Array type in YAML, it's format as it follows.  
`-` represents array

``` YAML
array:
  - item1
  - item2
  - { key: value}
```

```JSON
{
    "array": [
        "item1",
        "item2",
        {
            "key": "value"
        }
    ]
}
```

### json array format

``` YAML
array:
  - item1
  - item2
  - { key: value}
jsonArray: [item1, item2]
```

```JSON
{
    "array": [
        "item1",
        "item2",
        {
            "key": "value"
        }
    ],
    "jsonArray": [
        "item1",
        "item2"
    ]
}
```

### Complex Array

``` YAML
array:
  - item1
  - item2
  - { key: value}
jsonArray: [item1, item2]
objectsArray:
  - key: value
    key2: value2
  - key: value
    key2: value2
```

```JSON
{
  "array": [
    "item1",
    "item2",
    {
      "key": "value"
    }
  ],
  "jsonArray": [
    "item1",
    "item2"
  ],
  "objectsArray": [
    {
      "key": "value",
      "key2": "value2"
    },
    {
      "key": "value",
      "key2": "value2"
    }
  ]
```

### long text format

``` YAML
longText: jflajkdkjf lkjafljkj.rg;lkmfd.,ma fadfjlkjdafjk lkajdfljdflkj
```

```JSON
{
    "longText": "jflajkdkjf lkjafljkj.rg;lkmfd.,ma fadfjlkjdafjk lkajdfljdflkj"
}
```

if you use `>` symbol, it means continueous sentence in JSON. It is better to read in yaml.

``` YAML
longText: jflajkdkjf lkjafljkj.rg;lkmfd.,ma fadfjlkjdafjk lkajdfljdflkj

longText2: >
  jflajkdkjf lkjafljkj.rg;
  lkmfd.,ma fadfjlkjdafjk 
  lkajdfljdflkj
```

```JSON
{
    "longText": "jflajkdkjf lkjafljkj.rg;lkmfd.,ma fadfjlkjdafjk lkajdfljdflkj",
    "longText2": "jflajkdkjf lkjafljkj.rg; lkmfd.,ma fadfjlkjdafjk  lkajdfljdflkj\n"
}
```

if you use `|` symbol, it means create new line in JSON. It is better to read in yaml.

``` YAML
longText: jflajkdkjf lkjafljkj.rg;lkmfd.,ma fadfjlkjdafjk lkajdfljdflkj

longText2: |
  jflajkdkjf lkjafljkj.rg;
  lkmfd.,ma fadfjlkjdafjk 
  lkajdfljdflkj
```

```JSON
{
    "longText": "jflajkdkjf lkjafljkj.rg;lkmfd.,ma fadfjlkjdafjk lkajdfljdflkj",
    "longText2": "jflajkdkjf lkjafljkj.rg;\nlkmfd.,ma fadfjlkjdafjk \nlkajdfljdflkj\n"
}
```
