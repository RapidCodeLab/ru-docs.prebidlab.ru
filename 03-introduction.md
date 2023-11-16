---
title: Как это работает?
description: 
layout: libdoc/page

category: Введение
order: 3
---
* 
{:toc}

## Как это работает ?

Паблишер создает инвентарь(Inventory) и блоки размещения(Entity) с помощью Inventory API. Эти сущности содержат информацию о инвентаре и блоках размещения. Например id инвентаря, блока, IAB категории контента, тип блока(banner,native), размер картинки или баннера и т..д. Подробнее тут.

Паблишер подключает ad-provider.js на веб страницу, а также размещает рекламные блоки на веб странице в необходимых местах в виде простых div элементов с атрибутом data-entity-id=”entity identificator”. Весь код для размещения на странице можно получить через  Inventory API.

После загрузки страницы и инициализации DOM, ad-provider.js на странице все блоки размещения и подготавливает массив с их идентификаторами. Далее эти идентификаторы передаются http post запросом в  header bidder. 

Header Bidder получает идентификаторы рекламных блоков(Entity) и для каждого идентификатора на основе хранящейся информации о блоке подготавливается OpenRTB Imp объект соответствующий типу и метаинформации данного блока размещения(Imp.Banner , Imp.Native etc.). Все подготовленные Imp объекты добавляются в подготовленный OpenRTB BidRequest объект.

Подготовленный OpenRTB BidRequest асинхронно отправляется http post запросом в подключенные DSP. Если DSP ответила в указанный таймаут, креативы из полученного OpenRTB BidResponse добавляются в структуру для последующего аукциона.

Для каждого блока проводится аукцион среди всех полученных креативов от всех DSP для данного блока.

Все креативы победители для каждого блока отправляются одним ответом на ad-provider.js, который в соответствии с идентификаторами  отрисовывает креативы на странице в указанных блоках.

Примеры http запросов и ответов  ad-provider.js и OpenRTB можно посмотреть здесь

