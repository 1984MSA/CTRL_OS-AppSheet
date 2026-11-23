# 📱 Fluxos de Navegação e Views (UX) — CTRL OS

Este documento descreve como as telas (*Views*) do **CTRL OS** estão organizadas no aplicativo AppSheet.

---

## 🧭 Estrutura do Menu de Navegação

```
                    ┌───────────────────────────┐
                    │          CTRL OS          │
                    └─────────────┬─────────────┘
                                  │
         ┌────────────────────────┴────────────────────────┐
         ▼                                                 ▼
┌─────────────────────────┐                       ┌─────────────────┐
│   Navegação Primária    │                       │  Menu Lateral   │
├─────────────────────────┤                       ├─────────────────┤
│ • Tarefas de Hoje       │                       │ • Arquivos      │
│ • OS de Hoje            │                       │ • Disponibil.   │
│ • CTRL_                 │                       │ • Propostas     │
│ • Visitas               │                       │ • Resumo        │
│ • Notas                 │                       │ • Tarefas       │
└─────────────────────────┘                       └─────────────────┘
```

---

## 🖥️ Telas Primárias (Barra Inferior)

### 1. `Tarefas de Hoje`
* **Tipo de View:** List / Deck
* **Filtro:** Exibe tarefas onde `[Previsão] = TODAY()` e `[Concluída] = no`.
* **Propósito:** Garantir foco nas pendências imediatas do dia.

### 2. `OS de Hoje`
* **Tipo de View:** Table / Deck
* **Filtro:** Exibe chamados registrados no dia atual (`[Data] = TODAY()`).
* **Ação:** Permite abertura rápida do formulário de detalhamento e anexo de parecer técnico.

### 3. `CTRL_`
* **Tipo de View:** Dashboard
* **Propósito:** Central de acompanhamento consolidada dos principais indicadores operacionais em tempo real.

### 4. `Visitas`
* **Tipo de View:** Form / Map
* **Propósito:** Registro de entrada e saída de técnicos em clientes, exibindo o status da `Marcação Válida?` e os botões de captura de horário `TIMENOW()`.

### 5. `Notas`
* **Tipo de View:** Deck
* **Propósito:** Bloco de anotações técnicas rápidas em campo.

---

## ☰ Telas Secundárias (Menu Lateral)

* **`Arquivos`:** Consulta e download de documentos anexados e ordens em PDF.
* **`Disponibilidade`:** Exibição combinada das visões de escala e prontidão (`Disp. Brisa` e `Disp. Praia`).
* **`Propostas`:** Acompanhamento de propostas técnicas e orçamentos em andamento (`Propostas`) e concluídos (`Propostas_OK`).
* **`Resumo`:** Dashboard gerencial de resumos periódicos.
* **`Tarefas`:** Visão completa de todas as tarefas cadastradas (pendentes e concluídas).