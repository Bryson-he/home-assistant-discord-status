# Home Assistant Discord Game Status

A custom Home Assistant button card to display your Discord game status, including game name, state, details, and images. This project leverages the **Discord Game Integration** and a custom **Button Card** to create a visually appealing dashboard element.

## Features
- Displays the game you are playing on Discord.
- Shows game state, details, and associated image.
- Clean, responsive card design.
- Highly customizable layout and styles.

## Dependencies
- **[Home Assistant](https://www.home-assistant.io/)**
- **[HACS](https://hacs.xyz/)** (Home Assistant Community Store)
- **[Custom Button Card](https://github.com/custom-cards/button-card)**
- **[Discord Game Integration](https://github.com/LordBoos/discord_game)**

---

## Setup Guide

### Step 1: Set Up Discord Game Integration
1. Follow the [Discord Game Integration guide](https://github.com/LordBoos/discord_game) to set up the integration.
2. Create a Discord bot and get its token:
   - Go to [Discord Developer Portal](https://discordapp.com/developers/applications/) and create a new application.
   - Add a bot to the application.
   - Enable all "Privileged Gateway Intents."
   - Copy the bot token and invite the bot to your server.
3. Add the integration in Home Assistant:
   - Paste your bot token into the configuration.
   - Select the users and channels to track.

### Step 2: Install Custom Button Card
1. Open HACS in Home Assistant.
2. Go to **Frontend > Explore & Download Repositories**.
3. Search for **Button Card** and install it.
4. Restart Home Assistant.

### Step 3: Add the Button Card Configuration

1. Add the following configuration to your Lovelace dashboard using the **Manual Card** option:

```yaml
# Example button-card.yaml
- type: custom:button-card
  entity: sensor.discord_user_userid_game_image_large
  show_name: false
  show_state: false
  show_icon: false
  custom_fields:
    image: >
      [[[ if (states['sensor.discord_user_userid_game'].state !== 'unknown') 
      return `<img src="${states["sensor.discord_user_userid_game_image_large"].attributes.entity_picture}" style="width: 75px; height: 75px; border-radius: 10%;">`; 
      return ''; ]]]
    info: >
      [[[ if (states['sensor.discord_user_userid_game'].state === 'unknown') 
      return '<div><b>Not playing game</b></div>'; 
      return `
         <div style="display: flex; flex-direction: column; margin-left: 10px;">
           <div style="font-weight: bold; color: white; margin-bottom: 5px;">
             ${states['sensor.discord_user_userid_game'].state}
           </div>
           <div style="color: gray; margin-bottom: 5px;">
             ${states['sensor.discord_user_userid_game_state'].state}
           </div>
           <div style="color: gray;">
             ${states['sensor.discord_user_userid_game_details'].state}
           </div>
         </div>`; ]]]
  styles:
    card:
      - border-radius: 10px
      - padding: 10px
      - background-color: '#1c1c1c'
      - box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2)
      - color: white
      - display: flex
      - flex-direction: row
      - align-items: center
    custom_fields:
      image:
        - display: flex
        - justify-content: center
        - align-items: center
        - margin-right: 10px
      info:
        - display: flex
        - flex-direction: column
        - justify-content: center
        - align-items: flex-start
```
---
### Important: 
In the above configuration, replace userid with your own Discord user ID. You can find this ID from the Discord game integration sensors. The user ID is typically a numeric string specific to your Discord account and is required for correctly referencing the sensor data related to your Discord user.
---

## Screenshots
![image](https://github.com/user-attachments/assets/5f4765d9-1ed8-4155-83db-0dcf347b371e)

---

## Contributing
Contributions are welcome! If you have ideas for improvements or run into issues, please open an issue or submit a pull request.


