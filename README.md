import os
from telegram import Update
from telegram.ext import Application, CommandHandler, MessageHandler, filters, ContextTypes

BOT_TOKEN = os.getenv("BOT_TOKEN")

async def start(update: Update, context: ContextTypes.DEFAULT_TYPE):
    await update.message.reply_text("سلام! 🎉 به ربات معمایی ۱۳۶۴ خوش اومدی.\n\nبرای شروع معماها بنویس: شروع")

async def echo(update: Update, context: ContextTypes.DEFAULT_TYPE):
    text = update.message.text
    if text == "شروع":
        await update.message.reply_text("🔑 مرحله ۱: رمز اینه → کلمه‌ای که با ح شروع میشه و توی آسمونه چیه؟")
    else:
        await update.message.reply_text("فعلاً فقط بنویس 'شروع' تا اولین معما بیاد 🙂")

def main():
    app = Application.builder().token(BOT_TOKEN).build()
    app.add_handler(CommandHandler("start", start))
    app.add_handler(MessageHandler(filters.TEXT & ~filters.COMMAND, echo))
    app.run_polling()

if __name__ == "__main__":
    main()
