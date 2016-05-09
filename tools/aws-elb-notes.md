# AWS ELB Notes

- ELBs can be internally facing or public internet facing. Internally facing ELBs will contain `internal` as part of the name.
- A hosted zone `my_domain.com.` can contain an A record (ALIAS) that points to public ELB
  - From there, all instances behind ELB are accessible from internet, can use auth for example to restrict access
- For private ELBs, a similar thing can be done, create an A record (ALIAS) or CNAME
- For VPN, here's one way to do it (minus all the cert setup):
  - Setup `vpn` EC2 instance/SG, opening up correct ports for VPN configuration
  - Create an `ssh` SG, allowing all traffic from the VPN SG and TCP port 22 traffic from all other locations
  - Setup VPN client (i.e. Tunnelblick) to point to public IP of EC2 instance
  
[reference](https://aws.amazon.com/elasticloadbalancing/)
