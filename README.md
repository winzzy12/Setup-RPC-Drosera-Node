RPC
[RPC Alchemy](https://dashboard.alchemy.com/apps/jflmwxu6zgt5kj5t/metrics)


# Setup RPC Drosera Node

```bash
sudo systemctl stop drosera
sudo systemctl disable drosera
```

Edit Trap configuration
```bash
cd my-drosera-trap
nano drosera.toml
```
Edit Service
```bash
sudo nano /etc/systemd/system/drosera.service
```
Paste content:
```bash
sudo tee /etc/systemd/system/drosera.service > /dev/null <<EOF
[Unit]
Description=drosera node service
After=network-online.target

[Service]
User=$USER
Restart=always
RestartSec=15
LimitNOFILE=65535
ExecStart=$(which drosera-operator) node --db-file-path $HOME/.drosera.db --network-p2p-port 31313 --server-port 31314 \
    --eth-rpc-url https://ethereum-holesky-rpc.publicnode.com \
    --eth-backup-rpc-url https://1rpc.io/holesky \
    --drosera-address 0xea08f7d533C2b9A62F40D5326214f39a8E3A32F8 \
    --eth-private-key PV_KEY \
    --listen-address 0.0.0.0 \
    --network-external-p2p-address VPS_IP \
    --disable-dnr-confirmation true

[Install]
WantedBy=multi-user.target
EOF
```
(Change RPC Holskey) & SAVE

Start service:
```bash
sudo systemctl daemon-reload
sudo systemctl enable drosera
sudo systemctl start drosera
journalctl -u drosera.service -f
```

============================
reload systemd
```bash
sudo systemctl daemon-reload
```
```bash
sudo systemctl enable drosera
```

start systemd
```bash
sudo systemctl start drosera
```
restart systemd
```bash
sudo systemctl restart drosera
```

Check Node Health
```bash
journalctl -u drosera.service -f
```
