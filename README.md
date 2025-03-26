from aiogram import Bot, Dispatcher, types
from aiogram.types import InlineKeyboardMarkup, InlineKeyboardButton
from aiogram.utils import executor

TOKEN = "7730641662:AAHYFkPt53UTZrFvNZh3k5e03gSHngMDu1g"
CHANNEL_ID = -1002332580178  # Kanalingiz ID'si

bot = Bot(token=TOKEN)
dp = Dispatcher(bot)

@dp.message_handler(commands=['start'])
async def start(message: types.Message):
    user = await bot.get_chat_member(CHANNEL_ID, message.from_user.id)
    if user.status in ["member", "administrator", "creator"]:
        await message.answer("Kino kodini yozing:")
    else:
        markup = InlineKeyboardMarkup().add(
            InlineKeyboardButton("📢 Kanalga qo‘shilish", url="https://t.me/kinouzbek77")
        )
        await message.answer("Botdan foydalanish uchun avval kanalga a'zo bo‘ling!", reply_markup=markup)

if __name__ == "__main__":
    executor.start_polling(dp, skip_updates=True)
