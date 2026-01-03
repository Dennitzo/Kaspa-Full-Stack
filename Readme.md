Kaspa-Full-Stack
Tutorial for Kaspa Full Stack (Explorer, API, Indexer, Database, Rusty Kaspad, Stratum Bridge and K-Social)

1. Install Docker:
```
sudo apt install -y curl
curl -fsSL https://get.docker.com -o get-docker.sh
sudo sh get-docker.sh
sudo apt install -y docker-compose
```

2. K-indexer:
```
git clone https://github.com/thesheepcat/K-indexer.git
cd K-indexer/docker/PROD
rm .env
nano .env
---Copy paste from https://github.com/Dennitzo/Kaspa-Full-Stack/k-indexer_env.txt
---Save and close file
rm compose.yaml
nano compose.yaml
---Copy paste from https://github.com/Dennitzo/Kaspa-Full-Stack/compose.yaml
---Save and close file
docker compose up -d
```

3. Install NodeJS from https://nodejs.org/en/download

4. K-Social:
```
git clone https://github.com/thesheepcat/K.git
cd K
npm install
npm run dev
```

5. Wait for Kaspad and indexer to fully sync:
```
docker logs -n 100 -f kaspad
```

6. Open http://yourDomainOrIP:5173 for K-Social:
```
Go to Settings
Set Indexer to "Custom Indexer", and set "Indexer URL" to http://yourDomainOrIP:8600
Set Kaspa node connection to "Your Kaspa node", and set "Kaspa node URL" to ws://yourDomainOrIP:17110
```