# async_cron
[![Downloads](https://pepy.tech/badge/async_cron)](https://pepy.tech/project/async_cron)
[![PyPI version](https://badge.fury.io/py/async_cron.svg)](https://badge.fury.io/py/async_cron)

this repo is influenced by schedule.

we supply a async scheduler and async function support

you can easily integrate this lib to you async program,with no blocking

## Install

--------------

pip install async-cron

## Usage examples

--------------


```python
import asyncio

from async_cron.job import CronJob
from async_cron.schedule import Scheduler


async def test(*args, **kwargs):
    print(args, kwargs)


def tt(*args, **kwargs):
    print(args, kwargs)


msh = Scheduler()
myjob = CronJob(name='test').every(5).second.go(test, (1, 2, 3), name=123)
# tolerance means if now - at_exact_time <= tolerance,this job will still be applied
job2 = CronJob(name='tt', tolerance=100).at(
    "2019-01-15 16:12").go(tt, (5), age=99)

# msh.add_job(myjob)
msh.add_job(job2)


loop = asyncio.get_event_loop()

loop.run_until_complete(msh.start())
```

License
-------

The async_cron is offered under MIT license.
