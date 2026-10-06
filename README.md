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

## Sistema de salvamento (5 slots independentes)

O jogo tem **5 slots de salvamento totalmente independentes**, acessíveis
pelo botão **"Salvar Jogo"** no menu principal e no menu de pausa (tecla
ESC ou botão MENU durante a partida).

- **Slot vazio** → botão "SALVAR AQUI" salva ali direto.
- **Slot ocupado** → mostra dinheiro, picareta, fase (Montanha / Pedra
  Escura / Profundezas) e data do último save, com os botões "SALVAR AQUI"
  (pede confirmação antes de sobrescrever), "CARREGAR" e "EXCLUIR" (também
  com confirmação).
- **Continuar** (menu principal) retoma automaticamente o último slot
  usado. Se nenhum slot tiver sido salvo ainda, avisa que não há partida
  salva.
- **Novo Jogo** nunca mexe nos slots já salvos — ele só desvincula a sessão
  atual de qualquer slot até você escolher salvar em um.
- Cada slot guarda o estado completo: dinheiro, picareta, bolsa,
  investimento, eficiência, looting, drones, inventário, baús abertos,
  os blocos já minerados na montanha e a posição do jogador.

Internamente cada slot é uma chave própria no `localStorage`
(`save_slot_1` a `save_slot_5`), nunca compartilhada entre si. Progresso de
uma versão anterior (de slot único) é migrado automaticamente para o
**Slot 1** na primeira vez que o jogo carrega.

## Cheats de teste (console do navegador)

Com o jogo aberto e a partida em andamento:

```js
addMoney(500000)   // adiciona dinheiro ao saldo atual
setMoney(500000)   // define o saldo exato
debugState()       // retorna o objeto de estado completo p/ inspeção
```

Nenhum dos dois recarrega a página nem reinicia a partida. Eles só
persistem no slot ativo (se houver um).
