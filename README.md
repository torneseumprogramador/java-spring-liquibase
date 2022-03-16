# alicação feita para testar os conceitos de liquibase
# doc
https://docs.liquibase.com/

## start app e aplicar o script
```bash
gradle bootRun
```

# modificar tabelas
## alterar o arquivo que está em src/resources/db/changelog

# verificar mudanças 
## acessar o cliente do mysql
```bash
mysql -uroot -p'root'
show databases;
show tables;
desc clientes;
desc pedidos;
select * from clientes;
select * from pedidos;
```