# Validator

## Installation and usage


### Install

```shell
git clone <this repo> validator
cd validator
poetry env use 3.9
poetry install
poetry run pre-commit install
```

### Run

The environment variable `REDIS_URL` controls where the job requests are queued.  
If not set, it defaults to `localhost:6379`.

#### Start the http server:
```shell
poetry run dev # for dev
poetry run start # for prod
```

#### Start workers


- REDIS_URL
- REDIS_QUEUE_NAME

`REDIS_QUEUE_NAME` is needed only by standard worker and not rq_worker. It's an error if not set

```shell
poetry run start_worker  # to start a standard worker
poetry run start_rq_worker  # to start a worker using rq. This workers require the http server running
```
There is no need to start a worker on the same machine, as long as there is at least
another worker listening on the same redis server and queue.  
Otherwise no jobs will ever complete.
