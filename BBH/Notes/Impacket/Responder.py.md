
## Starting command

```bash
sudo responder -I eth0
```

## Common Options

- **Enable WPAD (Web Proxy Auto-Discovery) Poisoning:**  
    `sudo responder -I eth0 -w`
- **Force Authentication for NBT-NS/LLMNR:**  
    `sudo responder -I eth0 -f`
- **Run with Verbose Output:**  
    `sudo responder -I eth0 -v`
- **Run All Options (Recommended for testing):**  
    `sudo responder -I eth0 -dwv`