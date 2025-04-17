# Setting Up Your Own DERP Server

## 1. Obtain a TLS Certificate with Certbot

Ensure your domain points to this server's IP address. Then, run:

```bash
sudo certbot certonly --standalone -d dp.domain.com --non-interactive --agree-tos -m your@email.com
```

Replace `dp.domain.com` and `your@email.com` with your actual domain and email address.

## 2. Start the Server with Docker Compose

Run Docker Compose to start your DERP server. (Refer to your `docker-compose.yml` for details.)

## 3. Configure Tailscale ACLs

Go to [Tailscale ACLs](https://login.tailscale.com/admin/acls/file) and add the following to your configuration:

```json
{
  // ... other config
  "derpMap": {
    "OmitDefaultRegions": true,
    "Regions": {
      "999": {
        "RegionID": 998,
        "RegionCode": "vietnam",
        "Nodes": [
          {
            "Name": "vn",
            "RegionID": 998,
            "HostName": "dp.domain.com", // Your domain name
            "STUNPort": 3478,
            "DERPPort": 443
          }
        ]
      }
    }
  }
}
```

Replace `dp.domain.com` with your actual domain name.

---

If this project helps you, please consider leaving a star!

