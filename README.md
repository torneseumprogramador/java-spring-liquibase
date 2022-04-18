# O que é o liquibase
- Aplicação para gerenciar evolução de um banco de dados (Migrations)
- https://liquibase.com/

# Documentação
https://docs.liquibase.com/


# download drivers mysql
- https://www.mysql.com/products/connector/
- mysql-connector-java-8.0.28.jar

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

# install liquibase manual
https://docs.liquibase.com/install/liquibase-macos.html

## rodar update
```bash
vim test_exemplo_liquibase_comandline/liquibase.properties # configurar o arquivo
liquibase update
liquibase update --changelog-file=db.changelog-master.yml # roda arquivo isolado
liquibase --defaultsFile=liquibase.sql_server.properties update # aponta para o arquivo de config customizado
```

## rodar rollback
```bash     
liquibase rollback v1  # faz rollback por tag
liquibase rollbackOneUpdate --deploymentId=7529231118 --force  # o ID 7529231118 é o valor referente ao campo deployment_id da tabela DATABASECHANGELOG
```

## rodar export changlog de uma base existente
```bash
liquibase --changeLogFile=dbchangelog.json generateChangeLog
```

## Adicionando tag na ultima migração executada, caso queria mudar a versão da tag atrelada
```bash
liquibase tag v1 # Gera tag do ultimo changelog rodado
```

## Start app e aplicar o script liquibase em JavaSpring Boot e Gradle
```bash
gradle bootRun
```