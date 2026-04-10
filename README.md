**DIO BOOTCAMP:**

**Heineken - Inteligência Artificial Aplicada a Dados com Copilot.**



# 🔧 Esquema Conceitual EER — Sistema de OS para Oficina Mecânica

![Banner do Projeto](https://github.com/user-attachments/assets/87dd8a94-c5f8-4632-a7a0-a59db6725924)

> **Antes de escrever uma linha de SQL, você precisa entender o problema. O esquema conceitual é onde o negócio vira estrutura.**  

<div align="center">

[![Portfólio](https://img.shields.io/badge/Portfólio-Sérgio_Santos-111827?style=for-the-badge&logo=githubpages&logoColor=00eaff)](https://portfoliosantossergio.vercel.app)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Sérgio_Santos-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://linkedin.com/in/santossergioluiz)
[![Bootcamp](https://img.shields.io/badge/Bootcamp-Heineken_×_DIO-00A86B?style=for-the-badge&logo=databricks&logoColor=white)](https://www.dio.me)
[![MySQL](https://img.shields.io/badge/MySQL-EER_Modeling-4479A1?style=for-the-badge&logo=mysql&logoColor=white)](https://www.mysql.com)

</div>

---

## 📋 Índice

- [1. Problema de Negócio](#1-problema-de-negócio)
- [2. Contexto](#2-contexto)
- [3. Premissas da Análise](#3-premissas-da-análise)
- [4. Estratégia da Solução](#4-estratégia-da-solução)
- [5. Estrutura do Projeto](#5-estrutura-do-projeto)
- [6. Diagrama EER](#6-diagrama-eer)
- [7. Entidades e Atributos](#7-entidades-e-atributos)
- [8. Relacionamentos](#8-relacionamentos)
- [9. Insights Técnicos](#9-insights-técnicos)
- [10. Resultados](#10-resultados)
- [11. Aprendizados](#11-aprendizados)
- [12. Próximos Passos](#12-próximos-passos)
- [13. Como Utilizar](#13-como-utilizar)
- [14. Tecnologias Utilizadas](#14-tecnologias-utilizadas)
- [15. Contato](#15-contato)

---

## 1. Problema de Negócio

Oficinas mecânicas que operam sem um sistema estruturado de controle de Ordens de Serviço enfrentam três problemas recorrentes: **falta de rastreabilidade** — não é possível saber em qual etapa cada veículo se encontra; **inconsistência no cálculo de custos** — o valor da OS depende de consultas manuais a tabelas de mão de obra e preços de peças, sujeitas a erro; e **ausência de autorização formal** — sem registro estruturado, a oficina fica exposta a contestações do cliente sobre serviços executados.

O problema central deste projeto é: **como modelar conceitualmente um sistema de gestão de OS que represente fielmente as regras operacionais de uma oficina — equipes, mecânicos, serviços, peças e autorização do cliente — de forma que o modelo possa ser evoluído para um banco de dados relacional funcional?**

---

## 2. Contexto

Este projeto foi desenvolvido no **Bootcamp Heineken — Inteligência Artificial Aplicada a Dados com Copilot**, em parceria com a DIO. O desafio propõe criar do zero um esquema conceitual EER (Enhanced Entity-Relationship) para o contexto de uma oficina mecânica, a partir de uma narrativa de negócio fornecida.

A narrativa descreve o seguinte fluxo operacional:

- Clientes levam veículos à oficina para conserto ou revisão periódica.
- Cada veículo é designado a uma **equipe de mecânicos**, que identifica os serviços necessários e preenche uma **Ordem de Serviço** com data de entrega.
- O valor de cada serviço é calculado consultando uma **tabela de referência de mão de obra**.
- O valor das **peças utilizadas** também compõe o custo total da OS.
- O **cliente autoriza** a execução antes do início dos trabalhos.
- A mesma equipe que avaliou é responsável pela execução.

O modelo resultante é a base conceitual para toda a implementação lógica e física que vem nas fases seguintes do projeto.

---

## 3. Premissas da Análise

Para a modelagem conceitual, foram adotadas as seguintes premissas:

- A **Ordem de Serviço** é o objeto central do sistema — todas as entidades gravitam em torno dela.
- A autorização do cliente é representada por um atributo booleano `Autorizado` na entidade OS, garantindo rastreabilidade sem criar uma entidade separada.
- A **tabela de referência de mão de obra** mencionada na narrativa foi modelada como a entidade `Serviço`, com o atributo `Valor_Mao_de_Obra` — evitando uma tabela auxiliar desnecessária no modelo conceitual.
- Uma equipe pode ser atribuída a múltiplas OS, e uma OS é atribuída a uma equipe — cardinalidade 1:N no sentido Equipe → OS.
- Peças aparecem tanto vinculadas diretamente à OS quanto vinculadas a serviços específicos, permitindo rastrear o consumo de peças por tipo de serviço.
- O modelo foi construído para ser **tecnologia-agnóstico** nesta fase — as decisões de tipo de dado e constraints são resolvidas na modelagem lógica.

---

## 4. Estratégia da Solução

A solução foi construída em três etapas:

**Etapa 1 — Leitura e decomposição da narrativa**  
Identificação de todos os substantivos (candidatos a entidades), verbos (candidatos a relacionamentos) e qualificadores (candidatos a atributos) presentes na descrição do negócio.

**Etapa 2 — Modelagem EER**  
Construção do diagrama com as 7 entidades identificadas, seus atributos, chaves primárias, chaves estrangeiras e cardinalidades dos relacionamentos. Relacionamentos N:M foram identificados e marcados para resolução na fase lógica.

**Etapa 3 — Documentação e validação**  
Registro formal de cada entidade, atributo e relacionamento, com considerações explícitas sobre decisões de modelagem tomadas durante o processo.

---

## 5. Estrutura do Projeto

```
BdOSoficinaMecanica/
│
└── gerOrdemServico.md   # Diagrama EER, entidades, atributos, relacionamentos e considerações
```

---

## 6. Diagrama EER

![Diagrama EER — Sistema de OS da Oficina Mecânica](https://github.com/user-attachments/assets/d113c96b-bb05-4230-bfaf-d104279fed1c)

---

## 7. Entidades e Atributos

### Cliente
| Atributo | Tipo | Observação |
|---|---|---|
| `ID_Cliente` | INT | Chave Primária |
| `Nome` | STRING | Nome completo |
| `CPF` | STRING | Documento de identificação |
| `Telefone` | STRING | Contato principal |
| `Endereco` | STRING | Endereço completo |

### Veículo
| Atributo | Tipo | Observação |
|---|---|---|
| `ID_Veiculo` | INT | Chave Primária |
| `Placa` | STRING | Identificação única do veículo |
| `Modelo` | STRING | Modelo do veículo |
| `Marca` | STRING | Fabricante |
| `Ano` | INT | Ano de fabricação |
| `ID_Cliente` | INT | Chave Estrangeira → Cliente |

### Ordem de Serviço (OS)
| Atributo | Tipo | Observação |
|---|---|---|
| `ID_OS` | INT | Chave Primária — número da OS |
| `Data_Emissao` | DATE | Data de abertura da OS |
| `Horario_Recebimento` | TIME | Hora de entrada do veículo |
| `Valor_Total` | DECIMAL | Soma de serviços + peças |
| `Status` | ENUM | Em aberto / Em andamento / Concluída |
| `Data_Conclusao` | DATE | Prazo estimado de entrega |
| `Autorizado` | BOOLEAN | Aprovação do cliente para execução |
| `ID_Veiculo` | INT | Chave Estrangeira → Veículo |

### Equipe
| Atributo | Tipo | Observação |
|---|---|---|
| `ID_Equipe` | INT | Chave Primária |

### Mecânico
| Atributo | Tipo | Observação |
|---|---|---|
| `ID_Mecanico` | INT | Chave Primária |
| `Nome` | STRING | Nome completo |
| `Endereco` | STRING | Endereço do mecânico |
| `Telefone` | STRING | Contato |
| `Email` | STRING | E-mail profissional |
| `Especialidade` | STRING | Ex: motor, freios, suspensão, elétrica |

### Serviço
| Atributo | Tipo | Observação |
|---|---|---|
| `ID_Servico` | INT | Chave Primária |
| `Descricao` | STRING | Descrição do serviço prestado |
| `Valor_Mao_de_Obra` | DECIMAL | Tabela de referência de mão de obra |

### Peça
| Atributo | Tipo | Observação |
|---|---|---|
| `ID_Peca` | INT | Chave Primária |
| `Nome` | STRING | Nome da peça |
| `Valor_Unitario` | DECIMAL | Preço unitário da peça |

---

## 8. Relacionamentos

| Relacionamento | Cardinalidade | Descrição |
|---|---|---|
| Cliente **possui** Veículo | 1:N | Um cliente pode ter múltiplos veículos |
| Veículo **gera** OS | 1:N | Um veículo pode ter múltiplas OS ao longo do tempo |
| OS **é atribuída a** Equipe | N:1 | Cada OS é executada por uma equipe |
| Equipe **é composta por** Mecânico | 1:N | Uma equipe possui um ou mais mecânicos |
| OS **possui** Serviço | N:M | Uma OS pode incluir múltiplos serviços; um serviço pode aparecer em múltiplas OS |
| OS **utiliza** Peça | N:M | Uma OS pode usar múltiplas peças; uma peça pode ser usada em múltiplas OS |
| Serviço **utiliza** Peça | N:M | Um serviço pode consumir peças específicas |

### Visualização do modelo

```
CLIENTE (1) ────────────── (N) VEÍCULO (1) ────── (N) ORDEM_SERVIÇO
                                                        │       │       │
                                                    (N:M)   (N:M)   (N:1)
                                                   SERVIÇO  PEÇA  EQUIPE
                                                      │               │
                                                   (N:M)           (1:N)
                                                    PEÇA          MECÂNICO
```

> Os relacionamentos N:M entre OS ↔ Serviço, OS ↔ Peça e Serviço ↔ Peça serão resolvidos com tabelas de associação na fase de modelagem lógica.

---

## 9. Insights Técnicos

**Decisão: `Autorizado` como atributo booleano na OS, não como entidade separada**  
A autorização do cliente é um evento binário (autorizado / não autorizado) vinculado diretamente a uma OS específica. Criar uma entidade separada para isso adicionaria complexidade sem ganho analítico nesta fase. O atributo booleano é simples, direto e suficiente para rastrear compliance operacional.

**Decisão: Serviço como representação da tabela de mão de obra**  
A narrativa menciona uma "tabela de referência de mão de obra". Em vez de criar uma entidade auxiliar genérica, modelei `Serviço` com o atributo `Valor_Mao_de_Obra`, consolidando a referência dentro da própria entidade. Isso mantém o modelo coeso e evita junções desnecessárias na fase lógica.

**Decisão: relacionamento Serviço ↔ Peça como N:M explícito**  
A narrativa indica que serviços podem requerer peças específicas (ex: troca de óleo requer óleo + filtro). Modelar esse relacionamento explicitamente no EER — em vez de apenas conectar Peça à OS — preserva a semântica de quais peças são consumidas por qual tipo de serviço, viabilizando relatórios de custo por serviço na fase lógica.

**Trade-off: Equipe modelada como entidade mínima**  
A narrativa não descreve atributos para equipes além do agrupamento de mecânicos. Optei por modelar `Equipe` como entidade com apenas `ID_Equipe` para honrar o que a narrativa descreve, sem adicionar atributos assumidos. A evolução do modelo pode incluir nome, turno e especialidade principal da equipe.

---

## 10. Resultados

O esquema conceitual EER produzido neste projeto cumpre os seguintes objetivos operacionais:

- **Rastreabilidade completa**: é possível percorrer o caminho Cliente → Veículo → OS → Equipe → Mecânicos → Serviços → Peças em uma única estrutura coerente.
- **Base para implementação lógica**: todas as entidades, atributos e relacionamentos estão definidos com precisão suficiente para a tradução direta para o modelo relacional com DDL SQL.
- **Conformidade com a narrativa**: cada elemento da descrição do negócio está representado no modelo — sem omissões e sem adições arbitrárias.
- **Evolução controlada**: os relacionamentos N:M identificados já estão marcados para resolução via tabelas de associação na próxima fase.

Este modelo é a fundação sobre a qual o projeto `projetoLogicoDoZeroBD` foi construído.

---

## 11. Aprendizados

A parte mais desafiadora foi distinguir o que pertence ao modelo conceitual do que pertence à implementação. É tentador já pensar em tipos de dados, constraints e índices durante a modelagem EER — mas isso antecipa decisões que pertencem à fase lógica e física. Manter o foco em **entidades, atributos e relacionamentos** foi o exercício central deste projeto.

Outro aprendizado importante foi a leitura da narrativa como fonte de requisitos: cada substantivo é um candidato a entidade, cada verbo é um candidato a relacionamento, e cada qualificador descritivo é um candidato a atributo. Esse método de decomposição torna a modelagem sistemática em vez de intuitiva.

O que faria diferente hoje: adicionaria desde o início o atributo `Especialidade` como parte da entidade `Equipe`, não apenas em `Mecânico` — pois a narrativa implica que equipes são formadas por afinidade de especialidade.

---

## 12. Próximos Passos

- Evoluir o esquema conceitual para o **modelo lógico relacional**, resolvendo os relacionamentos N:M com tabelas de associação
- Implementar o **DDL SQL** completo com `CREATE TABLE`, constraints e índices
- Adicionar **dados de teste (DML)** para validação das queries
- Desenvolver **queries analíticas** cobrindo os casos de uso operacionais da oficina
- Containerizar o ambiente com **Docker + MySQL** para setup reproduzível

> Este modelo conceitual já foi evoluído para implementação lógica completa no repositório [projetoLogicoDoZeroBD](https://github.com/Santosdevbjj/projetoLogicoDoZeroBD).

---

## 13. Como Utilizar

**Pré-requisitos**

| Ferramenta | Finalidade |
|---|---|
| MySQL Workbench 8.0+ | Visualizar e editar o diagrama EER |
| Git | Clonar o repositório |

**Passos**

```bash
# 1. Clone o repositório
git clone https://github.com/Santosdevbjj/BdOSoficinaMecanica.git
cd BdOSoficinaMecanica
```

> Abra `gerOrdemServico.md` para revisar o diagrama, entidades, atributos e relacionamentos completos do modelo EER.

---

## 14. Tecnologias Utilizadas

| Tecnologia | Finalidade |
|---|---|
| MySQL Workbench | Criação do diagrama EER |
| Modelo EER | Notação de modelagem conceitual |
| GitHub | Versionamento e portfólio público |

---

## 15. Contato

<div align="center">

[![Portfólio](https://img.shields.io/badge/Portfólio-Sérgio_Santos-111827?style=for-the-badge&logo=githubpages&logoColor=00eaff)](https://portfoliosantossergio.vercel.app)
[![LinkedIn](https://img.shields.io/badge/LinkedIn-Sérgio_Santos-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://linkedin.com/in/santossergioluiz)

</div> 










---

**Contato:**

[![Portfólio Sérgio Santos](https://img.shields.io/badge/Portfólio-Sérgio_Santos-111827?style=for-the-badge&logo=githubpages&logoColor=00eaff)](https://santosdevbjj.github.io/portfolio/)
[![LinkedIn Sérgio Santos](https://img.shields.io/badge/LinkedIn-Sérgio_Santos-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white)](https://linkedin.com/in/santossergioluiz)





