### Project setup
1. Clone the repository
2. Up docker containers with command
```bash
docker-compose up -d
```
3. Enter into node container
```bash
docker exec -it vue-app bash
```
3. Install dependencies
```bash
npm i
```
4. Run the app
```bash
npm run dev
```
5. Open http://localhost:3000 in browser