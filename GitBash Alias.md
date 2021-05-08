### 建立 bash 快捷鍵 alias
`alias alias_name="command_to_run"`
為了要建立永久的 alias ，要在原資料夾下面建立 `.bash_profile` 或 `.bashrc` 檔案
裡面設定
```sh
# Aliases
# alias alias_name="command_to_run"

# Long format list
alias ll="ls -la"

# Print my public IP
alias myip='curl ipinfo.io/ip'
```