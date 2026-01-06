# Kaspa-Full-Stack

### Tutorial for Kaspa Full Stack (Explorer, API, Indexer, Database, Rusty Kaspad, Stratum Bridge and K-Social)

> 1. Install Docker:
```
sudo apt install -y curl
sudo curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
sudo apt install -y docker-compose
```

> 2. Install NodeJS from https://nodejs.org/en/download

> 3. K-indexer:
```
git clone https://github.com/thesheepcat/K-indexer.git
cd K-indexer/docker/PROD
rm .env
nano .env
---Copy paste from https://github.com/Dennitzo/Kaspa-Full-Stack/blob/main/K-indexer_env.txt
---Save and close file
rm compose.yaml
nano compose.yaml
---Copy paste from https://github.com/Dennitzo/Kaspa-Full-Stack/blob/main/compose.yaml
---Save and close file
sudo docker compose up -d
```

> 4. Wait for Kaspad and indexer to fully sync:
```
sudo docker logs -n 100 -f kaspad
```

> 5. Kaspa Stratum Bridge:
```
git clone https://github.com/rdugan/kaspa-stratum-bridge.git
cd kaspa-stratum-bridge/cmd/kaspabridge
nano config.yaml

---Change "extranonce_size = 0"
---to "extranonce_size = 2"
---Save and close File

cd ..
cd ..
nano docker-compose-all-src.yml

---Change "ports:
      - 3000:3000"
---to  "ports:
      - 5000:3000"
---Save and close File

sudo docker compose -f docker-compose-all-src.yml up -d --build
```

> 6. K-Social:
```
git clone https://github.com/thesheepcat/K.git
cd K
nano vite.config.ts
---Change "server: {
    host: true,
    port: 5173,
    fs: {
      allow: ['..']
    }
  },"
---to "server: {
    host: true,
    port: 5173,
    allowedHosts: [
    'yourDomainOrIP',
    ],
    fs: {
      allow: ['..']
    }
  },"
---Save and close File
sudo npm install
sudo npm run dev
---Open http://yourDomainOrIP:5173 in your Browser
---Go to Settings
---Set Indexer to "Custom Indexer", and set "Indexer URL" to http://yourDomainOrIP:3001
---Set Kaspa node connection to "Your Kaspa node", and set "Kaspa node URL" to ws://yourDomainOrIP:17110
```

> Ports:
```
Explorer: http://yourDomainOrIP:8080
K-Social: http://yourDomainOrIP:5173
API: http://yourDomainOrIP:8000
Stratum Bridge: http://yourDomainOrIP:5000
Miner Connection: stratum+tcp://yourDomainOrIP:5555
```
