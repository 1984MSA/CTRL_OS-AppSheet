🛠️ CTRL OS (Google AppSheet)

O CTRL OS é um sistema de gestão operacional e acompanhamento de campo construído na plataforma no-code Google AppSheet. Ele foi desenvolvido para centralizar a rotina diária de ordens de serviço, chamados, solicitações de materiais, registros de visitas com validação geográfica (GPS) e controle de tarefas.

📌 Visão Geral do Sistema

O objetivo principal do CTRL OS é eliminar a perda de informações no atendimento de campo e na rotina técnica, integrando:

Registro de Atividades: acompanhamento diário com numeração sequencial automática de OS.

Validação de Visitas em Campo: checagem de presença por geolocalização (GPS) com cálculo automático de raio de permanência e horas trabalhadas.

Gestão de Tarefas & Agenda: planejamento diário com datas previstas e controle de status.

Controle de Materiais: solicitações com classificação por prioridade, motivos e acompanhamento de status.

Relatórios Automatizados: geração de PDFs padronizados via bots/automações.

📁 Estrutura da Documentação

Para manter a organização e o versionamento técnico no GitHub, a documentação detalhada foi dividida na pasta docs/:

ctrl-os/
├── README.md                          # Visão geral do projeto e instruções
├── docs/
│   ├── arquitetura-dados.md           # Dicionário de dados, tabelas e colunas
│   ├── expressoes-e-automacoes.md     # Regras de negócio, expressões AppSheet e bots
│   └── fluxos-e-telas.md              # Navegação, views e fluxos de trabalho (UX)
├── assets/
│   └── screenshots/                   # Capturas de tela (sanitizadas)
└── template/
    └── modelo-tabelas.csv             # Cabeçalhos de referência das planilhas


🗂️ Tabelas Principais

Acompanhamento Diário: Tabela mestra de chamados e execução de ordens de serviço.

Visitas: Controle presencial em campo com validação GPS e tempo de permanência.

Tarefas (ID_Task): Agenda operacional e compromissos com data limite.

Solicitação de Materiais: Pedidos de insumos, ferramentas e materiais por contrato.

Propostas / Propostas_OK: Acompanhamento comercial e ordens aprovadas.

Disp. Brisa / Disp. Praia / Notas / Resumo: Apoio à disponibilidade operacional e resumos gráficos.

🛡️ Segurança e Privacidade (PII)

Nota: Este repositório contém estritamente a documentação da arquitetura, expressões, regras de negócio e estrutura técnica do aplicativo. Nenhuma planilha com dados operacionais, informações pessoais de clientes (PII) ou coordenadas sensíveis reais é exposta neste projeto.

🚀 Tecnologias

Plataforma: Google AppSheet (No-code / Low-code)

Base de Dados: Google Sheets / AppSheet Database

Recursos de Campo: Geolocalização (GPS), automação de e-mail/PDF e validações dinâmicas.

Desenvolvido por Manoel Araujo (1984MSA)
