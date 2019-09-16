Docker image for [PHP_CodeSniffer](https://github.com/squizlabs/PHP_CodeSniffer) already configured for [WordPress Coding Standards](https://github.com/WordPress-Coding-Standards/WordPress-Coding-Standards).

* https://hub.docker.com/r/joeyblake/phpcs-wordpress/

## Build

```bash
# No proxy
docker build --no-cache -t joeyblake/phpcs-wordpress .

```

## Test

Show the available standards:

```console
$ docker run joeyblake/phpcs-wordpress phpcs -i
The installed coding standards are MySource, PEAR, PHPCS, Squiz, Zend, PSR2, PSR1, WordPress, WordPress-Extra, WordPress-Docs, WordPress-Core and WordPress-VIP
$
```

## Run

```bash
# Check for code standards issues
docker run -v /path/to/php/files/:/scripts/ joeyblake/phpcs-wordpress phpcs  --standard=WordPress-Core .

# Fix code standards issues
docker run -v /path/to/php/files/:/scripts/ joeyblake/phpcs-wordpress phpcbf --standard=WordPress-Core .
```

## GitLab CI example

```yaml
# Run PHP_CodeSniffer in our custom WordPress plugin and theme
code_lint:
  stage: test
  image: joeyblake/phpcs-wordpress
  script:
    - phpcs --standard=WordPress-Core wp-content/plugins/my-awesome-plugin
    - phpcs --standard=WordPress-Core --ignore=/bootstrap/,/inc/ wp-content/themes/my-awesome-theme
```
