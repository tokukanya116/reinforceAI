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
```

##### **Ability**

注：技能包组需要在 Attributes 里 先打开 open Attributes 读取才能查看(!没有编辑权限，只能调用)

```
LocalCommand_SquadEntityAbility(player_id, official_gold, eg_single, bp_supervise, true, false)
```

##### 其他

###### 异常

实体生成错误会导致资源变成不可选(但游戏能正常运行且不报错，需要逐行注释差错)
