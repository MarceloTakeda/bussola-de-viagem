# Bússola de Viagem

Aplicativo web para organizar e planejar viagens: busca de atrações, alimentação, farmácias e serviços de saúde num raio escolhido, rotas no mapa, registro de voos e outros deslocamentos com recomendações de horários, roteiro editável e planilha de gastos.

Funciona no navegador de celulares, tablets e computadores, sem instalação e sem chaves de API.

## Funcionalidades

**Planejamento da viagem**
- Destino, datas de check-in e check-out e local de hospedagem (busca por endereço ou toque no mapa).
- Raio de busca livre, de 0,5 a 100 km.
- Viagens salvas no próprio navegador, com edição e exclusão.

**Explorar**
- Pontos turísticos, alimentação, farmácias, saúde e mercados ao redor da hospedagem ou da sua localização atual.
- Resumo e foto da Wikipédia para atrações.
- Índice de confiabilidade para restaurantes (horário publicado, contato, endereço, opções para dietas, dados recentes) e filtros vegetariano, vegano e sem glúten.
- Rotas a pé, de carro ou de bicicleta, com distância, tempo e link para navegar no Google Maps.

**Deslocamentos**
- Avião, carro próprio, carro alugado, ônibus, trem, navio/balsa, transfer/táxi e outros, marcados como ida, volta ou durante a viagem.
- Para voos: janela do check-in online, horário de chegada ao aeroporto, prazo de despacho de bagagem, horário no portão, hora de sair de casa ou da hospedagem e opções de traslado do aeroporto até a hospedagem (táxi/aplicativo, metrô/trem, ônibus, transfer).
- Para carro próprio: distância, tempo com paradas e custo estimado de combustível.
- Para carro alugado: retirada, devolução, diárias e cuidados.

**Roteiro**
- Geração automática que agrupa atrações próximas por dia, sugere almoço e respeita os horários de chegada e partida.
- Edição completa: horários, ordem, mover entre dias, atividades próprias com local no mapa, observações e anotações do dia.
- Previsão do tempo para os dias que estiverem a até 16 dias.

**Gastos**
- Lançamentos com categoria, forma de pagamento e moeda, com conversão para reais.
- Orçamento, saldo, média por dia e totais por categoria.
- Valores dos deslocamentos incluídos automaticamente.
- Exportação para Excel (.xlsx, com fórmulas), CSV e cópia para o Google Planilhas.

## Tecnologia

O app é uma página única em **HTML, CSS e JavaScript**, sem etapa de compilação.

- **Por que JavaScript no navegador:** roda em qualquer celular, tablet ou computador; pode ser adicionado à tela inicial; e as APIs abertas de mapas aceitam chamadas diretas do navegador, dispensando servidor.
- **Bibliotecas** (carregadas de CDN):
  - [Leaflet](https://leafletjs.com) 1.9.4 para o mapa.
  - [SheetJS](https://sheetjs.com) 0.18.5 para gerar a planilha Excel, carregado só quando a planilha é baixada.
- **Caminho para lojas de aplicativos:** se no futuro for necessário publicar na Play Store ou na App Store, o mesmo código pode ser empacotado com [Capacitor](https://capacitorjs.com).

## APIs gratuitas utilizadas

| Serviço | Uso |
|---|---|
| [Nominatim](https://nominatim.org) (OpenStreetMap) | Busca de endereços, destinos e aeroportos |
| [Overpass API](https://overpass-api.de) | Atrações, restaurantes, farmácias, saúde, mercados e estações |
| [OSRM / FOSSGIS](https://routing.openstreetmap.de) | Rotas a pé, de carro e de bicicleta |
| [Wikipédia](https://www.mediawiki.org/wiki/API) | Resumos das atrações |
| [Open-Meteo](https://open-meteo.com) | Previsão do tempo |
| [Frankfurter](https://frankfurter.dev) | Câmbio de referência do Banco Central Europeu |
| Tiles do [OpenStreetMap](https://www.openstreetmap.org/copyright) | Mapa base |

Esses serviços são mantidos por comunidades e têm políticas de uso justo (por exemplo, o Nominatim aceita no máximo uma requisição por segundo). O app espera entre as buscas e usa um servidor reserva do Overpass. Para muitos usuários simultâneos, o ideal é um servidor próprio com cache ou um provedor com cota maior.

## Como usar

### Abrir no computador
Baixe o repositório e abra o `index.html` no navegador.

### Publicar no GitHub Pages (recomendado para usar no celular)
1. No GitHub, abra o repositório e vá em **Settings → Pages**.
2. Em **Source**, escolha **Deploy from a branch**, a branch `main` e a pasta `/ (root)`. Salve.
3. Em alguns minutos o app fica disponível em `https://SEU-USUARIO.github.io/NOME-DO-REPOSITORIO/`.
4. No celular, abra o endereço e use **Adicionar à tela inicial** para ter um atalho como aplicativo.

O endereço `https` é necessário para o botão **Minha localização**, porque os navegadores só liberam o GPS em páginas seguras.

## Privacidade

As viagens, os roteiros e os gastos ficam guardados apenas no navegador do aparelho (`localStorage`). Nada é enviado a servidores do projeto. As buscas enviam aos serviços listados acima apenas o termo pesquisado e as coordenadas da região.

Limpar os dados do navegador apaga as viagens; exporte a planilha de gastos se quiser guardar uma cópia.

## Limitações conhecidas

- **Índice de alimentação segura:** mede quanto o estabelecimento está bem documentado no OpenStreetMap, não uma inspeção sanitária. Não há base pública gratuita com esse tipo de fiscalização.
- **Prazos de voo:** check-in e embarque são orientações gerais e variam por companhia. Confirme sempre no bilhete.
- **Fusos horários:** os horários de voo são os locais de cada aeroporto, como no bilhete. O app não converte fusos.
- **Buscas amplas:** em raios muito grandes, em áreas densas, a busca pode exceder o limite do servidor gratuito.

## Estrutura

```
Bússola de viagem/
├── index.html   # o aplicativo completo (HTML, CSS e JavaScript)
├── README.md
├── .gitignore
└── .nojekyll    # faz o GitHub Pages publicar os arquivos sem processamento
```

## Créditos

Dados de mapas © colaboradores do OpenStreetMap, disponíveis sob a licença ODbL.
