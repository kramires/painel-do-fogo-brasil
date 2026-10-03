# 🔥 Painel do Fogo – Brasil

Painel web de monitoramento de queimadas e incêndios florestais em todo o território nacional. Reúne em uma única página focos de calor, eventos de fogo, alertas, área queimada, combate, decretos de emergência e condições meteorológicas, com filtro por **região**, **UF** e **município**.

É um **arquivo HTML único** (`index.html`): não precisa de servidor, banco de dados nem instalação. Abra no navegador e o painel consulta as fontes oficiais diretamente, atualizando sozinho a cada 10 minutos.

---

## Funcionalidades

### Monitoramento · INPE e CENSIPAM
- **Focos de calor** do INPE nas janelas de 3 h, 24 h, 48 h e 7 dias, com todos os satélites ou só o satélite de referência.
- **Eventos de fogo ativos e em observação**, frente de fogo (24 h) e alertas do CENSIPAM: novos eventos (GOES), atividade em eventos, fogo junto a rodovias e junto a áreas urbanas.
- **Indicadores** com variação sobre o período anterior e acumulado do ano comparado com os dois anos anteriores.
- **Situação por região e por UF**, municípios com mais focos e eventos de maior persistência.
- **Série de 60 dias**, empilhada por região, comparada com o mesmo período do ano anterior.
- **Mapa** com focos por idade ou agregados por município, brigadas e camadas de contexto (Terras Indígenas, UC federais e estaduais, rodovias federais).

### Meteorologia
| Camada | Fonte |
|---|---|
| Satélite GOES, infravermelho (nuvens, topos frios, convecção) | INMET (imagem do satélite GOES-19 da NOAA) |
| Umidade relativa do ar, em faixas de atenção, alerta e emergência | NOAA, modelo GFS (via Open-Meteo) |
| Vento a 10 m (direção e velocidade) | NOAA, modelo GFS (via Open-Meteo) |
| Avisos meteorológicos vigentes (baixa umidade, tempestade etc.) | INMET |
| Estações automáticas, com a última leitura ao clicar | INMET |

Cada camada só busca os dados quando é ligada.

### Prevfogo · Ibama
- Área queimada mapeada (cicatrizes Sentinel-2) em 7 dias, 30 dias, 90 dias ou no ano, por região ou por UF.
- Brigadas Prevfogo, áreas de atuação e registros de combate (ROI).

### Decretos · Defesa Civil
- Municípios com decreto de situação de emergência ou de calamidade por incêndio florestal, a partir dos relatórios do S2iD. Os arquivos CSV são carregados pelo próprio usuário, com um passo a passo dentro do painel.

### Outros recursos
- **Relatório em PDF** (A4 paisagem) gerado a partir dos filtros atuais.
- **Tabela de fontes e rastreabilidade**, com a consulta exata feita a cada serviço e o horário do dado mais recente.
- Tema claro e escuro, modo tela cheia e layout responsivo.

---

## Como usar

**Localmente:** baixe o `index.html` e abra no navegador (Chrome, Edge, Firefox ou Safari atualizados).

**Online (GitHub Pages):**
1. No repositório, abra **Settings → Pages**.
2. Em *Source*, escolha **Deploy from a branch**, com a branch `main` e a pasta `/ (root)`.
3. Depois de alguns instantes, o painel fica disponível em `https://<seu-usuario>.github.io/<nome-do-repositorio>/`.

---

## Fontes de dados

| Dado | Órgão | Serviço |
|---|---|---|
| Focos de calor | INPE · Programa Queimadas | GeoServer TerraBrasilis (WFS `bdqueimadas2:focos`) |
| Eventos, alertas, frente de fogo e brigadas | CENSIPAM · Painel do Fogo | GeoServer `panorama.sipam.gov.br` (WFS e WMS) |
| Terras Indígenas, UC, rodovias | FUNAI, ICMBio/MMA, DNIT (via CENSIPAM) | WMS `painel_do_fogo` |
| Área queimada, brigadas e combates | Ibama · Prevfogo | ArcGIS REST `sisfogo.ibama.gov.br` |
| Satélite, avisos e estações | INMET | `apisat`, `apiprevmet3` e `apitempo.inmet.gov.br` |
| Umidade, temperatura e vento | NOAA · GFS | `api.open-meteo.com` |
| Decretos | MIDR · Defesa Civil (S2iD) | CSV exportado pelo usuário |
| Limites de municípios, UF e regiões | IBGE | embutidos no arquivo |
| Mapa de fundo | Esri | World Topo, World Imagery, Light/Dark Gray |

---

## Limitações

- **Disponibilidade:** os dados vêm diretamente de serviços públicos de terceiros. Se um serviço sair do ar, o painel mostra a falha na tabela de fontes e continua funcionando com as demais.
- **Focos não são incêndios confirmados:** um foco de calor é um pixel com temperatura anômala visto pelo satélite. Um mesmo fogo pode gerar vários focos, e alguns são queimas controladas.
- **Umidade e vento são de modelo:** os valores do GFS são previsão de modelo numa grade de 1,5° (cerca de 165 km), não medições. Para a leitura real, use as estações do INMET.
- **Satélite GOES:** a imagem publicada pelo INMET não traz coordenadas. O painel a posiciona por um georreferenciamento ajustado às fronteiras desenhadas na própria imagem.
- **Combates (ROI):** os registros do Prevfogo publicados vão só até 2025.

---

## Tecnologias

HTML, CSS e JavaScript puro · [Leaflet](https://leafletjs.com/) 1.9.4 · consultas WFS/WMS (OGC), ArcGIS REST e APIs JSON · polígonos do IBGE simplificados e embutidos no arquivo.

---

## Desenvolvedor

**Klayton Silva Ramires**
[linkedin.com/in/klayton-ramires](https://www.linkedin.com/in/klayton-ramires) · ramires.klayton@eb.mil.br

> Os dados exibidos pertencem às instituições citadas na seção *Fontes de dados*. Este painel apenas os consulta e organiza.
