# spiderwomen
爬虫程序

## 基于scrapy创建一个爬虫，并抓取数据
**创建爬虫**
```shell
scrapy startproject mySpider
```
**编写代码**
```python
import scrapy


class MySpiderItem(scrapy.Item):
    # define the fields for your item here like:
    # name = scrapy.Field()
    pass


class MySpiderSpider(scrapy.Spider):
    name = 'my_spider'
    allowed_domains = ['example.com']
    start_urls = ['http://example.com/']
 
    def parse(self, response):
        for href in response.css('a::attr(href)'):
            yield response.follow(href, self.parse)
 
        item = MySpiderItem()
        # fill the item
        yield item
```

**运行爬虫**
```shell
scrapy crawl my_spider
```
