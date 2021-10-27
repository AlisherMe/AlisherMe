import vk_api
from vk_api.longpoll import VkLongPoll, VkEventType

vk_session = vk_api.VkApi(token="fb904e4f89c934e9ed85c0b45f70bad0222f1ab613a8758c0cc45f3a8c4bda790c0f05591fb427e6fbb71")
session_api = vk_session.get_api()
longpool = VkLongPoll(vk_session)

def send_some_msg(id, some_text):
    vk_session.method("messages.send", {"user_id":id, "message":some_text,"random_id":0})

for event in longpool.listen():
    if event.type == VkEventType.MESSAGE_NEW:
        if event.to_me:
            msg = event.text.lower()
            id = event.user_id
            if msg == "Начать":
                send_some_msg(id, '''Приветствую
==========================================
Список доступных команд:
"команды" - повторная отправка данного сообщения.
"анкета" - образец анкеты для вступления в клан.
"инфо" - информация о клане.
==========================================
Бот отвечает только на команды. ''')

for event in longpool.listen():
    if event.type == VkEventType.MESSAGE_NEW:
        if event.to_me:
            msg = event.text.lower()
            id = event.user_id
            if msg == "начать":
                send_some_msg(id,'''Приветствую
==========================================
Список доступных команд:
"команды" - повторная отправка данного сообщения.
"анкета" - образец анкеты для вступления в клан.
"инфо" - информация о клане.
==========================================
Бот отвечает только на команды.''')
