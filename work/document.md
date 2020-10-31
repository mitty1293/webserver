# main.c の解説
## ソケットを作る
```c
int rsock
rsock = socket(AF_INET, SOCK_STREAM, 0);
```

## ソケットにアドレスを割り当てる
```c
struct sockaddr_in addr;
 
/* socket setting */
addr.sin_family      = AF_INET;
addr.sin_port        = htons(8080);
addr.sin_addr.s_addr = INADDR_ANY;
 
/* binding socket */    
bind(rsock, (struct sockaddr *)&addr, sizeof(addr));
```

## 接続を待ち受ける
```c
listen(rsock, 5);
```

## 接続を受け付ける
```c
int wsock;
int len;
struct sockaddr_in client;
 
len = sizeof(client);
wsock = accept(rsock, (struct sockaddr *)&client, &len);
```

## データを書き込む
```c
write(wsock, "HTTP1.1 200 OK", 14);
```

# 実際に通信してみる
```c
# gcc main.c
# ./a.out
```