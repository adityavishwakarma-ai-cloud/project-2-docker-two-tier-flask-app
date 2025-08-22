## 🔄 Project 2 Flow

1. **Web Container (`web`)**

   * Runs a Node.js Express server (`app.js`).
   * Listens on port `8080` on the host machine.
   * Handles HTTP requests from users.

2. **Database Container (`db`)**

   * Runs MySQL database (`appdb`).
   * Initialized with `init.sql` to create `users` table and sample data.
   * Stores data persistently using Docker volumes.

3. **Communication**

   * Web container connects to database container using **Docker network**.
   * Web server queries `users` table and returns JSON responses.

4. **Docker Compose Orchestration**

   * Both containers are defined in `docker-compose.yml`.
   * `docker-compose up` builds and starts containers together.
   * `docker-compose down` stops and removes containers safely.

5. **Persistent Data & Logs**

   * Database data persists in Docker volume (`db_data`).
   * Web app logs can be viewed using `docker logs web`.

