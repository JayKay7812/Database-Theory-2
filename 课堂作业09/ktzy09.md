# simpleTMX解析
## 结果
![ktzy09_1 pic]()
## 代码
```
<?php
$xml = simplexml_load_file("test1.tmx");
$num_of_rows = count($xml->body->tu);
$xmlTag = array(
    'seg'
);
$study=array();
foreach($xml->children() as $period) {
    $study[] = get_object_vars($period);//获取对象全部属性，返回数组
}
$i=0;
while($i < $num_of_rows)
{
	echo $xml->body->tu[$i]->tuv->seg;
	echo "<br>";
	$i++;
}
echo '<pre>';
print_r($study);

?>
```
#phpQuery解析
## 结果
![ktzy09_2 pic]()
## 代码
```
<?php
include 'phpQuery/phpQuery.php';
phpQuery::newDocumentFile('test1.tmx'); 
echo pq('contact > age:eq(0)');
?>
```
