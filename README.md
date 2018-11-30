# magento_note
### magento打印sql语句
```
  $query=$productCollection->getSelectSql(true);
```
```
   $category = Mage::getModel('catalog/category')->load($values['categories']);
        $productCollection = $category->getProductCollection()
       ->addStoreFilter(Mage::app()->getStore()->getId())           
       ->addAttributeToSort('position', 'ASC');
```
 使用命令行来刷新索引管理会极大降低系统消耗，容易成功。

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
