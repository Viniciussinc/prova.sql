#    1 -Cenário: Sistema de Gerenciamento de Loja de Bebidas
A loja de bebidas "Bebidas & Cia" necessita de um sistema de gerenciamento de banco de dados para otimizar suas operações tanto na loja física quanto no serviço de delivery. O sistema deve ser capaz de gerenciar informações sobre clientes, produtos (bebidas), pedidos e fornecedores, além de categorizar os tipos de bebidas disponíveis.
#    2 - Modelagem Conceitual

<img src = "https://raw.githubusercontent.com/Viniciussinc/prova.sql/main/imagens/Mer%20corrigido.png">

#    3 - Modelagem Lógica

<img src = "https://raw.githubusercontent.com/Viniciussinc/prova.sql/main/imagens/Opera%20Snapshot_2024-06-01_185115_app.brmodeloweb.com.png">

#    4 - Modelagem Física

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
    FOREIGN KEY (Bebida_ID) REFERENCES Bebida(ID_Bebida)
```


#4 - Inserção de dados 

``` sql
INSERT INTO Fornecedor (Nome_Empresa, CNPJ, Telefone, Endereco) VALUES
('Cervejaria XYZ', '12345678000100', '123456789', 'Rua A, 123, Bairro B, Cidade C, Estado D, 12345-678'),
('Destilaria ABC', '98765432000100', '987654321', 'Rua X, 456, Bairro Y, Cidade Z, Estado W, 87654-321');
INSERT INTO Tipo_Bebida (Descricao) VALUES
('Cerveja'),
('Vodka');
INSERT INTO Bebida (Nome, Tipo, Teor_Alcoolico, Volume, Preco, Fornecedor_ID, Tipo_ID) VALUES
('Cerveja Pilsen', 'Cerveja', 4.50, 500, 7.50, 1, 1),
('Vodka Absolut', 'Vodka', 40.00, 1000, 120.00, 2, 2);

INSERT INTO Cliente (Nome, Email, Telefone, Endereco, Data_Registro) VALUES
('Carlos Pereira', 'carlos@gmail.com', '123456789', 'Rua A, 123, Bairro B, Cidade C, Estado D, 12345-678', '2023-01-01'),
('Ana Santos', 'ana@gmail.com', '987654321', 'Rua X, 456, Bairro Y, Cidade Z, Estado W, 87654-321', '2023-02-01');
INSERT INTO Pedido (Data_Pedido, Cliente_ID, Bebida_ID, Quantidade) VALUES
('2024-01-01', 1, 1, 3),
('2024-02-01', 2, 2, 1);

```
