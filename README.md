[main.py](https://github.com/user-attachments/files/34246705/main.py)# animated-broccoli
[Upload# Welcome to your Python project!
import asyncio
import logging
import os
 
from aiogram import Bot, Dispatcher
from aiogram.client.default import DefaultBotProperties
from aiogram.enums import ParseMode
from aiogram.fsm.storage.memory import MemoryStorage, SimpleEventIsolation
from dotenv import load_dotenv
 
import db
import handlers_test
import handlers_user
 
 
async def main() -> None:
    load_dotenv()
    token = os.getenv("8816129790:AAHP4yN40SbO6nrsiLHJuhj4zaQM9ye7vqQ")
    if not token:
        raise SystemExit("8816129790:AAHP4yN40SbO6nrsiLHJuhj4zaQM9ye7vqQ topilmadi. .env faylini tekshiring (.env.example ga qarang).")
    db.DB_PATH = os.getenv("DB_PATH", "bot.db")
    await db.init_db()
 
    bot = Bot(token, default=DefaultBotProperties(parse_mode=ParseMode.HTML))
    # SimpleEventIsolation: bir foydalanuvchining tugmalari ketma-ket qayta ishlanadi
    # (ikki marta bosilganda ball ikki marta yozilmaydi).
    dp = Dispatcher(storage=MemoryStorage(), events_isolation=SimpleEventIsolation())
    dp.include_routers(handlers_user.router, handlers_test.router)
 
    await bot.delete_webhook(drop_pending_updates=True)
    await dp.start_polling(bot)  # long polling
 
 
if __name__ == "__main__":
    logging.basicConfig(level=logging.INFO)
    asyncio.run(main())ing main.py…]()
