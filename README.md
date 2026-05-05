# TaskApp

A simple task manager to practice Docker with Node.js and MongoDB.

## Project Structure

```
taskapp/
├── src/
│   └── server.js        # Express API + Mongoose models
├── public/
│   └── index.html       # Frontend UI (vanilla JS)
├── Dockerfile           # Node app container
├── docker-compose.yml   # Wires Node app + MongoDB
├── .dockerignore
└── package.json
```

## Running with Docker (Recommended)

```bash
# 1. Build and start both containers
docker-compose up --build

# 2. Open your browser
http://localhost:3000

# 3. Stop everything
docker-compose down

# To also delete the MongoDB data volume:
docker-compose down -v
```

## Running Locally (without Docker)

```bash
# Requires MongoDB running locally on port 27017
npm install
npm start
```

## API Endpoints

| Method | Endpoint         | Description       |
|--------|-----------------|-------------------|
| GET    | /api/tasks       | Get all tasks     |
| POST   | /api/tasks       | Create a task     |
| PATCH  | /api/tasks/:id   | Update a task     |
| DELETE | /api/tasks/:id   | Delete a task     |

### Example POST body
```json
{
  "title": "Learn Docker networking",
  "description": "Understand how containers talk to each other",
  "priority": "high"
}
```

## Key Docker Concepts Demonstrated

- **Named volumes** — `mongo-data` persists your DB across container restarts
- **Service discovery** — The app connects to MongoDB using the service name `mongo` (not `localhost`)
- **depends_on** — Ensures MongoDB starts before the Node app
- **Environment variables** — `MONGO_URI` and `PORT` injected at runtime
- **.dockerignore** — Keeps `node_modules` out of the build context
