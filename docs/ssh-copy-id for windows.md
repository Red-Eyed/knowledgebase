There is no `ssh-copy-id` on Windows.\
Here is `ssh-copy-id` in `PowerShell` (don't forget to change `USER` and `HOST` values):

```shell
type ~/.ssh/id_rsa.pub | `
ssh USER@HOST `
"mkdir -p ~/.ssh && chmod 700 ~/.ssh && LANG=C sed 's/[\d128-\d255]//g' >> ~/.ssh/authorized_keys && chmod 600 ~/.ssh/authorized_keys"
```