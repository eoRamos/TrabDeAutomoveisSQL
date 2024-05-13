CREATE TABLE Cliente (
    CPF VARCHAR(14) PRIMARY KEY,
    Nome VARCHAR(100),
    Data_Nascimento DATE
);

CREATE TABLE Locacao (
    Codigo_Locacao INT PRIMARY KEY,
    Veiculo VARCHAR(100),
    Cor VARCHAR(50),
    Placa VARCHAR(10),
    Diaria DECIMAL(10, 2),
    CPF_Cliente VARCHAR(14),
    Dias INT,
    Total DECIMAL(10, 2),
    FOREIGN KEY (CPF_Cliente) REFERENCES Cliente(CPF)
);
CREATE VIEW Locacao_Veiculo_Cliente AS
SELECT L.Codigo_Locacao, L.Veiculo, L.Cor, L.Placa, L.Diaria, C.Nome AS Nome_Cliente, C.CPF, C.Data_Nascimento, L.Dias, L.Total
FROM Locacao L
INNER JOIN Cliente C ON L.CPF_Cliente = C.CPF;
