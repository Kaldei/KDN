---
title: CURL
summary: A command line tool and library for transferring data with URL syntax.
description: A command line tool and library for transferring data with URL syntax.
tags:
  - http
---

# Resources

---

* [https://github.com/curl/curl](https://github.com/curl/curl)
* [HTTP Codes Mind Map - Ignitetechnologies](https://github.com/Ignitetechnologies/Mindmap/blob/main/HTTP%20Status%20Code/HTTP%20Status%20Codes%20UHD.png)

# Basis

---

### Basis


 > 
 > **<font color=red>curl</font> http://my.url**</br>
 > Get HTTP Content.

---

### Flags


 > 
 > **<font color=red>-s</font>**</br>
 > Silent (do not print curl info).
 > 
 > **<font color=red>-i</font>**</br>
 > Show response Headers.

 > 
 > **<font color=red>-L</font>**</br>
 > Follow redirections.

 > 
 > **<font color=red>-k</font>**</br>
 > Ignore HTTPS Errors.
 > 
 > **<font color=red>--tls-max</font> 1.2**</br>
 > Set the maximum TLS version.

 > 
 > **<font color=red>-u</font> admin<font color=red>:</font>admin**</br>
 > Provide Credentials.

 > 
 > **<font color=red>-H '</font>myHeader: myValue<font color=red>'</font>**</br>
 > Set Header.

 > 
 > **<font color=red>-X</font> POST**</br>
 > Specifies method.
 > 
 > **<font color=red>-d</font>**</br>
 > POST data.

 > 
 > **<font color=red>-o</font> myFile**</br>
 > Save response in a file.

# Examples

---

### GET current IPv4


 > 
 > **<font color=red>curl -4</font> https://ifconfig.me**</br>
 > Return current public IPv4 (`-4` force using IPv4 for hostname resolution).

---

### GET request with JWT


 > 
 > **<font color=red>curl '</font>http://\[TARGET_IP\]/api/book/1<font color=red>'  \\</font>**</br>
 > **<font color=red>-H 'Authorization: Bearer</font> \[JWT_TOKEN\]<font color=red>'</font>**</br>
 > Example GET request with JWT.

---

### POST request with JSON content


 > 
 > **<font color=red>curl '</font>http://\[TARGET_IP\]/api/auth/login<font color=red>' \\</font>**</br>
 > **<font color=red>-X POST \\</font>**</br>
 > **<font color=red>-H "Content-Type: application/json" \\</font>**</br>
 > **<font color=red>-d '{"</font>username<font color=red>":"</font>User<font color=red>","</font>password<font color=red>":"</font>P@ssw0rd<font color=red>"}'</font>**</br>
 > Example POST request with JSON content.
