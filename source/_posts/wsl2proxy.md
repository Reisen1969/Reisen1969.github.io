---
title: wsl2终端代理设置
categories: note
tags: [wsl2,proxy]
---

# wsl2终端代理设置

```
hostip=$(cat /etc/resolv.conf | grep nameserver | awk '{ print $2 }')
wslip=$(hostname -I | awk '{print $1}')
port=10809

PROXY_HTTP="http://${hostip}:${port}"

echo $PROXY_HTTP

export http_proxy="${PROXY_HTTP}"
export HTTP_PROXY="${PROXY_HTTP}"

export https_proxy="${PROXY_HTTP}"
export HTTPS_proxy="${PROXY_HTTP}"

export ALL_PROXY="${PROXY_SOCKS5}"
export all_proxy="${PROXY_SOCKS5}"

git config --global http.https://github.com.proxy ${PROXY_HTTP}
git config --global https.https://github.com.proxy ${PROXY_HTTP}

echo "Proxy has been opened."

test_proxy(){
  echo "Host IP:" ${hostip}
  echo "WSL IP:" ${wslip}
  echo "Try to connect to Google..."
  resp=$(curl -I -s --connect-timeout 5 -m 5 -w "%{http_code}" -o /dev/null www.google.com)
  if [ ${resp} = 200 ]; then
    echo "Proxy setup succeeded!"
  else
    echo "Proxy setup failed!"
  fi
}

unset_proxy(){
  unset http_proxy
  unset HTTP_PROXY
  unset https_proxy
  unset HTTPS_PROXY
  unset ALL_PROXY
  unset all_proxy
  git config --global --unset http.https://github.com.proxy
  git config --global --unset https.https://github.com.proxy

  echo "Proxy has been closed."
}
```