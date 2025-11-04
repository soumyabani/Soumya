

# CTFd Setup and Management

## Technology

CTFd is built using **Python** and the **Flask** web framework.

## Installation

1. Install Docker and Docker Compose.
2. Clone the CTFd repository:
   ```
   git clone https://github.com/CTFd/CTFd.git
   ```
3. Generate a secret key:
   ```
   head -c 64 /dev/urandom > .ctfd_secret_key
   ```
4. Export the secret key as an environment variable:
   ```
   export SECRET_KEY=$(cat .ctfd_secret_key | base64)
   ```
5. Modify `docker-compose.yml`. Set the `SECRET_KEY` environment variable for the CTFd service:
   ```
   SECRET_KEY=${SECRET_KEY}
   ```
6. Run the application:
   ```
   docker compose up
   ```
7. Access the CTFd instance at [http://localhost:8000](http://localhost:8000/)

Note: The default Docker Compose configuration does not configure SSL/TLS.

## Dependencies

- **WSGI server**: Installed by default; handles passing responses from the web application.
- **Database server**: By default, CTFd creates a SQLite database. Supported options include MySQL and MariaDB (not recommended with Postgres). CTFd supports the JSON data type.
- **Caching server**: Redis is the preferred option.

## Updating CTFd

- If using the `image` field in `docker-compose.yml`:
  ```
  docker-compose pull
  docker-compose up
  ```
- If using the `build` field:
  ```
  git pull
  docker-compose build
  docker-compose up
  ```

## Challenges

- **File upload**: Users can upload files for challenges.
- **Flags**: Admins configure different types of flags for challenges.

## Sign In Options

- **OAuth**: Allows users to sign in to a self-hosted CTFd instance using GitHub accounts and credentials from a GitHub OAuth app.

## Backups and Data Export

- CTFd allows exporting all instance data as a zip file for archival (admin only).
- Selected data can be exported in CSV format.

## Extending CTFd

### Plugins

- Develop plugins to:
  - Add new routes (pages, APIs)
  - Modify existing routes
  - Add new database tables
  - Replace templates
  - Add JavaScript or CSS files

#### Challenge Type Plugins

- Define custom challenge types, such as multi-flag challenges or challenges with dynamic properties.

#### Flag Type Plugins

- Add flexibility for flag validation (static, regex, or custom conditions).

(- Toggle plugins on or off from the admin interface.
- Protect endpoints for admin access only.
- Export challenge statistics, scoreboard, and admin metrics.
- Add custom metrics for plugins.)

## Management Tools

### ctfcli

- Command-line interface for uploading challenges.
- Integrates with CTFd REST API.
- Supports CI/CD build integrations and premade challenge templates.
- Each challenge managed by ctfcli should have a `challenge.yml` file.
- Supports plugins as CLI additions.
- **Note**: ctfcli is still considered an alpha project and may change frequently.

- More info: [ctfcli on GitHub](https://github.com/CTFd/ctfcli?tab=readme-ov-file)

### Terraform + CTFd Provider

- Terraform provider for CTFd allows infrastructure-as-code management.
- Documentation:
  - [Terraform Provider Docs](https://registry.terraform.io/providers/ctfer-io/ctfd/latest/docs)
  - [GitHub Repository](https://github.com/ctfer-io/terraform-provider-ctfd)

## Integrations

- **Custom Webhooks**: Slack, Discord (not available in open source version).
- **MajorLeagueCyber**: Official CTF event tracker for participant listing and performance tracking.
- **Crisp Chat**: Chat bubble for user communication.

***


