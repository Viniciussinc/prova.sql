# 1 -Cenário: Sistema de Gerenciamento de Loja de Bebidas
A loja de bebidas "Bebidas & Cia" necessita de um sistema de gerenciamento de banco de dados para otimizar suas operações tanto na loja física quanto no serviço de delivery. O sistema deve ser capaz de gerenciar informações sobre clientes, produtos (bebidas), pedidos e fornecedores, além de categorizar os tipos de bebidas disponíveis.
# 2 - Modelagem Conceitual
<img src = "https://raw.githubusercontent.com/Viniciussinc/prova.sql/main/imagens/Mer%20corrigido.png">
# 3 - Modelagem Lógica
<img src = "https://raw.githubusercontent.com/Viniciussinc/prova.sql/main/imagens/Opera%20Snapshot_2024-06-01_185115_app.brmodeloweb.com.png">
# 4 - Modelagem Física
``` sql
CREATE TABLE Fornecedor (
    ID_Fornecedor INT PRIMARY KEY IDENTITY(1,1),
    Nome_Empresa NVARCHAR(255) NOT NULL,
    CNPJ NVARCHAR(14) NOT NULL,
    Telefone NVARCHAR(15) NOT NULL,
    Endereco NVARCHAR(255) NOT NULL
);
CREATE TABLE Tipo_Bebida (
    ID_Tipo INT PRIMARY KEY IDENTITY(1,1),
    Descricao NVARCHAR(100) NOT NULL
);
CREATE TABLE Bebida (
    ID_Bebida INT PRIMARY KEY IDENTITY(1,1),
    Nome NVARCHAR(255) NOT NULL,
    Tipo NVARCHAR(50) NOT NULL,
    Teor_Alcoolico DECIMAL(5,2) NOT NULL,  -- Aumentando a precisão para Teor_Alcoolico
    Volume INT NOT NULL,
    Preco DECIMAL(7,2) NOT NULL,  -- Aumentando a precisão para Preco
    Fornecedor_ID INT NOT NULL,
    Tipo_ID INT NOT NULL,
    FOREIGN KEY (Fornecedor_ID) REFERENCES Fornecedor(ID_Fornecedor),
    FOREIGN KEY (Tipo_ID) REFERENCES Tipo_Bebida(ID_Tipo)
);
CREATE TABLE Cliente (
    ID_Cliente INT PRIMARY KEY IDENTITY(1,1),
    Nome NVARCHAR(100) NOT NULL,
    Email NVARCHAR(100) NOT NULL,
    Telefone NVARCHAR(15) NOT NULL,
    Endereco NVARCHAR(255) NOT NULL,
    Data_Registro DATE NOT NULL
);
CREATE TABLE Pedido (
    ID_Pedido INT PRIMARY KEY IDENTITY(1,1),
    Data_Pedido DATE NOT NULL,
    Cliente_ID INT NOT NULL,
    Bebida_ID INT NOT NULL,
    Quantidade INT NOT NULL,
    FOREIGN KEY (Cliente_ID) REFERENCES Cliente(ID_Cliente),
    FOREIGN KEY (Bebida_ID) REFERENCES Bebida(ID_Bebida)```
