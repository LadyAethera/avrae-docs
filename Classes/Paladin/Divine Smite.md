# Divine Smite
*by Aethera#2228*

Outputs smite in a way that matches the !spell output more closely. Checks to make sure you have a spell slot to spend, expends it, and shows you your remaining spell slots. Options include critical hits and undead targets.

Usage:        `!smite [args]`
Arguments: `-l <slot lvl>`
                  `-crit`
                  `-undead`

### Code
```  
!alias smite embed
{{lvl = 1 if "%*%"=="" else int("%2%") if ("%1%"=="-l" and "%2%".isdigit() and int("%2%")>0 and int("%2%")<=9) else int("%3%") if ("%2%"=="-l" and "%3%".isdigit() and int("%3%")>0 and int("%3%")<=9) else int("%4%") if ("%3%"=="-l" and "%4%".isdigit() and int("%4%")>0 and int("%4%")<=9) else 1}}
{{u = 1 if ("%*%"!="" and ("%1%"=="-undead" or "%2%"=="-undead" or "%3%"=="-undead" or "%4%"=="-undead")) else 0}}
{{cr = 1 if ("%*%"!="" and ("%1%"=="-crit" or "%2%"=="-crit" or "%3%"=="-crit" or "%4%"=="-crit")) else 0}}
{{good = 1 if (get_slots(lvl)>0 and lvl<=9) else 0}}
-title "<name> {{"channels a "+("**critical** " if cr else "")+"level "+str(lvl)+" Divine Smite"+(" against undead" if u==1 else "")+"!" if good else "can't muster the divine power to smite."}}"
-desc "{{use_slot(lvl)}}**Damage:** {{set("d",vroll(str(1+lvl+u)+"d8",1,(1+lvl+u if cr else 0)))}} {{d.dice}} [radiant] = `{{d.total}}`"
-f "{{slots_str(lvl)}}"
-footer "Paladin: Divine Smite | PHB 85" -color <color> -thumb <image>
```
