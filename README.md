# Laravel Sail Auto-Builder (GHCR)

This repository automatically builds and publishes **Docker images based on [Laravel Sail](https://github.com/laravel/sail)**  
to the **GitHub Container Registry (GHCR)**.

Images are rebuilt **daily** only when Laravel Sail itself changes.  
That means you always get up-to-date PHP runtimes without having to build Sail locally.


## 🚀 Features

- ✅ Builds official Sail images for **PHP 8.4, 8.3, 8.2**
- 🔄 Automatically updates when Laravel Sail changes
- 📦 Publishes to **GitHub Container Registry (GHCR)**
- 🕒 Runs daily at 03:00 UTC via GitHub Actions


## 🧰 How to use the images

Pull the prebuilt Sail images directly from GHCR:

```bash
# PHP 8.4
docker pull ghcr.io/<your-github-username>/sail:php-8.4

# PHP 8.3
docker pull ghcr.io/<your-github-username>/sail:php-8.3

# PHP 8.2
docker pull ghcr.io/<your-github-username>/sail:php-8.2
````

You can also use them in your own `docker-compose.yml`:

```yaml
services:
  laravel.test:
    image: ghcr.io/<your-github-username>/sail:php-8.4
    ports:
      - "80:80"
```


## ⚙️ How it works

The GitHub Actions workflow:

1. Runs every day at 03:00 UTC.
2. Clones the latest `laravel/sail` repository.
3. Checks if there are any new commits since the last build.
4. If there are updates:

   * Builds images for each PHP version listed in `PHP_VERSIONS`.
   * Tags and pushes them to `ghcr.io`.
5. If there are no changes, it skips the build.


## 🔓 Making images public

After the first successful build:

1. Go to your **GitHub profile → Packages**
   (e.g. [https://github.com/users/](https://github.com/users/)<your-github-username>/packages)
2. Click the `sail` package.
3. Open **Package settings** → set **“Public”**.

This makes the images publicly available without authentication.


## 🧩 Customization

* To change PHP versions, edit `PHP_VERSIONS` in
  `.github/workflows/build-sail-images.yml`.

* To change the build frequency, adjust the `cron` schedule.

* To use Docker Hub instead of GHCR, replace the login step and
  change `REGISTRY` + credentials accordingly.


## 👐 License

MIT License.
Based on [Laravel Sail](https://github.com/laravel/sail) and published images are provided **as-is**.

