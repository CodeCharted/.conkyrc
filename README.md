out_to_x no
out_to_console yes
short_units yes
update_interval 1

TEXT

[\
# MPD
{ "full_text" : ${if_mpd_playing} "now_playing ", "color" : "\#545454", "separator" : false, "separator_block_width" : 3 },\
{ "full_text" : "${mpd_artist 20} - ${mpd_title 30}"${else}""${endif}, "color" : "\#909737", "min_width" : 300, "separator" : false, "separator_block_width" : 3 },\
# CPU temperature:
{"full_text":"CPU","color":"\#545454","separator":false,"separator_block_width":6},\
{"full_text":"${if_match ${acpitemp}<45}${acpitemp}°C","color":"\#909737","separator":false,"separator_block_width":6},\
{"full_text":"${else}"},\
{"full_text":"${if_match ${acpitemp}<55}${acpitemp}°C","color":"\#b27d12","separator":false,"separator_block_width":6},\
{"full_text":"${else}"},\
{"full_text":"${if_match ${acpitemp}>=55}${acpitemp}°C","color":"\#802828","separator":false,"separator_block_width":6},\
{"full_text":"${else}"},\
{"full_text":"${endif}${endif}${endif}"},\
# Download:
{"full_text":"DOWN","color":"\#545454","separator":false,"separator_block_width":6},\
{"full_text":"${if_match ${downspeedf wlo1}<1000}${downspeed wlo1}","color":"\#909737","separator":false,"separator_block_width":6},\
{"full_text":"${else}"},\
{"full_text":"${if_match ${downspeedf wlo1}<3000}${downspeed wlo1}","color":"\#b27d12","separator":false,"separator_block_width":6},\
{"full_text":"${else}"},\
{"full_text":"${if_match ${downspeedf wlo1}>=3000}${downspeed wlo1}","color":"\#802828","separator":false,"separator_block_width":6},\
{"full_text":"${endif}${endif}${endif}"},\
# Upload:
{"full_text":"UP","color":"\#545454","separator":false,"separator_block_width":6},\
{"full_text":"${if_match ${upspeedf wlo1}<300}${upspeed wlo1}","color":"\#909737","separator":false,"separator_block_width":6},\
{"full_text":"${else}"},\
{"full_text":"${if_match ${upspeedf wlo1}<800}${upspeed wlo1}","color":"\#b27d12","separator":false,"separator_block_width":6},\
{"full_text":"${else}"},\
{"full_text":"${if_match ${upspeedf wlo1}>=800}${upspeed wlo1}","color":"\#802828","separator":false,"separator_block_width":6},\
{"full_text":"${endif}${endif}${endif}"},\
# Memory:
{"full_text":"MEM","color":"\#545454","separator":false,"separator_block_width":6},\
{"full_text":"${if_match ${memperc}<30}${memeasyfree}","color":"\#909737","separator":false,"separator_block_width":6},\
{"full_text":"${else}"},\
{"full_text":"${if_match ${memperc}<70}${memeasyfree}","color":"\#b27d12","separator":false,"separator_block_width":6},\
{"full_text":"${else}"},\
{"full_text":"${if_match ${memperc}>=70}${memeasyfree}","color":"\#802828","separator":false,"separator_block_width":6},\
{"full_text":"${endif}${endif}${endif}"},\
# Weather:
#{"full_text":"☂","color":"\#545454","separator":false,"separator_block_width":6},\
#{"full_text":"${execi 300 ~/bin/weather_simple "EUR|UK|UK241|LONDON"}","color":"\#EEEEEE","separator":false,"separator_block_width":6},\
# Mail:
{"full_text":"MAIL","color":"\#545454","separator":false,"separator_block_width":6},\
{"full_text":"${if_match ${execpi 60 python ~/bin/gmail.py}<=0}${execpi 60 python ~/bin/gmail.py}","color":"\#909737","separator":false,"separator_block_width":6},\
{"full_text":"${else}"},\
{"full_text":"${if_match ${execpi 60 python ~/bin/gmail.py}<2}${execpi 60 python ~/bin/gmail.py}","color":"\#b27d12","separator":false,"separator_block_width":6},\
{"full_text":"${else}"},\
{"full_text":"${if_match ${execpi 60 python ~/bin/gmail.py}>2}${execpi 60 python ~/bin/gmail.py}","color":"\#802828","separator":false,"separator_block_width":6},\
{"full_text":"${endif}${endif}${endif}"},\
# Battery:
#{"full_text":"BAT","color":"\#545454","separator":false,"separator_block_width":6},\
#{"full_text":"${if_match ${battery_percent}<#30}${battery_percent}%","color":"\#802828","separator":false,"separator_block_width":6},\
#{"full_text":"${else}"},\
#{"full_text":"${if_match ${battery_percent}<#70}${battery_percent}%","color":"\#b27d12","separator":false,"separator_block_width":6},\
#{"full_text":"${else}"},\
#{"full_text":"${if_match ${battery_percent}>#=70}${battery_percent}%","color":"\#909737","separator":false,"separator_block_width":6},\
#{"full_text":"${endif}${endif}${endif}"},\
# Dropbox
{"full_text":"DB","color":"\#545454","separator":false,"separator_block_width":6},\
{"full_text":"${execi 6 dropbox status | sed -n 1p}","color":"\#909737","separator":false},\
# Volume:
{"full_text":"VOL","color":"\#545454","separator":false,"separator_block_width":6},\
{"full_text":"${execi 1 amixer sget Master,0 | egrep -o '([0-9]+%|\[(on|off)\])' | sed ':a;N;$!ba;s/\n/ /g'}","color":"\#909737","separator":false},\
# Date:
{"full_text":"|","color":"\#545454","separator":false,"separator_block_width":6},\
{"full_text":"${time %D}","color":"\#aaaaaa","separator":false,"separator_block_width":6},\
# Time:
{"full_text":"|","color":"\#545454","separator":false,"separator_block_width":6},\
{"full_text":"${time %H:%M}","color":"\#aaaaaa","separator":false}\
],
