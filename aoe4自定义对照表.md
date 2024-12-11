```
AI_CreateEncounter 514 好像是给ai创建一个目标
```

##### 控制台命令

```

FOW_ForceRevealAllUnblockedAreas() 开全图
localPlayer = World_GetPlayerAt(index) 找玩家
AI_SetDifficulty(localPlayer, 3) 重设难度
localPlayer.raceName
print(localPlayer.raceName)
```

##### bluePrints映射

###### entity 实体

```
outpost:哨塔
ovoo:敖包
pasture:牧场
barracks:兵营
stable:马厩
archery_range:靶场
blacksmith:铁匠铺
scar_dock:码头
siege_workshop:攻城武器库
monastery:寺，教堂
university:大学
landmark_age1~3_defense:防御地标
landmark_age1~3_economy:经济地标
town_center_capital:首都tc
town_center:小tc
mining_camp:矿场
econ_food:磨坊
econ_wood:伐木场
scar_market:市场
house:房屋
wonder:奇观
farm:田
```

```
如需要生成新ui，参考 ags_diplomacy_ui.scar
```

##### scar  脚本

**超级有用的脚本**

```
返回a向b的方向 1935
计算两个实体的距离 857
根据 字符串 直接返回一个 技能包蓝图 560 (注意事项看 Ability)
根据 技能包原型的蓝图id 返回 一个技能蓝图 566 (注意事项看 Ability)
向SGroup下发攻击命令 653
命令一个小队攻击移动到一个位置（任何位置都可以查询）。可以排队，可以按照计划，可以在半径内搜索掩护。sgroup可以选择在到达标记附近时删除，如果没有标记，则在半径10内删除 705
命令攻击者sgroup攻击移动到战略点目标；当它是可捕获的，sgroup将捕获它 1556
命令班组捕获班组武器实体组 1611
命令小队在指定位置建造建筑物，或继续在现有建筑物上建造。该命令还检查该位置是否已经存在建筑物，如果建筑物类型正确，小队将继续建造它。1816

```

##### **Ability**

注：技能包组需要在 Attributes 里 先打开 open Attributes 读取才能查看(!没有编辑权限，只能调用)

```
LocalCommand_SquadEntityAbility(player_id, official_gold, eg_single, bp_supervise, true, false)
```

##### 其他

###### 异常

实体生成错误会导致资源变成不可选(但游戏能正常运行且不报错，需要逐行注释差错)
