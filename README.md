# TerraCraft

Jogo 2D de mineração e progressão em pixel art, em HTML + CSS + JavaScript puro.
Sem build, sem servidor e **sem recursos externos**: fontes, logo, favicon e texturas estão na pasta.
Funciona no computador (teclado e mouse) e no celular (controles de toque).

## Como rodar
Abra `index.html` no navegador. Se preferir um servidor local:

```bash
cd terracraft
python3 -m http.server 8000     # depois acesse http://localhost:8000
```

## Estrutura
```
terracraft/
├── index.html      # estrutura (menu, HUD, controles virtuais, janelas), título e favicon
├── style.css       # identidade visual, HUD compacto, controles de toque, layouts responsivos
├── script.js       # toda a lógica do jogo
└── assets/
    ├── branding/   # logo, favicons (PNG/ICO), ícone de iPhone, e os arquivos originais enviados
    ├── fonts/      # Silkscreen e Pixelify Sans (licença OFL incluída)
    ├── textures/   # texturas dos botões e painéis
    └── icons/      # ícones das lojas
```

## Controles
**Computador:** setas/A-D mover · Espaço/W pular · clique segurando num bloco para minerar · E interagir · ESC menu.

**Celular** (aparecem sozinhos em telas de toque; em computador com tela de toque aparecem no primeiro toque):
- **Joystick esquerdo:** andar (quanto mais longe do centro, mais rápido). **▲** pula (acima do joystick).
- **Joystick direito:** mira a picareta em qualquer direção (encaixa nas 8 direções principais).
  Um contorno tracejado mostra qual bloco será atingido. **⛏** (acima do joystick) segura para minerar na direção da mira.
- **INTERAGIR:** aparece no centro, embaixo, só quando há bancada, triturador ou baú ao alcance.
- **☰ / ⌂ / 🎒** (canto superior esquerdo): menu, voltar à superfície, inventário. Toque na faixa de status (canto superior direito) para expandir.
- Dedos independentes: dá para andar, mirar e pular ao mesmo tempo.
- Em **Configurações**: ligar/desligar os controles de toque e "Minerar ao mirar" (minera sem segurar o botão).

## Economia
- **Bolsa:** a capacidade é **por tipo** de bloco. Degraus: 10 · 20 · 30 · 40 · 50 · 100 · 150 · 200 · 500 · **1.000 (R$ 29.500)**.
- **Preços** (R$ por unidade, antes de multiplicadores) numa tabela única: grama 1, terra 2, pedra 3, carvão 4, ferro 5,
  ouro 6, esmeralda 7, diamante 8, totem 16; os minérios da Pedra Escura têm preço próprio.
  O triturador do jogador e a venda automática dos drones usam a mesma função de avaliação.
- **Drones:** buscam minérios (carvão, ferro, ouro, esmeralda, diamante) respeitando o nível da picareta; quando a carga enche, voltam,
  vendem o lote (uma única vez) e retomam o trabalho. Na Bancada de Máquinas: quantidade (1 a 40), velocidade (voo e mineração, 1x a 10x)
  e capacidade de carga (10 a 100), cada uma com nível atual e efeito real mostrados.

## Menu e mundos
Menu: **Iniciar Jogo · Configurações · Controles · Sair**. *Iniciar Jogo* → **Novo Jogo / Continuar** → 5 slots independentes
(`localStorage`: `save_slot_1` … `save_slot_5`). Substituir um mundo sempre pede confirmação.

## Testes no console
```js
addMoney(500000)   // soma ao saldo
setMoney(500000)   // define o saldo
debugState()       // estado completo
```
