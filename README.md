 ## Criação e modelagem de Banco de dados para empresa 💾

### Objetivo 🎯 

Esse projeto tem como objetivo praticar minhas habilidades com modelagem de dados, criação de database, criação de tabelas e consultas ao database criado. 

### Descrição

Nesse case uma empresa pediu para criar um modelo utilizando o Workbench do MySQL e criar um banco de dados a qual pudesse fazer consultas para análise de dados.

### Dados

O Banco de dados deveria conter informações de clientes, pagamentos, produtos, estoque, fornecedores e deveria conter identificação por CPF ou CNPJ. Os que deverão ser inseridos para dados se encontra no 'script de inserção de dados'.

### Construção do banco de dados

#### 1 - Utilizei um recurso 'CREATE DATABASE IF NOT EXISTS' para somente criar o banco de dados caso não exista outro banco de dados com nome semelhante.

#### 2 - Tabela clientes

Armazena informações sobre clientes (pessoas físicas - PF e jurídicas - PJ).

Colunas:
idCliente: Identificador único do cliente (chave primária).
Primeiro_nome, Nome_meio, Ultimo_nome: Nome completo do cliente.
Tipo_cliente: Tipo de cliente (PF ou PJ).
CPF e CNPJ: Documentos de identificação. Apenas um deve ser preenchido conforme o tipo de cliente.
Endereço: Endereço do cliente.
Data_de_nascimento: Data de nascimento (apenas para PF).
Restrições:
chk_cliente: Garante que CPF é preenchido apenas para PF, e CNPJ para PJ.
unico_cpf e unico_cnpj: Garantem que documentos sejam únicos.
Relacionamento: idCliente será usado como chave estrangeira em outras tabelas.

#### 3 - Tabela produto

Armazena informações sobre os produtos disponíveis.

Colunas:
idProduto: Identificador único do produto (chave primária).
Produto_nome: Nome do produto.
Classificação_criança: Indica se o produto é para crianças (booleano).
Categoria: Categoria do produto (enumeração com valores fixos).
Descrição: Descrição do produto.
Valor: Preço do produto.
Relacionamento: idProduto será referenciado em várias tabelas.

#### 4 - Tabela pedidos

Gerencia pedidos feitos por clientes.

Colunas:
idPedido: Identificador único do pedido (chave primária).
idCliente: Identificador do cliente que fez o pedido (chave estrangeira para clientes).
Status_pedido: Status atual do pedido (Cancelado, Confirmado, etc.).
Descrição_pedido: Detalhes do pedido.
Valor_envio: Custo do envio (padrão: 10).
Método_de_pagamento: Forma de pagamento.
Relacionamento:
Chave estrangeira fk_pedidos_cliente relaciona pedidos a clientes.

#### 5 - Tabela métodos_pagamentos

Armazena os métodos de pagamento associados a cada cliente.

Colunas:
idPagamento: Identificador único do pagamento (chave primária).
idCliente: Identificador do cliente (chave estrangeira para clientes).
Tipo_de_pagamento: Tipo de pagamento (enumeração).
Número_cartão: Número do cartão (se aplicável).
Data_expiração: Validade do cartão.
Relacionamento:
Chave estrangeira fk_pagamento_cliente conecta pagamentos a clientes.

#### 6 - Tabela entrega

Gerencia entregas de pedidos.

Colunas:
idEntrega: Identificador único da entrega (chave primária).
idPedido: Identificador do pedido (chave estrangeira para pedidos).
Status_entrega: Status atual da entrega.
Código_rastreio: Código para rastreamento.
Data_estimada_entrega: Data estimada para entrega.
Relacionamento:
Chave estrangeira fk_entrega_pedido conecta entregas a pedidos.

#### 7 - Tabela estoque

Gerencia os estoques disponíveis.

Colunas:
idEstoque: Identificador único do estoque (chave primária).
Local_estoque: Localização do estoque.
Quantidade: Quantidade de itens armazenados.

#### 8 - Tabela fornecedor

Armazena informações sobre os fornecedores.

Colunas:
idFornecedor: Identificador único do fornecedor (chave primária).
Nome_social: Nome social do fornecedor.
CNPJ: Documento de identificação.
Contato: Número de contato.
Restrições:
unico_fornecedor: Garante que o CNPJ é único.

#### 9 - Tabela vendedor

Gerencia vendedores que comercializam produtos.

Colunas:
idVendedor: Identificador único (chave primária).
Nome_social: Nome social do vendedor.
CNPJ ou CPF: Identificação.
Localização: Localização do vendedor.
Contato: Informações de contato.
Restrições:
chk_vendedor: Garante que apenas um documento (CNPJ ou CPF) é preenchido.
unico_cnpj_vendedor e unico_cpf_vendedor: Garantem unicidade dos documentos.

#### 10 - Tabela produto_por_vendedor

Relaciona produtos aos vendedores.

Colunas:
idPvendedor: Identificador do vendedor (chave estrangeira para vendedor).
idPproduto: Identificador do produto (chave estrangeira para produto).
Quantidade_produto: Quantidade disponível com o vendedor.
Relacionamentos:
Chaves estrangeiras para vendedor e produto.

#### 11 - Tabela relação_de_produto_por_pedido

Relaciona produtos com pedidos específicos.

Colunas:
idPPproduto: Identificador do produto.
idPPpedido: Identificador do pedido.
Quantidade_produto_pedido: Quantidade de produtos no pedido.
Status_produto_pedido: Disponibilidade do produto.
Relacionamentos:
Chaves estrangeiras para produto e pedidos.

#### 12 - Tabela localização_de_produtos_em_estoque

Relaciona produtos com seus locais no estoque.

Colunas:
idLproduto: Identificador do produto.
idLestoque: Identificador do estoque.
Localização: Localização específica no estoque.
Relacionamentos:
Chaves estrangeiras para produto e estoque.

#### 13 - Tabela produtos_de_fornecedores

Relaciona fornecedores com os produtos que fornecem.

Colunas:
idPSfornecedor: Identificador do fornecedor.
idPSproduto: Identificador do produto.
Quantidade: Quantidade fornecida.
Relacionamentos:
Chaves estrangeiras para fornecedor e produto.

### Consultas

As consultas foram criadas utilizando SELECT, WHERE, ORDER BY, JOIN, LEFT JOIN, GROUP BY.
As consultas se encontram em "Script de Consultas".
