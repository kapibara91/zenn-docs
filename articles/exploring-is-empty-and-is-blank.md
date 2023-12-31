---
title: "Java：isEmptyとisBlankの違い"
emoji: "👏"
type: "tech" # tech: 技術記事 / idea: アイデア
topics: ["java"]
published: true
---
# はじめに
普段、Java開発者としての皆は**isEmpty/isNotEmpty/isNotBlank/isBlank**が知っている方が多いですが、**isAnyEmpty/isNoneEmpty/isAnyBlank/isNoneBlank**が知らない方も少なくないかもしれません。それを一緒に探索しましょう。
# isEmpty
## StringUtils.isEmpty()
文字列が「**NULL**、**空文字**」かのチェックですが、「**空文字**」ではなく「**スペース**」のある場合に`isEmpty(" ")=false`となります。
```java
StringUtils.isEmpty(null) = true
StringUtils.isEmpty("") = true
StringUtils.isEmpty(" ") = false
StringUtils.isEmpty("bob") = false
StringUtils.isEmpty(" bob ") = false
```
## StringUtils.isNotEmpty()
`StringUtils.isEmpty()`とは逆です。
```java
StringUtils.isNotEmpty(null) = false
StringUtils.isNotEmpty("") = false
StringUtils.isNotEmpty(" ") = true
StringUtils.isNotEmpty("bob") = true
StringUtils.isNotEmpty(" bob ") = true
```
## StringUtils.isAnyEmpty()
複数の文字列にいずれか「**NULL**、**空文字**」があれば、`true`になります。
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
`StringUtils.isAnyEmpty()`とは逆です。複数の文字列に「**NULL**、**空文字**」がなければ、`true`になります。
```java
StringUtils.isNoneEmpty(null) = false
StringUtils.isNoneEmpty(null, "foo") = false
StringUtils.isNoneEmpty("", "bar") = false
StringUtils.isNoneEmpty("bob", "") = false
StringUtils.isNoneEmpty(" bob ", null) = false
StringUtils.isNoneEmpty(" ", "bar") = true
StringUtils.isNoneEmpty("foo", "bar") = true
```
# isBlank
## StringUtils.isBlank()
文字列は「**NULL**、**スペース**または**空文字**」かどうかのチェックです。
```java
StringUtils.isBlank(null) = true
StringUtils.isBlank("") = true
StringUtils.isBlank(" ") = true
StringUtils.isBlank("bob") = false
StringUtils.isBlank(" bob ") = false
```
## StringUtils.isNotBlank()
`StringUtils.isBlank()`とは逆です。
```java
StringUtils.isNotBlank(null) = false
StringUtils.isNotBlank("") = false
StringUtils.isNotBlank(" ") = false
StringUtils.isNotBlank("bob") = true
StringUtils.isNotBlank(" bob ") = true
```
## StringUtils.isAnyBlank()
複数の文字列にいずれか「**NULL**、**スペース**または**空文字**」があれば、`true`になります。
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
## StringUtils.isNoneBlank()
`StringUtils.isAnyBlank()`とは逆です。複数の文字列に「**NULL**、**スペース**または**空文字**」がなければ、`true`になります。
```java
StringUtils.isNoneBlank(null) = false
StringUtils.isNoneBlank(null, "foo") = false
StringUtils.isNoneBlank(null, null) = false
StringUtils.isNoneBlank("", "bar") = false
StringUtils.isNoneBlank("bob", "") = false
StringUtils.isNoneBlank(" bob ", null) = false
StringUtils.isNoneBlank(" ", "bar") = false
StringUtils.isNoneBlank("foo", "bar") = true
```
