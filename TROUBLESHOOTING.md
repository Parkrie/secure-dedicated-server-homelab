# Troubleshooting Guide

This document outlines common issues encountered when deploying or connecting to the dedicated server.

---

## Cannot Connect to Server

Possible causes:

- Incorrect port forwarding
- Firewall rules blocking traffic
- Incorrect server IP or port

Verify:

- Router port forwarding rules
- Server process is running
- Correct port is open

---

## Lost Connection to Host

This can occur if the server and client versions do not match.

Check:

- Game client version
- Dedicated server version

---

## Ping Works One Direction Only

If a machine can ping the server but the server cannot ping back, this is often caused by a **client firewall blocking ICMP**.

Verify firewall rules allow ICMP echo responses.

---

## Ports Appear Open but Connection Fails

Check:

- NAT rules
- Internal firewall rules
- Correct protocol (UDP vs TCP)
