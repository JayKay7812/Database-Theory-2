# 使用jqGrid加载json格式文件的数据

## index.html 核心代码
```
$(document).ready(function() {
            $("#jqGrid").jqGrid({
                url:'texts.json',
                datatype: "json",
                colNames: ['zh_CN', 'en_US'],
                colModel: [{
                    name: 'zh_CN',
                    width: 75
                }, {
                    name: 'en_US',
                    width: 150
                }, ],
                autowidth: false,
                height: 300,
                rowNum: 150,
                loadonce: true,
                pager: "#jqGridPager"
            });
        });
```

## texts.json
```
{
    "rows": [
        {
            "zh_CN": "桃花源记",
            "en_US": "Tale of the Peach Eden"
        },
        {
            "zh_CN": "晋太元中，武陵人捕鱼为业。",
            "en_US": "During the Taiyuan years of Eastern Jin Dynasty (376-396), there was a man from Wulin who lived on fishing. "
        },
        {
            "zh_CN": "缘溪行，忘路之远近。",
            "en_US": "One day he paddled his way along a creek and just forgot how far he had gone."
        },
        {
            "zh_CN": "忽逢桃花林，夹岸数百步，中无杂树，芳草鲜美，落英缤纷，渔人甚异之。",
            "en_US": "When he came to his mind, he found himself in a vast forest of peach trees with flower blooming everywhere. It seemed to stretch for several hundred Bu and no other trees were among them except peach tree. The grass land was tender and beautiful, while the trees were flourishing their petals, which made it a curious view for the fisherman."
        },
        {
            "zh_CN": "复前行，欲穷其林。",
            "en_US": "So, he carried on, hoping to reach the end of the forest."
        }
    ]
}
```

# 将数据库中的数据包装为json格式，并使用jqGrid加载
## 数据库截图
![khzy04_1 pic]()

## index.html
```
$(document).ready(function() {
            $("#jqGrid").jqGrid({
                <font color=blue>url:'db.php',</font>
                datatype: "json",
                colNames: ['zh_CN', 'en_US'],
                colModel: [{
                    name: 'zh_CN',
                    width: 75
                }, {
                    name: 'en_US',
                    width: 150
                }, ],
                autowidth: false,
                height: 300,
                rowNum: 150,
                loadonce: true,
                pager: "#jqGridPager"
            });
        });
```
## db.php
```
<?php
  $dbhost = 'localhost:3306';  //mysql服务器主机地址
  $dbuser = 'root';      //mysql用户名
  $dbpass = '';//mysql用户名密码
  $conn = mysqli_connect($dbhost, $dbuser, $dbpass);
  if(! $conn )
  {
  die('Could not connect: ' . mysqli_error());
  }

  mysqli_select_db( $conn,'jqgrid_test' );
  mysqli_query($conn,"set names utf8");
  $sql="SELECT * FROM texts";
  $return = array();
  $huoqu = mysqli_query($conn,$sql);
  while($row= mysqli_fetch_array($huoqu,MYSQLI_ASSOC)){
      $return['rows'][] = $row;
    }
  
  echo(json_encode($return));
?>
```
