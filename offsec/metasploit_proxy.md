# Setup ProxyChains

```
use multi/manage/autoroute
set session 1
exploit 


use auxiliary/server/socks_
use auxiliary/server/socks_unc    
use auxiliary/server/socks_proxy 
set srvhost 127.0.0.1
exploit -j

```
**NOTE:** You need to configure your `/etc/proxychains4.conf` by default metasploit uses port `1080` so at the end of the file you would have to add the following configuration `socks4 127.0.0.1 1080`

