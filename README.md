# Projeto Banco de Dados – Loja de Suplementos

Projeto desenvolvido para modelagem e implementação de um banco de dados relacional para uma loja de suplementos. O projeto contempla a estrutura completa para o gerenciamento de clientes, fornecedores, produtos (com controle de sabores e tamanhos), categorias, pedidos e o detalhamento dos itens comprados.

# Objetivo

Desenvolver a modelagem e implementação de um banco de dados representando o funcionamento de uma loja de suplementos, aplicando conceitos de modelagem relacional, integridade referencial e scripts adaptados para o dialeto do Oracle Database.

# Tecnologias utilizadas

- Oracle Database
- Oracle SQL Developer (ou DBeaver / Oracle Live SQL)
- SQL (DDL e DML com tipos nativos Oracle: `VARCHAR2`, `NUMBER`, `TIMESTAMP`, `CLOB`)

# Estrutura do projeto

- `modelo_logico.png`  
  Imagem com o modelo lógico estrutural (entidades e relacionamentos) do banco de dados.

- `loja_suplementos_oracle.sql`  
  Script SQL contendo a criação das tabelas (DDL) e inserção de dados (DML).

- `README.md`  
  Documentação do projeto.

# Entidades do banco

- Cliente
- Fornecedor
- Categoria
- Produto
- Pedido
- Item_Pedido
- Contem (Tabela Associativa / Relacionamento N:M)

# Atributos principais

### Categoria
- ID_Categoria (PK)
- Nome (Ex: Proteínas, Creatina, Pré treino)
- Descricao

### Fornecedor
- ID_Fornecedor (PK)
- Razao_Social
- CNPJ
- Contatos (Email e Telefone)

### Cliente
- ID_Cliente (PK)
- Nome, Cpf, Data_Nascimento
- Contatos (Email e Telefone)
- Endereco_Entrega

### Produto
- ID_Produto (PK)
- Nome, Descricao, Sabor, Peso_Volume (Ex: 900g, 300g)
- Preco_Venda, Quantidade_Estoque
- fk_Categoria_ID_Categoria (FK)
- fk_Fornecedor_ID_Fornecedor (FK)

### Pedido
- ID_Pedido (PK)
- Data_Hora (Timestamp)
- Valor_Total, Status, Metodo_Pagamento
- fk_Cliente_ID_Cliente (FK)

### Item_Pedido
- ID_Item (PK)
- Quantidade
- Preco_Unitario

### Contem (Associativa)
- fk_Item_Pedido_ID_Item (PK/FK)
- fk_Produto_ID_Produto (PK/FK)
- fk_Pedido_ID_Pedido (PK/FK)

# Relacionamentos

- Cliente (1) → (N) Pedido
- Categoria (1) → (N) Produto
- Fornecedor (1) → (N) Produto
- Pedido (1) → (N) Contem
- Produto (1) → (N) Contem
- Item_Pedido (1) → (N) Contem

# Funcionalidades implementadas

- Criação de tabelas com sintaxe e tipagem Oracle (`VARCHAR2`, `NUMBER`, conversões com `TO_DATE` e `TO_TIMESTAMP`).
- Definição de Chaves Primárias (PK) e Estrangeiras (FK).
- Resolução de relacionamento N:M através da tabela associativa (`Contem`).
- Inserção de dados reais focados em suplementação:
  - **Categorias:** Proteínas, Creatina e Pré treino.
  - **Produtos:** Whey Protein Isolado (Morango/Chocolate - 900g), Creatina (Monohidratada/Pure - 300g), Pré Treinos (Laranja/Uva - 300g).
- Integridade referencial testada na inserção em cascata (Categoria/Fornecedor → Produto → Pedido → Contem).

# Como executar

1. Abrir sua ferramenta de gestão de banco de dados Oracle (SQL Developer, DBeaver, ou Oracle Live SQL via navegador).
2. Criar ou conectar-se ao seu schema do Oracle.
3. Abrir o arquivo `projeto.sql`.
4. Executar primeiro os blocos `CREATE TABLE` (respeitando a ordem do script para evitar erros de Foreign Key).
5. Executar os blocos `INSERT INTO` (DML) para popular as tabelas.
6. Realizar comandos `SELECT` para verificar as tabelas populadas (ex: `SELECT * FROM Produto;`).
