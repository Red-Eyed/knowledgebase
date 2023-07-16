```bash
for i in `ssh -Q cipher`; 
do dd if=/dev/zero bs=1M cunt=100 2> /dev/null \
  | ssh -c $i $USER@localhost "(time -p cat) > /dev/null" 2>&1 \
  | grep real | awk '{print "'$i': "100 / $2" MB/s" }'; done
```

#ssh #cipher 
