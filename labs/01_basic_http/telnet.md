# Using Telnet to communicate with your web server

Telnet[^1] is an application protocol for bidirectional text-otiented communication, introduced in the late 1960s - and still working.

## Simple HTTP Request

The following show how to use Telnet to communicate with any web server using HTTP.

**[ ] Start Telnet**

Start telnet by typing `telnet` into your shell:

```shell
WebDev Lab01: telnet
telnet>
```
**[ ] Connect to a server**

Connect to stackoverflow.com by opening a connection using port 80 by typing `open stackoverflow.com 80`:

```shell
telnet> open stackoverflow.com 80
Trying 151.101.129.69...
Connected to stackoverflow.com.
Escape character is '^]'.
```
By now you have established a connection to the serve on TCP level. 


**[ ] Simple HTTP request**

Send a simple request using HTTP version 1.0 by typing the two lines below. To send the request you have to enter <kbd>RETURN</kbd> twice.:

```shell
GET /questions HTTP/1.0
Host: stackoverflow.com
```
The server will send a HTTP respond similar to the one below. 

```shell
HTTP/1.1 301 Moved Permanently
cache-control: no-cache, no-store, must-revalidate
location: https://stackoverflow.com/questions
server: Microsoft-IIS/10.0
x-flags: AA
x-aspnet-duration-ms: 0
x-request-guid: e4725eff-c9c5-4180-8de7-dee98e733402
x-is-crawler: 1
x-providence-cookie: dabba25f-fd7d-df0d-89fb-a0c2ff555e23
feature-policy: microphone 'none'; speaker 'none'
content-security-policy: upgrade-insecure-requests; frame-ancestors 'self' https://stackexchange.com
Accept-Ranges: bytes
Age: 0
Accept-Ranges: bytes
Date: Thu, 22 Oct 2020 20:03:10 GMT
Via: 1.1 varnish
Age: 0
Connection: close
X-Served-By: cache-hhn4070-HHN
X-Cache: MISS
X-Cache-Hits: 0
X-Timer: S1603396991.845237,VS0,VE79
Vary: Fastly-SSL
X-DNS-Prefetch-Control: off
Set-Cookie: prov=dabba25f-fd7d-df0d-89fb-a0c2ff555e23; domain=.stackoverflow.com; expires=Fri, 01-Jan-2055 00:00:00 GMT; path=/; HttpOnly

Connection closed by foreign host.
```

**[ ] Understanding the web server's response**

While you find various depatable header fields in the response, we learn the following: 

The server let us know the requested resource has benn moved to a new location by replying with HTTP status code 301[^2].

The previous and all further request should been send to the new location at `https://stackoverflow.com/questions`.

The new location also tells us to use HTTPS instead. 

## Simple HTTPS request

While using Telnet and plain HTTP worked quite well in the past, most web servers provide secure communication ony using encryption resulting in HTTPS (Hyper Text Transfer Protocol Secure). Historically HTTPS was based on SSL certificates but is replaced by TLS certificates nowadays, offering various options for encryption such as DSA, RSA or ECC. While TLS is a more secure successor of SSL, we commonly use SSL as a synonym. 

To use SSL (or TSL) based protocols, we need to shift away from Telnet and use other tools. OpenSSL[^3] will please ou r needs as a widely adapted toolkit for such use cases. OpenSSL works similar to Telnet by handling SSL/TLS layer but allows you to fully control the superior layer where we are using HTTP.

**[ ] Start OpenSSL** 

Start OpenSSL by typing `openssl s_client -connect stackoverflow.com:443`.

While you used oprt 80 to communicate with the HTTP based web server, we are using port 443 to establish encrypted communication.

```shell
WebDev Lab01: openssl s_client -connect stackoverflow.com:443
CONNECTED(00000003)
depth=2 O = Digital Signature Trust Co., CN = DST Root CA X3
verify return:1
depth=1 C = US, O = Let's Encrypt, CN = Let's Encrypt Authority X3
verify return:1
depth=0 CN = *.stackexchange.com
verify return:1
---
Certificate chain
 0 s:CN = *.stackexchange.com
   i:C = US, O = Let's Encrypt, CN = Let's Encrypt Authority X3
 1 s:C = US, O = Let's Encrypt, CN = Let's Encrypt Authority X3
   i:O = Digital Signature Trust Co., CN = DST Root CA X3
---
Server certificate
-----BEGIN CERTIFICATE-----
MIIHJTCCBg2gAwIBAgISA/c80WOrBS1B0YKU1WnbOIwuMA0GCSqGSIb3DQEBCwUA
MEoxCzAJBgNVBAYTAlVTMRYwFAYDVQQKEw1MZXQncyBFbmNyeXB0MSMwIQYDVQQD
ExpMZXQncyBFbmNyeXB0IEF1dGhvcml0eSBYMzAeFw0yMDEwMDUxMzAyNDRaFw0y
MTAxMDMxMzAyNDRaMB4xHDAaBgNVBAMMEyouc3RhY2tleGNoYW5nZS5jb20wggEi
MA0GCSqGSIb3DQEBAQUAA4IBDwAwggEKAoIBAQDgvEf4788HVB81wIAnFbY556Qb
7BOB5IhjozLwLS9OsOAn2Dmr+P/456nysCXQAFw/Y98R+INfjTScScZa+WfKM9tk
TSLrrHuPyFQ0IEwpy59+cdnPoJQWrAu6Y0RGRv27yOOVRyeAqge2pArDiYqrc0sE
HSrBSS1wsq/nnzcaSZroL9uBqGi8hhe5GJUYk2F5EiexsYxv9jx8uLQ7vpBmk3Et
JbOlP00unQZH5Wd6swTntOhFUHSE2g3Bj3Wi/Mjhq6spTQmvjazN6+ZT6l+UEFSI
8PdlS9cH99DlPyVxiZfezobk9CGAfkhWhFRoecXKIeMGY49jUmicuZJfa5A7AgMB
AAGjggQvMIIEKzAOBgNVHQ8BAf8EBAMCBaAwHQYDVR0lBBYwFAYIKwYBBQUHAwEG
CCsGAQUFBwMCMAwGA1UdEwEB/wQCMAAwHQYDVR0OBBYEFK+7kfNW1XVWKaiJnPL+
LA+dQ6qqMB8GA1UdIwQYMBaAFKhKamMEfd265tE5t6ZFZe/zqOyhMG8GCCsGAQUF
BwEBBGMwYTAuBggrBgEFBQcwAYYiaHR0cDovL29jc3AuaW50LXgzLmxldHNlbmNy
eXB0Lm9yZzAvBggrBgEFBQcwAoYjaHR0cDovL2NlcnQuaW50LXgzLmxldHNlbmNy
eXB0Lm9yZy8wggHkBgNVHREEggHbMIIB14IPKi5hc2t1YnVudHUuY29tghIqLmJs
b2dvdmVyZmxvdy5jb22CEioubWF0aG92ZXJmbG93Lm5ldIIYKi5tZXRhLnN0YWNr
ZXhjaGFuZ2UuY29tghgqLm1ldGEuc3RhY2tvdmVyZmxvdy5jb22CESouc2VydmVy
ZmF1bHQuY29tgg0qLnNzdGF0aWMubmV0ghMqLnN0YWNrZXhjaGFuZ2UuY29tghMq
LnN0YWNrb3ZlcmZsb3cuY29tghUqLnN0YWNrb3ZlcmZsb3cuZW1haWyCDyouc3Vw
ZXJ1c2VyLmNvbYINYXNrdWJ1bnR1LmNvbYIQYmxvZ292ZXJmbG93LmNvbYIQbWF0
aG92ZXJmbG93Lm5ldIIUb3BlbmlkLnN0YWNrYXV0aC5jb22CD3NlcnZlcmZhdWx0
LmNvbYILc3N0YXRpYy5uZXSCDXN0YWNrYXBwcy5jb22CDXN0YWNrYXV0aC5jb22C
EXN0YWNrZXhjaGFuZ2UuY29tghJzdGFja292ZXJmbG93LmJsb2eCEXN0YWNrb3Zl
cmZsb3cuY29tghNzdGFja292ZXJmbG93LmVtYWlsghFzdGFja3NuaXBwZXRzLm5l
dIINc3VwZXJ1c2VyLmNvbTBMBgNVHSAERTBDMAgGBmeBDAECATA3BgsrBgEEAYLf
EwEBATAoMCYGCCsGAQUFBwIBFhpodHRwOi8vY3BzLmxldHNlbmNyeXB0Lm9yZzCC
AQMGCisGAQQB1nkCBAIEgfQEgfEA7wB1AJQgvB6O1Y1siHMfgosiLA3R2k1ebE+U
PWHbTi9YTaLCAAABdPkSXP4AAAQDAEYwRAIgVay70Cu9d46NEOmUt3XUu7bXIqkS
h+DQXw0Rdy5qIQ0CIH4GmNouXeCovRlx/T4B9Hh//+VvA1tBakgiq+6WEPR8AHYA
fT7y+I//iFVoJMLAyp5SiXkrxQ54CX8uapdomX4i8NcAAAF0+RJdVgAABAMARzBF
AiEAs4iZyvg1zC2zaFCs9CNuiGhkuD3cdmcuPCx1qi7rZqcCIAQIaxcyd5wkVWNj
1CeXrUriThrMyOElkNXaN34j3WqUMA0GCSqGSIb3DQEBCwUAA4IBAQA5BQYZcDBu
h1NnUYspMTFcuDjYSmZDlD9MBTSaA4alsHN2l+jsz/cLgPNZWdOhn1NPb6OU3x4J
AOz/4waQvqQ0VYhjBplLMiH3HPXHIiaHJw+p+Hdz0gi3gMcvuoz7ifu+9GemmdGV
wdpeGuZP4NQXJCnuNhwjrqFQHuoimKvm2M555fJB+ij+p3K2KhbQnq2BKnn2EqIR
OX9Euhv1TVpUz+rSSJJ89tIUAqzpHSS6CJt3Z3Ljgtyy1u0J1+UNlJ69JNEZIhsG
fcfc6rV6/wF3uRRBdJck9qyMCejg7NESyxTGnj+QcgbzEpMbGdzZ0PCyvaJWccl7
qysRzGiJF1WI
-----END CERTIFICATE-----
subject=CN = *.stackexchange.com

issuer=C = US, O = Let's Encrypt, CN = Let's Encrypt Authority X3

---
No client certificate CA names sent
Peer signing digest: SHA256
Peer signature type: RSA-PSS
Server Temp Key: X25519, 253 bits
---
SSL handshake has read 3671 bytes and written 412 bytes
Verification: OK
---
New, TLSv1.2, Cipher is ECDHE-RSA-AES128-GCM-SHA256
Server public key is 2048 bit
Secure Renegotiation IS supported
Compression: NONE
Expansion: NONE
No ALPN negotiated
SSL-Session:
    Protocol  : TLSv1.2
    Cipher    : ECDHE-RSA-AES128-GCM-SHA256
    Session-ID: 4BDC9F0D3403F47CD97BF9E51706D6C8803FD629613627DF1B225A945F0824E2
    Session-ID-ctx:
    Master-Key: BCFEAB426BFCB68A3004DE5258433EA6F6241C01FEA63591BBFE9B3B930DBD9238F8271A9408D932FF3F7C0E0322A26A
    PSK identity: None
    PSK identity hint: None
    SRP username: None
    TLS session ticket lifetime hint: 7200 (seconds)
    TLS session ticket:
    0000 - 51 26 2b a8 9c 8f 1f 58-8d 71 5e 67 ff da 73 37   Q&+....X.q^g..s7
    0010 - 2d 88 3a bf 48 f0 05 7a-ed 0c 19 c7 35 49 63 e9   -.:.H..z....5Ic.
    0020 - 07 17 d8 39 30 62 86 97-c0 c6 f4 87 bb dc 10 21   ...90b.........!
    0030 - 63 09 8b 9f 47 d2 e0 e1-9e 5a 0e 54 c2 52 23 2c   c...G....Z.T.R#,
    0040 - db fd 4c 39 27 50 45 51-84 04 56 80 93 af 8e 94   ..L9'PEQ..V.....
    0050 - ec cd 43 d1 8e d8 a8 65-cf 1d 81 c0 2b 20 8d f5   ..C....e....+ ..
    0060 - 99 73 40 a4 f7 d7 5e 90-e0 be a5 ad 85 27 c3 d1   .s@...^......'..
    0070 - 66 17 c8 44 5e 6a f0 eb-e3 6d 5f 0d b9 d1 d6 1f   f..D^j...m_.....
    0080 - c5 26 82 46 bf 79 ac 80-0b 9e 41 44 e3 15 bd 31   .&.F.y....AD...1
    0090 - 76 99 9a c8 e0 52 26 01-b8 07 d6 d3 c3 a5 38 08   v....R&.......8.
    00a0 - 8e 40 00 c9 a0 a2 62 a5-a8 31 4b 8e 75 44 a7 10   .@....b..1K.uD..
    00b0 - da fe 30 b9 31 45 a3 d3-06 e8 9e 35 50 5a 93 21   ..0.1E.....5PZ.!

    Start Time: 1603403425
    Timeout   : 7200 (sec)
    Verify return code: 0 (ok)
    Extended master secret: yes
---
```

Beside many othe rinformation you will get the serverside certificate as PEM-encoded[^4] certificate. Also you will see *TLSv1.2* is used for encryption. 

**[ ] Simple HTTP request**

Once the secure connection is established, perform the HTTPS request as before. In difference we will use HTTP version 1.1 instead as we already learned from the server's response before it is using HTTP verison 1.1.

```
GET /questions HTTP/1.1
Host: stackoverflow.com
```

**[ ] Receiving the web server's response**

```shell
HTTP/1.1 200 OK
Connection: keep-alive
cache-control: private
content-type: text/html; charset=utf-8
server: Microsoft-IIS/10.0
strict-transport-security: max-age=15552000
x-route-name: Questions/List
x-frame-options: SAMEORIGIN
x-sql-count: 4
x-sql-duration-ms: 6x-flags: AA
x-aspnet-duration-ms: 15
x-request-guid: 8ad58351-600f-4ef9-86cf-7bae4fac6dd5
x-is-crawler: 1
x-providence-cookie: d28f8eef-30c4-551d-2228-6736b54e9cb2
feature-policy: microphone 'none'; speaker 'none'
content-security-policy: upgrade-insecure-requests; frame-ancestors 'self' https://stackexchange.com
x-page-view: 1
Accept-Ranges: bytes
Age: 0
Accept-Ranges: bytes
Date: Thu, 22 Oct 2020 21:57:48 GMT
Via: 1.1 varnish
Age: 0
X-Served-By: cache-fra19163-FRA
X-Cache: MISS
X-Cache-Hits: 0
X-Timer: S1603403869.584131,VS0,VE108
Vary: Fastly-SSL
X-DNS-Prefetch-Control: off
Set-Cookie: prov=d28f8eef-30c4-551d-2228-6736b54e9cb2; domain=.stackoverflow.com; expires=Fri, 01-Jan-2055 00:00:00 GMT; path=/; HttpOnly
transfer-encoding: chunked

1361
<!DOCTYPE html>
    <html class="html__responsive">
    <head>
        <title>Newest Questions - Stack Overflow</title>
        ...
    </body>
    </html>
closed
```
In this particular case you should have received a `HTTP/1.1 200 OK` as well as a lenghty body containing the actual content you have requested. 

[^1]: https://tools.ietf.org/html/rfc854
[^2]: https://en.wikipedia.org/wiki/List_of_HTTP_status_codes 
[^3]: https://www.openssl.org/
[^4]: https://tools.ietf.org/html/rfc1421


