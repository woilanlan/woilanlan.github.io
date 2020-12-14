---
title: 获取角色对应的权限列表
date: 2019-03-02 00:02:01
categories:
- EasyUI
tags:
- EasyUI
---

需求描述：

点击某一个角色，查询出所有的权限列表，并勾选该角色已有的权限

建表语句：

```sql
CREATE TABLE `m_group_perm` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `group_id` int(11) DEFAULT NULL,
  `perm_id` int(11) DEFAULT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=11 DEFAULT CHARSET=utf8;

CREATE TABLE `m_perm` (
  `id` int(11) NOT NULL AUTO_INCREMENT,
  `name` varchar(45) DEFAULT NULL,
  `k` varchar(45) DEFAULT NULL,
  PRIMARY KEY (`id`)
) ENGINE=InnoDB AUTO_INCREMENT=6 DEFAULT CHARSET=utf8;
```

查询SQL语句

```sql
# 在关联查询前过滤
select t.*,t1.group_id as enable
from m_perm t
left join m_group_perm t1 on t.id=t1.perm_id and t1.group_id = '2';

# 对关联查询的结果过滤
select * from m_perm p left outer join m_group_perm gp on p.id = gp.perm_id
where gp.group_id = '2';
```

html代码

```html
<div region="west" style="width:230px;">
    <table id="grid-group" class="easyui-datagrid" url="${CTX}/admin/groupList"
    singleSelect="true" rownumbers="true" pagination="false" fit="true">
        <thead>
            <th data-options="field:'name',width:190">角色名称</th>
        </thead>
    </table>
</div>
<div region="center">
    <table id="group-permission" class="easyui-datagrid"
    url="${CTX}/permission/all-groupid"
    rownumbers="true" pagination="false" fit="true">
        <thead>
            <th data-options="field:'ck',checkbox:true"></th>
            <th data-options="field:'k',width:220">权限关键词</th>
            <th data-options="field:'name',width:320">权限名称</th>
        </thead>
    </table>
</div>
```

JS代码

```js
$("#grid-group").datagrid({
    onSelect:function(index, row){
        // 查询所有的权限列表
        console.log(row.id);
        $("#group-permission").datagrid("load",{groupId:row.id});
    }
});

$("#group-permission").datagrid({
    onClickRow:saveGroupPermission,
    onLoadSuccess:function(row){
        // 勾选已有的权限
        var rowData = row.rows;
        $.each(rowData,function(i,n){
            if(n.enable > 0){
                $("#group-permission").datagrid("selectRow",i);
            }
        });
    }
});

//点击增加或移除权限
function saveGroupPermission(index, row) {
    if(row.enable > 0){
        console.log("remove");
        permChange(row.id, false);
    }else {
        console.log("add");
        permChange(row.id, true);
    }
}
```

补充：

[设置checkbox时默认选中](https://blog.csdn.net/hongping626/article/details/10186495)

[自定义添加列](https://blog.csdn.net/nnn_net/article/details/51898502)

[jstl中判断list中是否包含某个值](https://www.cnblogs.com/unidentified/p/8567923.html)