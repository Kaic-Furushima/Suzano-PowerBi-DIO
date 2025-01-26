# Listar todos os clientes
SELECT * 

FROM Cliente;

# Recuperar apenas o nome e o endereço dos clientes
SELECT Nome, Endereço 

FROM Cliente;

# Recuperar veículos do cliente com ID específico
SELECT * 

FROM Veículo 

WHERE Cliente_idCliente = 1;

# Listar ordens de serviço com status "Em andamento"
SELECT * 

FROM `Ordem de Serviço` 

WHERE Status = 'Em andamento';

# Calcular o valor total de peças utilizadas em uma ordem de serviço
SELECT 
    `Ordem de Serviço_idOrdem de Serviço` AS OrdemServico, 
    SUM(Quantidade * CAST(`Peças OScol` AS DECIMAL)) AS ValorTotalPeças
    
FROM `Peças OS`

GROUP BY `Ordem de Serviço_idOrdem de Serviço`;

# Criar um campo com o nome completo do cliente concatenado com o endereço
SELECT 
    CONCAT(Nome, ' - ', Endereço) AS ClienteCompleto 
    
FROM Cliente;

# Listar veículos ordenados pelo ano de fabricação
SELECT * 

FROM Veículo 

ORDER BY Ano DESC;

# Listar ordens de serviço ordenadas pela data de emissão
SELECT * 

FROM `Ordem de Serviço` 

ORDER BY `Data de Emissão` ASC;

# Listar clientes com mais de 1 veículo cadastrado
SELECT 
    c.Nome, 
    COUNT(v.idVeículo) AS TotalVeiculos 
    
FROM Cliente c

JOIN Veículo v ON c.idCliente = v.Cliente_idCliente

GROUP BY c.idCliente

HAVING COUNT(v.idVeículo) > 1;

# Listar ordens de serviço com valor total acima de 500
SELECT 
    `Ordem de Serviço_idOrdem de Serviço`, 
    SUM(CAST(Quantidade AS DECIMAL) * CAST(`Peças OScol` AS DECIMAL)) AS ValorTotal 
    
FROM `Peças OS`

GROUP BY `Ordem de Serviço_idOrdem de Serviço`

HAVING SUM(CAST(Quantidade AS DECIMAL) * CAST(`Peças OScol` AS DECIMAL)) > 500;

# Listar ordens de serviço com o modelo do veículo associado
SELECT 
    os.idOrdem de Serviço AS OrdemServico, 
    v.Modelo AS Veiculo 
    
FROM `Ordem de Serviço` os

JOIN Veículo v ON os.Veículo_idVeículo = v.idVeículo;

# Listar peças utilizadas em ordens de serviço com o nome do mecânico responsável
SELECT 
    p.Nome AS Peca, 
    mos.`Ordem de Serviço_idOrdem de Serviço` AS OrdemServico, 
    m.Nome AS Mecanico 
    
FROM `Peças OS` p

JOIN `Mecânico OS` mos ON p.`Ordem de Serviço_idOrdem de Serviço` = mos.`Ordem de Serviço_idOrdem de Serviço`

JOIN Mecânico m ON mos.Mecânico_idMecânico = m.idMecânico;

# Listar todos os serviços realizados com descrição e valor por ordem de serviço
SELECT 
    s.Descrição AS Servico, 
    sos.Quantidade, 
    s.Valor * sos.Quantidade AS ValorTotal
    
FROM `Serviço OS` sos

JOIN Serviço s ON sos.Serviço_idServiço = s.idServiço;