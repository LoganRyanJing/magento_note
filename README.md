# magento_note
### magento打印sql语句
```angular2html
  $query=$productCollection->getSelectSql(true);
  echo $query;
  exit();
```
```angular2html
   $category = Mage::getModel('catalog/category')->load($values['categories']);
        $productCollection = $category->getProductCollection()
       ->addStoreFilter(Mage::app()->getStore()->getId())           
       ->addAttributeToSort('position', 'ASC');
```
 使用命令行来刷新索引管理会极大降低系统消耗，容易成功。
 
### magento清除索引
 
我们来看下步骤，如果你在使用linux服务器，登入你的ssh客户端，切换目录到你magento根文件夹中名字是shell的文件中。（切换文件夹的命令：cd）
```
php -f indexer.php -- -reindex catalog_url
```

**具体命令如下：**
```angular2html
        php -f indexer.php -- -reindex catalog_product_attribute
        php -f indexer.php -- -reindex catalog_product_price
        php -f indexer.php -- -reindex catalog_url
        php -f indexer.php -- -reindex catalog_product_flat
        php -f indexer.php -- -reindex catalog_category_flat//不是经常刷新
        php -f indexer.php -- -reindex catalog_category_product
        php -f indexer.php -- -reindex catalogsearch_fulltext
        php -f indexer.php -- -reindex cataloginventory_stock

        php -f indexer.php -- -reindex tag_summary
```

**下面的代码将通过每个索引循环，来重新建立索引**
```php
php indexer.php --reindexall
```

### cron 设置定时任务
一般编辑cron任务
```angular2html
    crontab -e
```
cron启动，停止，重启
```angular2html
    service cron start //启动服务
    
    service cron stop //关闭服务
    
    service cron restart //重启服务
    
    service cron reload //重新载入配置
```

