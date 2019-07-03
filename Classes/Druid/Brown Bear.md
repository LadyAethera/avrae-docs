# Brown Bear Wildshaped Attacks
*By Aethera#2228.*

Three commands for use with the brown bear shape, first a bite attack alone, then claws attack alone, and then the multiattack which *ought* to be the standard full attack for the wildshaped druid in brown bear form.

### Code
```GN
!alias bearbite embed
-title "<name> the bear attacks with a bite!" -f "Attack: |  
**To Hit:**  {{vroll("1d20+5")}}  
**Damage:** {{vroll("1d8+4[piercing]")}}"  
-color <color>  
-thumb https://tinyurl.com/beartoken3y25

!alias bearclaws embed
-title "<name> the bear attacks with their claws!" -f "Attack: |  
**To Hit:**  {{vroll("1d20+5")}}  
**Damage:** {{vroll("2d6+4[slashing]")}}"  
-color <color>  
-thumb https://tinyurl.com/beartoken3y25

!alias bearatk embed
{{ ba = vroll("1d20+5") }}
{{ bc = 1 if ba.dice[8:10]=="20" else 0 }}
{{ bd = vroll("1d8+4[piercing]",1,1 if bc==1 else 0) }}
{{ ca = vroll("1d20+5") }}
{{ cc = 1 if ca.dice[8:10]=="20" else 0 }}
{{ cd = vroll("2d6+4[slashing]",1,2 if cc==1 else 0) }}
-title "<name> the bear attacks with tooth and claw!"
-f "Bite Attack: |  
**To Hit:**  {{str(ba)}}  
**Damage{{" (CRIT!)" if bc==1 else ""}}:** {{str(bd)}}"
-f "Claws Attack: |  
**To Hit:**  {{str(ca)}}  
**Damage{{" (CRIT!)" if cc==1 else ""}}:** {{str(cd)}}"
-footer "Brown Bear | PHB 304 | http://monstercards.ca/5esrd/brown-bear"
-color <color> -thumb https://tinyurl.com/beartoken3y25
```
