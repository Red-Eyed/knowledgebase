```bash
for i in `ssh -Q cipher`;
do dd if=/dev/zero bs=1M count=100 2> /dev/null | \
ssh -c $i $USER@localhost \
"python3 -c 'import sys, time; s=time.time(); sys.stdin.read(); print(f\"$i {100 / (time.time() - s):0.2f} MB/s\")'"
done
```

To make it work on localhost without passwords, you can add hosts' public key to autorized_keys:
```bash
cat ~/.ssh/id_rsa.pub >> ~/.ssh/authorized_keys
```

#ssh #cipher 
