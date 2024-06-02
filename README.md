#    1 -Cenário: Sistema de Gerenciamento de Loja de Bebidas
A loja de bebidas "Bebidas & Cia" necessita de um sistema de gerenciamento de banco de dados para otimizar suas operações tanto na loja física quanto no serviço de delivery. O sistema deve ser capaz de gerenciar informações sobre clientes, produtos (bebidas), pedidos e fornecedores, além de categorizar os tipos de bebidas disponíveis.
#    2 - Modelagem Conceitual

<img src = "[https://raw.githubusercontent.com/Viniciussinc/prova.sql/main/imagens/Mer%20corrigido.png](https://raw.githubusercontent.com/Viniciussinc/prova.sql/main/imagens/Corrigido.png)">

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
    Teor_Alcoolico DECIMAL(5,2) NOT NULL,  
    Volume INT NOT NULL,
    Preco DECIMAL(7,2) NOT NULL,  
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


#    5 - Inserção de dados 


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
INSERT INTO Fornecedor (Nome_Empresa, CNPJ, Telefone, Endereco) VALUES
('Cervejaria XYZ', '12345678000100', '123456789', 'Rua A, 123, Bairro B, Cidade C, Estado D, 12345-678'),
('Destilaria ABC', '98765432000100', '987654321', 'Rua X, 456, Bairro Y, Cidade Z, Estado W, 87654-321'),
('Vinícola Bella Vista', '11111111000111', '555555555', 'Rua V, 789, Bairro W, Cidade Q, Estado R, 78945-123'),
('Cervejaria Malte Real', '22222222000122', '666666666', 'Rua M, 101, Bairro N, Cidade P, Estado O, 23456-789'),
('Destilaria Blue Moon', '33333333000133', '777777777', 'Rua S, 202, Bairro T, Cidade U, Estado V, 34567-890'),
('Vinícola Pura Uva', '44444444000144', '888888888', 'Rua I, 303, Bairro J, Cidade K, Estado L, 45678-901'),
('Cervejaria Sol Nascente', '55555555000155', '999999999', 'Rua E, 404, Bairro F, Cidade G, Estado H, 56789-012'),
('Destilaria White Label', '66666666000166', '111111111', 'Rua O, 505, Bairro P, Cidade Q, Estado R, 67890-123'),
('Vinícola Casa Verde', '77777777000177', '222222222', 'Rua A, 606, Bairro B, Cidade C, Estado D, 78901-234'),
('Cervejaria Top Brewer', '88888888000188', '333333333', 'Rua Q, 707, Bairro R, Cidade S, Estado T, 89012-345'),
('Destilaria Golden Spirit', '99999999000199', '444444444', 'Rua H, 808, Bairro I, Cidade J, Estado K, 90123-456'),
('Vinícola Valle do Vinho', '12121212000100', '555555551', 'Rua B, 909, Bairro C, Cidade D, Estado E, 10123-567'),
('Cervejaria Estrela Dourada', '23232323000111', '666666662', 'Rua W, 010, Bairro X, Cidade Y, Estado Z, 21234-678'),
('Destilaria Black Pearl', '34343434000122', '777777773', 'Rua F, 121, Bairro G, Cidade H, Estado I, 32345-789'),
('Vinícola Campo Alegre', '45454545000133', '888888884', 'Rua C, 232, Bairro D, Cidade E, Estado F, 43456-890'),
('Cervejaria Montanha Azul', '56565656000144', '999999995', 'Rua U, 343, Bairro V, Cidade W, Estado X, 54567-901'),
('Destilaria Red Dragon', '67676767000155', '111111116', 'Rua N, 454, Bairro O, Cidade P, Estado Q, 65678-012'),
('Vinícola Horizonte', '78787878000166', '222222227', 'Rua L, 565, Bairro M, Cidade N, Estado O, 76789-123'),
('Cervejaria Lua Cheia', '89898989000177', '333333338', 'Rua K, 676, Bairro L, Cidade M, Estado N, 87890-234'),
('Destilaria Crystal Clear', '90909090000188', '444444449', 'Rua D, 787, Bairro E, Cidade F, Estado G, 98901-345');
INSERT INTO Tipo_Bebida (Descricao) VALUES
('Cerveja'),
('Vodka'),
('Vinho Tinto'),
('Vinho Branco'),
('Whisky'),
('Cachaça'),
('Tequila'),
('Rum'),
('Gin'),
('Licor'),
('Champagne'),
('Conhaque'),
('Espumante'),
('Saké'),
('Sidra'),
('Cerveja Artesanal'),
('Cerveja Lager'),
('Cerveja IPA'),
('Cerveja Stout'),
('Cerveja Pilsen');
INSERT INTO Bebida (Nome, Tipo, Teor_Alcoolico, Volume, Preco, Fornecedor_ID, Tipo_ID) VALUES
('Cerveja Pilsen', 'Cerveja', 4.50, 500, 7.50, 1, 1),
('Vodka Absolut', 'Vodka', 40.00, 1000, 120.00, 2, 2),
('Vinho Tinto Malbec', 'Vinho Tinto', 13.50, 750, 45.00, 3, 3),
('Vinho Branco Chardonnay', 'Vinho Branco', 12.00, 750, 50.00, 4, 4),
('Whisky Johnnie Walker', 'Whisky', 40.00, 1000, 200.00, 5, 5),
('Cachaça 51', 'Cachaça', 39.00, 1000, 25.00, 6, 6),
('Tequila Jose Cuervo', 'Tequila', 38.00, 750, 100.00, 7, 7),
('Rum Bacardi', 'Rum', 37.50, 1000, 85.00, 8, 8),
('Gin Tanqueray', 'Gin', 47.30, 1000, 130.00, 9, 9),
('Licor Amarula', 'Licor', 17.00, 750, 70.00, 10, 10),
('Champagne Moet & Chandon', 'Champagne', 12.00, 750, 300.00, 11, 11),
('Conhaque Hennessy', 'Conhaque', 40.00, 1000, 450.00, 12, 12),
('Espumante Chandon', 'Espumante', 11.50, 750, 85.00, 13, 13),
('Saké Hakushika', 'Saké', 15.00, 750, 60.00, 14, 14),
('Sidra Cereser', 'Sidra', 4.50, 660, 12.00, 15, 15),
('Cerveja IPA Colorado', 'Cerveja Artesanal', 6.50, 600, 18.00, 16, 16),
('Cerveja Lager Heineken', 'Cerveja Lager', 5.00, 600, 10.00, 17, 17),
('Cerveja IPA Goose Island', 'Cerveja IPA', 5.90, 600, 20.00, 18, 18),
('Cerveja Stout Guinness', 'Cerveja Stout', 6.00, 440, 15.00, 19, 19),
('Cerveja Pilsen Brahma', 'Cerveja Pilsen', 4.50, 350, 3.50, 20, 20);
INSERT INTO Cliente (Nome, Email, Telefone, Endereco, Data_Registro) VALUES
('Carlos Pereira', 'carlos@gmail.com', '123456789', 'Rua A, 123, Bairro B, Cidade C, Estado D, 12345-678', '2023-01-01'),
('Ana Santos', 'ana@gmail.com', '987654321', 'Rua X, 456, Bairro Y, Cidade Z, Estado W, 87654-321', '2023-02-01'),
('Bruno Silva', 'bruno@gmail.com', '123123123', 'Rua D, 789, Bairro E, Cidade F, Estado G, 12345-678', '2023-03-01'),
('Carla Souza', 'carla@gmail.com', '987987987', 'Rua G, 1011, Bairro H, Cidade I, Estado J, 98765-432', '2023-04-01'),
('Daniel Almeida', 'daniel@gmail.com', '456456456', 'Rua J, 1213, Bairro K, Cidade L, Estado M, 87654-321', '2023-05-01'),
('Elena Costa', 'elena@gmail.com', '789789789', 'Rua M, 1415, Bairro N, Cidade O, Estado P, 76543-210', '2023-06-01'),
('Fernando Lima', 'fernando@gmail.com', '112233445', 'Rua P, 1617, Bairro Q, Cidade R, Estado S, 12345-678', '2023-07-01'),
('Gabriela Moreira', 'gabriela@gmail.com', '667788990', 'Rua S, 1819, Bairro T, Cidade U, Estado V, 98765-432', '2023-08-01'),
('Henrique Oliveira', 'henrique@gmail.com', '998877665', 'Rua V, 2021, Bairro W, Cidade X, Estado Y, 87654-321', '2023-09-01'),
('Isabela Ferreira', 'isabela@gmail.com', '334455667', 'Rua X, 2223, Bairro Y, Cidade Z, Estado A, 76543-210', '2023-10-01'),
('João Martins', 'joao@gmail.com', '112211223', 'Rua B, 2425, Bairro C, Cidade D, Estado E, 65432-109', '2023-11-01'),
('Karla Souza', 'karla@gmail.com', '223322334', 'Rua F, 2627, Bairro G, Cidade H, Estado I, 54321-098', '2023-12-01'),
('Lucas Almeida', 'lucas@gmail.com', '334433445', 'Rua H, 2829, Bairro I, Cidade J, Estado K, 43210-987', '2024-01-01'),
('Mariana Costa', 'mariana@gmail.com', '445544556', 'Rua J, 3031, Bairro K, Cidade L, Estado M, 32109-876', '2024-02-01'),
('Nicolas Santos', 'nicolas@gmail.com', '556655667', 'Rua M, 3233, Bairro N, Cidade O, Estado P, 21098-765', '2024-03-01'),
('Olivia Pereira', 'olivia@gmail.com', '667766778', 'Rua O, 3435, Bairro P, Cidade Q, Estado R, 10987-654', '2024-04-01'),
('Pedro Ferreira', 'pedro@gmail.com', '778877889', 'Rua Q, 3637, Bairro R, Cidade S, Estado T, 09876-543', '2024-05-01'),
('Quintino Silva', 'quintino@gmail.com', '889988990', 'Rua S, 3839, Bairro T, Cidade U, Estado V, 98765-432', '2024-06-01'),
('Rafaela Mendes', 'rafaela@gmail.com', '990099001', 'Rua V, 4041, Bairro W, Cidade X, Estado Y, 87654-321', '2024-07-01'),
('Sérgio Oliveira', 'sergio@gmail.com', '101010101', 'Rua X, 4243, Bairro Y, Cidade Z, Estado A, 76543-210', '2024-08-01');
INSERT INTO Pedido (Data_Pedido, Cliente_ID, Bebida_ID, Quantidade) VALUES
('2024-01-01', 1, 1, 3),
('2024-02-01', 2, 2, 1),
('2024-03-01', 3, 3, 2),
('2024-04-01', 4, 4, 1),
('2024-05-01', 5, 5, 4),
('2024-06-01', 6, 6, 1),
('2024-07-01', 7, 7, 2),
('2024-08-01', 8, 8, 1),
('2024-09-01', 9, 9, 3),
('2024-10-01', 10, 10, 1),
('2024-11-01', 11, 11, 2),
('2024-12-01', 12, 12, 1),
('2024-01-02', 13, 13, 4),
('2024-02-02', 14, 14, 2),
('2024-03-02', 15, 15, 1),
('2024-04-02', 16, 16, 3),
('2024-05-02', 17, 17, 1),
('2024-06-02', 18, 18, 2),
('2024-07-02', 19, 19, 1),
('2024-08-02', 20, 20, 2);
```

#    6 - CRUD

```sql

 INSERT INTO Fornecedor (Nome_Empresa, CNPJ, Telefone, Endereco) 
VALUES ('Zezim distribuidora', '12345678901234', '987654321', 'Rua Nova, 789, Bairro C, Cidade D, Estado E, 54321-098');

SELECT * FROM Fornecedor;

UPDATE Cliente 
SET Telefone = '999999999' 
WHERE ID_Cliente = 1

DELETE FROM Fornecedor 
WHERE ID_Fornecedor = 2;
```




