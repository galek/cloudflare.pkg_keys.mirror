# cloudflare.pkg_keys.mirror

## About this repository
In Russia, the Cloudflare WARP website is blocked and unavailable over TCP/HTTP. 
This is a problem because DPI (TSPU) blocks direct access to the repository. On the other hand, Cloudflare also blocks Russian clients, resulting in a 504 error.

Original key source (accessible outside Russia or via proxy/VPN):  
`https://pkg.cloudflareclient.com/pubkey.gpg`

## Solution
You can import the GPG key from this mirror, and the repositories will work.

### 1. Download and add the GPG key
Run the following command in your terminal to download the key and save it to the keyring:

```bash
curl -fsSL https://githubusercontent.com/galek/cloudflare.pkg_keys.mirror/main/cloudflare-warp-archive-keyring.gpg | sudo gpg --yes --dearmor -o /usr/share/keyrings/cloudflare-warp-archive-keyring.gpg
```

### 2. Verify the key (optional)
To make sure the imported key matches the official Cloudflare Package Repository key (`support@cloudflare.com`), you can check its fingerprint:

```bash
gpg --show-keys /usr/share/keyrings/cloudflare-warp-archive-keyring.gpg
```

### 3. Add the repository (if not added yet)
Add the Cloudflare WARP repository to your APT sources list:

```bash
echo "deb [signed-by=/usr/share/keyrings/cloudflare-warp-archive-keyring.gpg] https://cloudflareclient.com \$(lsb_release -cs) main" | sudo tee /etc/apt/sources.list.d/cloudflare-client.list
```

### 4. Update packages and install WARP
Update your package list and install the client:

```bash
sudo apt-get update && sudo apt-get install cloudflare-warp
```

## Tested OS
1. Ubuntu 24.04 LTS
2. Ubuntu 26.04 LTS
