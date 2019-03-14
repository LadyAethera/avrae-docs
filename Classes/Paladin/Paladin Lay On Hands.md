** Paladin Lay on Hands **  
*By Croebh#5603*  

*Update by minifig#1345*
  
An alias to use the Lay on Hands Paladin class feature. Please set up the CC as per the command, the first one is for Dicecloud, the second for PDFsheet or Gsheet.   
  
To use the lay on hand feature, the command structure is:  
  
`!lay [#|disease|poison]`  
eg. `!lay 8` or `!lay disease`  
  
`!cc create "Lay on Hands" -reset long -max {{5*PaladinLevel}} -min 0`  
`!cc create "Lay on Hands" -reset long -max {{5*level}} -min 0`  
  
```GN
!alias lay embed
-title "<name> Lays on Hands: {{"Cure Disease" if str("%1%")=="disease" and get_cc("Lay on Hands") >= 5 else "Neutralize Poison" if str("%1%")=="poison" and get_cc("Lay on Hands") >= 5 else "Heal for "+str(%1%) if "%1%".isdigit() and get_cc("Lay on Hands") >= %1% else "FIZZLE"}}"  
-desc "{{"Their eyes glow white briefly, channeling a sliver of divine energy, as they touch a creature and cure them of a disease." if str("%1%")=="disease" and get_cc("Lay on Hands") >= 5 else "Their eyes glow white briefly, channeling a sliver of divine energy, as they touch a creature and neutralize a poison afflicting them." if str("%1%")=="poison" and get_cc("Lay on Hands") >= 5 else "Their eyes glow white briefly, channeling a sliver of divine energy, as they touch a creature and heal them for **%1% Hit Points**." if "%1%".isdigit() and get_cc("Lay on Hands") >= %1% else "The lay on hands fails, as they need to have a long rest before channeling again."}}" {{mod_cc("Lay on Hands", -5) if str("%1%")=="disease" and get_cc("Lay on Hands") >= 5 else mod_cc("Lay on Hands", -5) if str("%1%")=="poison" and get_cc("Lay on Hands") >= 5 else mod_cc("Lay on Hands", -%1%) if "%1%".isdigit() and get_cc("Lay on Hands") >= %1% else ""}}   
-f "Lay on Hands Remaining | {{get_cc("Lay on Hands")}}/{{get_cc_max("Lay on Hands")}}" -thumb <image>
```
