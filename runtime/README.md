# google/python-runtime

[`google/python-runtime`](https://index.docker.io/u/google/python-runtime) is a [docker](https://docker.io) base image that makes it easy to dockerize standard [Python](http://python.org) application.

It can automatically bundle a Python application and its dependencies with a single line Dockerfile.

It is based on [`google/python`](https://index.docker.io/u/google/python) base image.

## Usage

- Create a Dockerfile in your python application directory with the following content:

        FROM google/python-runtime

- Run the following command in your application directory:

        docker build -t app .

## Sample
  
See the [sources](/hello) for [`google/python-hello`](https://index.docker.io/u/google/python-hello) based on this image.

## Notes

The image assumes that your application:

- has a [`requirements.txt`](https://pip.pypa.io/en/latest/user_guide.html#requirements-files) file to specify its dependencies
- listens on port `8080`
- either has a `main.py` script as entrypoint or defines `ENTRYPOINT ["/env/bin/python", "/app/some_other_file.py"]` in its `Dockerfile`

When building your application docker image, `ONBUILD` triggers:

- Create a new virtualenv under the `/env` directory in the container
- Fetch the dependencies listed in `requirements.txt` into the virtualenv using `pip install` and leverage docker caching appropriately
- Copy the application sources under the `/app` directory in the container

