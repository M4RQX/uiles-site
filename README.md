# Uiles Instalações Elétricas — Proposta de site (2 versões)

Proposta de website para a **Uiles Instalações Elétricas** ([@uiles.instalacoes.oficial](https://www.instagram.com/uiles.instalacoes.oficial/)),
empresa de Brendo Uiles. Duas direções completas, estáticas e autocontidas — zero build, zero dependências além de Google Fonts.

## Estrutura

| Caminho | O que é |
|---|---|
| `index.html` | Chooser de pitch — mostra as 2 versões lado a lado (para enviar ao cliente) |
| `v1/index.html` | **Versão 1 "A Gente Resolve!"** — bold, fiel ao Instagram (preto + dourado + vermelho, Anton/Archivo) |
| `v2/index.html` | **Versão 2 "Vermelho de Oficina"** — cores do mascote (vermelho Milwaukee + preto + dourado), etiquetas sticker, sombras duras (Saira Condensed/Saira); hero mascot-ready |
| `assets/obras/` | 6 fotos reais extraídas do reel do Instagram (frames hi-res) |
| `.claude/skills/` | Skills `copywriting` + `cro` (coreyhaines31/marketingskills) usadas na copy |

## Ver localmente

```bash
npx http-server uiles -p 5188 -c-1
# → http://localhost:5188 (chooser) · /v1/ · /v2/
```

## Dados do cliente (placeholders → reais)

Cada versão tem **um único ponto de edição**: o objeto `CONFIG` no `<script>` do fundo do ficheiro.

```js
const CONFIG = {
  whatsapp : "5500000000000",   // só dígitos: 55 + DDD + número
  phone    : "(00) 00000-0000", // como aparece no site
  cidade   : "Sua Cidade",
  cnpj     : "00.000.000/0001-00",
  instagram: "https://www.instagram.com/uiles.instalacoes.oficial/"
};
```

Além do CONFIG, atualizar **no `<head>` de cada versão**:
- JSON-LD: `telephone` e `addressLocality`
- `<link rel="canonical">` quando houver domínio

Procurar `TODO:client` nos ficheiros para ver tudo o que falta confirmar
(cidade, número, CNPJ, certificações tipo NR-10, depoimentos).

## Assets em falta (pedir ao cliente)

- **Logo original** (PNG/SVG com fundo transparente) → `assets/logo.png` — atualmente o badge é um SVG inline recriado
- **Arte do mascote** (PNG transparente) → `assets/mascote.png` — **a V2 já tem o slot armado**: assim que o ficheiro existir, o hero troca a foto pelo mascote sobre o painel vermelho automaticamente; até lá mostra foto de obra (fallback completo)
- **`assets/og.png`** — já existe um placeholder fotográfico (frame do reel + barras douradas); substituir por arte final com logo quando houver, e trocar o caminho por URL absoluto quando o domínio existir
- Mais fotos de obras (as atuais vêm do reel; comprimir com `sips -Z 1600 foto.jpg`)
- Confirmar com o cliente: atendem urgências/24h? (não prometido no site até confirmação)

## Decisões de design

- **Sem testemunhos inventados** — secção de prova social só entra com depoimentos reais
- **Sem embed do Instagram** (≈1 MB de JS e quebra no browser in-app) — galeria estática + link
- Links WhatsApp são `<a href="wa.me/...">` puros com mensagem pré-preenchida por serviço (escapam do webview do Instagram)
- Vermelho Milwaukee só decorativo (falha contraste AA em texto corrido)
- `prefers-reduced-motion` desliga ticker/circuito/reveals

## Deploy (Vercel)

```bash
cd uiles && vercel --prod   # site estático, sem config extra
```

Sugestão de domínio a verificar com o cliente: `uilesinstalacoes.com.br` / `uiles.com.br`.
