# pivot

```mermaid 
flowchart LR
    subgraph a[WAN]
        direction LR
        A[KALI] --- B[Service]
        subgraph b[DMZ]
            B --- C[DB]
        end
    end
```
- If `B[Service]` / `Service` has 2 network interfaces. One on `WAN` and one on `DMZ` then we can that `Service` is **straddling** both the WAN and DMZ. 


## Linux 



## Windows
