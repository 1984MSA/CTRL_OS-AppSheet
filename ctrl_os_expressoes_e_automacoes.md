# ⚡ Expressões e Automações — CTRL OS

Este arquivo documenta as fórmulas e lógicas de negócio utilizadas no editor do **Google AppSheet** para o **CTRL OS**.

---

## 1. Gerador Sequencial de Ordens de Serviço (`OS`)

Para garantir que cada ordem de serviço receba um número inteiro sequencial sem depender do `_RowNumber`:

```appsheet
MAX( LIST(113) + Acompanhamento Diário[OS] ) + 1
```

* **Lógica:** Une a lista de números já existentes na coluna `OS` ao valor base `113` e incrementa `+ 1` sobre o maior valor encontrado.

---

## 2. Validação Geográfica de Presença (`Marcação Válida?`)

Verifica se a marcação de ponto/visita foi realizada dentro do raio permitido de atendimento:

```appsheet
AND(
  ISNOTBLANK([GPS]),
  ISNOTBLANK([Endereço_GPS]),
  DISTANCE([GPS], [Endereço_GPS]) <= 0.3
)
```

* **Lógica:** Avalia se o sinal de GPS local e as coordenadas do contrato existem e se a distância entre ambos é menor ou igual a `0.3` km (300 metros).

---

## 3. Mapeamento Automático de Endereço e Coordenadas (`SWITCH`)

Preenchimento automático do endereço e coordenadas GPS de referência a partir da escolha do contrato:

```appsheet
SWITCH(
  [Contrato],
  "Praiamar", "Rua Alexandre Martins, 80 - Aparecida, Santos",
  "Brisamar", "Rua Frei Gaspar, 365 - Centro, São Vicente",
  "Home Office", "Av. Pres. Getúlio Vargas, 152 - Morro dos Barbosas",
  "CCN", "Av. Miruna, 700 - Indianópolis",
  ""
)
```

---

## 4. Cálculo do Tempo Trabalhado (`Horas Trabalhadas`)

Calcula a duração total da visita técnica tratando possíveis erros de registro:

```appsheet
IF(
  AND(
    ISNOTBLANK([Saída]),
    ISNOTBLANK([Entrada]),
    [Saída] >= [Entrada]
  ),
  [Saída] - [Entrada],
  "000:00"
)
```

---

## 5. Chaves Únicas (`UNIQUEID`)

Utilizadas nas tabelas `Visitas`, `Tarefas` (`ID_Task`) e `Solicitação de Materiais` (`C.C.`):

```appsheet
UNIQUEID()
```

* **Aplicação:** Define um hash de 8 caracteres alfanuméricos como valor inicial para garantir integridade e evitar colisões na sincronização offline.