from instabot import Bot
import schedule
import time

# Configuração do bot
bot = Bot()

# Faça login na sua conta
bot.login(username="seu_usuario", password="sua_senha")

# Função para postar conteúdo
def postar_publicacao():
    bot.upload_photo("caminho/para/sua_imagem.jpg", caption="Legenda inspiradora para empreendedores!")
    print("Publicação realizada com sucesso!")

# Função para postar stories
def postar_story():
    bot.upload_story("caminho/para/seu_story.jpg")
    print("Story postado com sucesso!")

# Função para interagir com usuários (comentários e likes)
def engajar_publico():
    hashtags = ["empreendedorismo", "sucesso", "negócios", "mentoria"]
    for hashtag in hashtags:
        bot.like_hashtag(hashtag)
        bot.comment_hashtag(hashtag, text="Conteúdo incrível! Sucesso nos negócios!")
    print("Engajamento realizado com sucesso!")

# Função para seguir usuários de um perfil-alvo
def seguir_perfis_alvo():
    perfis = ["perfil_alvo1", "perfil_alvo2"]
    for perfil in perfis:
        seguidores = bot.get_user_followers(perfil)
        for seguidor in seguidores[:50]:  # Limite de interações
            bot.follow(seguidor)
    print("Seguindo perfis-alvo com sucesso!")

# Agendar tarefas
schedule.every().day.at("08:00").do(postar_publicacao)
schedule.every().day.at("12:00").do(postar_story)
schedule.every(2).hours.do(engajar_publico)
schedule.every().day.at("18:00").do(seguir_perfis_alvo)

# Loop infinito para executar as tarefas agendadas
while True:
    schedule.run_pending()
    time.sleep(1)
