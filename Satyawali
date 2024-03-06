from telegram import Update
from telegram.ext import Updater, CommandHandler, MessageHandler, Filters, CallbackContext
import logging
import time
from datetime import timedelta

# Replace 'YOUR_BOT_TOKEN' with the actual token obtained from BotFather
TOKEN = '6788141668:AAE7HF6LQXxYEyNSqYStvOkPuJSzlbOu-HA'
# Replace 'YOUR_CHANNEL_ID' with your channel ID
CHANNEL_ID = -1001960613798  # Example format: -1001234567890
# Replace 'YOUR_OWNER_ID' with your Telegram user ID
OWNER_ID = 5290927296  # Example user ID

# Dictionary to store last message time for admins
admin_last_post_time = {}

def start(update: Update, context: CallbackContext) -> None:
    update.message.reply_text('🤘 SATYAWALI BOT IS HERE 🤘')

# Function to handle when a user leaves the channel
def handle_left_member(update: Update, context: CallbackContext) -> None:
    user_id = update.message.left_chat_member.id
    context.bot.kick_chat_member(chat_id=CHANNEL_ID, user_id=user_id)
    update.message.reply_text(f"User {user_id} has left the channel and has been banned.")

# Function to handle messages from admins in the channel
def handle_admin_message(update: Update, context: CallbackContext) -> None:
    user_id = update.message.from_user.id
    current_time = time.time()

    # Check if the user is the owner
    if user_id != OWNER_ID:
        # Check if the admin has posted within the last 20 minutes
        if user_id in admin_last_post_time and current_time - admin_last_post_time[user_id] < 1200:
            # Calculate the remaining time for the time limit
            remaining_time = int(1200 - (current_time - admin_last_post_time[user_id]))

            # Delete the message and notify the admin
            update.message.delete()
            update.message.reply_text(f"Admins are limited to one message every 20 minutes. "
