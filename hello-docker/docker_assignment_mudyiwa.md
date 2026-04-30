## Task 1.1

```
$ docker build -t hello-docker .
[+] Building 5.0s (9/9) FINISHED                                 docker:default
 => [internal] load build definition from Dockerfile                       0.0s
 => => transferring dockerfile: 114B                                       0.0s
 => [internal] load metadata for docker.io/library/python:3.9-slim         1.1s
 => [auth] library/python:pull token for registry-1.docker.io              0.0s
 => [internal] load .dockerignore                                          0.0s
 => => transferring context: 2B                                            0.0s
 => [1/3] FROM docker.io/library/python:3.9-slim@sha256:2d97f6910b16bd338  2.3s
 => => resolve docker.io/library/python:3.9-slim@sha256:2d97f6910b16bd338  0.0s
 => => sha256:ea56f685404adf81680322f152d2cfec62115b30dda481c 251B / 251B  0.1s
 => => sha256:fc74430849022d13b0d44b8969a953f842f59c6e9 13.88MB / 13.88MB  0.5s
 => => sha256:b3ec39b36ae8c03a3e09854de4ec4aa08381dfed84a 1.29MB / 1.29MB  0.5s
 => => sha256:38513bd7256313495cdd83b3b0915a633cfa475dc 29.78MB / 29.78MB  0.8s
 => => extracting sha256:38513bd7256313495cdd83b3b0915a633cfa475dc2a07072  0.9s
 => => extracting sha256:b3ec39b36ae8c03a3e09854de4ec4aa08381dfed84a9daa0  0.1s
 => => extracting sha256:fc74430849022d13b0d44b8969a953f842f59c6e9d1a0c2c  0.5s
 => => extracting sha256:ea56f685404adf81680322f152d2cfec62115b30dda481c2  0.0s
 => [internal] load build context                                          0.0s
 => => transferring context: 144B                                          0.0s
 => [2/3] WORKDIR /app                                                     1.2s
 => [3/3] COPY hello.py .                                                  0.0s
 => exporting to image                                                     0.2s
 => => exporting layers                                                    0.1s
 => => exporting manifest sha256:5c0288af0e0987b6eba6c79e3ec8450f0dc82d53  0.0s
 => => exporting config sha256:0620f1ee37d7dea6e7659881115a7cd1127dc88c47  0.0s
 => => exporting attestation manifest sha256:3d9342ba2b8780592b9bc941c6a7  0.0s
 => => exporting manifest list sha256:412b3f948bece2e3d9e1e6297c07b30498b  0.0s
 => => naming to docker.io/library/hello-docker:latest                     0.0s
 => => unpacking to docker.io/library/hello-docker:latest                  0.0s

$ docker run --rm hello-docker
Hello from Python 3.9 inside a container!
```

## Task 1.2

```
$ docker build -t hello-docker .
[+] Building 0.6s (8/8) FINISHED                                 docker:default
 => [internal] load build definition from Dockerfile                       0.0s
 => => transferring dockerfile: 114B                                       0.0s
 => [internal] load metadata for docker.io/library/python:3.9-slim         0.3s
 => [internal] load .dockerignore                                          0.0s
 => => transferring context: 2B                                            0.0s
 => [1/3] FROM docker.io/library/python:3.9-slim@sha256:2d97f6910b16bd338  0.0s
 => => resolve docker.io/library/python:3.9-slim@sha256:2d97f6910b16bd338  0.0s
 => [internal] load build context                                          0.0s
 => => transferring context: 150B                                          0.0s
 => CACHED [2/3] WORKDIR /app                                              0.0s
 => [3/3] COPY hello.py .                                                  0.0s
 => exporting to image                                                     0.1s
 => => exporting layers                                                    0.1s
 => => exporting manifest sha256:5dd632a05a76f08ee00275e2e569e9f82d72521a  0.0s
 => => exporting config sha256:fc7872677702c3a230417a828cdbbcc0715f4cd3bc  0.0s
 => => exporting attestation manifest sha256:70c1577bda9493b582636d0d5ddd  0.0s
 => => exporting manifest list sha256:95a2f9cd08b4069caf0198f4d42620ef4af  0.0s
 => => naming to docker.io/library/hello-docker:latest                     0.0s
 => => unpacking to docker.io/library/hello-docker:latest                  0.0s

$ docker run --rm hello-docker
Traceback (most recent call last):
  File "/app/hello.py", line 1, in <module>
    import sys, pandas
ModuleNotFoundError: No module named 'pandas'

Command exited with code 1
```

```
$ cat Dockerfile
FROM python:3.9-slim
WORKDIR /app
RUN pip install pandas==2.2.3
COPY hello.py .
CMD ["python", "hello.py"]
```

```
$ docker build -t hello-docker .
[+] Building 22.8s (9/9) FINISHED                                docker:default
 => [internal] load build definition from Dockerfile                       0.0s
 => => transferring dockerfile: 144B                                       0.0s
 => [internal] load metadata for docker.io/library/python:3.9-slim         0.2s
 => [internal] load .dockerignore                                          0.0s
 => => transferring context: 2B                                           0.0s
 => [1/4] FROM docker.io/library/python:3.9-slim@sha256:2d97f6910b16bd338  0.0s
 => => resolve docker.io/library/python:3.9-slim@sha256:2d97f6910b16bd338  0.0s
 => [internal] load build context                                          0.0s
 => => transferring context: 29B                                           0.0s
 => CACHED [2/4] WORKDIR /app                                              0.0s
 => [3/4] RUN pip install pandas==2.2.3                                   12.7s
 => [4/4] COPY hello.py .                                                  0.1s 
 => exporting to image                                                     9.8s 
 => => exporting layers                                                    8.1s 
 => => exporting manifest sha256:bd5f732c5ab816bf08edd9c3598e4a5bc9883db4  0.0s 
 => => exporting config sha256:f7e9eed7707221ab8f40dec9fae1e11e7ad2fc8c9f  0.0s 
 => => exporting attestation manifest sha256:144cffaed6ace4ce228ffc49ffd4  0.0s 
 => => exporting manifest list sha256:e93c9259c2ebc04a124545f60be270fc0db  0.0s
 => => naming to docker.io/library/hello-docker:latest                     0.0s
 => => unpacking to docker.io/library/hello-docker:latest                  1.6s

$ docker run --rm hello-docker
Python 3.9, pandas 2.2.3
```

## Final Dockerfile

```
FROM python:3.9-slim
WORKDIR /app
RUN pip install pandas==2.2.3
COPY hello.py .
CMD ["python", "hello.py"]
```

## Question 2.1 — Why pin?

If I had used `RUN pip install pandas` with no version, the build would succeed now but could break later because `pip` would install whatever version is newest at build time. A new pandas release in the future might drop support for Python 3.9, change APIs, or introduce a bug, so the same Dockerfile would produce a different image tomorrow. Pinning ensures the container is reproducible by locking the exact package version used.

## Question 2.2 — Recipe or cake?

For reproducible research, sending the Dockerfile and `hello.py` is better than sending the built image. The Dockerfile is the recipe, so others can rebuild the image themselves with the same base image and dependencies; that means they can verify the build process and inspect the code. A built image is a binary artifact that hides the exact dependency versions and build steps, so it is harder to audit, modify, or reproduce from source.
