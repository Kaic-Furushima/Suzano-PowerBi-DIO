-- Recuperar todos os clientes
SELECT * FROM Cliente;

-- Recuperar apenas o nome e o endereço dos clientes
SELECT Nome, Endereço FROM Cliente;

-- Recuperar pedidos cujo status seja "Em Processamento"
SELECT * 
FROM Pedido 
WHERE `Status do Pedido` = 'Em Processamento';

-- Recuperar produtos cujo valor seja maior que 100
SELECT * 
FROM Produto 
WHERE CAST(Valor AS FLOAT) > 100;

-- Calcular o valor total de cada item no estoque baseado na quantidade
SELECT 
    p.Descrição AS Produto, 
    ep.Quantidade, 
    CAST(p.Valor AS FLOAT) * ep.Quantidade AS ValorTotal
FROM Produto p
JOIN Estoque_has_Produto ep ON p.idProduto = ep.Produto_idProduto;

-- Concatenar o nome e a identificação do cliente
SELECT 
    CONCAT(Nome, ' (', Identificação, ')') AS ClienteCompleto 
FROM Cliente;

-- Listar os produtos ordenados por categoria em ordem alfabética
SELECT * 
FROM Produto 
ORDER BY Categoria ASC;

-- Listar os pedidos mais recentes primeiro
SELECT * 
FROM Pedido 
ORDER BY idPedido DESC;

-- Listar categorias de produtos com valor médio acima de 50
SELECT 
    Categoria, 
    AVG(CAST(Valor AS FLOAT)) AS ValorMedio 
FROM Produto 
GROUP BY Categoria 
HAVING AVG(CAST(Valor AS FLOAT)) > 50;

-- Listar clientes com mais de 5 pedidos
SELECT 
    c.Nome, 
    COUNT(p.idPedido) AS TotalPedidos
FROM Cliente c
JOIN Pedido p ON c.idCliente = p.Cliente_idCliente
GROUP BY c.idCliente
HAVING COUNT(p.idPedido) > 5;

-- Listar todos os pedidos com o nome do cliente
SELECT 
    p.idPedido, 
    p.`Status do Pedido`, 
    c.Nome AS Cliente 
FROM Pedido p
JOIN Cliente c ON p.Cliente_idCliente = c.idCliente;

-- Listar produtos, fornecedores e os locais de estoque em que estão disponíveis
SELECT 
    p.Descrição AS Produto, 
    f.`Razão Social` AS Fornecedor, 
    e.`Local` AS Estoque 
FROM Produto p
JOIN Disponibilizando_um_Produto dp ON p.idProduto = dp.Produto_idProduto
JOIN Fornecedor f ON dp.Fornecedor_idFornecedor = f.idFornecedor
JOIN Estoque_has_Produto ep ON p.idProduto = ep.Produto_idProduto
JOIN Estoque e ON ep.Estoque_idEstoque = e.idEstoque;

-- Listar o valor total dos pedidos e o nome do cliente
SELECT 
    c.Nome AS Cliente, 
    SUM(CAST(p.`Frete` AS FLOAT)) AS ValorTotal 
FROM Pedido p
JOIN Cliente c ON p.Cliente_idCliente = c.idCliente
GROUP BY c.idCliente;