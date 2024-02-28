# SaveEcoBot sensor for Home Assistant

[SaveEcoBot](https://www.saveecobot.com/en) is a nice Ukrainian environmental project.

[Home Assistant](https://www.home-assistant.io/) is an awesome home automation system

This piece of code adds SaveEcoBot API info with Home Assistant. 

## Installation HACS

- go to HACS -> Integrations
- press + Explore & Add repositories button
- type SaveEcoBot2 in search field and click at integration name
- press Install this repository to HACS button
- press Install button (if you have outdated version of Home Assistant -- check integration version in Wiki )
- restart Home Assistant
- go to Home Assistant Settings -> Integrations -> Add Integration (right bottom conner)
- type SaveEcoBot2 in search field and click at integration name. Clean browser cache if nothing found.


## Initial steps (manual)
- Copy this repo's files into `<home assistant config directory>/custom_components/save_eco_bot2` (don't forget to [install HASS](https://www.home-assistant.io/getting-started/) first)

## Next step

2.  Enable `SaveEcoBot2` platform in `configuration.yaml`:
```yaml
sensor:
 - platform: save_eco_bot2
```
3. Restart Home Asssistant

## Customizing configuration

After initial configuration (and if SaveEcoBot data available, of course, check the logs) you'll see two new HASS services:

- save_eco_bot2.show_cities
- save_eco_bot2.show_city_stations

(See the `Developer tools - Services` page of your HASS at `<HASS_url>:<HASS_PORT>/developer-tools/service`)

Calling these services will give you an additional info for filtering available data. Service calls will create a notifications in notifications area:

`save_eco_bot2.show_cities` will show the list of available cities

`save_eco_bot2.show_city_stations` will show stations for certain city. You'll have to provide the city name as shown in `save_eco_bot.show_cities` call in service parameters:
```yaml
city: Kyiv
```

the output will give you Stations IDs, e.g.

```
SaveEcoBot Stations
Stations in Kyiv:

SAVEDNIPRO_010 - Mykhaila Lomonosova Street, 73
SAVEDNIPRO_1004 - vulytsia Henerala Zhmachenka, 4
SAVEDNIPRO_1266 - vulytsia Kostiantynivska, 73
SAVEDNIPRO_1274 - prospekt Heroiv Stalinhrada, 6K8
...
```

## Final settings

Update your `configuration.yaml` with filtering parameters and restart HASS. This will create all available sensors for all chosen stations.
All three filters are applied together, so i wouldn't recommend you to use them all, consider getting all IDs you need, or provide city name only 

## Example config

```yaml
sensor:
 - platform: save_eco_bot2
   station_ids:
     - SAVEDNIPRO_3422
     - SAVEDNIPRO_1294
     - SAVEDNIPRO_1004
   city_names:
     - Kyiv
     - Lviv
     - Odesa
   station_names:
     - "prospekt Slobozhanskyi, 127A"
```

Have fun! 