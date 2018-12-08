##  Magento刷新索引的几种方法
在数据表中经常会使用索引，下面简单介绍一下索引的利弊：

创建索引可以大大提高系统的性能:

    通过创建唯一性索引，可以保证数据库表中每一行数据的唯一性。
    可以大大加快数据的检索速度，这也是创建索引的最主要的原因。
    可以加速表和表之间的连接，特别是在实现数据的参考完整性方面特别有意义。
    在使用分组和排序 子句进行数据检索时，同样可以显著减少查询中分组和排序的时间。
    通过使用索引，可以在查询的过程中，使用优化隐藏器，提高系统的性能。
    增加索引也有许多不利的方面:

创建索引和维护索引要耗费时间，这种时间随着数据量的增加而增加。
索引需要占物理空间，除了数据表占数据空间之外，每一个索引还要占一定的物理空间，如果要建立聚簇索引，那么需要的空间就会更大。
当对表中的数据进行增加、删除和修改的时候，索引也要动态的维护，这样就降低了数据的维护速度。
magento有三种刷新索引的方法：

**第一种：在magento后台->system->Index Management** 

这里有整个网站的索引，选择所有Index，并重建索引数据Reindex Data就OK了，但是这种方法刷索引当数据量较大的时候容易刷新不成功。 

**第二种：用脚本刷新索引** 

Magento包含索引脚本，你可以找到shell文件夹在这个文件夹，你可以执行一些命令

**检查所有索引的状态**
```php
php indexer.php --status
```

应该会输出类似下面：
```php
Product Attributes:            Pending
Product Prices:                Pending
Stock Status:                  Pending
Tag Aggregation Data:          Pending
Default Values:                Pending
Catalog URL Rewrites:          Pending
Product Flat Data:             Require Reindex
Category Flat Data:            Pending
Category Products:             Pending
Catalog Search Index:          Pending
```
重新索引单个索引

每个索引都有自己的索引键，当magento需要重新索引时就需要引用它，要获得这些键，你可以使用一下命令
```php
php indexer.php --info
```

你将会得到：
```php
catalog_product_attribute     Product Attributes
catalog_product_price         Product Prices
cataloginventory_stock        Stock Status
tag_summary                   Tag Aggregation Data
mana_db_replicator            Default Values
catalog_url                   Catalog URL Rewrites
catalog_product_flat          Product Flat Data
catalog_category_flat         Category Flat Data
catalog_category_product      Category Products
catalogsearch_fulltext        Catalog Search Index
```

重新索引单个索引，运行一下命令:
```php
php indexer.php --reindex [Index Option Code]
```

可以用逗号来分离多个索引:
```php
php indexer.php --reindex catalog_product_price,catalog_url,catalog_product_flat
```

重新刷新所有索引

下面的代码将通过每个索引循环，来重新建立索引
```php
php indexer.php --reindexall
```

**第三种：在程序中用代码对相应的字段进行刷新索引，这里我拿我用过的刷新价格索引来举例：**
```php
Mage::getResourceModel('catalog/product_indexer_price')->reindexProductIds($productIds)
```

在程序中用代码进行针对性的刷新索引更方便，更省时并且实时性强。
