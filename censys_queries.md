#### Basic Search Syntax

| OpenDir + C2                | labels:"open-dir" and "c2"                                                                      |
| --------------------------- | ----------------------------------------------------------------------------------------------- |
| OpenDir + "exe" keyword     | labels:"open-dir" and services.http.response.body:"exe"                                         |
| OpenDir + "exploit" keyword | labels:"open-dir" and services.http.response.body:"exploit"                                     |
| OpenDir + "beacon" keyword  | labels:"open-dir" and services.http.response.body:"beacon"                                      |
| Python servers              | (labels:"open-dir" and services.http.response.body:"exe" and services.software.product=`python` |
| OpenDir + "payload" keyword | labels:"open-dir" and services.http.response.body:"payload"                                     |
| JARM Fingerprint            | services.jarm.fingerprint:                                                                      |
| TLS Certificate             | services.certificate:                                                                           |
| ASN<br>                     | autonomous_system.name                                                                          |
| Subject CN                  | services.tls.certificates.leaf_data.subject_dn                                                  |
| Issuer CN                   | services.tls.certificates.leaf_data.issuer_dn                                                   |
| Find Botnets                | services.http.response.body:"botnet"                                                            |
| Find DDoS                   | services.http.response.body:"stressor"                                                          |

# C2 Frameworks
### Cobalt Strike

| Censys | services.tls.certificates.leaf_data.issuer.common_name="Major Cobalt Strike"                                                                                                                                                                                                                                                                                 |
| ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Censys | services.certificate: {  <br>"64257fc0fac31c01a5ccd816c73ea86e639260da1604d04db869bb603c2886e6",  <br>"87f2085c32b6a2cc709b365f55873e207a9caa10bffecf2fd16d3cf9d94d390c"  <br>}  <br>OR services.tls.certificates.leaf_data.issuer.common_name: "Major Cobalt Strike"  <br>OR services.tls.certificates.leaf_data.subject.common_name: "Major Cobalt Strike" |


### Mythic

| Censys | services.http.response.html_title="Mythic"                                                                                                                                                                                                                                                                |
| ------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Censys | same_service(services.tls.certificates.leaf_data.subject_dn="O=Mythic" AND services.http.response.html_title="Mythic") OR services.banner_hashes="sha256:fb8b5d212f449a8ba61ab9ed9b44853315c33d12a07f8ce4642892750e251530" OR services.http.response.favicons.md5_hash="6be63470c32ef458926abb198356006c" |
| Censys | same_service(services.tls.certificates.leaf_data.subject_dn="O=Mythic" AND services.http.response.html_title="Mythic") OR services.banner_hashes="sha256:fb8b5d212f449a8ba61ab9ed9b44853315c33d12a07f8ce4642892750e251530" OR services.http.response.favicons.md5_hash="6be63470c32ef458926abb198356006c" |

### Metasploit

| Censys | services.http.response.html_title: "Metasploit" AND (  <br>services.tls.certificates.leaf_data.subject.organization: "Rapid7"  <br>OR services.tls.certificates.leaf_data.subject.common_name: "MetasploitSelfSignedCA"  <br>)  <br>OR services.jarm.fingerprint: {  <br>"07d14d16d21d21d00042d43d000000aa99ce74e2c6d013c745aa52b5cc042d",  <br>"07d14d16d21d21d07c42d43d000000f50d155305214cf247147c43c0f1a823"  <br>} |
| ------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Censys | services.http.response.html_title: "Metasploit"                                                                                                                                                                                                                                                                                                                                                                         |

### Sliver
| Censys | services.tls.certificates.leaf_data.subject_dn:"multiplayer"                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
| ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------ |
| Censys | same_service(  <br>services.tls.certificates.leaf_data.pubkey_bit_size: 2048 and  <br>services.tls.certificates.leaf_data.subject.organization: /(ACME\|Partners\|Tech\|Cloud\|Synergy\|Test\|Debug)? ?(co\|llc\|inc\|corp\|ltd)?/ and  <br>services.jarm.fingerprint: 3fd21b20d00000021c43d21b21b43d41226dd5dfc615dd4a96265559485910 and  <br>services.tls.certificates.leaf_data.subject.country: US and  <br>services.tls.certificates.leaf_data.subject.postal_code: /<1001-9999>/  <br>)                                                                                                                                                                                                                                                                                                                                                                                        |
| Censys | (services.tls.certificates.leaf_data.subject.common_name="multiplayer" and same_service(services.jarm.fingerprint= 00000000000000000043d43d00043de2a97eabb398317329f027c66e4c1b01 and NOT services.port=31337 )) OR (services.banner_hashes="sha256:1f25c454ae331c582fbdb7af8a9839785a795b06a6649d92484b79565f7174ae" and services.jarm.fingerprint=3fd21b20d00000021c43d21b21b43d41226dd5dfc615dd4a96265559485910) OR same_service(services.tls.certificates.leaf_data.pubkey_bit_size: 2048 and services.tls.certificates.leaf_data.subject.organization: /(ACME\|Partners\|Tech\|Cloud\|Synergy\|Test\|Debug)? ?(co\|llc\|inc\|corp\|ltd)?/ and services.jarm.fingerprint: 3fd21b20d00000021c43d21b21b43d41226dd5dfc615dd4a96265559485910 and services.tls.certificates.leaf_data.subject.country: US and services.tls.certificates.leaf_data.subject.postal_code: /<1001-9999>/) |

### Havoc

| Censys | services.banner: "X-Havoc" |
| ------ | -------------------------- |

### Empire

| Censys | same_service(  <br>services.http.response.body_hash: {"sha1:bc517bf173440dad15b99a051389fadc366d5df2", "sha1:dcb32e6256459d3660fdc90e4c79e95a921841cc"}  <br>AND services.http.response.headers.expires: 0  <br>AND services.http.response.headers.cache_control: "*"  <br>) |
| ------ | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
### Viper

| Censys | services.software.product: Viper                                                                                                                                  |
| ------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Censys | services.http.response.body_hashes="sha1:cd40dbcdae84b1c8606f29342066547069ed5a33" OR services.http.response.favicons.md5_hash="a7469955bff5e489d2270d9b389064e1" |
### Covenant

| Censys | same_service(  <br>http.response.body: {"Blazor", "covenant.css"}  <br>AND tls.certificates.leaf_data.issuer.common_name: "Covenant"  <br>)                                                                                                     |
| ------ | ----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| Censys | same_service(services.tls.certificates.leaf_data.subject_dn="CN=Covenant" AND services.tls.certificates.leaf_data.issuer_dn="CN=Covenant") OR (services.software.product="Kestrel web server" AND services.http.response.html_title="Covenant") |
| Shodan | http.favicon.hash:-737603591<br>ssl:Covenant http.component:Blazor                                                                                                                                                                              |
### SuperShell 

| Censys | services.http.response.html_title="Supershell - 登录" OR services.http.response.body_hashes="sha256:21ec9c71669486c5b874b1be3b9c341133e83939fdbeefa2080df1b1703c4928" |
| ------ | ------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
### Brute Ratel

| Censys | services.http.response.body_hash="sha1:1a279f5df4103743b823ec2a6a08436fdf63fe30" OR same_service(services.http.response.body_hash="sha1:bc3023b36063a7681db24681472b54fa11f0d4ec" and services.jarm.fingerprint="3fd21b20d00000021c43d21b21b43de0a012c76cf078b8d06f4620c2286f5e") |
| ------ | --------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

### PenTera Red Team

| Censys | services.certificate:'5af04204203d6a96fae375b8be231f1f0dae750713d68a5a6c07f678dbd0aae8' |
| ------ | --------------------------------------------------------------------------------------- |
| Censys | services.http.response.html_title="Pentera™"                                            |
