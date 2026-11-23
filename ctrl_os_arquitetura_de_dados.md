# 📐 Arquitetura de Dados — CTRL OS

Este documento detalha o dicionário de dados, tipos de campos, chaves e fórmulas de inicialização de todas as tabelas do **CTRL OS**.

---

## 1. Tabela `Acompanhamento Diário`

Armazena os registros diários de ordens de serviço, atendimentos e manutenções.

| Coluna | Tipo | Regra / Fórmula / Valor Inicial | Descrição |
| :--- | :--- | :--- | :--- |
| `_RowNumber` | Número | Padrão do sistema | Número da linha na planilha fonte. |
| `OS` | Texto | Valor inicial: `MAX(LIST(113) + Acompanhamento Diário[OS]) + 1` | Numeração incremental de OS a partir do índice 113. |
| `Data` | Data | Valor inicial: `TODAY()` | Data do registro da OS. |
| `Responsável` | Enum | Lista predefinida | Técnico ou operador responsável pela atividade. |
| `Contrato` | Enum | Lista predefinida | Contrato ou cliente associado. |
| `Infraestrutura` | Enum | Lista predefinida | Tipo de infraestrutura atendida (ex: HVAC, Elétrica). |
| `Equipamento` | Enum | Lista predefinida | Identificação do equipamento específico. |
| `Local` | Enum | Lista predefinida | Localização física no cliente. |

---

## 2. Tabela `Visitas`

Validação presencial de técnicos em campo com checagem de geofencing e cálculo de permanência.

| Coluna | Tipo | Regra / Fórmula / Valor Inicial | Descrição |
| :--- | :--- | :--- | :--- |
| `ID_Visita` | Texto | Valor inicial: `UNIQUEID()` | Chave primária única do registro. |
| `Data` | Data | Valor inicial: `TODAY()` | Data da visita técnica. |
| `Contrato` | Enum | Lista predefinida | Seleção do contrato/local da visita. |
| `Endereço` | Texto | `SWITCH([Contrato], ...)` | Preenchimento automático do endereço via contrato. |
| `Endereço_GPS` | LatLong | `SWITCH([Contrato], ...)` | Coordenada fixa de referência do local de contrato. |
| `GPS` | LatLong | Valor inicial / Fórmula: `HERE()` | Coordenada GPS capturada no dispositivo no momento. |
| `Marcação Válida?` | Sim/Não | `AND(ISNOTBLANK([GPS]), ISNOTBLANK([Endereço_GPS]), DISTANCE([GPS], [Endereço_GPS]) <= 0.3)` | Valida se o técnico está a no máximo 300m do local. |
| `Entrada` | Hora | Valor inicial: `TIMENOW()` | Registra a hora inicial da visita. |
| `Saída` | Hora | Valor inicial: `TIMENOW()` | Registra a hora final da visita. |
| `Horas Trabalhadas`| Duração | `IF(AND(ISNOTBLANK([Saída]), ISNOTBLANK([Entrada]), [Saída] >= [Entrada]), [Saída] - [Entrada], "000:00")` | Calcula o intervalo entre entrada e saída. |

---

## 3. Tabela `Tarefas` (`ID_Task`)

Controle de compromissos operacionais e planos de ação.

| Coluna | Tipo | Regra / Fórmula / Valor Inicial | Descrição |
| :--- | :--- | :--- | :--- |
| `_RowNumber` | Número | Padrão do sistema | Número da linha. |
| `ID_Task` | Texto | Valor inicial: `UNIQUEID()` | Chave primária única da tarefa. |
| `Data` | Data | Fórmula: `TODAY()` | Data associada ao registro. |
| `Contrato` | Enum | Lista predefinida | Contrato relacionado à demanda. |
| `Tarefa` | LongText | — | Descrição da atividade a ser realizada. |
| `Previsão` | Data | Valor inicial: `TODAY()` | Data limite prevista para conclusão. |
| `Concluída` | Sim/Não | Valor inicial: `no` | Flag de status (Pendente / Concluída). |

---

## 4. Tabela `Solicitação de Materiais`

Controle de requisição de peças, ferramentas e suprimentos.

| Coluna | Tipo | Regra / Fórmula / Valor Inicial | Descrição |
| :--- | :--- | :--- | :--- |
| `_RowNumber` | Número | Padrão do sistema | Número da linha. |
| `C.C.` | Texto | Valor inicial: `UNIQUEID()` | Código de controle / Chave da solicitação. |
| `Contrato` | Enum | Lista predefinida | Contrato requisitante. |
| `DATA` | Data | Valor inicial: `TODAY()` | Data do pedido de material. |
| `MATERIAIS SOLICITADOS` | Texto | — | Descrição dos itens necessários. |
| `QTD` | Número | — | Quantidade requerida. |
| `MOTIVO` | Texto | — | Justificativa técnica do pedido. |
| `PRIORIDADE` | Enum | Alta / Média / Baixa | Grau de urgência da solicitação. |
| `STATUS` | Enum | Pendente / Em Cotação / Entregue | Estágio atual do atendimento do pedido. |

---

## 5. Tabelas Suplementares

* **`Propostas` & `Propostas_OK`:** Tabela de orçamentos pendentes e histórico de propostas aprovadas.
* **`Disp. Brisa` & `Disp. Praia`:** Bases operacionais específicas para checagem de disponibilidade por unidade/região.
* **`Notas`:** Anotações gerais e diário técnico livre.
* **`Resumo`:** Tabela gerada para apoio a indicadores visuais no aplicativo.