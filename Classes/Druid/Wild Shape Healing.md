# Combat Wild Shape Healing (Circle of the Moon)
*by Aethera#2228*

Rolls Xd8 healing for the wildshaped druid and sacrifices a spell slot. Defaults to a level 1 spell if that is available.

Usage:        `!wildheal [args]`
Arguments:    `-l <slot lvl>`

### Code
```  
!alias wildheal embed
{{ lvl = 1 if "&*&"=="" else int("&2&") if ("&1&"=="-l" and "&2&".isdigit() and int("&2&")>0 and int("&2&")<=9) else 1 }}
{{good = 1 if (get_slots(lvl)>0 and lvl<=9 and get_hp()<hp) else 0}}
-title "<name> {{"heals using a level "+str(lvl)+" spell slot!" if good else "doesn't have the magical strength to heal." if get_hp()<hp else "doesn't need to heal at this time."}}"
{{set("heal",vroll(str(lvl)+"d8"))}}
{{set_hp(min(get_hp()+heal.total,hp)) if good else ""}}
{{"-f 'Healing:|"+str(heal)+"'" if good else ""}}
-f "HP|{{hp_str()}}"
-f "{{use_slot(lvl) if good else ""}}{{slots_str(lvl)}}"
-footer "Circle of the Moon: Combat Wild Shape | PHB 69" -color <color> -thumb <image>
```
