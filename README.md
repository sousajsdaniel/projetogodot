# Futebol Adventure

Jogo de plataforma 2D em Godot 4.7.2, com uma única fase contínua. Um jogador de futebol atravessa o bairro e a avenida, enfrenta a arbitragem e o VAR e derrota o Cartão Vermelho para entrar no Estádio da Vitória.

## Executar

Importe `project.godot` no Godot e pressione **F5**. Na tela inicial, escolha **Iniciar** com o mouse, Enter ou Espaço.

## Controles

| Ação | Teclas |
| --- | --- |
| Andar | A/D ou setas esquerda/direita |
| Pular | Espaço, W ou seta para cima |
| Carrinho (curto alcance) | J, no chão |
| Chutar bola (longo alcance) | K ou Enter |
| Pausar / continuar | Esc ou P; botão Pausar na interface |
| Ativar / desativar áudio | M |

A bola acompanha o jogador enquanto há munição. Cada chute consome uma bola e acerta o primeiro inimigo ou obstáculo no trajeto. O carrinho não consome munição. Os ataques têm intervalo e não se repetem ao manter a tecla pressionada.

## Objetivo e sobrevivência

- Siga para a direita, saltando sobre os buracos e caixas. Plataformas opcionais oferecem itens e posições para enfrentar inimigos elevados.
- Você começa com **3 vidas**, **100 de saúde** e **10 bolas**.
- Bolas no percurso repõem **5 munições**; kits recuperam **30 de saúde**, até 100. Kits ficam disponíveis quando a saúde está cheia.
- Ao zerar a saúde ou cair em um buraco, perde-se uma vida. Com vidas restantes, o jogador reaparece no último ponto de apoio, com saúde restaurada e pelo menos 5 bolas. Os inimigos derrotados permanecem derrotados.
- As bandeiras marcam três pontos de apoio. Perder a última vida leva à tela de **Game Over**, com opções de tentar novamente e voltar ao menu.
- Árbitros lançam cartões amarelos e vermelhos. Robôs VAR perseguem e causam dano por contato.
- O chefão **Cartão Vermelho**, com braços e pernas, usa saltos, impacto e cartões. Derrote-o para abrir os portões e **atravesse a entrada do estádio** para vencer.
- A pausa congela a simulação e oferece continuar, reiniciar e voltar ao menu. Reiniciar começa uma nova partida com o estado inicial.

## Áudio

Trilhas instrumentais distintas para menu, fase, Game Over e vitória. Efeitos de carrinho, chute, dano no jogador e nos inimigos, coleta, cartões, VAR e chefão. O áudio é sintetizado localmente pelo jogo; não depende de downloads ou serviços externos.

## Estrutura

- `scenes/globals.gd`: controles, saúde, vidas, munição, pontos de apoio e troca de telas.
- `scenes/menu/` e `scenes/screens/`: início, derrota e vitória.
- `scenes/main/`: percurso, câmera, colisões, cenário e portões do estádio.
- `scenes/player/` e `scenes/characters/`: física de plataforma, combate e desenho do jogador.
- `scenes/enemy/`: arbitragem, VAR, chefão e cartões lançados.
- `scenes/projectile/`: bolas chutadas e colisão contínua.
- `scenes/item/`: munição e kits médicos.
- `scenes/ui/`: interface e pausa.
- `scenes/audio/`: músicas e efeitos sonoros.
- `tests/`: testes de integração executáveis sem interface.

## Testar

Com Godot no PATH, execute na raiz:

```powershell
godot --headless --path . --script tests/gameplay.gd
godot --headless --path . --script tests/projectiles.gd
godot --headless --path . --script tests/attacks.gd
godot --headless --path . --script tests/enemies.gd
godot --headless --path . --script tests/interface.gd
```

As cinco suítes cobrem movimento, combate, munição, coleta, vidas, pontos de apoio, inimigos, pausa, áudio e fluxo até a vitória. O percurso também foi validado em uma partida automatizada com inimigos ativos, sem teleporte ou munição extra.

## Exportar

Instale os templates de exportação da mesma versão do editor. O projeto tem presets **web** e **Windows Desktop**.

```powershell
New-Item -ItemType Directory -Force build/web, build/desktop
godot --headless --path . --export-release web build/web/Futebol.html
godot --headless --path . --export-release 'Windows Desktop' 'build/desktop/Futebol Adventure.exe'
python -m http.server 8000 --directory build/web
```

Abra `http://localhost:8000/Futebol.html`. No navegador, clique em Iniciar para liberar o áudio. A exportação usa Compatibility e não requer threads.
