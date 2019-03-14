# Wand of Magic Missiles
*By LadyAethera.*

Usage: `!wandmm`
    `!wandmm [cast-at level]`
    `!wandmm recharge`

### Setup
`!cc create "Wand of Magic Missiles" -reset none -max 7 -min 0 -type bubble`

### Code
```GN
!alias wandmm embed
{{counter = "Wand of Magic Missiles"}}
{{breaks = 1 if get_cc(counter)==1 and roll("1d20")==1 else 0}}
{{d1 = roll("1d4")}}{{d2 = roll("1d4")}}{{d3 = roll("1d4")}}{{d4 = roll("1d4")}}{{d5 = roll("1d4")}}{{d6 = roll("1d4")}}{{d7 = roll("1d4")}}{{d8 = roll("1d4")}}{{d9 = roll("1d4")}}
{{regain = roll("1d6+1")}}
{{level = 0-int(%*%) if ("%*%".isdigit() and int(%*%)>0 and str(%*%)!="recharge") else -1}}
{{active = 1 if get_cc(counter)>0 else 0}}
{{mod_cc(counter, level, True) if (active==1 and "%*%"!="recharge") else 0}}
-title "The Wand of Magic Missiles{{" recharges." if "%*%"=="recharge" else " fires "+str(max(3,2-level))+" missiles." if active==1 else " fizzles." if (active==0 and breaks==0) else " suddenly goes POP!" if breaks==1 else ""}}"
-desc "{{"The wand regains 1d6 + 1 expended charges daily at dawn. This morning you regain "+str(regain)+" charges." if "%*%"=="recharge" else " \n\n**Damage:** "+str(max(3,2-level))+"x d4+1 ["+str(d1+1)+", "+str(d2+1)+", "+str(d3+1)+(", "+str(d4+1) if 2-level>=4 else "")+(", "+str(d5+1) if 2-level>=5 else "")+(", "+str(d6+1) if 2-level>=6 else "")+(", "+str(d7+1) if 2-level>=7 else "")+(", "+str(d8+1) if 2-level>=8 else "")+(", "+str(d9+1) if 2-level>=9 else "")+"]\n\nThe darts all strike simultaneously and you can direct them to hit one creature or several which you can see within range." if (active==1 and breaks==0) else "No charges available to expend, so sad! Better luck next time." if (active==0 and breaks==0) else "The wand explodes into a number of tiny pieces. So much for that." if breaks==1 else "Something strange is going on here. Contact your broker for alternate wand options."}}"
-f "{{set_cc(counter, min(get_cc(counter)+regain,get_cc_max(counter)), True) if "%*%"=="recharge" else ""}}Charges Remaining|{{'◉'*get_cc(counter) + '〇'*(get_cc_max(counter)-get_cc(counter))}}"
-footer "Magic Missile | PHB 257" -color <color>
```
