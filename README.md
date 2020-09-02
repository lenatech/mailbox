你好！
很冒昧用这样的方式来和你沟通，如有打扰请忽略我的提交哈。我是光年实验室（gnlab.com）的HR，在招Golang开发工程师，我们是一个技术型团队，技术氛围非常好。全职和兼职都可以，不过最好是全职，工作地点杭州。
我们公司是做流量增长的，Golang负责开发SAAS平台的应用，我们做的很多应用是全新的，工作非常有挑战也很有意思，是国内很多大厂的顾问。
如果有兴趣的话加我微信：13515810775  ，也可以访问 https://gnlab.com/，联系客服转发给HR。
Mailbox  [![GitHub release](https://img.shields.io/github/release/toomore/mailbox.svg)](https://github.com/toomore/mailbox/releases) [![license](https://img.shields.io/github/license/toomore/mailbox.svg)](https://github.com/toomore/mailbox/blob/master/LICENSE)
=====================
簡易電子報發送系統，使用 Golang 實作。建立發送 `campaign` 資訊、匯入訂閱者資訊（群組標記）、簡易發送系統、開信追蹤與連結點擊追蹤。

以 docker container 運行。

Cmd
----
1. `mailbox campaign`：建立 `campaign`，包含產生該 `campaign` 的亂數種子。
2. `mailbox user`：匯入訂閱者的資訊。
3. `mailbox send`：發送電子報，以 **HTML** 格式發送。
4. `mailbox server`：接收開信訊息。

相關的操作請參考 `-h` 的說明，或 [cmd/docs](cmd/docs/mailbox.md)

Build Docker Image
-------------------
### `toomore/mailbox:base`
將基本的程式碼放入，相關的套件也一併下載。

    sh ./build-base.sh

### `toomore/mailbox:cmd`
只將編譯過的 `cmd` 程式放入。

    sh ./build-min.sh;

Required
---------
1. AWS SES `KEY`, `Token`.
2. Update `./Makefile run_cmd`, `./dev-run-cmd.sh` files.
    1. `mailbox_ses_key`：AWS SES KEY
    2. `mailbox_ses_token`：AWS SES Token
    3. `mailbox_ses_sender`：發送者的 `email`。如：`Toomore Chiang <toomore0929@gmail.com>`.
    4. `mailbox_web_site`：接收開信網址，不包含 `https` 與結尾。如：`open.example.com`.
3. Nginx

Nginx config
-------------
需加入以下資訊到網域設定檔。

    proxy_set_header X-Real-IP $remote_addr;
    proxy_set_header X-Forwarded-For $proxy_add_x_forwarded_for;
    proxy_set_header X-Args $query_string;
    proxy_set_header X-Uri $uri;

Run
----
Into container

    make run_cmd

Support bash-completion

    mailbox [tab][tab]
    campaign  send      server    user

... and pretty help (using [spf13/cobra](https://github.com/spf13/cobra))

    mailbox -h

Import User data from csv
--------------------------
匯入訂閱者資訊與建立 csv 檔案，檔案內需包含 `email`, `groups`, `f_name`, `l_name` 欄位。

    mailbox user import ./list.csv

可以使用 `-d` 來預覽資料讀取狀況

    mailbox user import ./list.csv -d
    ...
