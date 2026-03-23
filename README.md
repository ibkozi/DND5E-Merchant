Multi-Shop Merchant System
Note: Only works with 2014 Sheets
How the system works
This version has no built-in shop items.
That means:
•	every item must be created with !additem
•	shops start empty
•	a shop only sells items whose stock you set on that merchant
•	templates only work if the items already exist
Basic workflow
Step 1: create items
!additem healing_potion|Healing Potion|60|0.5|Consumables|Standard healing potion.
!additem rope_hempen|Rope (Hempen, 50 ft)|2|10|Standard Gear|A sturdy 50-foot hemp rope.
!additem feather_fall_coin|Feather Fall Coin|25|0|Minor Magic|A Sharn trinket that slows a fall.
Step 2: stock a merchant
!setstock healing_potion 3 @{target|Merchant|token_id}
!setstock rope_hempen 5 @{target|Merchant|token_id}
!setstock feather_fall_coin 1 @{target|Merchant|token_id}
Step 3: players use the shop
!shop @{target|Merchant|token_id}
!buy healing_potion 1 @{target|Merchant|token_id}
________________________________________
Important setup rules
For merchants
Each shop needs:
•	a character sheet
•	a token on the map
•	that token must represent the merchant character
For players
For buy/sell commands, the player must:
•	select their own token
•	target the merchant token
________________________________________
GM COMMANDS
1. Add a new item to the master catalog
Command
!additem key|Name|Cost|Weight|Category|Description
What it does
Creates a new item that can be used in shops, templates, granting, buying, and selling.
Example
!additem healing_potion|Healing Potion|60|0.5|Consumables|Standard healing potion.
Another example
!additem brass_spyglass|Brass Spyglass|75|1|Curios|A dented but functional spyglass from Upper Dura.
Notes
•	key should be short and unique
•	cost is in gp
•	weight can be decimal
•	category is used for grouping in shop menus
________________________________________
2. Remove an item from the master catalog
Command
!removeitem item_key
What it does
Deletes an item from the catalog.
Example
!removeitem brass_spyglass
Warning
This removes it from the system catalog. Existing stock attributes or player inventory rows are not automatically cleaned up.
________________________________________
3. List all catalog items
Command
!items
What it does
Shows every item currently defined in the system.
Example
!items
Use this for
•	checking item keys
•	confirming that an item was added correctly
________________________________________
4. Add a template
Command
!addtemplate template_key|item_key:qty,item_key:qty
What it does
Creates a reusable shop template.
Example
!addtemplate starter|healing_potion:2,rope_hempen:5,feather_fall_coin:1
Another example
!addtemplate magic_shop|feather_fall_coin:4,phial_clear_mind:3,whisper_key:1
Notes
•	items in the template must already exist in the catalog
•	quantities must be whole numbers
________________________________________
5. List all templates
Command
!templates
What it does
Shows all saved template keys.
Example
!templates
________________________________________
6. Load a template into a shop
Command
!loadtemplate template_key @{target|Merchant|token_id}
What it does
Clears the targeted merchant’s current stock, then loads the template stock.
Example
!loadtemplate starter @{target|Merchant|token_id}
Another example
!loadtemplate magic_shop @{target|Merchant|token_id}
Important
This is a wipe and replace action.
________________________________________
7. Clear a shop’s stock
Command
!clearshop @{target|Merchant|token_id}
What it does
Removes all stock attributes for all known items from the targeted merchant.
Example
!clearshop @{target|Merchant|token_id}
Use this for
•	emptying a store
•	resetting a merchant before loading a new template
________________________________________
8. View full stock for a shop
Command
!stock @{target|Merchant|token_id}
What it does
Shows every catalog item for that merchant, including items at 0 stock.
Example
!stock @{target|Merchant|token_id}
Use this for
•	full inventory management
•	checking what is missing
•	confirming zeros
________________________________________
9. Set exact stock for one item
Command
!setstock item_key qty @{target|Merchant|token_id}
What it does
Sets a merchant’s stock for one item to an exact number.
Example
!setstock healing_potion 5 @{target|Merchant|token_id}
Another example
!setstock feather_fall_coin 0 @{target|Merchant|token_id}
Use this for
•	direct control
•	making an item unavailable
•	resetting stock precisely
________________________________________
10. Add to current stock
Command
!restock item_key qty @{target|Merchant|token_id}
What it does
Adds the quantity to the merchant’s current stock.
Example
!restock healing_potion 3 @{target|Merchant|token_id}
Another example
!restock rope_hempen 10 @{target|Merchant|token_id}
________________________________________
11. Show low-stock items
Command
!stocklow @{target|Merchant|token_id}
What it does
Shows items at or below the default threshold of 2.
Example
!stocklow @{target|Merchant|token_id}
Custom threshold
!stocklow @{target|Merchant|token_id} 0
!stocklow @{target|Merchant|token_id} 5
Meaning
•	0 = only out of stock
•	2 = low stock warning
•	5 = broader restock view
________________________________________

PLAYER COMMANDS
12. Browse a shop
Command
!shop @{target|Merchant|token_id}
What it does
Shows only items the targeted merchant currently has in stock.
Example
!shop @{target|Merchant|token_id}
Important
Player should select their token before clicking Buy buttons.
________________________________________
13. Buy an item
Command
!buy item_key qty @{target|Merchant|token_id}
What it does
Buys an item from the targeted merchant.
Example
!buy healing_potion 1 @{target|Merchant|token_id}
Another example
!buy rope_hempen 2 @{target|Merchant|token_id}
Requirements
•	player token selected
•	merchant token targeted
•	enough gold
•	enough merchant stock
________________________________________
14. Open sell menu
Command
!sellshop @{target|Merchant|token_id}
What it does
Shows the selected character’s sellable items with clickable Sell buttons.
Example
!sellshop @{target|Merchant|token_id}
Requirements
•	player token selected
•	merchant token targeted
________________________________________
15. Sell an item
Command
!sell item_key qty @{target|Merchant|token_id}
What it does
Sells an item from the selected character to the targeted merchant.
Example
!sell healing_potion 1 @{target|Merchant|token_id}
Another example
!sell rope_hempen 2 @{target|Merchant|token_id}
Notes
•	sale value is 50% of listed price
•	merchant stock increases
•	player gold increases
________________________________________
RECOMMENDED GM WORKFLOWS
Create a new item and stock it in one shop
1. Add item
!additem healing_potion|Healing Potion|60|0.5|Consumables|Standard healing potion.
2. Set stock
!setstock healing_potion 4 @{target|Merchant|token_id}
3. Players can now buy it
!shop @{target|Merchant|token_id}
________________________________________
Create a reusable starter shop
1. Add items
!additem healing_potion|Healing Potion|60|0.5|Consumables|Standard healing potion.
!additem rope_hempen|Rope (Hempen, 50 ft)|2|10|Standard Gear|A sturdy 50-foot hemp rope.
!additem feather_fall_coin|Feather Fall Coin|25|0|Minor Magic|A Sharn trinket that slows a fall.
2. Create template
!addtemplate starter|healing_potion:2,rope_hempen:5,feather_fall_coin:1
3. Load template into merchant
!loadtemplate starter @{target|Merchant|token_id}
________________________________________
Reset a store and make it empty
!clearshop @{target|Merchant|token_id}
________________________________________
Check what needs restocking
!stocklow @{target|Merchant|token_id}
________________________________________
Open quick-click restock menu
!restockmenu @{target|Merchant|token_id}
________________________________________
TROUBLESHOOTING
“Target a merchant token”
You forgot to target the merchant token.
“Select your token before buying/selling”
The player did not select their own token.
“Invalid item key”
The item does not exist in the custom catalog.
Use:
!items
“Template not found”
The template key does not exist.
Use:
!templates
Shop shows nothing
That merchant has no stock above 0.
Use:
!stock @{target|Merchant|token_id}
Buy fails
Check:
•	player selected token
•	merchant targeted
•	stock exists
•	enough gp
________________________________________
FAST REFERENCE
GM
!additem key|Name|Cost|Weight|Category|Description
!removeitem item_key
!items
!addtemplate template_key|item_key:qty,item_key:qty
!templates
!loadtemplate template_key @{target|Merchant|token_id}
!clearshop @{target|Merchant|token_id}
!stock @{target|Merchant|token_id}
!setstock item_key qty @{target|Merchant|token_id}
!restock item_key qty @{target|Merchant|token_id}

Players
!shop @{target|Merchant|token_id}
!buy item_key qty @{target|Merchant|token_id}
!sellshop @{target|Merchant|token_id}
!sell item_key qty @{target|Merchant|token_id}

