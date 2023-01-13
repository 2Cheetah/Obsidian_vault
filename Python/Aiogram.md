# Aiogram
#python #asyncio #aiogram #telegram

[Aiogram link](https://docs.aiogram.dev/en/latest/)
[Aiogram 3 book in Russian](https://mastergroosha.github.io/aiogram-3-guide/quickstart/)

Первый бот:
```python
import asyncio
import logging
from aiogram import Bot, Dispatcher, types

# Включаем логирование, чтобы не пропустить важные сообщения
logging.basicConfig(level=logging.INFO)
# Объект бота
bot = Bot(token="12345678:AaBbCcDdEeFfGgHh")
# Диспетчер
dp = Dispatcher()

# Хэндлер на команду /start
@dp.message(commands=["start"])
async def cmd_start(message: types.Message):
    await message.answer("Hello!")

# Запуск процесса поллинга новых апдейтов
async def main():
    await dp.start_polling(bot)

if __name__ == "__main__":
    asyncio.run(main())
```