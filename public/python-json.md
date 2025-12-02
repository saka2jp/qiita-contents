---
title: 複雑なJSONから特定のデータを取り出す
tags:
  - Python
  - JSON
  - Python3
private: false
updated_at: '2025-12-02T00:09:48+09:00'
id: 3b138d3ebbdaa873eaa5
organization_url_name: null
slide: false
ignorePublish: false
---
# はじめに
　本来、複雑なデータ構造をシンプルに表現するためのJSONですが、適切な設計がされていなかったり、仕様が決まってなかったりすることで複雑になってしまうことがあります。
ここでいう複雑というのは、JSONから取得したいデータが何階層目にあるのか、いくつあるのか確かでないことです。

　そんな複雑なJSONから、特定のデータを取得することが今回の目的です。

# 今回のゴール
input

```json:test.json
{"a": [{
  "b": 1, 
  "c": [{
    "star": [{"Deneb": "デネブ", "Altair": "アルタイル", "Vega": "ベガ"}], 
    "d": [2,3]
    }], 
  "e": {"g": "x"}
  }],
 "f": "y",
}
```
output

```json
[{"Deneb": "デネブ", "Altair": "アルタイル", "Vega": "ベガ"}]
```
取得したいデータは、

* 何階層目にあるかわからない
* いくつあるかわからない

→　JSONを再帰的に探索する

# 実装

```py:
import json

def search(arg, cond):
    res =[]
    if cond(arg):
        res.append(arg)
    if isinstance(arg, list):
        for item in arg:
            res += search(item, cond)
    elif isinstance(arg, dict):
        for value in arg.values():
            res += search(value, cond)
    return res

def has_star_key(arg):
    if isinstance(arg, dict):
        return arg.keys() == {"Deneb", "Altair", "Vega"}
            
def get_star(arg):
    return search(arg, has_star_key)


if __name__ == "__main__":
    with open('test.json', encoding='utf-8') as f:
        data = json.load(f)
        print(get_star(data)) # [{"Deneb": "デネブ", "Altair": "アルタイル", "Vega": "ベガ"}]

```
目的のデータを取得することができました！

# 解説
① **JSONを探索する関数**

```py:
def search(arg, cond):
    res =[]
    if cond(arg):
        res.append(arg)
    if isinstance(arg, list):
        for item in arg:
            res += search(item, cond)
    elif isinstance(arg, dict):
        for value in arg.values():
            res += search(value, cond)
    return res
```
第一引数： Str型 or Int型 or List型 or Dict型
第二引数： 取得したいデータかどうか判定する関数（②の関数）
戻り値： List型

② **データを判定する関数**
取り出したいデータがあればTrue、なければFalseを返すようにします。

```py:
def has_star_key(arg):
    if isinstance(arg, dict):
        return arg.keys() == {"Deneb", "Altair", "Vega"}
```
第一引数： Str型 or Int型 or List型 or Dict型
戻り値： Bool型

③ **データを取得する関数**

```py:
def get_star(arg):
    return search(arg, has_star_key)
```
第一引数： Dict型
戻り値： List型


# テスト
　条件を変えた場合や他のJSONデータでも取得できるか確認してみます。取得したいデータの判定条件を変更するだけで実行できます。
（②の関数の変更とそれに伴う③の関数の変更）

**Case1. Str型のデータを全て取得する**
input

```json:
{"a": [{
  "b": 1, 
  "c": [{
    "star": [{"Deneb": "デネブ", "Altair": "アルタイル", "Vega": "ベガ"}], 
    "d": [2,3]
    }], 
  "e": {"g": "x"}
  }],
 "f": "y",
}
```
condition

```py:
def has_str(s):
    return isinstance(s, str)
```
output

```json:
["デネブ", "ベガ", "アルタイル", "x", "y"]
```

取得したいデータがいくつあってもちゃんと取得してくれました。


**Case2. データが大きいJSONから特定のデータを取得する**
input

```json:
{"DBEngineVersions":[{"Engine":"mysql","DBEngineVersionDescription":"MySQL 5.1.73a","DBParameterGroupFamily":"mysql5.1","DBEngineDescription":"MySQL Community Edition","EngineVersion":"5.1.73a"},{"Engine":"mysql","DBEngineVersionDescription":"MySQL 5.1.73b","DBParameterGroupFamily":"mysql5.1","DBEngineDescription":"MySQL Community Edition","EngineVersion":"5.1.73b"},{"Engine":"mysql","DBEngineVersionDescription":"MySQL 5.5.40","DBParameterGroupFamily":"mysql5.5","DBEngineDescription":"MySQL Community Edition","EngineVersion":"5.5.40"},{"Engine":"mysql","DBEngineVersionDescription":"MySQL 5.5.40a","DBParameterGroupFamily":"mysql5.5","DBEngineDescription":"MySQL Community Edition","EngineVersion":"5.5.40a"},{"Engine":"mysql","DBEngineVersionDescription":"MySQL 5.5.40b","DBParameterGroupFamily":"mysql5.5","DBEngineDescription":"MySQL Community Edition","EngineVersion":"5.5.40b"},{"Engine":"mysql","DBEngineVersionDescription":"MySQL 5.5.41","DBParameterGroupFamily":"mysql5.5","DBEngineDescription":"MySQL Community Edition","EngineVersion":"5.5.41"},{"Engine":"mysql","DBEngineVersionDescription":"MySQL 5.6.19a","DBParameterGroupFamily":"mysql5.6","DBEngineDescription":"MySQL Community Edition","EngineVersion":"5.6.19a"},{"Engine":"mysql","DBEngineVersionDescription":"MySQL 5.6.19b","DBParameterGroupFamily":"mysql5.6","DBEngineDescription":"MySQL Community Edition","EngineVersion":"5.6.19b"},{"Engine":"mysql","DBEngineVersionDescription":"MySQL 5.6.21","DBParameterGroupFamily":"mysql5.6","DBEngineDescription":"MySQL Community Edition","EngineVersion":"5.6.21"},{"Engine":"mysql","DBEngineVersionDescription":"MySQL 5.6.21b","DBParameterGroupFamily":"mysql5.6","DBEngineDescription":"MySQL Community Edition","EngineVersion":"5.6.21b"},{"Engine":"mysql","DBEngineVersionDescription":"MySQL 5.6.22","DBParameterGroupFamily":"mysql5.6","DBEngineDescription":"MySQL Community Edition","EngineVersion":"5.6.22"},
{"Engine":"oracle-ee","DBParameterGroupFamily":"oracle-ee-11.2","DefaultCharacterSet":{"CharacterSetName":"AL32UTF8","CharacterSetDescription":"Unicode 5.0 UTF-8 Universal character set"},"DBEngineDescription":"Oracle Database Enterprise Edition","EngineVersion":"11.2.0.2.v3","DBEngineVersionDescription":"Oracle 11.2.0.2.v3"},{"Engine":"oracle-ee","DBParameterGroupFamily":"oracle-ee-11.2","DefaultCharacterSet":{"CharacterSetName":"AL32UTF8","CharacterSetDescription":"Unicode 5.0 UTF-8 Universal character set"},"DBEngineDescription":"Oracle Database Enterprise Edition","EngineVersion":"11.2.0.2.v4","DBEngineVersionDescription":"Oracle 11.2.0.2.v4"},{"Engine":"oracle-ee","DBParameterGroupFamily":"oracle-ee-11.2","DefaultCharacterSet":{"CharacterSetName":"AL32UTF8","CharacterSetDescription":"Unicode 5.0 UTF-8 Universal character set"},"DBEngineDescription":"Oracle Database Enterprise Edition","EngineVersion":"11.2.0.2.v5","DBEngineVersionDescription":"Oracle 11.2.0.2.v5"},{"Engine":"oracle-ee","DBParameterGroupFamily":"oracle-ee-11.2","DefaultCharacterSet":{"CharacterSetName":"AL32UTF8","CharacterSetDescription":"Unicode 5.0 UTF-8 Universal character set"},"DBEngineDescription":"Oracle Database Enterprise Edition","EngineVersion":"11.2.0.2.v6","DBEngineVersionDescription":"Oracle 11.2.0.2.v6"},{"Engine":"oracle-ee","DBParameterGroupFamily":"oracle-ee-11.2","DefaultCharacterSet":{"CharacterSetName":"AL32UTF8","CharacterSetDescription":"Unicode 5.0 UTF-8 Universal character set"},"DBEngineDescription":"Oracle Database Enterprise Edition","EngineVersion":"11.2.0.2.v7","DBEngineVersionDescription":"Oracle 11.2.0.2.v7"},
{"Engine":"oracle-ee","DBParameterGroupFamily":"oracle-ee-11.2","DefaultCharacterSet":{"CharacterSetName":"AL32UTF8","CharacterSetDescription":"Unicode 5.0 UTF-8 Universal character set"},"DBEngineDescription":"Oracle Database Enterprise Edition","EngineVersion":"11.2.0.3.v1","DBEngineVersionDescription":"Oracle 11.2.0.3.v1"},{"Engine":"oracle-ee","DBParameterGroupFamily":"oracle-ee-11.2","DefaultCharacterSet":{"CharacterSetName":"AL32UTF8","CharacterSetDescription":"Unicode 5.0 UTF-8 Universal character set"},"DBEngineDescription":"Oracle Database Enterprise Edition","EngineVersion":"11.2.0.3.v2","DBEngineVersionDescription":"Oracle 11.2.0.3.v2"},{"Engine":"oracle-ee","DBParameterGroupFamily":"oracle-ee-11.2","DefaultCharacterSet":{"CharacterSetName":"AL32UTF8","CharacterSetDescription":"Unicode 5.0 UTF-8 Universal character set"},"DBEngineDescription":"Oracle Database Enterprise Edition","EngineVersion":"11.2.0.4.v1","DBEngineVersionDescription":"Oracle 11.2.0.4.v1"},{"Engine":"oracle-ee","DBParameterGroupFamily":"oracle-ee-11.2","DefaultCharacterSet":{"CharacterSetName":"AL32UTF8","CharacterSetDescription":"Unicode 5.0 UTF-8 Universal character set"},"DBEngineDescription":"Oracle Database Enterprise Edition","EngineVersion":"11.2.0.4.v3","DBEngineVersionDescription":"Oracle 11.2.0.4.v3"},{"Engine":"oracle-ee","DBParameterGroupFamily":"oracle-ee-12.1","DefaultCharacterSet":{"CharacterSetName":"AL32UTF8","CharacterSetDescription":"Unicode 5.0 UTF-8 Universal character set"},"DBEngineDescription":"Oracle Database Enterprise Edition","EngineVersion":"12.1.0.1.v1","DBEngineVersionDescription":"Oracle 12.1.0.1.v1"},{"Engine":"oracle-se","DBParameterGroupFamily":"oracle-se-11.2","DefaultCharacterSet":{"CharacterSetName":"AL32UTF8","CharacterSetDescription":"Unicode 5.0 UTF-8 Universal character set"},"DBEngineDescription":"Oracle Database Standard Edition","EngineVersion":"11.2.0.2.v3","DBEngineVersionDescription":"Oracle 11.2.0.2.v3"},
{"Engine":"oracle-se","DBParameterGroupFamily":"oracle-se-11.2","DefaultCharacterSet":{"CharacterSetName":"AL32UTF8","CharacterSetDescription":"Unicode 5.0 UTF-8 Universal character set"},"DBEngineDescription":"Oracle Database Standard Edition","EngineVersion":"11.2.0.2.v4","DBEngineVersionDescription":"Oracle 11.2.0.2.v4"},{"Engine":"oracle-se","DBParameterGroupFamily":"oracle-se-11.2","DefaultCharacterSet":{"CharacterSetName":"AL32UTF8","CharacterSetDescription":"Unicode 5.0 UTF-8 Universal character set"},"DBEngineDescription":"Oracle Database Standard Edition","EngineVersion":"11.2.0.2.v5","DBEngineVersionDescription":"Oracle 11.2.0.2.v5"},{"Engine":"oracle-se","DBParameterGroupFamily":"oracle-se-11.2","DefaultCharacterSet":{"CharacterSetName":"AL32UTF8","CharacterSetDescription":"Unicode 5.0 UTF-8 Universal character set"},"DBEngineDescription":"Oracle Database Standard Edition","EngineVersion":"11.2.0.2.v6","DBEngineVersionDescription":"Oracle 11.2.0.2.v6"},{"Engine":"oracle-se","DBParameterGroupFamily":"oracle-se-11.2","DefaultCharacterSet":{"CharacterSetName":"AL32UTF8","CharacterSetDescription":"Unicode 5.0 UTF-8 Universal character set"},"DBEngineDescription":"Oracle Database Standard Edition","EngineVersion":"11.2.0.2.v7","DBEngineVersionDescription":"Oracle 11.2.0.2.v7"},{"Engine":"oracle-se","DBParameterGroupFamily":"oracle-se-11.2","DefaultCharacterSet":{"CharacterSetName":"AL32UTF8","CharacterSetDescription":"Unicode 5.0 UTF-8 Universal character set"},"DBEngineDescription":"Oracle Database Standard Edition","EngineVersion":"11.2.0.3.v1","DBEngineVersionDescription":"Oracle 11.2.0.3.v1"},{"Engine":"oracle-se","DBParameterGroupFamily":"oracle-se-11.2","DefaultCharacterSet":{"CharacterSetName":"AL32UTF8","CharacterSetDescription":"Unicode 5.0 UTF-8 Universal character set"},"DBEngineDescription":"Oracle Database Standard Edition","EngineVersion":"11.2.0.3.v2","DBEngineVersionDescription":"Oracle 11.2.0.3.v2"},
{"Engine":"oracle-se","DBParameterGroupFamily":"oracle-se-11.2","DefaultCharacterSet":{"CharacterSetName":"AL32UTF8","CharacterSetDescription":"Unicode 5.0 UTF-8 Universal character set"},"DBEngineDescription":"Oracle Database Standard Edition","EngineVersion":"11.2.0.4.v1","DBEngineVersionDescription":"Oracle 11.2.0.4.v1"},{"Engine":"oracle-se","DBParameterGroupFamily":"oracle-se-11.2","DefaultCharacterSet":{"CharacterSetName":"AL32UTF8","CharacterSetDescription":"Unicode 5.0 UTF-8 Universal character set"},"DBEngineDescription":"Oracle Database Standard Edition","EngineVersion":"11.2.0.4.v3","DBEngineVersionDescription":"Oracle 11.2.0.4.v3"},{"Engine":"oracle-se","DBParameterGroupFamily":"oracle-se-12.1","DefaultCharacterSet":{"CharacterSetName":"AL32UTF8","CharacterSetDescription":"Unicode 5.0 UTF-8 Universal character set"},"DBEngineDescription":"Oracle Database Standard Edition","EngineVersion":"12.1.0.1.v1","DBEngineVersionDescription":"Oracle 12.1.0.1.v1"},{"Engine":"oracle-se1","DBParameterGroupFamily":"oracle-se1-11.2","DefaultCharacterSet":{"CharacterSetName":"AL32UTF8","CharacterSetDescription":"Unicode 5.0 UTF-8 Universal character set"},"DBEngineDescription":"Oracle Database Standard Edition One","EngineVersion":"11.2.0.2.v3","DBEngineVersionDescription":"Oracle 11.2.0.2.v3"},{"Engine":"oracle-se1","DBParameterGroupFamily":"oracle-se1-11.2","DefaultCharacterSet":{"CharacterSetName":"AL32UTF8","CharacterSetDescription":"Unicode 5.0 UTF-8 Universal character set"},"DBEngineDescription":"Oracle Database Standard Edition One","EngineVersion":"11.2.0.2.v4","DBEngineVersionDescription":"Oracle 11.2.0.2.v4"},{"Engine":"oracle-se1","DBParameterGroupFamily":"oracle-se1-11.2","DefaultCharacterSet":{"CharacterSetName":"AL32UTF8","CharacterSetDescription":"Unicode 5.0 UTF-8 Universal character set"},"DBEngineDescription":"Oracle Database Standard Edition One","EngineVersion":"11.2.0.2.v5","DBEngineVersionDescription":"Oracle 11.2.0.2.v5"},
{"Engine":"oracle-se1","DBParameterGroupFamily":"oracle-se1-11.2","DefaultCharacterSet":{"CharacterSetName":"AL32UTF8","CharacterSetDescription":"Unicode 5.0 UTF-8 Universal character set"},"DBEngineDescription":"Oracle Database Standard Edition One","EngineVersion":"11.2.0.2.v6","DBEngineVersionDescription":"Oracle 11.2.0.2.v6"},{"Engine":"oracle-se1","DBParameterGroupFamily":"oracle-se1-11.2","DefaultCharacterSet":{"CharacterSetName":"AL32UTF8","CharacterSetDescription":"Unicode 5.0 UTF-8 Universal character set"},"DBEngineDescription":"Oracle Database Standard Edition One","EngineVersion":"11.2.0.2.v7","DBEngineVersionDescription":"Oracle 11.2.0.2.v7"},{"Engine":"oracle-se1","DBParameterGroupFamily":"oracle-se1-11.2","DefaultCharacterSet":{"CharacterSetName":"AL32UTF8","CharacterSetDescription":"Unicode 5.0 UTF-8 Universal character set"},"DBEngineDescription":"Oracle Database Standard Edition One","EngineVersion":"11.2.0.3.v1","DBEngineVersionDescription":"Oracle 11.2.0.3.v1"},{"Engine":"oracle-se1","DBParameterGroupFamily":"oracle-se1-11.2","DefaultCharacterSet":{"CharacterSetName":"AL32UTF8","CharacterSetDescription":"Unicode 5.0 UTF-8 Universal character set"},"DBEngineDescription":"Oracle Database Standard Edition One","EngineVersion":"11.2.0.3.v2","DBEngineVersionDescription":"Oracle 11.2.0.3.v2"},{"Engine":"oracle-se1","DBParameterGroupFamily":"oracle-se1-11.2","DefaultCharacterSet":{"CharacterSetName":"AL32UTF8","CharacterSetDescription":"Unicode 5.0 UTF-8 Universal character set"},"DBEngineDescription":"Oracle Database Standard Edition One","EngineVersion":"11.2.0.4.v1","DBEngineVersionDescription":"Oracle 11.2.0.4.v1"},{"Engine":"oracle-se1","DBParameterGroupFamily":"oracle-se1-11.2","DefaultCharacterSet":{"CharacterSetName":"AL32UTF8","CharacterSetDescription":"Unicode 5.0 UTF-8 Universal character set"},"DBEngineDescription":"Oracle Database Standard Edition One","EngineVersion":"11.2.0.4.v3","DBEngineVersionDescription":"Oracle 11.2.0.4.v3"},
{"Engine":"oracle-se1","DBParameterGroupFamily":"oracle-se1-12.1","DefaultCharacterSet":{"CharacterSetName":"AL32UTF8","CharacterSetDescription":"Unicode 5.0 UTF-8 Universal character set"},"DBEngineDescription":"Oracle Database Standard Edition One","EngineVersion":"12.1.0.1.v1","DBEngineVersionDescription":"Oracle 12.1.0.1.v1"},{"Engine":"postgres","DBEngineVersionDescription":"PostgreSQL 9.3.1-R1","DBParameterGroupFamily":"postgres9.3","DBEngineDescription":"PostgreSQL","EngineVersion":"9.3.1"},{"Engine":"postgres","DBEngineVersionDescription":"PostgreSQL 9.3.2-R1","DBParameterGroupFamily":"postgres9.3","DBEngineDescription":"PostgreSQL","EngineVersion":"9.3.2"},{"Engine":"postgres","DBEngineVersionDescription":"PostgreSQL 9.3.3-R1","DBParameterGroupFamily":"postgres9.3","DBEngineDescription":"PostgreSQL","EngineVersion":"9.3.3"},{"Engine":"postgres","DBEngineVersionDescription":"PostgreSQL 9.3.5-R1","DBParameterGroupFamily":"postgres9.3","DBEngineDescription":"PostgreSQL","EngineVersion":"9.3.5"},{"Engine":"postgres","DBEngineVersionDescription":"PostgreSQL 9.3.6-R1","DBParameterGroupFamily":"postgres9.3","DBEngineDescription":"PostgreSQL","EngineVersion":"9.3.6"},{"Engine":"postgres","DBEngineVersionDescription":"PostgreSQL 9.4.1-R1","DBParameterGroupFamily":"postgres9.4","DBEngineDescription":"PostgreSQL","EngineVersion":"9.4.1"},{"Engine":"sqlserver-ee","DBEngineVersionDescription":"SQL Server 2008 R2 10.50.2789.0.v1","DBParameterGroupFamily":"sqlserver-ee-10.5","DBEngineDescription":"Microsoft SQL Server Enterprise Edition","EngineVersion":"10.50.2789.0.v1"},{"Engine":"sqlserver-ee","DBEngineVersionDescription":"SQL Server 2012 11.00.2100.60.v1","DBParameterGroupFamily":"sqlserver-ee-11.0","DBEngineDescription":"Microsoft SQL Server Enterprise Edition","EngineVersion":"11.00.2100.60.v1"},
{"Engine":"sqlserver-ex","DBEngineVersionDescription":"SQL Server 2008 R2 10.50.2789.0.v1","DBParameterGroupFamily":"sqlserver-ex-10.5","DBEngineDescription":"Microsoft SQL Server Express Edition","EngineVersion":"10.50.2789.0.v1"},{"Engine":"sqlserver-ex","DBEngineVersionDescription":"SQL Server 2012 11.00.2100.60.v1","DBParameterGroupFamily":"sqlserver-ex-11.0","DBEngineDescription":"Microsoft SQL Server Express Edition","EngineVersion":"11.00.2100.60.v1"},{"Engine":"sqlserver-se","DBEngineVersionDescription":"SQL Server 2008 R2 10.50.2789.0.v1","DBParameterGroupFamily":"sqlserver-se-10.5","DBEngineDescription":"Microsoft SQL Server Standard Edition","EngineVersion":"10.50.2789.0.v1"},{"Engine":"sqlserver-se","DBEngineVersionDescription":"SQL Server 2012 11.00.2100.60.v1","DBParameterGroupFamily":"sqlserver-se-11.0","DBEngineDescription":"Microsoft SQL Server Standard Edition","EngineVersion":"11.00.2100.60.v1"},{"Engine":"sqlserver-web","DBEngineVersionDescription":"SQL Server 2008 R2 10.50.2789.0.v1","DBParameterGroupFamily":"sqlserver-web-10.5","DBEngineDescription":"Microsoft SQL Server Web Edition","EngineVersion":"10.50.2789.0.v1"},{"Engine":"sqlserver-web","DBEngineVersionDescription":"SQL Server 2012 11.00.2100.60.v1","DBParameterGroupFamily":"sqlserver-web-11.0","DBEngineDescription":"Microsoft SQL Server Web Edition","EngineVersion":"11.00.2100.60.v1"}]}
```
condition

```py:
def judge_mysql51(d):
    if isinstance(d, dict):
        return "mysql5.1" in d.values()
```
output

```json:
[{"DBEngineVersionDescription": "MySQL 5.1.73a", "DBEngineDescription": "MySQL Community Edition", "Engine": "mysql", "EngineVersion": "5.1.73a",
 "DBParameterGroupFamily": "mysql5.1"}, 
{"DBEngineVersionDescription": "MySQL 5.1.73b", "DBEngineDescription": "MySQL Community Edition", "Engine": "mysql", "EngineVersion": "5.1.73b",
 "DBParameterGroupFamily": "mysql5.1"}]
```

　JSONのデータが大きくても特定のデータを取得できました。

# さいごに
より詳細な記事を書きましたのでぜひ参考にしてみてください。

- [複雑なJSONから特定のデータを再帰で取り出せるようになるための4ステップ](https://jumpyoshim.hatenablog.com/entry/four-steps-to-get-specific-data-from-complex-json)
- [Pythonで再帰関数を理解するための最も簡単な例](https://jumpyoshim.hatenablog.com/entry/the-easiest-example-for-understanding-recursive-functions-in-python)

