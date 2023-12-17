create table produto (
id int auto_increment not null,
 nome varchar(128) not null,
 preco double not null,
 validade date not null,
 unique(nome),
 constraint pk_produto primary key (id));

create table identificacao (
id int not null,
 nome varchar(128) not null,
 descricao varchar(256) not null,
 constraint pk_identificacao primary key (id),
 constraint fk_identificacao foreign key (id) references produto (id));

Adiciona valores na tabela produto: 

insert into produto (nome, preco, validade) values ('arroz', 16.57, '2023-12-17');
insert into produto (nome, preco, validade) values ('detergente', 3.97, '2037-08-23');
insert into produto (nome, preco, validade) values ('calça', 184.91, '2045-01-27');
insert into produto (nome, preco, validade) values ('desinfetante', 8.60, '2036-02-14');
insert into produto (nome, preco, validade) values ('camisa', 48.99, '2043-04-03');
insert into produto (nome, preco, validade) values ('feijão', 12.31, '2023-09-11');
insert into produto (nome, preco, validade) values ('vestido', 89.99, '2041-05-16');
insert into produto (nome, preco, validade) values ('leite', 4.28, '2023-10-03');
insert into produto (nome, preco, validade) values ('sabão', 1.85, '2035-03-05');

Adiciona valores na tabela identificacao: 

insert into identificacao (id, nome, descricao) values (1, 'parboilizado', 'pré-cozido');
insert into identificacao (id, nome, descricao) values (2, 'neutro', 'sem corante e aditivos');
insert into identificacao (id, nome, descricao) values (3, 'jeans', 'reta');
insert into identificacao (id, nome, descricao) values (4, 'cloro', 'bactericida');
insert into identificacao (id, nome, descricao) values (5, 'algodão', 'sem estampa');
insert into identificacao (id, nome, descricao) values (6, 'carioca', 'orgânico');
insert into identificacao (id, nome, descricao) values (7, 'algodão', 'estampado');
insert into identificacao (id, nome, descricao) values (8, 'integral', 'com vitaminas');
insert into identificacao (id, nome, descricao) values (9, 'barra', 'banho');

Aqui ele retorna as colunas de ambas as tabelas onde tem o valor do campo id, assim combinando dados

select *
from produto as p, identificacao as i
where p.id = i.id;

Altere o exemplo dessa prática:

a) Apresentando o identificador, nome, descrição e preço dos produtos em ordem
descrescente de preço.

SELECT p.id, p.nome, i.descricao, p.preco
FROM produto AS p
JOIN identificacao AS i ON p.id = i.id
ORDER BY p.preco DESC;

b) Apresentando o identificador, nome, descrição e preço dos produtos em ordem
crescente de nome e descrescente de preço.

SELECT p.id, p.nome, i.descricao, p.preco
FROM produto AS p
JOIN identificacao AS i ON p.id = i.id
ORDER BY p.nome ASC, p.preco DESC;

c) Inserindo novos registros que permitam agrupamento por nome de
indentificação.

ISELECT i.nome AS nome_identificacao, p.nome AS nome_produto, p.preco
FROM identificacao AS i
JOIN produto AS p ON i.id = p.id
ORDER BY i.nome, p.nome;


d) Inserindo novos registros que permitam agrupamento por nome de
indentificação e a soma de preços por cada um desses agrupamentos.


SELECT i.nome AS nome_identificacao, SUM(p.preco) AS total_preco
FROM identificacao AS i
JOIN produto AS p ON i.id = p.id
GROUP BY i.nome;

e) Inserindo novos registros que permitam agrupamento por nome de
indentificação e a média de preços por cada um desses agrupamentos.

SELECT i.nome AS nome_identificacao, AVG(p.preco) AS media_preco
FROM identificacao AS i
JOIN produto AS p ON i.id = p.id
GROUP BY i.nome;

f) Inserindo novos registros que permitam agrupamento por nome de
indentificação e apresente a soma de preços por cada um desses agrupamentos com
valor acima de R$ 100,00.

SELECT i.nome AS nome_identificacao, SUM(p.preco) AS total_preco
FROM identificacao AS i
JOIN produto AS p ON i.id = p.id
GROUP BY i.nome
HAVING SUM(p.preco) > 100.00;





