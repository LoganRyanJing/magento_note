# magento_note
### magento打印sql语句
''' 
  $query=$productCollection->getSelectSql(true);
        echo $query;
        exit();
'''

   $category = Mage::getModel('catalog/category')->load($values['categories']);
//        $productCollection = $category->getProductCollection()
//            ->addStoreFilter(Mage::app()->getStore()->getId())
//            ->addAttributeToSort('position', 'ASC');
