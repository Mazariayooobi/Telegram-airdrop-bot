# Telegram-airdrop-botimport telebot from telebot.types import InlineKeyboardMarkup, InlineKeyboardButton import os

TOKEN = os.getenv("7655086279:AAH6-wt2m77mBKHekYGEE-ClqJcBP3y0Kxk")  # توکن را از متغیر محیطی می‌خواند bot = telebot.TeleBot(TOKEN)

CHANNELS = ["@Shortvideos553", "@ATOM_Chanel", "@Airdropchannel786"]  # لیست کانال‌ها

@bot.message_handler(commands=['start']) def start(message): user_id = message.chat.id keyboard = InlineKeyboardMarkup() keyboard.add(InlineKeyboardButton("بررسی عضویت ✅", callback_data="check")) bot.send_message(user_id, "سلام! برای دریافت ایردراپ، در کانال‌های زیر عضو شو:", reply_markup=keyboard)

def check_membership(user_id): for channel in CHANNELS: chat_member = bot.get_chat_member(channel, user_id) if chat_member.status not in ["member", "administrator"]: return False return True

@bot.callback_query_handler(func=lambda call: call.data == "check") def callback_check(call): user_id = call.message.chat.id if check_membership(user_id): bot.send_message(user_id, "✅ عضویت تأیید شد! حالا می‌توانی از ایردراپ استفاده کنی.") else: bot.send_message(user_id, "❌ هنوز در همه کانال‌ها عضو نیستی! دوباره تلاش کن.")

bot.polling()

