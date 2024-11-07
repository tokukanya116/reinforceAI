

```
设置游戏模式的表(95)
将当前模块注册到全局(445)
--这函数的用法是：括号中填入字符，这个函数会把带这个字段前缀且在全局范围内的所有函数全部调用。
--即AGS_GLOBAL_SETTINGS_MODULE = "AGS_GlobalSettings"表示只要你函数是AGS_GlobalSettings_xxxx这种的都会被调用(scardoc:445)
```

未确认函数

```
ags_tree_bombardment貌似是找出实体周边的树删掉(AGS_TreeBombardment_DestroyTreeGroup)
通过EGroup_GetClosestEntity

 Entity_CalculatePassableSpawnPosition貌似返回安全位置？
 
```

```
EGroup_GetClosestEntity
```

