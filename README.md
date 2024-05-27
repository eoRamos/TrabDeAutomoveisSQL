CREATE TABLE Locação (
  Cód_Locação INT PRIMARY KEY,
  Diária DECIMAL(5,2),
  Dias INT,
  Total DECIMAL(8,2)
);

CREATE TABLE Veículo (
  Cód_Veículo INT PRIMARY KEY,
  Veículo VARCHAR(255),
  Cor VARCHAR(255),
  Placa VARCHAR(255)
);

CREATE TABLE Cliente (
  Cód_Cliente INT PRIMARY KEY,
  Cliente VARCHAR(255),
  CPF VARCHAR(255),
  Nascimento DATE
);

CREATE TABLE Locação_Veículo (
  Cód_Locação INT,
  Cód_Veículo INT,
  PRIMARY KEY (Cód_Locação, Cód_Veículo),
  FOREIGN KEY (Cód_Locação) REFERENCES Locação(Cód_Locação),
  FOREIGN KEY (Cód_Veículo) REFERENCES Veículo(Cód_Veículo)
);

CREATE TABLE Locação_Cliente (
  Cód_Locação INT,
  Cód_Cliente INT,
  PRIMARY KEY (Cód_Locação, Cód_Cliente),
  FOREIGN KEY (Cód_Locação) REFERENCES Locação(Cód_Locação),
  FOREIGN KEY (Cód_Cliente) REFERENCES Cliente(Cód_Cliente)
);
CREATE VIEW Locações_Veículos_Clientes AS
SELECT 
  L.Cód_Locação,
  L.Diária,
  L.Dias,
  L.Total,
  V.Veículo,
  V.Cor,
  V.Placa,
  C.Cliente,
  C.CPF,
  C.Nascimento
FROM Locação AS L
JOIN Locação_Veículo AS LV ON L.Cód_Locação = LV.Cód_Locação
JOIN Veículo AS V ON LV.Cód_Veículo = V.Cód_Veículo
JOIN Locação_Cliente AS LC ON L.Cód_Locação = LC.Cód_Locação
JOIN Cliente AS C ON LC.Cód_Cliente = C.Cód_Cliente;
