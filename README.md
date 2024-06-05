#   - Cenário: Sistema de Gerenciamento de Loja de Bebidas
A loja de bebidas "Bebidas & Cia" necessita de um sistema de gerenciamento de banco de dados para otimizar suas operações tanto na loja física quanto no serviço de delivery. O sistema deve ser capaz de gerenciar informações sobre clientes, produtos (bebidas), pedidos e fornecedores, além de categorizar os tipos de bebidas disponíveis.
#     - Modelagem Conceitual

<img src = "https://github.com/Viniciussinc/prova.sql/blob/main/imagens/2000110.png">

#     - Modelagem Lógica

<img src = "https://github.com/Viniciussinc/prova.sql/blob/main/imagens/fatec_bar.png">

#     - Modelagem Física

``` sql
CREATE TABLE Fornecedor (
    ID_Fornecedor INT PRIMARY KEY IDENTITY(1,1),
    Nome_Empresa NVARCHAR(255) NOT NULL,
    CNPJ NVARCHAR(14) NOT NULL,
    Telefone NVARCHAR(15) NOT NULL,
    Rua NVARCHAR(255) NOT NULL,
    Numero NVARCHAR(10) NOT NULL,
    Bairro NVARCHAR(100) NOT NULL,
    Cidade NVARCHAR(100) NOT NULL,
    Estado NVARCHAR(2) NOT NULL,
    CEP NVARCHAR(10) NOT NULL
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
    Telefone NVARCHAR(15) NOT NULL,
    Data_Registro DATE NOT NULL,
    Total_Pedidos INT NOT NULL DEFAULT 0
);
CREATE TABLE Email_Cliente (
    ID_Email INT PRIMARY KEY IDENTITY(1,1),
    Cliente_ID INT NOT NULL,
    Email NVARCHAR(100) NOT NULL,
    FOREIGN KEY (Cliente_ID) REFERENCES Cliente(ID_Cliente)
);
CREATE TABLE Pedido (
    ID_Pedido INT PRIMARY KEY IDENTITY(1,1),
    Data_Pedido DATE NOT NULL,
    Cliente_ID INT NOT NULL,
    FOREIGN KEY (Cliente_ID) REFERENCES Cliente(ID_Cliente)
);
CREATE TABLE Pedido_Bebida (
    ID_Pedido INT NOT NULL,
    ID_Bebida INT NOT NULL,
    Quantidade INT NOT NULL,
    PRIMARY KEY (ID_Pedido, ID_Bebida),
    FOREIGN KEY (ID_Pedido) REFERENCES Pedido(ID_Pedido),
    FOREIGN KEY (ID_Bebida) REFERENCES Bebida(ID_Bebida)
);
```
<img src = "https://github.com/Viniciussinc/prova.sql/blob/main/imagens/cvasdsadasdadas.png">

#     - Inserção de dados 


``` sql
INSERT INTO Fornecedor (Nome_Empresa, CNPJ, Telefone, Rua, Numero, Bairro, Cidade, Estado, CEP) VALUES
('Cervejaria XYZ', '12345678000100', '123456789', 'Rua A', '123', 'Bairro B', 'Cidade C', 'SP', '12345-678'),
('Destilaria ABC', '98765432000100', '987654321', 'Rua X', '456', 'Bairro Y', 'Cidade Z', 'RJ', '87654-321'),
('Vinícola do Vale', '32345678000144', '323456789', 'Rua C', '300', 'Bairro D', 'Cidade E', 'MG', '32345-333'),
('Cervejaria Imperial', '22345678000122', '223456789', 'Rua D', '400', 'Bairro F', 'Cidade G', 'PR', '22345-222'),
('Destilaria Fina', '62345678000177', '623456789', 'Rua E', '500', 'Bairro H', 'Cidade I', 'RS', '52345-555'),
('Vinícola Encosta', '42345678000155', '423456789', 'Rua F', '600', 'Bairro J', 'Cidade K', 'SC', '42345-444'),
('Cervejaria Moderna', '72345678000188', '723456789', 'Rua G', '700', 'Bairro L', 'Cidade M', 'BA', '72345-777'),
('Destilaria do Norte', '82345678000199', '823456789', 'Rua H', '800', 'Bairro N', 'Cidade O', 'CE', '82345-888'),
('Vinícola Vista Alegre', '92345678000200', '923456789', 'Rua I', '900', 'Bairro P', 'Cidade Q', 'PE', '92345-999'),
('Cervejaria Continental', '10345678000211', '103456789', 'Rua J', '1000', 'Bairro R', 'Cidade S', 'ES', '10345-000'),
('Destilaria Especial', '11345678000222', '113456789', 'Rua K', '1100', 'Bairro T', 'Cidade U', 'GO', '11345-111'),
('Vinícola Colheita', '12345678000233', '123456789', 'Rua L', '1200', 'Bairro V', 'Cidade W', 'MT', '12345-222'),
('Cervejaria Regional', '13345678000244', '133456789', 'Rua M', '1300', 'Bairro X', 'Cidade Y', 'MS', '13345-333'),
('Destilaria Premium', '14345678000255', '143456789', 'Rua N', '1400', 'Bairro Z', 'Cidade AA', 'DF', '14345-444'),
('Vinícola Solar', '15345678000266', '153456789', 'Rua O', '1500', 'Bairro AB', 'Cidade AC', 'AL', '15345-555'),
('Cervejaria Nacional', '16345678000277', '163456789', 'Rua P', '1600', 'Bairro AD', 'Cidade AE', 'PB', '16345-666'),
('Destilaria Central', '17345678000288', '173456789', 'Rua Q', '1700', 'Bairro AF', 'Cidade AG', 'RN', '17345-777'),
('Vinícola Monte Verde', '18345678000299', '183456789', 'Rua R', '1800', 'Bairro AH', 'Cidade AI', 'PI', '18345-888'),
('Cervejaria Internacional', '19345678000300', '193456789', 'Rua S', '1900', 'Bairro AJ', 'Cidade AK', 'TO', '19345-999'),
('Destilaria do Sul', '20345678000311', '203456789', 'Rua T', '2000', 'Bairro AL', 'Cidade AM', 'RR', '20345-000');
INSERT INTO Tipo_Bebida (Descricao) VALUES
('Cerveja'),
('Vodka'),
('Vinho'),
('Whisky'),
('Rum'),
('Tequila'),
('Gin'),
('Cachaça'),
('Licores'),
('Champagne'),
('Conhaque'),
('Saké'),
('Prosecco'),
('Sidra'),
('Vermouth'),
('Aperitivo'),
('Brandy'),
('Porto'),
('Madeira'),
('Espumante');
INSERT INTO Bebida (Nome, Tipo, Teor_Alcoolico, Volume, Preco, Fornecedor_ID, Tipo_ID) VALUES
('Cerveja Pilsen', 'Cerveja', 4.5, 500, 7.50, 1, 1),
('Vodka Absolut', 'Vodka', 40.0, 1000, 120.00, 2, 2),
('Vinho Tinto', 'Vinho', 13.5, 750, 50.00, 3, 3),
('Whisky Johnnie Walker', 'Whisky', 40.0, 1000, 180.00, 4, 4),
('Rum Bacardi', 'Rum', 37.5, 700, 65.00, 5, 5),
('Tequila Jose Cuervo', 'Tequila', 38.0, 750, 90.00, 6, 6),
('Gin Tanqueray', 'Gin', 47.3, 1000, 130.00, 7, 7),
('Cachaça 51', 'Cachaça', 39.0, 1000, 25.00, 8, 8),
('Licor Amarula', 'Licores', 17.0, 750, 85.00, 9, 9),
('Champagne Moet', 'Champagne', 12.0, 750, 350.00, 10, 10),
('Conhaque Hennessy', 'Conhaque', 40.0, 700, 230.00, 11, 11),
('Saké Junmai', 'Saké', 15.0, 750, 75.00, 12, 12),
('Prosecco Italiano', 'Prosecco', 11.5, 750, 90.00, 13, 13),
('Sidra Cereser', 'Sidra', 4.7, 660, 12.00, 14, 14),
('Vermouth Martini', 'Vermouth', 16.0, 1000, 65.00, 15, 15),
('Aperitivo Campari', 'Aperitivo', 25.0, 900, 70.00, 16, 16),
('Brandy Domecq', 'Brandy', 36.0, 750, 95.00, 17, 17),
('Vinho do Porto', 'Porto', 20.0, 750, 120.00, 18, 18),
('Vinho Madeira', 'Madeira', 19.0, 750, 110.00, 19, 19),
('Espumante Chandon', 'Espumante', 11.5, 750, 130.00, 20, 20);
INSERT INTO Cliente (Nome, Telefone, Data_Registro, Total_Pedidos) VALUES
('João Silva', '11987654321', '2023-01-15', 3),
('Maria Souza', '21987654321', '2023-02-20', 5),
('Carlos Pereira', '31987654321', '2023-03-25', 2),
('Ana Oliveira', '41987654321', '2023-04-30', 4),
('Pedro Santos', '51987654321', '2023-05-05', 1),
('Lucas Lima', '61987654321', '2023-06-10', 6),
('Mariana Costa', '71987654321', '2023-07-15', 3),
('Gabriel Almeida', '81987654321', '2023-08-20', 2),
('Juliana Machado', '91987654321', '2023-09-25', 5),
('Felipe Braga', '101987654321', '2023-10-30', 4),
('Larissa Ferreira', '111987654321', '2023-11-05', 1),
('Thiago Barros', '121987654321', '2023-12-10', 6),
('Isabela Melo', '131987654321', '2023-01-15', 3),
('Rafael Rocha', '141987654321', '2023-02-20', 2),
('Fernanda Cunha', '151987654321', '2023-03-25', 5),
('Marcelo Mendes', '161987654321', '2023-04-30', 4),
('Aline Gomes', '171987654321', '2023-05-05', 1),
('Bruno Ribeiro', '181987654321', '2023-06-10', 6),
('Paula Duarte', '191987654321', '2023-07-15', 3),
('André Nogueira', '201987654321', '2023-08-20', 2);
INSERT INTO Email_Cliente (Cliente_ID, Email) VALUES
(1, 'joao.silva@gmail.com'),
(2, 'maria.souza@yahoo.com'),
(3, 'carlos.pereira@outlook.com'),
(4, 'ana.oliveira@hotmail.com'),
(5, 'pedro.santos@gmail.com'),
(6, 'lucas.lima@yahoo.com'),
(7, 'mariana.costa@outlook.com'),
(8, 'gabriel.almeida@hotmail.com'),
(9, 'juliana.machado@gmail.com'),
(10, 'felipe.braga@yahoo.com'),
(11, 'larissa.ferreira@outlook.com'),
(12, 'thiago.barros@hotmail.com'),
(13, 'isabela.melo@gmail.com'),
(14, 'rafael.rocha@yahoo.com'),
(15, 'fernanda.cunha@outlook.com'),
(16, 'marcelo.mendes@hotmail.com'),
(17, 'aline.gomes@gmail.com'),
(18, 'bruno.ribeiro@yahoo.com'),
(19, 'paula.duarte@outlook.com'),
(20, 'andre.nogueira@hotmail.com');
INSERT INTO Pedido (Data_Pedido, Cliente_ID) VALUES
('2023-01-20', 1),
('2023-01-25', 1),
('2023-02-10', 1),
('2023-02-20', 2),
('2023-02-25', 2),
('2023-03-05', 2),
('2023-03-15', 2),
('2023-03-25', 2),
('2023-04-05', 3),
('2023-04-15', 3),
('2023-04-25', 4),
('2023-05-05', 4),
('2023-05-15', 4),
('2023-05-25', 4),
('2023-06-05', 5),
('2023-06-15', 6),
('2023-06-25', 6),
('2023-07-05', 6),
('2023-07-15', 6),
('2023-07-25', 6);
INSERT INTO Pedido_Bebida (ID_Pedido, ID_Bebida, Quantidade) VALUES
(1, 1, 2),
(1, 2, 1),
(2, 3, 1),
(3, 4, 1),
(4, 5, 1),
(5, 6, 1),
(6, 7, 1),
(7, 8, 1),
(8, 9, 1),
(9, 10, 1),
(10, 11, 1),
(11, 12, 1),
(12, 13, 1),
(13, 14, 1),
(14, 15, 1),
(15, 16, 1),
(16, 17, 1),
(17, 18, 1),
(18, 19, 1),
(19, 20, 1),
(20, 1, 1);

```


<img src = "https://github.com/Viniciussinc/prova.sql/blob/main/imagens/Inserçao%20de%20dados.png">
#    6 - CRUD

```sql

INSERT INTO Fornecedor (Nome_Empresa, CNPJ, Telefone, Rua, Numero, Bairro, Cidade, Estado, CEP) 
VALUES ('Barbichina', '12345678000100', '123456789', 'Rua Flores', '123', 'Bairro Santa cruz', 'Franca', 'SP', '12345-678');

SELECT * FROM Fornecedor;

UPDATE Fornecedor 
SET Nome_Empresa = 'Robertoss', Telefone = '1123456789'
WHERE ID_Fornecedor = 1;


DELETE FROM Pedido_Bebida 
WHERE ID_Pedido = 1 AND ID_Bebida = 1;

```

# 1 - Create 
<img src = "https://github.com/Viniciussinc/prova.sql/blob/main/imagens/Create.png">


# 2 - Read 
<img src = "https://github.com/Viniciussinc/prova.sql/blob/main/imagens/Reading.png">


# 3 - Update 
<img src = "https://github.com/Viniciussinc/prova.sql/blob/main/imagens/Updating.png">


# 4 - Delete 
<img src = "https://github.com/Viniciussinc/prova.sql/blob/main/imagens/bebida_delete.png">

# Relatorios 


# Seleção Simples de Fornecedores
Propósito: Exibir todos os fornecedores cadastrados.


``` sql
SELECT * FROM Fornecedor;
```

<img src = "https://github.com/Viniciussinc/prova.sql/blob/main/imagens/Reading.png">


# Seleção com Filtro em Clientes
Propósito: Exibir os clientes que se registraram após uma data específica.


```sql
SELECT * FROM Cliente
WHERE Data_Registro > '2023-01-01';
```

<img src = "https://github.com/Viniciussinc/prova.sql/blob/main/imagens/Correçao1.png">


# Seleção e Ordenação de Bebidas por Preço
Propósito: Exibir todas as bebidas ordenadas pelo preço, do mais barato ao mais caro.


``` sql
SELECT * FROM Bebida
ORDER BY Preco ASC;
```


<img src = "https://github.com/Viniciussinc/prova.sql/blob/main/imagens/correçao_2.png">


# Seleção com Junção entre Bebida e Fornecedor
Propósito: Exibir os nomes das bebidas junto com o nome da empresa fornecedora.


```sql
SELECT Bebida.Nome, Fornecedor.Nome_Empresa
FROM Bebida
JOIN Fornecedor ON Bebida.Fornecedor_ID = Fornecedor.ID_Fornecedor;
```

<img src = "https://github.com/Viniciussinc/prova.sql/blob/main/imagens/corrçao_4.png">


# Seleção com Filtro e Ordenação em Pedidos
Propósito: Exibir todos os pedidos feitos por um cliente específico, ordenados pela data do pedido.


```sql
SELECT * FROM Pedido
WHERE Cliente_ID = 1
ORDER BY Data_Pedido DESC;
```


<img src = "https://github.com/Viniciussinc/prova.sql/blob/main/imagens/Correçao_5.png">


# Consulta : Listar todos os clientes e seus e-mails.


```sql
SELECT c.Nome, e.Email
FROM Cliente c
JOIN Email_Cliente e ON c.ID_Cliente = e.Cliente_ID
ORDER BY c.Nome;
```


<img src = "https://github.com/Viniciussinc/prova.sql/blob/main/imagens/Listar8.png">

# Seleção com Agregação para Contar Bebidas por Tipo
Propósito: Contar quantas bebidas existem de cada tipo.


```sql
SELECT Tipo_Bebida.Descricao, COUNT(Bebida.ID_Bebida) AS Quantidade_Bebidas
FROM Bebida
JOIN Tipo_Bebida ON Bebida.Tipo_ID = Tipo_Bebida.ID_Tipo
GROUP BY Tipo_Bebida.Descricao;
```


<img src = "https://github.com/Viniciussinc/prova.sql/blob/main/imagens/Lista9.png">


# Seleção com Junção e Filtro por Tipo de Bebida
Propósito: Exibir os nomes das bebidas e seus preços para um tipo específico de bebida.


```sql
SELECT Bebida.Nome, Bebida.Preco
FROM Bebida
JOIN Tipo_Bebida ON Bebida.Tipo_ID = Tipo_Bebida.ID_Tipo
WHERE Tipo_Bebida.Descricao = 'Cerveja';
```


<img src = "https://github.com/Viniciussinc/prova.sql/blob/main/imagens/Select10.png">


# Seleção com Junção e Ordenação por Cliente e Pedido
Propósito: Exibir todos os pedidos, ordenados pelo nome do cliente e depois pela data do pedido.


```sql
SELECT Pedido.ID_Pedido, Cliente.Nome, Pedido.Data_Pedido
FROM Pedido
JOIN Cliente ON Pedido.Cliente_ID = Cliente.ID_Cliente
ORDER BY Cliente.Nome, Pedido.Data_Pedido;
```

<img src = "https://github.com/Viniciussinc/prova.sql/blob/main/imagens/selct11.png">


# Seleção com Filtro em Bebidas e Fornecedores
Propósito: Esta consulta mostra o total de pedidos feitos por cada cliente, ordenados em ordem decrescente pelo total de pedidos.



```sql
SELECT c.Nome, COUNT(p.ID_Pedido) AS TotalPedidos
FROM Cliente c
JOIN Pedido p ON c.ID_Cliente = p.Cliente_ID
GROUP BY c.Nome
ORDER BY TotalPedidos DESC;
```

<img src = "https://github.com/Viniciussinc/prova.sql/blob/main/imagens/slclt44.png">








