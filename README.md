[TOC]

#### Ubuntu 安装

- sudo apt update ;
- sudo apt install shadowsocks-libev;

#### docker 安装
    
			 docker pull shadowsocks/shadowsocks-libev
			 docker run -e PASSWORD=<password> -p<server-port>:8388 -p<server-port>:8388/udp -d
			 shadowsocks/shadowsocks-libev

           

#### 配置
	 vim /etc/shadowsocks.json
	 {
     "server":"172.31.40.237",
     "server_port":58388,
     "local_port":1080,
     "password":"",
     "timeout":600,
     "method":"aes-256-cfb"
	}
           

#
sudo ssserver -d stop
#
ssserver -c /etc/shadowsocks.json -d start
#
vi /etc/security/limits.conf
* soft nofile 51200
* hard nofile 51200
#
vim /usr/local/lib/python2.7/dist-packages/shadowsocks/crypto/openssl.py
#
libcrypto.EVP_CIPHER_CTX_cleanup.argtypes =（c_void_p，） 
并替换为： libcrypto.EVP_CIPHER_CTX_reset.argtypes =（c_void_p，） 另外，
替换这部分： libcrypto.EVP_CIPHER_CTX_cleanup 同 libcrypto.EVP_CIPHER_CTX_reset
