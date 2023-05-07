# App local deployment

After initial local setup and running, the project will be accessible at <http://localhost>

## Initial local setup

1. Add this alias to your shell configuration file in your home directory, such as ~/.zshrc or ~/.bashrc

    ```bash
    alias sail='[ -f sail ] && sh sail || sh vendor/bin/sail'
    ```

    and then restart your shell or run `source ~/.bashrc` on Linux, or `source ~/.zshrc` on Mac

2. Stop legacy dev environment if one is in use

    ```bash
    docker-compose down --remove-orphans
    ```

3. Temporarily rename the file .env if it exists

    ```bash
    mv .env .env.backup
    ```

4. Run the project setup script from the application root directory

    ```bash
    ./.scripts/install
    ```

5. Customize default environment configuration if needed

    ```bash
    nano .env
    ```

    or restore it from backup

    ```bash
    mv .env.backup .env
    ```

6. Run modern dev environment

    ```bash
    sail up -d
    ```

    Ensure all containers are started successfully and have healthy status

    ```bash
    sail ps
    ```

7. Generate API key, if `APP_KEY` in .env not specified yet

    ```bash
    sail artisan key:generate --ansi
    ```

8. For the first time, install npm packages

    ```bash
    sail npm ci
    ```

9. Compile assets

    ```bash
    sail npm run build
    ```

10. Run migrations

    ```bash
    sail artisan migrate
    ```
