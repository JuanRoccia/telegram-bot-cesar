estoy trabajando en un bot de telegram y uiero subirlo a pythonanywhere para mantenerlo activo, el proyecto cuenta con una carpeta telegram-bot-env que adentro tiene las carpetas include lib scripts y un archivo pyvenv, ademas el proyecto cuenta con un archivo .env con el BOT_TOKEN y el archivo bot.py:

# Token de telegram para conectar el bot

# Comandos:
# saludo - Saludo de prueba
# start - Inicia el bot y muestra información útil
# info - Obtiene las últimas noticias sobre trading
# update - Recibe la última actualización de precios de criptomonedas
# help - Muestra ayuda sobre cómo usar el bot
# comm - Muestra los comandos disponibles
# criptomonedas - Lista las principales criptomonedas
# definiciones - Definiciones básicas del trading cripto
# analisis - Últimos análisis y noticias criptográficas
# herramientas - Herramientas útiles para traders
# cursos - Cursos y recursos educativos
# soporte - Contacto para soporte tecnico

# os library in order to read the environment variables stored in the system.
import os
from dotenv import load_dotenv
load_dotenv()
import telebot

BOT_TOKEN = os.environ.get('BOT_TOKEN')
print("TOKEN: ", BOT_TOKEN)
if BOT_TOKEN is None:
    raise ValueError("BOT_TOKEN is not set. Please check your .env file.")

bot = telebot.TeleBot(BOT_TOKEN, parse_mode='Markdown') # You can set parse_mode by default. HTML or MARKDOWN
# bot = telebot.TeleBot("TOKEN", parse_mode=None)

@bot.message_handler(commands=['saludo', 'hello', 'iniciar', 'hola', 'inicio'])
def send_welcome(message):
    bot.reply_to(message, "Como andas Cesar xd")

@bot.message_handler(commands=['start'])
def send_welcome(message):
    welcome_text = (
        "*¡Hola! Bienvenido a JuanRocciaBot* 🤖\n\n"
        "Aquí podrás *mantenerte actualizado* con las últimas noticias e información sobre *trading y criptomonedas*.\n"
        "Utiliza los siguientes comandos para explorar el bot:\n\n"
        "/info - *Noticias recientes sobre trading*\n"
        "/update - *Última actualización de precios de criptomonedas*\n"
        "/help - *Más información sobre cómo usar el bot*\n"
        "/comm - *Lista de comandos disponibles*\n"
        "/criptomonedas - *Lista las principales criptomonedas*\n"
        "/definiciones - *Definiciones básicas del trading de criptomonedas*\n"
        "/analisis - *Últimos análisis y noticias criptográficas*\n"
        "/herramientas - *Herramientas útiles para traders*\n"
        "/cursos - *Cursos y recursos educativos*\n"
        "/soporte - *Contacto para soporte técnico*"
    )
    bot.reply_to(message, welcome_text)

@bot.message_handler(func=lambda msg: True)
def echo_all(message):
    bot.reply_to(message, message.text)

bot.infinity_polling()

Actualmente estoy configurando una nueva web app en pythonanywhere y necesito que me guies para hacer todo correctamente, como framework creo que voy a elegir django o flask y luego tengo que poner la version de python correctamente, como hago apra saber que version me corresopnde? tendria que ver la version que estoy usando en mi proyecto?