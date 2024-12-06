-- 2
CREATE DATABASE christopher_sub;
\c christopher_sub;
DROP TABLE IF EXISTS viagem;
DROP TABLE IF EXISTS turista;
DROP TABLE IF EXISTS pais;

CREATE TABLE pais (
  id serial PRIMARY KEY,
  nome varchar(100) NOT NULL,
  cidade varchar(100) NOT NULL
);

CREATE TABLE turista (
  id varchar(14) PRIMARY KEY,
  nome varchar(255) NOT NULL,
  cpf varchar(12) NOT NULL,
  celular varchar(30) NOT NULL,
  endereco varchar(100) NOT NULL
);

CREATE TABLE viagem (
  turista_id varchar(14) NOT NULL REFERENCES turista (id),
  pais_id integer NOT NULL REFERENCES pais (id),
  data date NOT NULL,
  PRIMARY KEY (turista_id, pais_id)
);

-- 3
INSERT INTO pais (nome, cidade)
  VALUES ('Estados Unidos', 'Orlando'),
  ('França', 'Paris'),
  ('Argentina', 'Buenos Aires'),
  ('Nova Zelândia', 'Auckland');

INSERT INTO turista (id, nome, cpf, celular, endereco)
  VALUES ('1', 'José', '123456789-00', '(12)99781-1111', 'Rua 1, Jd. Aquárius-SJC'),
  ('2', 'João', '456789123-99', '(12)98142-2222', 'Rua 2, Jd. Das Indústris-SJC'),
  ('3', 'Maria', '789123456-66', '(12)99185-3333', 'Rua 3, Santa Maria-Jacareí'),
  ('4', 'Ana', '159486726-33', '(12)99999-4444', 'Rua 4, Rio Cumprido-Jacareí');

INSERT INTO viagem (turista_id, pais_id, data)
  VALUES ('1', '1', '2023-09-07'),
  ('2', '2', '2022-12-25'),
  ('3', '3', '2023-06-12'),
  ('4', '1', '2023-10-12'),
  ('1', '2', '2023-01-01'),
  ('2', '3', '2023-07-15'),
  ('3', '4', '2023-10-31'),
  ('4', '3', '2023-11-26');

-- 4
SELECT
  t.id AS "IDTurista",
  t.nome AS "Nome",
  t.cpf AS "CPF",
  t.celular AS "Celular",
  t.endereco AS "Endereco",
  p.id AS "IDPais",
  p.nome AS "Nome",
  p.cidade AS "Cidade",
  v.data AS "DataViagem"
FROM
  turista t,
  pais p,
  viagem v
WHERE
  t.id = turista_id
  AND p.id = pais_id;

-- 5
SELECT
  t.nome AS "Nome"
FROM
  turista t,
  pais p,
  viagem v
WHERE
  t.id = turista_id
  AND p.id = pais_id
  AND p.nome ILIKE 'argentina';