# Picareta & Montanha

Jogo 2D de mineração e progressão (pixel art), em HTML + CSS + JavaScript puro — sem build, sem dependências de servidor.

## Estrutura

```
picareta-e-montanha/
├── index.html   # estrutura da página (HUD, menus, modais)
├── style.css    # todo o visual (HUD, bancadas, menus, slots, responsivo)
├── script.js    # toda a lógica do jogo (mundo, física, mineração,
│                #   picaretas, bolsa, investimento, triturador,
│                #   drones, Pedra Escura, Profundezas, baús,
│                #   menu/pausa, os 5 slots de salvamento e os ícones)
├── assets/icons/        # os 13 ícones já recortados (PNG com transparência)
│   ├── sprite_sheet_original.png   # a folha de sprites original enviada, para referência
│   ├── picareta_madeira.png
│   ├── picareta_pedra.png
│   ├── picareta_carvao.png
│   ├── picareta_ferro.png
│   ├── picareta_ouro.png
│   ├── picareta_esmeralda.png
│   ├── picareta_diamante.png
│   ├── bolsa_jogador.png
│   ├── drone.png
│   ├── velocidade_drone.png
│   ├── capacidade_drone.png
│   ├── encantamento.png     # usado tanto em Eficiência quanto em Looting
│   └── investimento.png
└── README.md    # este arquivo
```

> **Nota sobre os ícones:** o jogo em si (`script.js`) já carrega os 13 ícones
> embutidos como base64 (recortados da folha de sprites que você enviou), então
> não depende dos arquivos em `assets/icons/` para funcionar — eles estão aí
> apenas como referência, caso você queira editar algum ícone depois.

## Como rodar

Abra `index.html` diretamente no navegador (duplo clique) ou sirva a pasta
com um servidor local simples:

```bash
cd picareta-e-montanha
python3 -m http.server 8000
```

e acesse `http://localhost:8000`.

> Se algo não carregar (fontes do Google Fonts, salvamento) ao abrir direto
> via `file://`, tente rodar via servidor local como acima.

## Menu e sistema de mundos (5 slots independentes)

Menu principal: **Iniciar Jogo · Continuar · Novo Jogo · Configurações · Controles · Sair**.
Os três primeiros abrem a tela de 5 slots (cada slot mostra VAZIO ou MUNDO SALVO + dinheiro,
picareta, fase e data do último save). Clique no slot para agir; **VOLTAR** retorna ao menu.

- **Iniciar Jogo** → abre a tela "NOVO JOGO". Slot vazio: cria um mundo novo ali e entra no jogo.
  Slot ocupado: pede "Este slot já possui um mundo salvo. Deseja substituir este mundo?"
  (CANCELAR / SUBSTITUIR). Nada é apagado antes de SUBSTITUIR.
- **Novo Jogo** → mesma regra do item acima.
- **Continuar** → slot salvo: carrega aquele mundo exatamente como foi salvo; slot vazio mostra
  "Este slot está vazio." e permanece na tela.
- **Salvar Jogo** (menu de pausa: ESC ou botão MENU) → vazio: salva direto; ocupado: pede
  confirmação. Também permite carregar e excluir (com confirmação).

Cada slot é uma chave própria no `localStorage` (`save_slot_1` a `save_slot_5`) com o estado
completo do mundo: dinheiro, picareta, bolsa, investimento, encantamentos, drones, inventário,
baús abertos, blocos já minerados, profundidade máxima e posição. O autosave (~2s, ações
importantes, ao abrir o menu de pausa e ao fechar a aba) grava só no slot da sessão atual.

## Cheats de teste (console do navegador)

Com o jogo aberto e a partida em andamento:

```js
addMoney(500000)   // adiciona dinheiro ao saldo atual
setMoney(500000)   // define o saldo exato
debugState()       // retorna o objeto de estado completo p/ inspeção
```

Nenhum dos dois recarrega a página nem reinicia a partida. Eles só
persistem no slot ativo (se houver um).
