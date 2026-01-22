# Unofficial Yougile skill for Claude code

## Usage
1. Copy files to `~\.claude\skills\yougile`
2. Get your api_key (see https://yougile.com/api-v2)
3. Use `/yougile` command in claude code

### Optional

Add permissions to `~/.claude/settings.json` 

```
 "permissions": {                                       
   "allow": [                                           
     "Edit(~/.claude/skills/yougile/yougile.log)",      
     "Bash(curl https://yougile.com:*)",                
     "Read(~/.claude/skills/yougile/docs/**/*.md)"      
   ]   
 }                                                                                               
```