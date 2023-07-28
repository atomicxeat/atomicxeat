import pygame

# Inicialização do Pygame
pygame.init()

# Configurações da tela
largura_tela, altura_tela = 800, 600
tela = pygame.display.set_mode((largura_tela, altura_tela))
pygame.display.set_caption("Personagem Movendo-se")

# Cores
BRANCO = (255, 255, 255)

# Carregamento do personagem (substitua "personagem.png" pelo nome do arquivo de imagem do seu personagem)
personagem_img = pygame.image.load("personagem.png")
personagem_pos = [100, altura_tela - personagem_img.get_height()]

# Configurações do movimento
velocidade_personagem = 5
pulo_velocidade = 10
gravidade = 1
no_ar = False

# Loop principal do jogo
running = True
while running:
    for event in pygame.event.get():
        if event.type == pygame.QUIT:
            running = False

    # Captura das teclas pressionadas
    teclas = pygame.key.get_pressed()
    
    # Movimento para a esquerda
    if teclas[pygame.K_LEFT]:
        personagem_pos[0] -= velocidade_personagem

    # Movimento para a direita
    if teclas[pygame.K_RIGHT]:
        personagem_pos[0] += velocidade_personagem

    # Lógica do pulo
    if not no_ar:  # Se o personagem não estiver no ar
        if teclas[pygame.K_SPACE]:  # Se a tecla de espaço for pressionada, inicia o pulo
            no_ar = True
    else:  # Se o personagem estiver no ar
        personagem_pos[1] -= pulo_velocidade
        pulo_velocidade -= gravidade

        if pulo_velocidade < -10:  # Define o limite da altura do pulo
            no_ar = False
            pulo_velocidade = 10

    # Limpeza da tela
    tela.fill(BRANCO)

    # Desenho do personagem na tela
    tela.blit(personagem_img, personagem_pos)

    # Atualização da tela
    pygame.display.update()

# Encerra o Pygame
pygame.quit()
