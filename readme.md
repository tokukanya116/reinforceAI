

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

```
	if EGroup_Exists("eg_gold_deposit") == false then
			eg_gold_deposit = EGroup_Create("eg_gold_deposit")
		else
			EGroup_Clear(eg_gold_deposit)
		end
			
			
		-- 查找周边金矿类型(先查小金，不存在则找大金)
		local gold_type = 'small'
		World_GetEntitiesNearPoint(localPlayer, eg_gold_deposit, pos_town_center, 60, OT_Neutral)
		EGroup_Filter(eg_gold_deposit, BP_GetEntityBlueprint("resource_gold_deposit_small"), FILTER_KEEP)
			
		if EGroup_Count(eg_gold_deposit) == 0 then
			World_GetEntitiesNearPoint(localPlayer, eg_gold_deposit, pos_town_center, 60, OT_Neutral)
			EGroup_Filter(eg_gold_deposit, BP_GetEntityBlueprint("resource_gold_deposit"), FILTER_KEEP)
			gold_type = 'big'
		end
			
		-- 如果还是没有，补木头和两个农民给玩家
		if EGroup_Count(eg_gold_deposit) == 0 then
				
			return
		end
			
			
		-- 最近的单个金矿
		local eg_gold_single = EGroup_GetEntityAt(eg_gold_deposit, 1)
		-- 这个金矿对应的坐标
		local gold_position = Entity_GetPosition(eg_gold_single)
			
		-- 设置偏移
		-- 默认小金+标准矿场
		local pos_minecamp = Util_GetPositionFromAtoB(gold_position,pos_town_center,10)
			
		if gold_type == 'big' then
			pos_minecamp = Util_GetPositionFromAtoB(gold_position,pos_town_center,15)
		end
			
		if prefix == 'jpn' then
			pos_minecamp = Util_GetPositionFromAtoB(gold_position,pos_town_center,15)
			if gold_type == 'big' then
				pos_minecamp = Util_GetPositionFromAtoB(gold_position,pos_town_center,20)
			end
		end
			
		local fieldShortName
		-- 根据民族类型找不同的蓝图
		if prefix == 'mal' or prefix == 'ott' or prefix == 'jpn' then
			fieldShortName = 'building_econ_mining_camp_'
		elseif prefix == 'mon' then
			fieldShortName = 'building_house_'  
		else
			fieldShortName ='building_econ_mining_camp_control_'
		end
			
		-- fieldLocation
		field = Entity_CreateFacing(BP_GetEntityBlueprint(fieldShortName..prefix), player.id, pos_minecamp, pos_town_center, true)

		Entity_ForceConstruct(field)
		Entity_SnapToGridAndGround(field, false) --false表示即时构建
		Entity_Spawn(field)
			
		--Entity_SetInvulnerableMinCap(entity, 1.0, 0.0)
			
		local sbp_villager = BP_GetSquadBlueprint("unit_villager_1_"..prefix)
		local sg_player_goldminer = SGroup_CreateIfNotFound("sg_player_goldminer")
		UnitEntry_DeploySquads(localPlayer, sg_player_goldminer, {{sbp = sbp_villager, numSquads = 2 }}, pos_minecamp)
			
		-- 获取玩家农民
		eg_farms = Player_GetEntitiesFromType(localPlayer, "farm")
			
		SGroup_ForEach(sg_player_goldminer, _AssignGoldminer)
```

```
 -- 每次提出一个组成员
    SGroup_Single(sg_single, sid)

    if EGroup_Exists("eg_gold_deposit") == false then
      eg_gold_deposit = EGroup_Create("eg_gold_deposit")
    else
      EGroup_Clear(eg_gold_deposit)
    end
    
    World_GetEntitiesNearPoint(localPlayer, eg_gold_deposit, Util_GetPosition(sid), 25, OT_Neutral)
    EGroup_Filter(eg_gold_deposit, BP_GetEntityBlueprint("resource_gold_deposit_small"), FILTER_KEEP)
    if EGroup_Count(eg_gold_deposit) == 0 then
      World_GetEntitiesNearPoint(localPlayer, eg_gold_deposit, Util_GetPosition(sid), 25, OT_Neutral)
      EGroup_Filter(eg_gold_deposit, BP_GetEntityBlueprint("resource_gold_deposit"), FILTER_KEEP)
    end 

    if eg_gold_deposit ~=nil then
      LocalCommand_SquadEntity(localPlayer, sg_single, SCMD_Gather, eg_gold_deposit, false)
      --EGroup_Clear(eg_gold_deposit)
    else
      print("没有匹配的金矿!"
```

