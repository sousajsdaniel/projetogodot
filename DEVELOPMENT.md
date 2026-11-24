# Desenvolvimento — Futebol Adventure

## Implementação atual

Uma fase de plataforma de 6400 × 720, com câmera horizontal, gravidade, plataformas, obstáculos, buracos, três pontos de apoio e entrada do estádio bloqueada até a derrota do chefão.

A jogabilidade inclui carrinho, bolas com munição finita e colisão contínua, saúde, três vidas, recuperação por kits e reaparecimento no último apoio. Há árbitros atiradores, robôs VAR perseguidores e um chefão Cartão Vermelho com ataques sinalizados. Menu, pausa, Game Over e vitória integram o fluxo completo. As músicas e efeitos são sintetizados pelo próprio jogo.

## Personalizar

- Percurso, inimigos e itens: `scenes/main/main.gd`.
- Arte do cenário: `scenes/main/background.gd`.
- Vida, munição e controles: `scenes/globals.gd`.
- Movimento e combate: `scenes/player/player.gd`.
- Aparência do jogador: `scenes/characters/footballer.gd`.
- Comportamento dos inimigos: `scenes/enemy/enemy.gd`.
- Interface e telas: `scenes/ui/`, `scenes/menu/`, `scenes/screens/`.
- Áudio: `scenes/audio/audio.gd`.

O terreno usa a camada 1, o jogador a 2 e os inimigos a 4. As bolas colidem com terreno e inimigos; os cartões atingem o terreno e o jogador. O menu e a interface usam coordenadas de tela, enquanto a fase usa coordenadas do mundo.

## Verificação

Execute os scripts em `tests/` conforme o README. Para revisão visual, execute F5 e confira menu, primeira região, pontos de apoio, arena, pausa e telas de resultado. Ao alterar o percurso, confirme que cada salto obrigatório cabe no alcance do jogador e que a munição continua acessível.