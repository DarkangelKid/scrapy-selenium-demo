# Scrapy + Selenium Demo

This repo contains the code for Part V of my tutorial: A Minimalist End-to-End Scrapy Tutorial (https://medium.com/p/11e350bcdec0).

The website to crawl is https://dribbble.com/designers, which is an infinite scroll page.

I borrowed some code from "[Web Scraping: A Less Brief Overview of Scrapy and Selenium, Part II](https://towardsdatascience.com/web-scraping-a-less-brief-overview-of-scrapy-and-selenium-part-ii-3ad290ce7ba1)" - many thanks to the author!

## Setup
Tested with Python 3.6 via virtual environment:
```shell
$ python3.6 -m venv venv
$ source venv/bin/activate
$ pip install -r requirements.txt
```

Chrome Driver:

You need to download the chrome driver from: https://chromedriver.chromium.org/downloads

Note: the version of the driver must match the version of chrome installed on your machine for this to work.

For example, this repo uses the chromedriver 77.0.3865.40 that supports Chrome version 77 - you need to make sure installed Chrome is version 77 (check it from Menu--> Chrome --> About Google Chrome)

## Run

Run `scrapy crawl dribbble`, which should start an instance of Chrome and scroll to the bottom of the page automatically. The extracted data is logged to the console.

## Use ProxyMesh with Scrapy

You must set the `http_proxy` environment variable, then activate the HttpProxyMiddleware.

For HTTP:

```bash
$ export http_proxy=http://USERNAME:PASSWORD@HOST:PORT
```

such as:
```bash
$ export http_proxy=http://harrywang:mypassword@us-wa.proxymesh.com:31280
```

For HTTPS:

For https requests, you should use  IP authentication, and remove USERNAME:PASSWORD@ from the http_proxy variable.

To activate the HttpProxyMiddleware, uncomment the following part in `settings.py`:

```python
DOWNLOADER_MIDDLEWARES = {
    'scrapy.downloadermiddlewares.httpproxy.HttpProxyMiddleware': 100,
}
```
## Use ProxyMesh with Selenium

IP authentication must be set first: add the IP of the machine running this script to you ProxyMesh account for IP authentication. Then, uncomment the following two lines in the spider file.

```python
# PROXY = "us-wa.proxymesh.com:31280"
# chrome_options.add_argument('--proxy-server=%s' % PROXY)
```
