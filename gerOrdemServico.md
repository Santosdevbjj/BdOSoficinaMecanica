**Descrição do Projeto:**

Este projeto consiste na modelagem de dados conceitual para um sistema de controle e gerenciamento de ordens de serviço (OS) em uma oficina mecânica. O objetivo é criar um esquema EER (Enhanced Entity Relationship) que represente as entidades, atributos e relacionamentos relevantes para o contexto da oficina, permitindo o armazenamento e gerenciamento eficiente das informações.
Entidades e Atributos.

**Abaixo apresento o diagrama de entidade de relacionamento.**

![Screenshot_20250318-164509](https://github.com/user-attachments/assets/d113c96b-bb05-4230-bfaf-d104279fed1c)



 * **Cliente:**
   * ID_Cliente (Chave Primária): Identificador único do cliente.
   * Nome: Nome completo do cliente.
   * CPF: Cadastro de Pessoa Física do cliente.
   * Telefone: Número de telefone do cliente.
   * Endereco: Endereço completo do cliente.
   * 
 * **Veículo:**
   * ID_Veiculo (Chave Primária): Identificador único do veículo.
   * Placa: Número da placa do veículo.
   * Modelo: Modelo do veículo.
   * Marca: Marca do veículo.
   * Ano: Ano de fabricação do veículo.
   * ID_Cliente (Chave Estrangeira): Referência ao cliente proprietário do veículo.
 
 * **Mecânico:**
   * ID_Mecanico (Chave Primária): Identificador único do mecânico.
   * Nome: Nome completo do mecânico.
   * Endereco: Endereço completo do mecânico.
   * Telefone: Número de telefone do mecânico.
   * Email: Endereço de e-mail do mecânico.
   * Especialidade: Especialidade do mecânico (ex: motor, freios, suspensão).

 * **Ordem de Serviço (OS):**
   * ID_OS (Chave Primária): Número da ordem de serviço.
   * Data_Emissao: Data de emissão da OS.
   * Horario_Recebimento: Horário em que o veículo foi recebido para serviço.
   * Valor_Total: Valor total da OS.
   * Status: Status da OS (ex: em aberto, em andamento, concluída).
   * Data_Conclusao: Data prevista para conclusão dos serviços.
   * ID_Veiculo (Chave Estrangeira): Referência ao veículo relacionado à OS.
 
 * **Serviço:**
   * ID_Servico (Chave Primária): Identificador único do serviço.
   * Descricao: Descrição do serviço.
   * Valor_Mao_de_Obra: Valor da mão de obra para o serviço.
 
 * **Peça:**
   * ID_Peca (Chave Primária): Identificador único da peça.
   * Nome: Nome da peça.
   * Valor_Unitario: Valor unitário da peça.

 * **Equipe:**
   * ID_Equipe (Chave Primária): Identificador único da equipe.

**Relacionamentos**
 * Cliente possui Veículo: Um cliente pode possuir um ou mais veículos. (1:N)
 * Veículo gera OS: Um veículo pode gerar uma ou mais ordens de serviço. (1:N)
 * OS é atribuída a Equipe: Uma ordem de serviço é atribuída a uma equipe. (1:N)
 * Equipe é composta por Mecânico: Uma equipe é composta por um ou mais mecânicos. (1:N)
 * OS possui Serviço: Uma ordem de serviço pode incluir um ou mais serviços. (1:N)
 * OS utiliza Peça: Uma ordem de serviço pode utilizar uma ou mais peças. (1:N)
 * Serviço utiliza Peça: Um serviço pode utilizar uma ou mais peças. (1:N)



**Considerações:*"

 * A tabela de referência de mão de obra foi representada pela entidade Serviço, que contém o atributo Valor_Mao_de_Obra.
 * A autorização do cliente para execução dos serviços pode ser representada por um atributo booleano na entidade OS (ex: Autorizado).
 * A relação entre Serviço e Peça permite representar serviços que utilizam peças específicas.

 * 
 
