# Kijiji iPhone Scraper
Scrapes the newest listings from Kijiji and sends a Telegram notification when a new listing is posted.

## How to Run the Application
1. **Create a Bot on Telegram using BotFather**
   - Open Telegram and search for `@BotFather`
   - Send `/start`
   - Send `/newbot`
   - Choose a name and a username (the username must end in **“bot”**, e.g., `kijijisniper_bot`)
   - You’ll receive a token that looks like this:  
     `123456789:ABCDefGhIjkLmNoPqRsTuVwXyZ`
   - Save this token — it’s how your scraper will communicate with Telegram.

2. **Get Your Telegram Chat ID**
   - Open Telegram and search for `@userinfobot`
   - Send `/start`
   - Take note of your chat ID — you’ll need it later.

3. **Create a `.env` File in the Project Folder**
   - Add the following lines:

     ```bash
     TELEGRAM_BOT_TOKEN=
     TELEGRAM_CHAT_ID=
     LOCATION_ID=
     CATEGORY_ID=760
     KEYWORDS=iphone
     ```

   - Add the bot token you received in Step 1 and the chat ID from Step 2.
   - To find the location ID, open [https://www.kijiji.ca/](https://www.kijiji.ca/)
   - Set your location to the city you want to scrape listings from.
   - Press **“Buy & Sell”** and navigate to any category.
   - The URL will look something like this:  
     `https://www.kijiji.ca/b-bmx-bike/saskatoon/c645l1700197?address=Saskatoon%2C%20SK&ll=52.157902%2C-106.6701577&radius=50`
   - The location ID starts with **1700** and is seven digits long.  
   - In this example, the location ID is **1700197** (Saskatoon).
   - Add the location ID to the file.

4. **Update the SEARCH_URL in Kijiji-bot.js**
   - Modify this line
  
      ```JavaScript
      const SEARCH_URL = `https://www.kijiji.ca/b-cell-phone/CityName/${encodeURIComponent(process.env.KEYWORDS)}/k0c${process.env.CATEGORY_ID}l${process.env.LOCATION_ID}?sort=dateDesc`;
      ```
   - Replace CityName with your actual city.
   - For example, if you’re scraping listings in Saskatoon, it should look like this:
  
     ```JavaScript
     const SEARCH_URL = `https://www.kijiji.ca/b-cell-phone/saskatoon/${encodeURIComponent(process.env.KEYWORDS)}/k0c${process.env.CATEGORY_ID}l${process.env.LOCATION_ID}?sort=dateDesc`;
      ```
5. **Run the Application with Docker**
    - Make sure Docker is installed and running.
    - In the project folder, run:
       ```docker
       docker compose build
       ```
    - Once the build completes, run:
       ```docker
       docker compose up
       ```
## Tech Stack
- **Node.js** – Core runtime environment for executing JavaScript on the server.  
- **Cheerio** – For parsing and extracting data from Kijiji HTML pages.  
- **Telegraf** – For interacting with the Telegram Bot API.  
- **dotenv** – For securely loading environment variables from a `.env` file.  
- **Docker** – For containerizing and running the scraper with consistent dependencies.
      
     



