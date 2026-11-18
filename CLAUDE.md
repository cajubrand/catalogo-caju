# Catálogo Cajú: instruções para o Claude

Site do catálogo de semijoias da **Cajú** (brechó da Jú). As peças são da marca **VERI by Veridiana Quirino**, vendidas em consignação. Cada peça é **única**: tem só uma de cada.

- **Site publicado:** https://cajubrand.github.io/catalogo-caju/ (GitHub Pages, branch `main`, pasta raiz)
- **Publicar:** fazer commit e push na `main`. O site atualiza sozinho em 1 ou 2 minutos.
- **Idioma:** tudo em português do Brasil.

## Estrutura

- `index.html`: o site inteiro (HTML, CSS e JS num arquivo só).
- `img/`: fotos das peças (`.jpg`), `logo-caju.png` (logo bordô, fundo transparente) e `favicon.png`.
- `og-image.jpg`: imagem de prévia do link no WhatsApp (1200 × 630).

Os dados ficam no topo do `<script>` do `index.html`:

- `MES`: nome da coleção (ex.: "Coleção de Novembro").
- `WHATS`: número do WhatsApp do botão "Quero essa".
- `TIPOS`: seções/filtros (Brincos, Colares, Anéis, Pulseiras, Veri Kids). Uma seção só aparece se tiver peça.
- `PECAS`: lista de peças, uma por linha:

```js
{cod:"BR5788", item:"5569209", tipo:"brincos", nome:"Brinco espiral cravejado | prateado", preco:119.00, foto:"img/B14.jpg", vendida:false, obs:"..."},
```

| Campo | Regra |
|---|---|
| `cod` | Referência VERI em maiúsculas (BR5788, CL1305, PL1088, AN…). É o código que a cliente vê e que vai na mensagem do WhatsApp. |
| `item` | Número do Item na planilha (uso interno, para achar a linha). |
| `tipo` | `brincos`, `colares`, `aneis`, `pulseiras` ou `kids` (linha Veri Kids vai em `kids`). |
| `nome` | Nome curto + ` \| dourado`, ` \| prateado` ou ` \| Prata 925`. |
| `preco` | Número. **Sempre o da planilha**, nunca o do site da VERI. |
| `foto` | Primeira foto exibida. |
| `fotos` | Opcional, quando houver mais de uma foto: `["img/a.jpg","img/b.jpg"]`. **A foto no corpo (orelha, pescoço, pulso) vem primeiro.** |
| `vendida` | `true` mostra a faixa VENDIDA e manda a peça para o fim da seção. |
| `obs` | Opcional. Aviso curto embaixo do nome. |

## Planilha de controle

Planilha Google **"Controle de Vendas - Brechó Caju"**, aba **Semijoias**. É a fonte de verdade de preço, metal e código.

- Colunas: Origem, Item, Tipo, **Metal** (O = ouro → dourado; R = ródio → prateado; P = Prata 925), **Modelo** (referência VERI, ex. br5788), Descrição, **Valor**, **Status** (Disponível, Reservado, Vendido, Devolvido), Data da venda, Valor vendido, Forma de pagamento, 20% do valor vendido, Cliente, Observações.
- Não colocar link, ID da planilha nem dados de clientes neste repositório (ele é público).

## Como fazer cada coisa

**Cadastrar peça nova** (a Jú manda a foto, às vezes com nome e preço):
1. Achar a peça na planilha pelo Modelo, pela descrição ou pelo preço. O preço e o metal vêm de lá.
2. Salvar a foto em `img/` como `<COD>.jpg`, quadrada (recorte centralizado ou fundo branco), no máximo 900 px, qualidade ~82.
3. Inserir a linha em `PECAS`, junto das peças do mesmo tipo.
4. Se a foto mostrar outras peças que não vêm junto, colocar `obs` dizendo o que **não** está incluso.
5. Kits: `obs:"Kit com 2 pares."` / `"Kit com 3 pares."`. Pares de ear cuff: `"Vendido em par."`. Peça miúda: `"Peça bem pequena e delicada."`.
6. Se a foto for de outra cor que a peça real, avisar no `obs` até ter a foto certa.

**Marcar venda** ("vendeu a BR5788"):
1. Site: `vendida:true` na peça.
2. Planilha: Status → **Vendido** (conferir antes se a linha é a peça certa). Data, valor, pagamento e cliente só se a Jú informar. Se a cliente não estiver na aba Cadastro Clientes, perguntar antes.
3. Se a peça fazia parte de um conjunto, tirar o aviso de conjunto da outra peça.

**Conjuntos:** quando duas peças combinam, colocar nas duas: `"Faz conjunto com o colar CL2000 (zircônia colorida). Juntos: R$ 198,00."` (soma simples, sem desconto, a menos que a Jú peça).

**Troca de coleção** (todo mês):
1. Antes de apagar, passar para a Jú a lista do que **não** vendeu (para devolução e acerto com a VERI).
2. Remover todas as peças antigas de `PECAS` e as fotos de `img/` (manter `logo-caju.png` e `favicon.png`).
3. Atualizar `MES` e cadastrar as peças novas.

## Identidade visual

- Nome com acento: **Cajú**.
- Topo e rodapé: fundo **sálvia** com o logo **bordô** (`img/logo-caju.png`). Corpo do site em creme.
- Cores: creme `#FBF5EA`, sálvia `#859C7D`, bordô `#7D2337`, azul-noite `#1D2B4D`, azul-pétala `#5669B1`, mostarda `#E2B548`, magenta `#C65081`.
- Fontes: Caveat Brush (títulos das seções) e DM Sans (textos e preços). Não usar mais fontes que isso.
- Botão "Quero essa": magenta. Faixa VENDIDA: bordô.
- Linha de banhos no topo: "Banho de Ródio ou Ouro. Prata 925."

## Funcionalidades já prontas

- Filtro por tipo no topo.
- Botão "Quero essa" abre o WhatsApp com a mensagem pronta (código, nome e preço).
- Tocar na foto abre a foto ampliada; com várias fotos, dá para passar com setas ou deslizando o dedo.

## Cuidados

- Conferir a página depois de mudar (ex.: Chrome headless em 420 px de largura) antes do push.
- Mensagens de commit em português, curtas e descritivas.
