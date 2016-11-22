---
layout: post
title:  "Navegando links de tabla con Scrapy"
date:   2016-11-21 23:16:00
categories: programming python scrapy spanish
---
Mientras investigaba alguna manera rapida de parsear links de una tabla y navegar hacia ellos
hice este ejemplo el cual navega a una tabla en una pagina html y luego hacia el link, trayendo
consigo contenido de cada uno de las paginas a las que navega cada link.

En este caso es informacion de atletas de BJJ.

{% highlight python %}
import scrapy
from scrapy.selector import Selector
from scrapy.http import Request

from bjjheroes.items import BjjheroesItem

base_url = 'http://www.bjjheroes.com'

class BasicSpider(scrapy.Spider):
    name = "basic"
    allowed_domains = ["bjjheroes.com"]
    start_urls = (
        'http://www.bjjheroes.com/a-z-bjj-fighters-list',
    )

    def parse(self, response):

        sel = Selector(response)
        rows = sel.xpath('//tr[position()>1]')

        for row in rows:
            item = BjjheroesItem()

            # name
            item['name'] = row.xpath('./td[1]/a/text()').extract()[0]

            # last name
            item['lastname'] = row.xpath('./td[2]/a/text()').extract()[0]

            # url
            url = row.xpath('./td[1]/a/@href').extract()
            url = str(url[0])
            if not url.startswith('http'):
                url = base_url + url
            request = Request(url, callback=self.parse_info)
            request.meta['item'] = item
            yield request


    def parse_info(self, response):
        item = response.meta['item']
        item['url'] = response.url
        sel = Selector(response)
        raw = sel.xpath('//*[@id="post-2729"]/div/*/text()').extract()
        content =  [x for x in raw if x != '\n' and x != ' ' and '\r\n' not in x and x != '\n \n \n']
        item['content'] = content
        yield item

{% endhighlight %}

Claro que para esto debemos contar con nuestro 'contenedor' de items definido para ir almacenando los datos.

{% highlight python %}

from scrapy.item import Item, Field
class BjjheroesItem(Item):
    # define the fields for your item here like:
    name = Field()
    lastname = Field()
    url = Field()
    content = Field()

{% endhighlight %}

El código completo [aqui][repo] en github.

[repo]: https://github.com/izaac/scrapbjj
