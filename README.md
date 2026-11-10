<div align="center">

# Carcará

### A visão de cima que protege a sua terra embaixo.

[![Python](https://img.shields.io/badge/Python-3.11%2B-3776AB?logo=python&logoColor=white)](https://www.python.org/)
[![FastAPI](https://img.shields.io/badge/FastAPI-0.110%2B-009688?logo=fastapi&logoColor=white)](https://fastapi.tiangolo.com/)
[![Next.js](https://img.shields.io/badge/Next.js-14%2B-000000?logo=next.js&logoColor=white)](https://nextjs.org/)
[![Licença](https://img.shields.io/badge/licença-MIT-green.svg)](#licença)
[![Hack Brasil](https://img.shields.io/badge/Hack%20Brasil-2026%20%7C%20Trilha%2001-FF6B35)](#impacto-socioambiental--métricas-de-sucesso)

[Demo Online](https://carcara.demo.example) · [Vídeo Pitch de 3 Minutos](https://video.example/carcará-pitch) · [Pitch Deck](https://docs.example/carcará-pitch-deck)

</div>

## Resumo executivo

O **Carcará** é uma plataforma de inteligência geoespacial que transforma dados orbitais e bases ambientais públicas em alertas simples, acionáveis e acessíveis para pequenos e médios produtores rurais. O sistema monitora focos de calor, supressão de vegetação e sobreposições ambientais na propriedade cadastrada, avisando o produtor pelo WhatsApp antes que uma ocorrência se transforme em perda de safra, risco à vida ou bloqueio de crédito rural.

O projeto foi submetido ao **Hack Brasil 2026 — Trilha 01: Meio ambiente & economia verde**. Sua proposta conecta prevenção de incêndios, conformidade socioambiental e inclusão tecnológica: a mesma informação que normalmente exige um especialista em SIG/GIS chega ao produtor em linguagem direta, com distância, severidade, coordenadas e orientação para agir.

### Por que Carcará?

Inspirado no carcará (*Caracara plancus*), ave de rapina emblemática dos biomas brasileiros, o projeto combina visão aguçada, inteligência adaptativa e vigilância sobre áreas de queimada. Na solução, o carcará é o algoritmo sentinela que sobrevoa a terra por meio de dados orbitais e avisa quem está no solo antes que o fogo tome proporções incontroláveis.

## O problema

O produtor familiar enfrenta uma assimetria de informação que tem efeitos econômicos, ambientais e jurídicos concretos:

- **Exclusão tecnológica:** sistemas avançados de geomonitoramento são desenhados para grandes corporações e órgãos públicos. Pequenos e médios produtores normalmente não dispõem de computadores com ArcGIS/QGIS, especialistas ou tempo para interpretar rasters, shapefiles e camadas cartográficas.
- **Risco ambiental e responsabilidade objetiva:** queimadas originadas em propriedades vizinhas podem invadir lavouras e pastagens, causar prejuízos devastadores e ainda expor o proprietário a multas ambientais até que a origem externa do foco seja comprovada.
- **Crédito e mercado bloqueados:** notificações tardias de desmatamento ou sobreposição com áreas embargadas podem travar linhas como Pronaf e Pronamp no Plano Safra. Compradores, frigoríficos e cooperativas recusam safras sem evidência de conformidade socioambiental.
- **Janela crítica de ação:** quando o fogo é percebido visualmente na cerca, o combate se torna perigoso e financeiramente inviável. Um alerta prévio, acompanhado de raio de aproximação, permite acionar vizinhos, brigadas e autoridades com antecedência.

## A solução em uma jornada

1. O produtor acessa uma aplicação web responsiva pelo celular ou computador.
2. Desenha o polígono da propriedade no mapa, envia um GeoJSON/KML ou informa o código do Cadastro Ambiental Rural (CAR).
3. O Carcará valida a geometria e registra o perímetro monitorado.
4. O pipeline consulta dados de focos de calor do **BDQueimadas/INPE** e alertas de supressão de vegetação do **MapBiomas Alertas/DETER**.
5. O motor espacial calcula interseções, distância e zonas de risco.
6. O produtor recebe um alerta acionável pelo WhatsApp e pode gerar um laudo digital de regularidade ambiental em PDF.

### Quadro comparativo

| Antes: acompanhamento manual e caro | Depois: automação com o Carcará |
| --- | --- |
| Produtor precisa descobrir sozinho que há fogo ou desmatamento próximo. | Monitoramento contínuo com alertas reativos a eventos geoespaciais. |
| Dados espalhados em portais públicos, mapas complexos e formatos técnicos. | Resultado consolidado em mapa simples, WhatsApp e relatório PDF. |
| Dependência de consultoria especializada em SIG/GIS. | Cadastro por desenho no mapa, GeoJSON, KML ou referência ao CAR. |
| Reação quando o incêndio já chegou à cerca. | Detecção por zonas, distância estimada e janela antecipada de ação. |
| Dificuldade para comprovar origem externa de um foco. | Histórico de ocorrências, coordenadas, data/hora e perímetro registrado. |
| Conformidade apresentada de forma fragmentada a bancos e compradores. | Laudo digital padronizado para cooperativas, tradings e gerentes bancários. |

## Funcionalidades-chave

### Cadastro de propriedade sem atrito

- Desenho interativo do perímetro com Leaflet ou Mapbox GL.
- Upload de arquivos simples em GeoJSON e KML.
- Preparação para consulta e vinculação ao código do CAR.
- Validação de geometria no cliente com Turf.js e no servidor com Shapely.

### Monitoramento geoespacial

- Consumo de focos de calor orbitais do BDQueimadas/INPE, com referência a Aqua, Terra, NOAA-20 e VIIRS.
- Consumo de polígonos de supressão de vegetação nativa e cortes rasos de MapBiomas Alertas/DETER.
- Operações de *point-in-polygon*, buffers, interseções e cálculo de distância.
- Registro de data, fonte, coordenadas, severidade e propriedade afetada para auditoria.

### Zonas de risco

| Zona | Regra operacional | Ação sugerida |
| --- | --- | --- |
| 🔴 **Vermelha — Crítica** | Foco detectado dentro do perímetro da fazenda. | Acionar imediatamente a equipe local, vizinhos, brigada e órgãos competentes. |
| 🟡 **Amarela — Atenção** | Foco detectado entre 1 km e 5 km da propriedade. | Reforçar vigilância, verificar direção do vento e preparar prevenção. |
| 🟢 **Verde — Segura** | Nenhuma anomalia térmica ou vetorial registrada nas últimas 24h a 72h. | Manter o monitoramento e guardar o status como evidência temporal. |

### Alertas diretos pelo WhatsApp

O produtor não precisa entrar diariamente na plataforma. Webhooks da WhatsApp Cloud API disparam mensagens com nível de severidade, distância, direção aproximada do foco ou vento, coordenadas e link para rota.

> 🔴 **CARCARÁ — ALERTA CRÍTICO**
>
> Foco de calor detectado **dentro do perímetro** da Fazenda Boa Esperança.
>
> Distância do centro da propriedade: **0,8 km**
>
> Coordenadas: **-15.793889, -47.882778**
>
> Ação recomendada: acione sua brigada e os órgãos locais com segurança. [Abrir rota no mapa](https://maps.google.com/)

> 🟡 **CARCARÁ — ATENÇÃO**
>
> Foco de calor detectado a **3,4 km**, na direção nordeste da sua propriedade.
>
> Janela de monitoramento: últimas **24h**. Verifique a direção do vento e mantenha a equipe em alerta.
>
> Coordenadas: **-15.771200, -47.851000** · [Ver no Google Maps](https://maps.google.com/)

### Laudo Digital de Regularidade Ambiental

Geração de PDF com mapa satelital da propriedade, dados cadastrais, histórico de focos nas últimas safras, declaração de não sobreposição com áreas embargadas e carimbo de validação com data/hora. O documento pode ser apresentado a cooperativas, tradings e instituições financeiras para apoiar processos de conformidade e liberação de crédito rural verde.

## Arquitetura de dados e fluxo do sistema

```mermaid
flowchart LR
    P[Produtor rural] --> F[Frontend Web responsivo\nNext.js + Leaflet/Mapbox]
    F -->|GeoJSON, KML ou CAR| API[FastAPI\nAPI assíncrona]
    API --> DB[(PostgreSQL/PostGIS\nMVP: persistência geoespacial)]
    API --> PIPE[Pipeline geoespacial\nGeoPandas + Shapely + PyProj]
    INPE[BDQueimadas / INPE\nAqua, Terra, NOAA-20, VIIRS] --> ING[Ingestão e polling agendado]
    MAP[MapBiomas Alertas / DETER] --> ING
    ING --> PIPE
    PIPE -->|focos, buffers, interseções| API
    PIPE -->|evento de severidade| WH[Webhook WhatsApp Cloud API]
    WH --> W[WhatsApp do produtor]
    API --> PDF[Emissor de PDF\nWeasyPrint/ReportLab + mapa estático]
    PDF --> D[Laudo Digital de Regularidade]
```

### Camadas e responsabilidades

- **Apresentação:** Next.js com App Router, TypeScript e Tailwind CSS; experiência mobile-first para cadastro e consulta rápida.
- **API e orquestração:** FastAPI com endpoints assíncronos, autenticação futura e contratos versionados em `/api/v1`.
- **Persistência:** propriedades, geometrias normalizadas, fontes dos alertas, histórico de verificações e documentos emitidos.
- **Processamento:** GeoPandas, Shapely e PyProj para reprojeção, buffers de segurança, interseções e validações topológicas.
- **Ingestão:** tarefas agendadas para consultar dados abertos, normalizar fontes e evitar duplicidade por coordenada, timestamp e satélite.
- **Saída:** notificações reativas no WhatsApp e PDFs auditáveis com snapshot das evidências utilizadas na análise.

## Stack tecnológica

| Camada | Tecnologias | Uso no projeto |
| --- | --- | --- |
| Frontend | Next.js, React, TypeScript, Tailwind CSS | Interface responsiva, rotas, formulários e experiência mobile-first. |
| Mapa | Leaflet ou Mapbox GL, Turf.js | Visualização, desenho de polígonos, validação e cálculo preliminar no cliente. |
| Backend | Python 3.11+, FastAPI, Pydantic, Uvicorn | API assíncrona, validação de payloads e documentação OpenAPI. |
| Geoespacial | GeoPandas, Shapely, PyProj | Pontos em polígonos, buffers, interseções, distâncias e sistemas de referência. |
| Dados | BDQueimadas/INPE, MapBiomas Alertas, DETER | Focos de calor e alertas de supressão de vegetação. |
| Agendamento | APScheduler ou Celery + Redis | Polling, normalização e processamento desacoplado. |
| Mensageria | WhatsApp Cloud API, Webhooks | Alertas reativos e confirmação de entrega. |
| Documentos | WeasyPrint ou ReportLab, Mapbox Static API | Laudos PDF com mapas, evidências e carimbo temporal. |
| Operação | Docker, Docker Compose, PostgreSQL/PostGIS | Ambiente reprodutível e base para implantação. |

## Instalação e execução local

### Pré-requisitos

- Docker Engine e Docker Compose;
- Python 3.11 ou superior;
- Node.js 18 ou superior e npm;
- Git;
- credenciais de desenvolvimento para Mapbox, WhatsApp Cloud API e, quando aplicável, serviços de mapas estáticos.

### 1. Clonar e configurar o ambiente

```bash
git clone https://github.com/seu-usuario/carcara.git
cd carcara
cp .env.example .env
```

No Windows PowerShell, use `Copy-Item .env.example .env`.

### 2. Variáveis de ambiente

O arquivo `.env` deve conter valores reais apenas no ambiente local; nunca publique tokens ou chaves no repositório.

```dotenv
APP_ENV=development
APP_NAME=Carcará
API_V1_PREFIX=/api/v1
SECRET_KEY=troque-esta-chave-em-desenvolvimento
ALLOWED_ORIGINS=http://localhost:3000

BACKEND_HOST=0.0.0.0
BACKEND_PORT=8000
DATABASE_URL=postgresql+asyncpg://carcara:carcara@localhost:5432/carcara
REDIS_URL=redis://localhost:6379/0

NEXT_PUBLIC_API_URL=http://localhost:8000
NEXT_PUBLIC_MAP_PROVIDER=mapbox
NEXT_PUBLIC_MAPBOX_TOKEN=seu-token-mapbox

INPE_BDQUEIMADAS_URL=https://queimadas.dgi.inpe.br/queimadas/
MAPBIOMAS_ALERTAS_URL=https://alertas.mapbiomas.org/
DETER_BASE_URL=https://terrabrasilis.dpi.inpe.br/
POLLING_INTERVAL_MINUTES=30
ALERT_LOOKBACK_HOURS=72

WHATSAPP_API_VERSION=v20.0
WHATSAPP_PHONE_NUMBER_ID=seu-phone-number-id
WHATSAPP_ACCESS_TOKEN=seu-token-whatsapp
WHATSAPP_VERIFY_TOKEN=seu-token-de-verificacao
WHATSAPP_WEBHOOK_URL=https://seu-dominio/api/v1/webhooks/whatsapp

REPORT_STORAGE_PATH=./storage/reports
MAPBOX_STATIC_TOKEN=seu-token-mapbox-static
REPORT_SIGNING_SECRET=segredo-para-validacao-do-laudo
```

### 3. Executar o backend

```bash
cd backend
python -m venv .venv

# Linux/macOS
source .venv/bin/activate

# Windows PowerShell
# .\\.venv\\Scripts\\Activate.ps1

pip install -r requirements.txt
uvicorn app.main:app --reload --host 0.0.0.0 --port 8000
```

A API e a documentação interativa ficam disponíveis em `http://localhost:8000/docs`.

### 4. Executar o frontend

Em outro terminal:

```bash
cd frontend
npm install
npm run dev
```

A aplicação fica disponível em `http://localhost:3000`.

### 5. Subir o ambiente completo com Docker Compose

```bash
docker compose up --build
```

Para executar em segundo plano:

```bash
docker compose up --build -d
```

As portas padrão são `3000` para o frontend, `8000` para a API, `5432` para PostgreSQL/PostGIS e `6379` para Redis. Os serviços de ingestão devem ser habilitados conforme o perfil definido no `docker-compose.yml`.

## Endpoints principais da API

Todos os endpoints do MVP são versionados sob `/api/v1` e retornam JSON, salvo a emissão de relatório.

| Método | Rota | Objetivo | Resposta esperada |
| --- | --- | --- | --- |
| `POST` | `/api/v1/properties` | Cadastrar uma propriedade a partir de GeoJSON, KML normalizado ou referência ao CAR. | `201 Created` com `property_id`, área, centroide e status de monitoramento. |
| `GET` | `/api/v1/properties/{property_id}` | Consultar perímetro, dados cadastrais e última verificação. | `200 OK` com geometria simplificada e metadados. |
| `POST` | `/api/v1/alerts/check` | Executar verificação de focos e alertas vetoriais para uma propriedade. | `200 OK` com zona, severidade, distância, fonte e coordenadas. |
| `GET` | `/api/v1/alerts/{property_id}` | Listar histórico de alertas por período. | `200 OK` com eventos paginados e filtros de data/severidade. |
| `POST` | `/api/v1/reports/compliance` | Gerar laudo digital de regularidade ambiental. | `202 Accepted` com `report_id` e status de processamento. |
| `GET` | `/api/v1/reports/compliance/{report_id}` | Baixar ou consultar o status do PDF. | `200 OK` com URL temporária e hash de validação. |
| `POST` | `/api/v1/webhooks/whatsapp` | Receber confirmações e eventos da WhatsApp Cloud API. | `200 OK` após validação do webhook. |

Exemplo de solicitação de verificação:

```bash
curl -X POST http://localhost:8000/api/v1/alerts/check \
  -H "Content-Type: application/json" \
  -d '{"property_id":"prop_123","lookback_hours":72}'
```

## Impacto socioambiental e métricas de sucesso

O Carcará se alinha à Trilha 01 ao usar infraestrutura digital e dados públicos para reduzir danos ambientais, proteger a produção e democratizar acesso a inteligência territorial. A solução apoia metas ESG em três frentes:

- **Ambiental:** antecipar incêndios, registrar evidências de conformidade e apoiar a preservação de vegetação nativa.
- **Social:** levar tecnologia de monitoramento a produtores familiares sem exigir domínio de ferramentas GIS.
- **Governança:** gerar trilhas de auditoria, laudos datados e informações verificáveis para crédito e cadeias de compra.

| Indicador | Meta inicial do MVP | Como medir |
| --- | --- | --- |
| Tempo entre detecção e aviso | Menos de 15 minutos após ingestão do evento | Timestamp da fonte versus entrega do WhatsApp. |
| Propriedades monitoradas | 100 propriedades no piloto | Cadastros ativos com ao menos uma verificação em 30 dias. |
| Entrega de alertas críticos | Acima de 95% | Confirmações de entrega da API do WhatsApp. |
| Falsos positivos em zona crítica | Abaixo de 10% após validação de campo | Amostragem de ocorrências confirmadas pelo produtor. |
| Laudos emitidos | 80% dos produtores do piloto | Relatórios gerados e baixados por propriedade. |
| Acesso a crédito ou compradores | Casos documentados de uso | Relatos de cooperativas, bancos e tradings parceiros. |
| Área potencialmente protegida | Medida acumulada das propriedades monitoradas | Soma da área cadastrada com histórico de alertas e ações preventivas. |

## Roadmap

### MVP atual

- [x] Cadastro de propriedade por polígono e arquivos espaciais simples.
- [x] Classificação conceitual em zonas vermelha, amarela e verde.
- [x] API versionada para propriedades, alertas e relatórios.
- [x] Pipeline geoespacial com foco em point-in-polygon, buffers e interseções.
- [x] Desenho de alertas acionáveis via WhatsApp Cloud API.
- [x] Modelo de laudo digital em PDF com carimbo temporal.
- [ ] Conectar credenciais de produção às fontes INPE, MapBiomas e DETER.

### Próximas evoluções

- [ ] Integração direta com o CAR federal e importação assistida de perímetros.
- [ ] Análise de vento usando previsão meteorológica e direção provável de propagação.
- [ ] Integração com cooperativas, brigadas, compradores e instituições de crédito.
- [ ] Aplicativo PWA com operação offline e sincronização quando houver conectividade.
- [ ] Modelos de priorização de risco combinando combustível vegetal, histórico e topografia.
- [ ] Painel multi-propriedade para técnicos de cooperativas e secretarias municipais.
- [ ] Assinatura digital e validação pública do hash dos laudos.

## Equipe

| Pessoa | Papel | Responsabilidade |
| --- | --- | --- |
| A definir | Produto e impacto | Estratégia, descoberta com produtores e métricas ESG. |
| A definir | Engenharia geoespacial | Pipeline de dados, projeções, buffers e validações espaciais. |
| A definir | Engenharia full-stack | Frontend, API, autenticação e experiência de uso. |
| A definir | Dados e infraestrutura | Ingestão, agendamento, observabilidade e implantação. |
| A definir | Parcerias e campo | Cooperativas, brigadas, crédito rural e validação das mensagens. |

## Licença

Este projeto é distribuído sob a **Licença MIT**. O texto integral da licença deve ser mantido no arquivo `LICENSE` na publicação do repositório. O uso de dados, imagens, mapas e marcas de terceiros permanece sujeito aos termos de suas respectivas fontes e provedores.

## Observação sobre dados e segurança

Os alertas são instrumentos de apoio à decisão e não substituem a atuação do Corpo de Bombeiros, da Defesa Civil, de brigadas treinadas ou dos órgãos ambientais. O produtor deve priorizar a segurança das pessoas e confirmar a ocorrência em campo sem se expor ao risco. Em uma implantação real, tokens, dados cadastrais, telefones e documentos devem ser protegidos por controle de acesso, criptografia, retenção mínima e conformidade com a LGPD.

