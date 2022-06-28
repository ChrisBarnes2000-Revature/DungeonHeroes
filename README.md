# Flask Demo

- Build the image:

```zsh
$ docker build -t flask-image .
  [+] Building 18.5s (10/10) FINISHED
  => [internal] load build definition from Dockerfile                                                                              0.0s
  => => transferring dockerfile: 1.13kB                                                                                            0.0s
  => [internal] load .dockerignore                                                                                                 0.0s
  => => transferring context: 2B                                                                                                   0.0s
  => [internal] load metadata for docker.io/library/python:3.10.5-slim-bullseye                                                    2.1s
  => [auth] library/python:pull token for registry-1.docker.io                                                                     0.0s
  => [internal] load build context                                                                                                 1.1s
  => => transferring context: 19.56MB                                                                                              1.1s
  => [1/4] FROM docker.io/library/python:3.10.5-slim-bullseye@sha256:2ae2b820fb...                                                 7.6s
  => => resolve docker.io/library/python:3.10.5-slim-bullseye@sha256:2ae2b820fb...                                                 0.0s
  => => sha256:e2be974225eda2dba71b5e519b9cef7d7958fa2bd12448b10eaecb4b95000eeb 1.08MB / 1.08MB                                    1.4s
  => => sha256:b41d2e1d193740ed01d296c0bf6a6aeb72501da60451735f8422318ae9e5401b 11.77MB / 11.77MB                                  3.4s
  => => sha256:2ae2b820fbcf4e1c5354ec39d0c7ec4b3a92cce71411dfde9ed91d640dcdafd8 1.86kB / 1.86kB                                    0.0s
  => => sha256:df9e675c0f6f0f758f7d49ea1b4e12cf7b8688d78df7d9986085fa0f24933ade 1.37kB / 1.37kB                                    0.0s
  => => sha256:24aa51b1b3e99edfe6ba347e3e9347528a683686d0387a76c775ed40c8d62713 7.50kB / 7.50kB                                    0.0s
  => => sha256:b85a868b505ffd0342a37e6a3b1c49f7c71878afe569a807e6238ef08252fcb7 31.38MB / 31.38MB                                  3.9s
  => => sha256:f6edef4f72a413275f1493dee2ce8413be5a8223a378294b6e77a4c47a455922 233B / 233B                                        1.9s
  => => sha256:3968cb080aabd142a7d5a2576e5f3282083fe194b2266e852603383136ca19b4 3.17MB / 3.17MB                                    3.4s
  => => extracting sha256:b85a868b505ffd0342a37e6a3b1c49f7c71878afe569a807e6238ef08252fcb7                                         1.9s
  => => extracting sha256:e2be974225eda2dba71b5e519b9cef7d7958fa2bd12448b10eaecb4b95000eeb                                         0.2s
  => => extracting sha256:b41d2e1d193740ed01d296c0bf6a6aeb72501da60451735f8422318ae9e5401b                                         0.6s
  => => extracting sha256:f6edef4f72a413275f1493dee2ce8413be5a8223a378294b6e77a4c47a455922                                         0.0s
  => => extracting sha256:3968cb080aabd142a7d5a2576e5f3282083fe194b2266e852603383136ca19b4                                         0.3s
  => [2/4] ADD . /app                                                                                                              1.7s
  => [3/4] WORKDIR /app                                                                                                            0.0s
  => [4/4] RUN pip install -r requirements.txt                                                                                     6.7s
  => exporting to image                                                                                                            0.4s
  => => exporting layers                                                                                                           0.4s
  => => writing image sha256:d19c5aa35b968a5d85c4ae6749b0dfb8e729b5099a270d0b7d77c1e570388d2a                                      0.0s
  => => naming to docker.io/library/flask-image                                                                                    0.0s
```

- Build the container:

```zsh
$ docker run -p 5000:5000 --rm --name flask-container flask-image
  * Serving Flask app 'app.py' (lazy loading)
  * Environment: development
  * Debug mode: on
  * Running on all addresses (0.0.0.0)
    WARNING: This is a development server. Do not use it in a production deployment.
  * Running on http://127.0.0.1:5000
  * Running on http://172.17.0.2:5000 (Press CTRL+C to quit)
  * Restarting with stat
  * Debugger is active!
  * Debugger PIN: 830-583-367
```

- Search for all images with names that contain `flask`

```zsh
$ docker images -a | grep "flask"
  `flask`-image   latest    d19c5aa35b96   23 minutes ago   157MB
```

- Remove all images with names that contain `flask`

```zsh
$ docker images -a | grep "flask" | awk '{print $3}' | xargs docker rmi
  Untagged: flask-image:latest
  Deleted: sha256:d19c5aa35b968a5d85c4ae6749b0dfb8e729b5099a270d0b7d77c1e570388d2a
```

- Remove all containers with names that contain `flask`

```zsh
docker ps -a | grep "flask" | awk '{print $2}' | xargs docker rmi
```
