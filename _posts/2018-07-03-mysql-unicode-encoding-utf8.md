---
layout: post
title: "MySQL Unicode Encoding: utf8 vs utf8mb4"
date: 2018-07-03 23:00:00 +0100
category: tutorial
tagline: ""
tags: [Database, MySQL, Unicode]
---
{% include JB/setup %}

* [Background](#background)
  * [UTF-8](#utf-8)
  * [utf8 in MySQL](#utf8-in-mysql)
* [UTF-8 in MySQL](#utf-8-in-mysql)
  * [MySQL's utf8mb4](#mysqls-utf8mb4)
  * [Switching from utf8mb3 to utf8mb4](#switching-from-utf8mb3-to-utf8mb4)
* [Summary](#summary)
* [References](#references)

## Background

### UTF-8

Before discussing about the problem of UTF-8 encoding in MySQL, I will make a brief introduction to UTF-8.

ISO 10646 defines a large set of characters called Universal Character Set (UCS). There is also another same set of characters (Unicode) which is defined by the Unicode Standard. But in fact, these two sets are not exactly the same.
Then ISO 10646 and Unicode define several encoding forms of their common repertoire. UTF-8 is one of those.

UTF-8 is short for Unicode Transformation Format-8-bit.
It is a variable width character encoding, characters ranging from U+0000 to U+10FFFF and using sequences of 1 to 4 octets.
The table below shows the format of coding for different octet types. The letter x represents the bits available for encoding bits.

| Bytes | Char range (hexadecimal) | UTF-8 octet sequence |
|------|------|------|
| 1 | 0000 0000-0000 007F | 0xxxxxxx |
| 2 | 0000 0080-0000 07FF | 110xxxxx 10xxxxxx |
| 3 | 0000 0800-0000 FFFF | 1110xxxx 10xxxxxx 10xxxxxx |
| 4 | 0001 0000-0010 FFFF | 11110xxx 10xxxxxx 10xxxxxx 10xxxxxx |

More detailed information could be found in [RFC 3629](https://www.rfc-editor.org/info/rfc3629){:target="_blank"}.

### utf8 in MySQL

I think many people including me used MySQL's `utf8` charset in MySQL, because we think this `utf8` is the same as the UTF-8 encoding.

However, according to the official manual in MySQL, MySQL's `utf8` charset only implements some parts of the whole UTF-8 encoding and it only uses 1 to 3 bytes for encoding. So when you try to use some characters occupying 4 bytes, those characters cannot be stored and there are some warnings.

Try the commands in MySQL below:

```sql
SET NAMES utf8;

UPDATE [db_name].[table_name] SET [column_name] = 'foo𝌆bar' WHERE id = 9001;

SELECT [column_name] FROM [db_name].[table_name] WHERE id = 9001;

SHOW WARNINGS;
```

In MySQL, `utf8` is an alias for `utf8mb3`.


## UTF-8 in MySQL

Luckily, MySQL (version 5.5.3 or later) provides another better and larger charset.
You could use `SHOW CHARACTER SET;` to check all the available character sets in your MySQL.

### MySQL's utf8mb4

If you want to use more UTF-8 encoding characters, you could use MySQL's `utf8mb4`.
For the Basic Multilingual Plane (BMP) characters, `utf8mb4` and `utf8mb3` have identical storage characteristics: same code values, same encoding, same length.
For a supplementary character, `utf8mb4` using 4 bytes to store it could store more when `utf8mb3` cannot at all.

### Switching from utf8mb3 to utf8mb4

If your database is using `utf8` charset, you could try to switch it to `utf8mb4` charset.

1. Create a backup. Always, keep that in mind - create a backup.
2. Upgrade the MySQL server if the version of your MySQL is older than 5.5.3.
3. Modify databases, tables and columns. Use the commands below:
```sql
# For each database:
ALTER DATABASE [db_name] CHARACTER SET = utf8mb4 COLLATE = utf8mb4_unicode_ci;
# For each table:
ALTER TABLE [table_name] CONVERT TO CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
# For each column:
ALTER TABLE [table_name] CHANGE [column_name] [column_name] VARCHAR(191) CHARACTER SET utf8mb4 COLLATE utf8mb4_unicode_ci;
```
4. Check the maximum length of columns and index keys. This is because `utf8mb4` allows 4 bytes at maximum instead of 3 bytes and it would lead to that the columns or index keys store less characters than before.
5. Modify connection, client and server character sets. In application, use `SET NAMES utf8mb4` or `SET NAMES utf8mb4 COLLATE utf8mb4_unicode_ci`. In the server, modify the configuration file (my.cnf) and update "default-character-set=utf8mb4" for client, mysql and mysqld.
6. Repair and optimize all tables using the commands:
```sql
REPAIR TABLE [table_name];
OPTIMIZE TABLE [table_name];
```


## Summary

In a conclusion, I think it would be better to use `utf8mb4` instead of `utf8` if you don't need to consider so much about the storage limitation.


## References

1. [UTF-8, a transformation format of ISO 10646. No. RFC 3629. 2003](https://www.rfc-editor.org/info/rfc3629)
2. [How to support full Unicode in MySQL databases](https://mathiasbynens.be/notes/mysql-utf8mb4)
3. [MySQL 5.5 Reference Manual: The utf8mb4 Character Set (4-Byte UTF-8 Unicode Encoding)](https://dev.mysql.com/doc/refman/5.5/en/charset-unicode-utf8mb4.html)
4. [MySQL 5.5 Reference Manual: The utf8mb3 Character Set (3-Byte UTF-8 Unicode Encoding) ](https://dev.mysql.com/doc/refman/5.5/en/charset-unicode-utf8mb3.html)
