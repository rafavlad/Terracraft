# TerraCraft

Jogo 2D de mineração e progressão em pixel art, feito em HTML + CSS + JavaScript puro.
Sem build, sem servidor e **sem nenhum recurso externo**: fontes, logo, favicon e texturas estão na pasta.

## Como rodar
Abra `index.html` no navegador (duplo clique). Se preferir um servidor local:

```bash
cd terracraft
python3 -m http.server 8000     # depois acesse http://localhost:8000
```

## Estrutura
```
terracraft/
├── index.html      # estrutura da página (menu, HUD, modais) + favicon/título
├── style.css       # identidade visual (paleta, botões de madeira/terra, painéis, responsivo)
├── script.js       # toda a lógica do jogo + cenário pixel art do menu
└── assets/
    ├── branding/
    │   ├── logo.png                      # logo horizontal usada no menu (fundo transparente)
    │   ├── favicon.ico / favicon-16|32|48|64.png / apple-touch-icon.png / icon-192|512.png
    │   └── original/                     # as duas imagens enviadas, intactas
    ├── fonts/                            # Silkscreen e Pixelify Sans (licença OFL incluída)
    ├── textures/                         # texturas dos botões e painéis
    └── icons/                            # ícones das lojas (recortados da folha de sprites)
```

## Identidade visual
- **Logo e favicon** vêm das duas imagens fornecidas. Como elas tinham fundo preto *opaco*, o fundo foi
  removido (ficando transparente) preservando a arte e o contorno escuro; os originais continuam em
  `assets/branding/original/`. O favicon usa a logo **quadrada**, centralizada, sem distorcer nem cortar a arte.
- **Paleta:** verdes (grama), marrons (terra/madeira), cinzas (pedra e minérios), azul (céu) e contornos escuros.
- **Fontes locais:** Silkscreen (títulos/botões) e Pixelify Sans (texto), ambas SIL Open Font License.
- Se o navegador continuar mostrando o ícone antigo, é cache: recarregue forçado (Ctrl+F5) ou limpe o cache do site.

## Menu e mundos (5 slots independentes)
Menu: **Iniciar Jogo · Configurações · Controles · Sair**. *Iniciar Jogo* abre **Novo Jogo / Continuar / Voltar**,
e cada uma leva aos 5 slots (VAZIO ou MUNDO SALVO + dinheiro, picareta, fase e data).

- **Novo Jogo:** slot vazio cria o mundo na hora; slot ocupado pede confirmação (CANCELAR / SUBSTITUIR).
- **Continuar:** carrega o mundo do slot; slot vazio mostra "Este slot está vazio.".
- **Salvar Jogo** (pausa: ESC ou botão MENU): salva num slot (confirma antes de sobrescrever); também carrega/exclui.

Cada slot é uma chave própria do `localStorage` (`save_slot_1` … `save_slot_5`) com o estado completo do mundo.

## Bolsa
A capacidade é **por tipo de bloco** (uma bolsa de 10 guarda 10 de grama, 10 de terra, 10 de pedra...).
Degraus: 10 · 20 · 30 · 40 · 50 · 100 · 150 · 200 · 500.

## Testes no console do navegador
```js
addMoney(500000)   // soma ao saldo
setMoney(500000)   // define o saldo
debugState()       // estado completo do jogo
```
