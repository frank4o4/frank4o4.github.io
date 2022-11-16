---
layout: post
title: HAPROXY Sharepoint
date: 2022-03-08 17:06
author: frank
comments: true
categories: [Linux]
---
This article covers how I setup a hproxy to serve a sharepoint farm.

&nbsp;

Using apt to install haproxy
<pre><code>apt update
apt install haproxy haproxyctl</code></pre>
haproxy.conf
<pre><code>global
    log /dev/log    local0
    log /dev/log    local1 notice
    chroot /var/lib/haproxy
    stats socket /run/haproxy/admin.sock mode 660 level admin expose-fd listeners
    stats timeout 30s
    user haproxy
    group haproxy
    daemon
    maxconn 3000
     nbproc 1
        nbthread 4
        cpu-map auto:1/1-4 0-3
    # Default SSL material locations
    ca-base /etc/ssl/certs
    crt-base /etc/ssl/private

    # Default ciphers to use on SSL-enabled listening sockets.
    # For more information, see ciphers(1SSL). This list is from:
    #  https://hynek.me/articles/hardening-your-web-servers-ssl-ciphers/
    # An alternative list with additional directives can be obtained from
    #  https://mozilla.github.io/server-side-tls/ssl-config-generator/?server=haproxy
    ssl-default-bind-ciphers ECDH+AESGCM:DH+AESGCM:ECDH+AES256:DH+AES256:ECDH+AES128:DH+AES:RSA+AESGCM:RSA+AES:!aNULL:!MD5:!DSS
    ssl-default-bind-options no-sslv3

defaults
    log    global
    mode    http
    option    httplog
    option    dontlognull
        timeout connect 5000
        timeout client  50000
        timeout server  50000
    errorfile 400 /etc/haproxy/errors/400.http
    errorfile 403 /etc/haproxy/errors/403.http
    errorfile 408 /etc/haproxy/errors/408.http
    errorfile 500 /etc/haproxy/errors/500.http
    errorfile 502 /etc/haproxy/errors/502.http
    errorfile 503 /etc/haproxy/errors/503.http
    errorfile 504 /etc/haproxy/errors/504.http


backend sharepoint
    fullconn   3000
        balance leastconn
        option redispatch
        cookie SERVERID insert nocache
        server spweb1      192.168.x.x:80  cookie spweb1 weight 30 check minconn 100 maxconn 1500
        server spweb2      192.168.x.x:80  cookie spweb2 weight 30 check minconn 100 maxconn 1500

frontend httpid
    maxconn 3000
        bind 192.168.x.x:80
        acl hosts_sharepoint hdr_end(host) -i intranet.example.com
        acl hosts_sharepoint hdr_end(host) -i intranet.example:80
     acl hosts_sharepoint hdr_end(host) -i teamsite.example.com
        acl hosts_sharepoint hdr_end(host) -i teamsite.example.com:80
    use_backend sharepoint if hosts_sharepoint
        default_backend sharepoint
    option forwardfor



frontend stats
    bind 192.168.x.x:8404
    stats enable
    stats uri /stats
    stats refresh 10s
    #stats admin if LOCALHOST
</code></pre>
Setup Keepalive to be able have floating virtual IP Addresses between two haproxy servers
<pre><code>apt install keepalived</code></pre>
After keepalived is installed we will need to alter some kernel parameters.
<pre><code>    sed -i 's/#net.ipv4.ip_forward=1/net.ipv4.ip_forward=1/' /etc/sysctl.conf</code></pre>
Similarly, you need to enable HAProxy and Keepalived to bind to non-local IP address, that is to bind to the failover IP address (Floating IP).
<pre><code>    echo "net.ipv4.ip_nonlocal_bind = 1" &gt;&gt; /etc/sysctl.conf
    Reload sysctl settings;
    sysctl -p</code></pre>
Configure Keepalived The default configuration file for Keepalived should be /etc/keepalived/keepalived.conf. However, this configuration is not created by default. Create the configuration with the content below;
<pre><code>    nano -w /etc/keepalived/keepalived.conf</code></pre>
nlb1 configuration
<pre><code>
global_defs {
    notification_email {
        support@example.com     # Email address for notifications
    }
    notification_email_from nlb@example.com        # The from address for the notifications
    smtp_server 192.168.x.x                             # SMTP server address
    smtp_connect_timeout 15
}


vrrp_script chk_haproxy {
    script "/usr/bin/killall -0 haproxy"
    interval 2
    weight 2
}

vrrp_instance LB_VIP {
    interface eth0
    state MASTER
    priority 100
    virtual_router_id 51

    smtp_alert

    authentication {
        auth_type PASS
        auth_pass somepassword
    }
    unicast_src_ip 192.168.x.x # Private IP address of the master haproxy
    unicast_peer {
        192.168.x.x    # Private IP address of the master haproxy
   }

    virtual_ipaddress {
        192.168.x.x
    }

    track_script {
        chk_haproxy
    }
}</code></pre>
nlb2 configuration
<pre><code>global_defs {
    notification_email {
        support@example.com     # Email address for notifications
    }
    notification_email_from nlb@example.com        # The from address for the notifications
    smtp_server 192.168.x.x                             # SMTP server address
    smtp_connect_timeout 15
}


vrrp_script chk_haproxy {
    script "/usr/bin/killall -0 haproxy"
    interval 2
    weight 2
}

vrrp_instance LB_VIP {
    interface eth0
    state BACKUP
    priority 100
    virtual_router_id 51

    smtp_alert

    authentication {
        auth_type PASS
        auth_pass somepassword
    }
    unicast_src_ip 192.168.x.x # Private IP address of the backup haproxy
    unicast_peer {
        192.168.x.x    # Private IP address of the master haproxy
   }

    virtual_ipaddress {
        192.168.x.x
    }

    track_script {
        chk_haproxy
    }
}

</code></pre>
Now start keepalived on both nodes
<pre><code>    systemctl enable --now keepalived</code></pre>
Needed to install this on both nodes to have killall script
<pre><code>     apt install psmisc</code></pre>
<blockquote>Using haproxyctl functions</blockquote>
<pre><code>root@nlb1:/etc/haproxy# haproxyctl show health
# pxname                       svname                         status  weight
sharepoint                     spweb1                     UP       30
sharepoint                     spweb2                     UP       30
sharepoint                     BACKEND                        UP       60
httpid                         FRONTEND                       OPEN
stats                          FRONTEND                       OPEN


root@brm-nlb1:/etc/haproxy# haproxyctl disable server sharepoint/spweb2

root@brm-nlb1:/etc/haproxy# haproxyctl show health
# pxname                       svname                         status  weight
sharepoint                     spweb1                     UP       30
sharepoint                     spweb2                     MAINT    30
sharepoint                     BACKEND                        UP       30
httpid                         FRONTEND                       OPEN
stats                          FRONTEND                       OPEN


root@brm-nlb1:/etc/haproxy# haproxyctl enable server sharepoint/spweb2

root@brm-nlb1:/etc/haproxy# haproxyctl show health
# pxname                       svname                         status  weight
sharepoint                     spweb1                     UP       30
sharepoint                     spweb2                     UP       30
sharepoint                     BACKEND                        UP       60
httpid                         FRONTEND                       OPEN
stats                          FRONTEND                       OPEN</code></pre>
&nbsp;
