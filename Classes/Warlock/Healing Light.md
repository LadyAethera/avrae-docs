# Healing Light  
*by ChaoticUnreal#4387*  
  
*updated by LittleBlueNA#0570*

Subtracts from Healing Light counter, creating counter if there is none. Rolls healing for Healing Light and displays remaining dice pool.
  
```GN
!alias hl embed  
{{set("counter", "Healing Light")}}  
{{set("heal",1 if "%1%" == "%1"+"%" or (("%1%").isdigit() == False) else int("%1%"))}}  
{{create_cc_nx(counter, 0, 1 + level, "long", "default")}}  
{{set("cast", 1 if get_cc(counter)>=int(heal) else "")}}  
{{mod_cc(counter,-int(heal),"True") if cast else ""}}  
{{set("healdice",vroll(str(heal)+"d6"))}}  
-title "<name> uses Healing Light!"  
-desc "At 1st level, you gain the ability to channel celestial energy to heal wounds. You have a pool of d6s that you spend to fuel this healing. The number of dice in the pool equals 1 + your warlock level.  
As a bonus action, you can heal one creature you can see within 60 feet of you, spending dice from the pool. The maximum number of dice you can spend at once equals your Charisma modifier (minimum of one die). Roll the dice you spend, add them together, and restore a number of hit points equal to the total.  
Your pool regains all expended dice when you finish a long rest."  
{{"-f \"Healing|**Healing: **"+str(healdice)+"\"" if cast else "-f \"**Not enough dice**\""}}  
-f "{{counter}}|{{get_cc(counter)}}/{{get_cc_max(counter)}}"  
-color <color> -thumb <image>
```
