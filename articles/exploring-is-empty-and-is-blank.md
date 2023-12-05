---
title: "Java：isEmptyとisBlankの違い"
emoji: "👏"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: []
published: false
---
普段、Java開発者としての皆は**isEmpty/isNotEmpty/isNotBlank/isBlank**が知っている方が多いですが、**isAnyEmpty/isNoneEmpty/isAnyBlank/isNoneBlank**が知らない方も少なくないかもしれません。では、`org.apache.commons.lang3.StringUtils`を一緒に探索しましょうか。
# isEmpty系
## StringUtils.isEmpty()
文字列が「空文字」かのチェックですが、「空文字」ではなく「スペース」のある場合に`isEmpty(" ")=false`となります。
```java
StringUtils.isEmpty(null) = true
StringUtils.isEmpty("") = true
StringUtils.isEmpty(" ") = false
StringUtils.isEmpty("bob") = false
StringUtils.isEmpty(" bob ") = false
```
## StringUtils.isNotEmpty()
`StringUtils.isEmpty()`と逆です。
```java
StringUtils.isEmpty(null) = false
StringUtils.isEmpty("") = false
StringUtils.isEmpty(" ") = true
StringUtils.isEmpty("bob") = true
StringUtils.isEmpty(" bob ") = true
```
## StringUtils.isAnyEmpty()
複数の文字列にいずれか「空文字」があれば、`true`になります。
```java
StringUtils.isAnyEmpty(null) = true
StringUtils.isAnyEmpty(null, "foo") = true
StringUtils.isAnyEmpty("", "bar") = true
StringUtils.isAnyEmpty("bob", "") = true
StringUtils.isAnyEmpty(" bob ", null) = true
StringUtils.isAnyEmpty(" ", "bar") = false
StringUtils.isAnyEmpty("foo", "bar") = false
```
## StringUtils.isNoneEmpty()
`StringUtils.isAnyEmpty()`と逆です。文字列は全部「空文字」ではなければ、`true`になります。
```java
StringUtils.isAnyEmpty(null) = false
StringUtils.isAnyEmpty(null, "foo") = false
StringUtils.isAnyEmpty("", "bar") = false
StringUtils.isAnyEmpty("bob", "") = false
StringUtils.isAnyEmpty(" bob ", null) = false
StringUtils.isAnyEmpty(" ", "bar") = true
StringUtils.isAnyEmpty("foo", "bar") = true
```
# isBlank系
## StringUtils.isBlank()
文字列は「スペースまたは空文字」かどうかのチェックです。
```java
StringUtils.isBlank(null) = true
StringUtils.isBlank("") = true
StringUtils.isBlank(" ") = true
StringUtils.isBlank("bob") = false
StringUtils.isBlank(" bob ") = false
```
## StringUtils.isNotBlank()
`StringUtils.isBlank()`と逆です。
```java
StringUtils.isBlank(null) = false
StringUtils.isBlank("") = false
StringUtils.isBlank(" ") = false
StringUtils.isBlank("bob") = true
StringUtils.isBlank(" bob ") = true
```
##　StringUtils.isAnyBlank()
複数の文字列にいずれか「スペースまたは空文字」があれば、`true`になります。
```java
StringUtils.isAnyBlank(null) = true
StringUtils.isAnyBlank(null, "foo") = true
StringUtils.isAnyBlank(null, null) = true
StringUtils.isAnyBlank("", "bar") = true
StringUtils.isAnyBlank("bob", "") = true
StringUtils.isAnyBlank(" bob ", null) = true
StringUtils.isAnyBlank(" ", "bar") = true
StringUtils.isAnyBlank("foo", "bar") = false
```
##　StringUtils.isAnyBlank()
`StringUtils.isAnyBlank()`と逆です。文字列は全部「スペースまたは空文字」ではなければ、`true`になります。
```java
StringUtils.isAnyBlank(null) = false
StringUtils.isAnyBlank(null, "foo") = false
StringUtils.isAnyBlank(null, null) = false
StringUtils.isAnyBlank("", "bar") = false
StringUtils.isAnyBlank("bob", "") = false
StringUtils.isAnyBlank(" bob ", null) = false
StringUtils.isAnyBlank(" ", "bar") = false
StringUtils.isAnyBlank("foo", "bar") = true
```
