## mailbox send

Send paper

### Synopsis


寄送電子報，處理開信連結與替換點擊連結。

```
mailbox send [flags]
```

### Examples

```
群組寄送：mailbox send -p {path} -s 'Title: #1' -g {group} --cid {cid}
個人寄送：mailbox send -p {path} -s 'Title: #1' --uid='6,12' --cid {cid}
```

### Options

```
      --cid string       Campaign ID
  -d, --dryrun           Dry run
  -g, --groups string    User groups
  -h, --help             help for send
  -p, --path string      HTML file path
      --rl               Replace A tag links (default true)
  -s, --subject string   Mail subject
      --uid string       User ID, support more by splited with ','
```

### Options inherited from parent commands

```
      --config string   config file (default is $HOME/.mailbox.yaml)
```

### SEE ALSO
* [mailbox](mailbox.md)	 - 簡易電子報發送系統

###### Auto generated by spf13/cobra on 29-Jun-2017
