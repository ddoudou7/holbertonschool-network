# What happens when you type `https://www.google.com` and press Enter

This is a classic interview question that many engineers face. It’s designed to check if you understand how the internet and web infrastructure really work. Let’s walk step by step, like a story, from your keyboard all the way to Google’s servers and back.

## 1. DNS request
Your browser doesn’t yet know where “www.google.com” lives. So it asks: “who has the IP of this domain?”. It first checks your cache, then your operating system, then it asks a DNS resolver (like your ISP’s or Google DNS). The resolver goes on a journey: root → .com TLD → Google’s authoritative servers. Finally, it comes back with an IP.

## 2. TCP/IP handshake
Now that we have the address, it’s time to knock on Google’s door. Using TCP, your machine sends a SYN packet, Google replies SYN-ACK, you answer ACK. Boom, a reliable connection is established, all wrapped in IP packets.

## 3. Firewalls
On the way, packets cross multiple firewalls (your router, ISP, Google’s perimeter). Firewalls are like bouncers at a club: only allowing known, safe traffic (like HTTPS on port 443).

## 4. HTTPS/SSL
Before any data is exchanged, your browser and Google establish trust via TLS. They agree on ciphers, your browser checks Google’s certificate, and once all is good, communication is encrypted. No one on the path can snoop on your searches.

## 5. Load balancing
The IP you reached usually belongs to a load balancer, not a single server. Think of it as a traffic cop: it decides which Google server should handle you, spreading millions of users fairly and keeping things fast and reliable.

## 6. Web server
Your request finally lands on a web server (like Nginx). If it’s just static content (an image, CSS), the web server can reply directly.

## 7. Application server
But Google is dynamic. Your request goes deeper, into app servers that handle business logic, search algorithms, ads ranking… the heavy lifting happens here.

## 8. Database
Need to fetch data? App servers query massive, replicated, distributed databases. Some replicas handle reads, primaries handle writes. This ensures speed and reliability.

## 9. Back to you
The response travels back through the same chain: app → web → load balancer → encrypted TLS → your browser. Your browser parses HTML, loads CSS/JS, builds the DOM, and paints pixels on screen.

## TL;DR
DNS finds the address, TCP connects, TLS secures, load balancers distribute, servers respond, databases store, and your browser renders.

---
In short, pressing Enter on “google.com” triggers a whole symphony of systems working together in milliseconds. Understanding this flow is essential for every full-stack engineer.
