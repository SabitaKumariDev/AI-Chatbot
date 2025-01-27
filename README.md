**Rock-Paper-Scissors Chatbot** 🤖
This is a simple AI-powered chatbot built using the Rasa framework. The bot can engage in basic conversations and play a game of Rock-Paper-Scissors with the user.

**Project Overview**
This project is a conversational AI chatbot built with Rasa, an open-source framework for building contextual AI assistants. The bot can:
Handle basic intents like greetings, farewells, and affirmations.
Play a game of Rock-Paper-Scissors with the user.
Use custom actions to manage game logic.

**Features**
**Basic Conversations**: The bot can respond to greetings, farewells, and simple questions.
**Rock-Paper-Scissors Game**: The bot can play a game of Rock-Paper-Scissors with the user.
**Custom Actions**: The bot uses custom actions to handle game logic and determine the winner.
**Session Management**: The bot maintains session data and can carry over slots to new sessions.

**Files Overview**
Here’s a brief description of the key files in this project:

**config.yml**: Contains the configuration for the NLU pipeline and dialogue management policies.
**credentials.yml**: Stores credentials for connecting to external platforms (currently not used).
**domain.yml**: Defines the intents, entities, slots, responses, and session configuration.
**endpoints.yml**: Configures the action server and model storage.
**actions.py**: (Not included yet) This file will contain the custom actions, such as the logic for the Rock-Paper-Scissors game.

**Prerequisites**
Before running the project, ensure you have the following installed:
Python 3.7 or higher
Rasa (Install via pip install rasa)

**Installation**
1. Clone the repository:
git clone https://github.com/your-username/your-repo-name.git
cd your-repo-name

2. Install dependencies:
pip install -r requirements.txt

**Usage**
**1. Train the Rasa model:**
rasa train

**2. Run the action server:**
rasa run actions

**3. Start the chatbot:**
rasa shell

**4. Interact with the bot:** You can now chat with the bot and play Rock-Paper-Scissors!

**Custom Actions**
The bot uses custom actions to handle the Rock-Paper-Scissors game logic. These actions are defined in the actions.py file (not included in the repository yet). Here’s an example of what the action_play_rps might look like:

from rasa_sdk import Action, Tracker
from rasa_sdk.executor import CollectingDispatcher
import random

class ActionPlayRPS(Action):
    def name(self) -> str:
        return "action_play_rps"

    def run(self, dispatcher: CollectingDispatcher, tracker: Tracker, domain: dict) -> list:
        user_choice = tracker.get_slot("choice")
        bot_choice = random.choice(["rock", "paper", "scissors"])
        
        if user_choice == bot_choice:
            result = "It's a tie!"
        elif (user_choice == "rock" and bot_choice == "scissors") or \
             (user_choice == "paper" and bot_choice == "rock") or \
             (user_choice == "scissors" and bot_choice == "paper"):
            result = "You win!"
        else:
            result = "I win!"
        
        dispatcher.utter_message(text=f"I chose {bot_choice}. {result}")
        return []

**Future Improvements**
Here are some ideas for improving the project:
1. Add more intents and entities to handle more complex conversations.
2. Integrate with external APIs (e.g., weather, news) to provide additional functionality.
3. Deploy the bot to messaging platforms like Facebook Messenger, Slack, or WhatsApp.
4. Use advanced NLU models like BERT or Transformers for better understanding of user input.
