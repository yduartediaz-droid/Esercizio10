-- TABELLA REPARTI
CREATE TABLE reparti (
    id INT PRIMARY KEY AUTO_INCREMENT,
    nome VARCHAR(100) NOT NULL,
    responsabile_id INT UNIQUE
);

-- TABELLA DIPENDENTI
CREATE TABLE dipendenti (
    id INT PRIMARY KEY AUTO_INCREMENT,
    nome VARCHAR(100) NOT NULL,
    cognome VARCHAR(100) NOT NULL,
    email VARCHAR(150) UNIQUE NOT NULL,
    stipendio DECIMAL(10,2),
    data_assunzione DATE,
    reparto_id INT,
    
    FOREIGN KEY (reparto_id) REFERENCES reparti(id)
);

-- AGGIUNTA FK RESPONSABILE (dopo dipendenti)
ALTER TABLE reparti
ADD CONSTRAINT fk_responsabile
FOREIGN KEY (responsabile_id) REFERENCES dipendenti(id);

-- TABELLA PROGETTI
CREATE TABLE progetti (
    id INT PRIMARY KEY AUTO_INCREMENT,
    nome VARCHAR(150) NOT NULL,
    data_inizio DATE
);

-- TABELLA ASSEGNAZIONI (N:M)
CREATE TABLE assegnazioni (
    dipendente_id INT,
    progetto_id INT,
    data_assegnazione DATE DEFAULT CURRENT_DATE,
    
    PRIMARY KEY (dipendente_id, progetto_id),
    
    FOREIGN KEY (dipendente_id) REFERENCES dipendenti(id),
    FOREIGN KEY (progetto_id) REFERENCES progetti(id)
);