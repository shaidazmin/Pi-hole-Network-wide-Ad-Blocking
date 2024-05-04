# Pi-hole-Network-wide-Ad-Blocking
Run Pi-hole – Network-wide Ad Blocking in Docker 


```
version: "3"

# More info at https://github.com/pi-hole/docker-pi-hole/ and https://docs.pi-hole.net/
services:
  pihole:
    container_name: pihole
    image: pihole/pihole:latest
    # For DHCP it is recommended to remove these ports and instead add: network_mode: "host"
    ports:
      - "8053:53/tcp"
      - "8053:53/udp"
      - "67:67/udp" # Only required if you are using Pi-hole as your DHCP server
      - "8081:80/tcp"
    environment:
      TZ: 'America/Chicago'
      # WEBPASSWORD: 'set a secure password here or it will be random'
    # Volumes store your data between container upgrades
    volumes:
      - 'etc-pihole:/etc/pihole'
      - 'etc-dnsmasq.d:/etc/dnsmasq.d'
    #   https://github.com/pi-hole/docker-pi-hole#note-on-capabilities
    cap_add:
      - NET_ADMIN # Required if you are using Pi-hole as your DHCP server, else not needed
    restart: unless-stopped

volumes:
  etc-pihole:
  etc-dnsmasq.d:
```
