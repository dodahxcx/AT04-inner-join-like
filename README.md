# AT04-inner-join-like
atividade mysql montando um banco de dados do zero para fazer consultar com "inner join" &amp; "like"

CREATE DATABASE Clientes;
USE Clientes;

CREATE TABLE Cliente (
    id_cliente INT PRIMARY KEY AUTO_INCREMENT,
    nome VARCHAR(100),
    email VARCHAR(100),
    telefone VARCHAR(15)
);

CREATE TABLE Pedido (
    id_pedido INT PRIMARY KEY AUTO_INCREMENT,
    id_cliente INT,
    data_pedido DATE,
    valor DECIMAL(10,2),
    FOREIGN KEY (id_cliente) REFERENCES Cliente(id_cliente)
);

CREATE TABLE Produto (
    id_produto INT PRIMARY KEY AUTO_INCREMENT,
    nome VARCHAR(100),
    preco DECIMAL(10,2)
);

CREATE TABLE ItemPedido (
    id_item INT PRIMARY KEY AUTO_INCREMENT,
    id_pedido INT,
    id_produto INT,
    quantidade INT,
    FOREIGN KEY (id_pedido) REFERENCES Pedido(id_pedido),
    FOREIGN KEY (id_produto) REFERENCES Produto(id_produto)
);

INSERT INTO Cliente (nome, email, telefone) VALUES
('João Silva', 'joao@email.com', '11987654321'),
('Maria Oliveira', 'maria@email.com', '21987654321'),
('Carlos Souza', 'carlos@email.com', '31987654321'),
('Ana Pereira', 'ana@email.com', '41987654321'),
('Pedro Santos', 'pedro@email.com', '51987654321'),
('Fernanda Costa', 'fernanda@email.com', '61987654321'),
('Lucas Lima', 'lucas@email.com', '71987654321'),
('Camila Mendes', 'camila@email.com', '81987654321'),
('Gustavo Almeida', 'gustavo@email.com', '91987654321'),
('Juliana Ferreira', 'juliana@email.com', '101987654321');

INSERT INTO Pedido (id_cliente, data_pedido, valor) VALUES
(1, '2025-05-10', 120.50),
(2, '2025-05-11', 75.00),
(3, '2025-05-12', 200.00),
(4, '2025-05-13', 50.00),
(5, '2025-05-14', 300.00),
(6, '2025-05-15', 150.00),
(7, '2025-05-16', 90.00),
(8, '2025-05-17', 220.00),
(9, '2025-05-18', 130.00),
(10, '2025-05-19', 170.00);

INSERT INTO Produto (nome, preco) VALUES
('Notebook', 2500.00),
('Mouse', 50.00),
('Teclado', 100.00),
('Monitor', 800.00),
('Impressora', 600.00),
('Headset', 200.00),
('Cadeira Gamer', 900.00),
('Mesa para PC', 500.00),
('HD Externo', 400.00),
('Placa de Vídeo', 1800.00);

INSERT INTO ItemPedido (id_pedido, id_produto, quantidade) VALUES
(1, 1, 1), (1, 2, 2), (2, 3, 1), (2, 4, 1), 
(3, 5, 1), (3, 6, 2), (4, 7, 1), (4, 8, 1), 
(5, 9, 2), (5, 10, 1);

SELECT Cliente.nome, Pedido.id_pedido, Pedido.data_pedido 
FROM Cliente 
INNER JOIN Pedido ON Cliente.id_cliente = Pedido.id_cliente;

SELECT Pedido.id_pedido, Cliente.nome, Produto.nome, ItemPedido.quantidade 
FROM Pedido
INNER JOIN Cliente ON Pedido.id_cliente = Cliente.id_cliente
INNER JOIN ItemPedido ON Pedido.id_pedido = ItemPedido.id_pedido
INNER JOIN Produto ON ItemPedido.id_produto = Produto.id_produto;

SELECT * FROM Cliente WHERE nome LIKE '%Silva%';
SELECT * FROM Produto WHERE preco > 500.00;
SELECT * FROM Pedido WHERE data_pedido BETWEEN '2025-05-10' AND '2025-05-15';
