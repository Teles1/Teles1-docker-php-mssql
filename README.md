# docker-php-mssql

Docker images based on the [official Docker PHP images](https://hub.docker.com/_/php/) with
the [Microsoft SQL Server Driver](https://github.com/Microsoft/msphpsql) already installed.

The images are built and retagged based on their corresponding upstream once a week at night.

## Usage

You can pull one of the images with `docker pull Teles1/php-mssql:<tag>`.
To run a container with an image, you can also use `docker run Teles1/php-mssql:<tag>` directly.

## Available Versions
 
- PHP 7.4 (based on apache) + Microsoft ODBC Driver 17 + sqlsrv + pdo_sqlsrv (FPM and CLI)

## Configuration

To change the PHP configuration, have a look at [the official PHP Docker image repository](https://hub.docker.com/_/php/).

## Building the Images locally

After cloning the repository, the images can be built locally using the following command:

```sh
docker build -t Teles1/php-mssql:<tag> <version>/<type>
```

Building the PHP 8.0 CLI image looks like this:

```sh
docker build -t Teles1/php-mssql:7.4-apache
```

## Contributing

If you want to contribute the sources for other PHP versions, I'll appreciate it. Please send a pull request.

## License

The code is licensed under the [MIT license](LICENSE).
