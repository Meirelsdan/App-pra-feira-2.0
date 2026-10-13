# App-pra-feira-2.0
Um aplicativo criado pra senhoras(es) de idade que não conseguem ir para a feira e tem a opção de comprar de casa.   ainda em teste.
# FeiraApp

Aplicativo para quem não consegue ir à feira (pensado principalmente para pessoas com mais idade) comprar de casa, direto dos feirantes.

## Como rodar

```bash
npm install
npm run dev
```

Abra http://localhost:8080.

## Google Maps

O mapa de feiras usa a biblioteca oficial [`@vis.gl/react-google-maps`](https://visgl.github.io/react-google-maps/).

1. No [Google Cloud Console](https://console.cloud.google.com/google/maps-apis), crie um projeto e ative:
   - **Maps JavaScript API** (mostrar o mapa)
   - **Geocoding API** (transformar endereço em ponto no mapa e vice-versa)
2. Crie uma chave de API e **restrinja** a chave ao domínio do app (HTTP referrers) e a essas duas APIs.
3. Copie `.env.example` para `.env` e preencha `VITE_GOOGLE_MAPS_API_KEY`.
4. (Opcional) Crie um Map ID em *Map Management* e coloque em `VITE_GOOGLE_MAPS_MAP_ID`. Sem ele o app usa o `DEMO_MAP_ID`.

Sem chave o app continua funcionando: as feiras aparecem em lista e o botão "Como chegar" abre o Google Maps normalmente.

## O que tem no app

- **Início** — atalhos do catálogo, feiras próximas, feirantes e produtos em destaque.
- **Catálogo** — 13 categorias (frutas, verduras, legumes, raízes, temperos, ovos e laticínios, peixes, grãos, pães, doces e mel, pastel e bebidas, flores, cestas). Cada categoria é separada por tipo (ex.: Frutas → cítricas, tropicais, vermelhas, de pomar, melões). Busca ignora acentos e há filtro "só orgânicos".
- **Feiras (mapa)** — mapa com as feiras oficiais (verde) e as marcadas pela comunidade (laranja). Clientes e feirantes podem marcar uma feira nova tocando no mapa, buscando o endereço ou usando a localização atual.
- **Sacola Fixa** — barra sempre visível acima do menu, separada da navegação, mostrando total e itens. Ao tocar, abre a lista completa agrupada por feirante.
- **Perfil → Carteira** — Pix, cartão de crédito/débito, vale-alimentação e dinheiro (com troco). Do cartão só ficam salvos bandeira e 4 últimos dígitos.

## Antes de ir para produção

Hoje os dados ficam no `localStorage` do navegador (sacola, carteira e feiras marcadas). Para valer de verdade é preciso:

- um backend (ex.: Supabase) para salvar as feiras marcadas e compartilhá-las entre usuários, com moderação;
- um gateway de pagamento (Mercado Pago, Pagar.me, Stripe…) que tokenize os cartões — o app nunca deve receber o número completo nem o CVV.
