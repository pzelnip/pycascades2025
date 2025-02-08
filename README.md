# Pycascades 2025

<https://2025.pycascades.com>

---

## Opening Remarks

Same format as previous years.

* <https://2025.pycascades.com/about/health-and-safety-policy>
* <https://2025.pycascades.com/about/code-of-conduct>

Snowball Rule, intro yourself to one person per day for every year you've come

Goals:

* Have Fun
* Learn Something New
* Make new friends

---

## Web Maps, 2 Ways with Streamlit and PyScript

Christy Heaton

<https://pretalx.com/pycascades-2025/talk/LQCJYR/>

* <mas.to/@christyheaton>
* <https://github.com/christyheaton/web_maps_2_ways_pycascades_2025>
* <https://streamlit.io/>

Neat demo/walkthrough of using Streamlit and Pyscript to build a
web app with a hiking map that supports interactivity (all Python).

Streamlit feels more like a targetted tool, but is straight Python.
Pyscript feels more general purpose but there's a Python/JS split.

---

## You are sharing your code wrong (and what to do about it)

Jeremiah Paige

<https://pretalx.com/pycascades-2025/talk/3US9MT/>

"If you write code, you share code"

Everyone shares code, even if only with themselves on a single machine.

```shell
PYTHONPATH="/path/to/zip/file.zip:$PYTHONPATH" python
```

Didn't realize you could just add a zip file like this to PYTHONPATH.

Sharing Code is a 3 step exercise:

* wrapping
* delivering
* unwrapping

or

* packaging
* dsitributig
* installing (I think?  missed this one before slide moved on)

THe best sharing strategy is the one that works every time

Strategies:

* reduce number of steps
* reduce choices for users
* following best practices, represent inertia & community knowledge
  * ex `pip install`, etc

Inline metadata, new thing:
<https://packaging.python.org/en/latest/specifications/inline-script-metadata/>
-- look into this

Restructure into package, outline Python project structure:

* have a pyproject.toml
* python code in a dir of python files
* all Python di has an `__init__.py` file

hatch example of building package

Arrive at wheel as output distribution mechanism

Code is installed much more than it is packaged

---

## Goodbye GIL: Exploring the Free-threaded mode in Python 3.13

Adarsh Divakaran

<https://pretalx.com/pycascades-2025/talk/MSBEKD/>


GIL overview

PEP 703

* free threaded mode build
* backward compatibility issues with C extensions that assume GIL is in effect
* some single threaded code will be slower

<https://py-free-threading.github.io/installing_cpython>

* There's official installers

Verify setup (only present in the freethreaded build):

```python
sys._is_gil_enabled()
sysconfig.get_config_vars().get('Py_GIL_DISABLED')
```

The changes - huge diff, changing 15K LOC, and adding 15K LOC from mimalloc

Benchmarks

* demo single threaded program.
  * using timeit module
  * for loop that just goes for several million iterations
  * with GIL, about 3.9, 3.04 secs (around 3 secs)
  * with free threaded, about 4.7, 4.0 secs (around 3.9 secs)
  * for single threaded programs, free threaded mode has negative impact on perf
* cpu bounded, single threaded vs multithreaded
  * summing numbers in single thread and in a threadpool
  * with free threaded interpreter:
    * single 3.7, 3.8
    * multi 1.3, 1.38
  * with GIL enabled:
    * single 5, 3.6
    * multi 3.4, 3.5
  * again free threaded perf hit on single thread, but multithread huge gain
* IO bounded program
  * opening file, write to it, seek, read, and then remove
  * with gil enabled
    * single thread 5.57, 5.6
    * free threaded with threadpool 5.14, 4.3
  * with free threaded no GIL
    * single thread 6, 3.9, 4.5
    * free threaded with threadpool 5.3, 4.8, 4.4
* wsgi example using flask
  * 2 api endpoints 1 with io bound & other cpu bound
  * use k6 tool for benchmarking (looks like a mini vresion of locust)
  * with gil enabled
    * cpu bound: 36 requests in 20 secs
    * io bound: 95 requests in 20 secs
  * with free threaded no GIL,
    * cpu bound: 80 requests in 20 secs
    * io bound: 66 requests in 20 secs

In future perf penalties will be reduced for free threaded interpreter

<https://linkhq.co/adarsh>

---

## Only You Can Prevent Data Fires - Getting Proactive About Data Quality

Sev Leonard

<https://pretalx.com/pycascades-2025/talk/F7NMZ3/>

Wrote Cost Effective Data Pipelines from O'Reilly

data fire risk analogy to wild fire risk

* Prevention
  * less combustable materials -> data validation
* Monitoring
  * websites -> data quality
* Alerting
  * etc

JSON schemas to validate data

PySpark example of reading corrupted data.  Kafka example & DLQ,
Airflow example, databricks example with constraints, dbt example

Automated unit testing to create defensible space

* barriers:
  * code structure
  * maintaining test data

Example of taking spark code & breaking into functions

`tenacity` library for retrying: <https://pypi.org/project/tenacity/> and <https://tenacity.readthedocs.io/en/latest/>

* <https://thedatascout.com>
* <https://github.com/gizm00>

---

## Ctrl+Alt+Heal: Python and the Future of MedTech

Lilinoe Harbottle

<https://pretalx.com/pycascades-2025/talk/WNYFCT/>

1 in 5 cancer deaths are lung cancer in the US

---

## Observability Matters: Empowering Python Developers with OpenTelemetry

Yash Verma

<https://pretalx.com/pycascades-2025/talk/P9VSLS/>


---

## Re-Py-Ducible Builds

Vagrant Cascadian

<https://pretalx.com/pycascades-2025/talk/DUZVPC/>


---

## Seeing is Believing: Solve Communication Gaps with the Lost Art of Diagrams

Tadeh Hakopian

<https://pretalx.com/pycascades-2025/talk/EAN3TM/>


---

## Quantifying Nebraska

Adam Harvey

<https://pretalx.com/pycascades-2025/talk/P9SHDD/>


---

## Mono-repositories in Python

Avik Basu

<https://pretalx.com/pycascades-2025/talk/LVWE7D/>


---

## Error Culture

Ryan Cheley

<https://pretalx.com/pycascades-2025/talk/XFEF8V/>


---

## Data Science Garage: Building Tools for Genomic Research

Liam Beckman, Quinn Wai Wong, Nasim, Kyle Ellrott

<https://pretalx.com/pycascades-2025/talk/REDHTM/>


---

## Building Resilient Applications with Circuit Breakers and Retries in FastAPI

Sameer Shukla

<https://pretalx.com/pycascades-2025/talk/ZWYR8S/>


---

## Unlocking Concurrency and Performance in Python with ASGI and Async I/O

Allen Y, M Aswin Kishore

<https://pretalx.com/pycascades-2025/talk/SJ7K3G/>


---

## Let Me Introduce Y’all to Y’all

Mason Egger

<https://pretalx.com/pycascades-2025/talk/GYAF3K/>


---

## Optimal Performance Over Basic as a Perfectionist with Deadlines

Velda Kiara

<https://pretalx.com/pycascades-2025/talk/UNPUQD/>


---

## Community Doesn’t Equate to Visibility – What Can You Do Differently?

Aji Fama Jobe

<https://pretalx.com/pycascades-2025/talk/PKDT8S/>


---

## Python for Planet Earth: Climate Modeling and Sustainability in Action

Drishti Jain

<https://pretalx.com/pycascades-2025/talk/PY9SJT/>


---

## You Should Build a Robot (MicroPython & Microprocessors)

Sage Elliott

<https://pretalx.com/pycascades-2025/talk/SYYPNE/>


---

## PyLadies Panel: Talking about experiences and roles within the Python community

Drishti Jain, Parul Gupta, Lilinoe Harbottle, Nasim

<https://pretalx.com/pycascades-2025/talk/DNFUQ8/>
