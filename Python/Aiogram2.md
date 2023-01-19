# Aiogram2
#python #asyncio #aiogram #telegram

[Aiogram link](https://docs.aiogram.dev/en/latest/)
[Aiogram 2 book in Russian](https://mastergroosha.github.io/aiogram-2-guide/)
[Aiogram 3 book in Russian](https://mastergroosha.github.io/aiogram-3-guide/quickstart/)

## Введение
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

## Ответы на сообщения

Методы ответа на сообщение:
- `await message.reply('Hello')` отвечает на конкретное сообщение пользователя

![[Pasted image 20230113140632.png]]

- `await message.answer('Hello')` отправляет сообщение в чат, без ответа на конкретное сообщение

![[Pasted image 20230113140654.png]]

Диспетчер регистрирует функции-обработчики, дополнительно ограничивая перечень вызывающих их событий через фильтры. После получения очередного апдейта (события от Telegram), диспетчер выберет нужную функцию обработки, подходящую по всем фильтрам.

Зарегистрировать обработчик можно двумя способами:
- С помощью декоратора:
```python
@dp.message_handler(commands=['start'])
async def test_function(message: types.Message):
	# blah blah
	await message.reply('test passed')
```
- Явно в отдельной строке с помощью метода `register_message_handler`:
```python
async def test_function(message: types.Message):
	# blah blah
	await message.reply('test passed')

dp.register_message_handler(test_function, commands=["start"])
```

В телеграме есть возможность бросать игральную кость с помощью эмодзи 🎲 [Ссылка на документацию, поиск по "dice"](https://docs.aiogram.dev/en/latest/telegram/types/message.html)
В коде реализовывается следующим образом:
```python
await message.answer_dice(emoji="🎲")
```

## id бота и чата

Для того, чтобы узнать *id* бота, можно использовать метод `getMe`:
```shell
curl 'https://api.telegram.org/bot'$AIOGRAM3_TELEGRAM_BOT_API_TOKEN'/getMe'
```

Результатом будет `json`:
```json
{"ok":true,"result":{"id":5863212265,"is_bot":true,"first_name":"aiogram test bo
t","username":"aiogram3_training_Bot","can_join_groups":true,"can_read_all_group
_messages":false,"supports_inline_queries":false}}
```

Для того, чтобы узнать *id* чата:
1. Чат должен быть публичный. Здесь для примера используется `@aiogram_testing_chatgroup`. Дальше чат можно опять сделать приватным.
2. Отправить запрос. Можно использовать, например, метод `sendDice`:
```shell
curl 'https://api.telegram.org/bot'$AIOGRAM3_TELEGRAM_BOT_API_TOKEN'/sendDice?chat_id=@aiogram_testing_chatgroup'
```
3. В ответ будет получен `json` следующего содержания:
```json
{"ok":true,"result":{"message_id":2,"from":{"id":5863212265,"is_bot":true,"first_name":"aiogram test bot","username":"aiogram3_training_Bot"},"chat":{"id":-1001672407335,"title":"test","username":"aiogram_testing_chatgroup","type":"supergroup"},"date":1673602587,"dice":{"emoji":"\ud83c\udfb2","value":4}}}
```

, где *id* чата `-1001672407335`

Зная id какого-либо чата, туда можно отправлять сообщения с помощью метода `bot.send_dice()`. Для этого необходимо, чтобы бот был в этом чате, или чат был публичным:
```python
@dp.message_handler(commands=["dice"])
async def cmd_dice(message: types.Message, bot: Bot):
    await bot.send_dice(-1001672407335, emoji="🎲")
```

## Форматирование текста

Форматирование текста возможно с использованием *HTML тегов*, разметки  *MarkdownV2*.

[MarkdownV2 разметка](https://core.telegram.org/bots/api#markdownv2-style)
Разметка +- похожа на *Markdown* разметку.

За форматирование отвечает аргумент `parse_mode`:
```python
from aiogram import types

# где-то в функции...
await message.answer("Hello, <b>world</b>!", parse_mode=types.ParseMode.HTML)
# Вместо Enum-а можно задать parse_mode в виде обычной строки:
await message.answer("Hello, *world*\!", parse_mode="MarkdownV2")
```

Для того чтобы не указывать в каждом отдельном случае парсер, его можно глобально передать в качестве аргумента объекта `Bot`:
```python
bot = Bot(token="123:abcxyz", parse_mode=types.ParseMode.HTML)

# где-то в функции...
await message.answer("Сообщение с <u>HTML-разметкой</u>")
await message.answer("Сообщение без <s>какой-либо разметки</s>", parse_mode="")
```

Так же можно импортировать модуль `markdown` из `aiogram.utlis` и с помощью метода `text` формировать текст:
```python
from aiogram.utils import markdown

# где-то в функции...
async def text_sample(message: types.Message):
    await message.answer(
        markdown.text(
            markdown.text("__Яблоки__ вес 1 кг\."),
            markdown.text('Старая цена: ~50~ рублей\.'),
            markdown.text('Новая цена: *25* рублей\.'),
            sep="\n",
        ),
    )
```

![[Pasted image 20230113175918.png]]

Есть возможность извлечь текст из полученного сообщения с форматированием и без. Может пригодится для изменения исходного текста:
```python
async def any_text_message(message: types.Message):
    await message.answer(message.text)
    await message.answer(message.md_text)
    await message.answer(message.html_text)
    # Дополняем исходный текст:
    await message.answer(
        f"<u>Ваш текст</u>:\n\n{message.html_text}", parse_mode="HTML"
    )
```

Для экранирования от инъекции можно использовать встроенный метод `escape_md()` и `quote_html()`:
```python
async def any_text_message2(message: types.Message):
    await message.answer(f"Привет, <b>{markdown.quote_html(message.text)}</b>", parse_mode=types.ParseMode.HTML)
    # А можно и так:
    await message.answer(markdown.text("Привет,", markdown.hbold(message.text)), parse_mode=types.ParseMode.HTML)
```

## Медиафайлы

Фото, видео, гифки, геолокация, стикеры итд.
У большинства медиафайлов есть свойства `file_id` и `file_unique_id`. Для повторной отправки файла, следует использовать `file_id`, который указывает на файл, уже загруженный на серверы телеграма.
```python
@dp.message_handler(content_types=[types.ContentType.ANIMATION])
async def echo_document(message: types.Message):
    await message.reply_animation(message.animation.file_id)
```

В *aiogram* встроен метод для загрузки файлов (до 20 MB) на сервер, где крутится бот:
```python
@dp.message_handler(content_types=[types.ContentType.DOCUMENT])
async def download_doc(message: types.Message):
    # Скачивание в каталог с ботом с созданием подкаталогов по типу файла
    await message.document.download()


# Типы содержимого тоже можно указывать по-разному.
@dp.message_handler(content_types=["photo"])
async def download_photo(message: types.Message):
    # Убедитесь, что каталог /tmp/somedir существует!
    await message.photo[-1].download(destination="/tmp/somedir/")
```

Обратите внимание на конструкцию `message.photo[-1]`. Когда пользователь присылает боту изображение, Telegram присылает не один объект, а целый массив с разными размерами одного и того же изображения, отсортированными по возрастанию. В общем случае нас будет интересовать изображение наибольшего размера, стоящее последним (индекс «минус один»).

## hide_link()

Бывают ситуации, когда хочется отправить длинное сообщение с картинкой, но лимит на подписи к медиафайлам составляет всего 1024 символа против 4096 у обычного текстового, а вставлять внизу ссылку на медиа — выглядит некрасиво. Более того, когда Telegram делает предпросмотр ссылок, он берёт первую из них и считывает метатеги, в результате сообщение может отправиться не с тем превью, которое хочется увидеть.  
Для решения этой проблемы ещё много лет назад придумали подход со «скрытыми ссылками» в HTML-разметке. Суть в том, что можно поместить ссылку в [пробел нулевой ширины](http://www.fileformat.info/info/unicode/char/200b/index.htm) и вставить всю эту конструкцию в начало сообщения. Для наблюдателя в сообщении никаких ссылок нет, а сервер Telegram всё видит и честно добавляет предпросмотр.  
Разработчики aiogram для этого даже сделали специальный вспомогательный метод `hide_link()`:
```python
import aiogram.utils.markdown as fmt

@dp.message_handler(commands="test4")
async def with_hidden_link(message: types.Message):
    await message.answer(
        f"{fmt.hide_link('https://telegram.org/blog/video-calls/ru')}Кто бы мог подумать, что "
        f"в 2020 году в Telegram появятся видеозвонки!\n\nОбычные голосовые вызовы "
        f"возникли в Telegram лишь в 2017, заметно позже своих конкурентов. А спустя три года, "
        f"когда огромное количество людей на планете приучились работать из дома из-за эпидемии "
        f"коронавируса, команда Павла Дурова не растерялась и сделала качественные "
        f"видеозвонки на WebRTC!\n\nP.S. а ещё ходят слухи про демонстрацию своего экрана :)",
        parse_mode=types.ParseMode.HTML)
```

## buttons

Два вида кнопок:
- Обычные
- Инлайн-кнопки (inline)
![[Pasted image 20230113225830.png]]

### Обычные кнопки

Такая кнопка представляет собой шаблон сообщения. Следовательно, для нее нужен хендлер.
```python
@dp.message_handler(commands="start")
async def cmd_start(message: types.Message):
    keyboard = types.ReplyKeyboardMarkup()
    button_1 = types.KeyboardButton(text="С пюрешкой")
    keyboard.add(button_1)
    button_2 = "Без пюрешки"
    keyboard.add(button_2)
    await message.answer("Как подавать котлеты?", reply_markup=keyboard)
```

Данный код создает две огромные кнопки шириной во все поле чата. Чтобы исправить это недоразумение, необходимо использовать атрибут `resize_keyboard=True`. С точки зрения API бота, клавиатура - это массив массивов кнопок (массив строк). Метод `add()` каждый раз создает новую строку. Следовательно, чтобы обе кнопки были на одной строке:
```python
@dp.message_handler(commands="start")
async def cmd_start(message: types.Message):
    keyboard = types.ReplyKeyboardMarkup(resize_keyboard=True)
    button_1 = types.KeyboardButton(text="С пюрешкой")
    button_2 = "Без пюрешки"
    keyboard.add(button_1, button_2)
    await message.answer("Как подавать котлеты?", reply_markup=keyboard)
```

### Меню с кнопками

Для того, чтобы добавить в бота меню с кнопками, необходимо создать несколько функций:
```python
async def set_default_commands(dp: Dispatcher) -> None:
    commands = [
        types.BotCommand("start", "Запустить / обновить бота"),
        types.BotCommand("wanna_play", "Сыграем?"),
        types.BotCommand("help", "Помощь"),
    ]
    print("### The default COMMANDS setup has been successfully completed")
    await dp.bot.set_my_commands(commands)


async def set_default_menu(dp: Dispatcher) -> None:
    menu = types.MenuButtonCommands()
    print("### The default MENU setup has been successfully completed")
    await dp.bot.set_chat_menu_button(menu_button=menu)


async def on_startup(dp: Dispatcher) -> None:
    await set_default_commands(dp)
    await set_default_menu(dp)
```

И зарегистрировать это меню во время запуска поллинга с помощью передачи аргумента `on_startup=on_startup`:
```python
if __name__ == '__main__':
    executor.start_polling(dp, on_startup=on_startup, skip_updates=True)
```

