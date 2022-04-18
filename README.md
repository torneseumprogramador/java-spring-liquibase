# O que é o liquibase
- Aplicação para gerenciar evolução de um banco de dados (Migrations)
- https://liquibase.com/

# Documentação
- https://docs.liquibase.com/

# Download driver connector mysql
- https://www.mysql.com/products/connector/
- mysql-connector-java-8.0.28.jar

# Install liquibase
https://docs.liquibase.com/install/liquibase-macos.html

# Sintaxe XML
```xml
<?xml version="1.0" encoding="UTF-8"?>
<databaseChangeLog xmlns="http://www.liquibase.org/xml/ns/dbchangelog" xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" xmlns:pro="http://www.liquibase.org/xml/ns/pro" xsi:schemaLocation="http://www.liquibase.org/xml/ns/dbchangelog
  http://www.liquibase.org/xml/ns/dbchangelog/dbchangelog-3.8.xsd
  http://www.liquibase.org/xml/ns/pro http://www.liquibase.org/xml/ns/pro/liquibase-pro-3.8.xsd">
  <changeSet id="20220316152800" author="Danilo Aparecido">
    <createTable tableName="clientes">
      <column name="id" type="bigint">
        <constraints primaryKey="true" primaryKeyName="clientes_id_pk" />
      </column>
      <column name="nome" type="varchar(150)">
        <constraints nullable="false" notNullConstraintName="cliente_nome_nn" />
      </column>
      <column name="telefone" type="varchar(20)">
        <constraints nullable="false" notNullConstraintName="cliente_telefone_nn" />
      </column>
      <column name="cpf" type="varchar(30)">
        <constraints unique="true" uniqueConstraintName="clientes_cpf_unq" />
      </column>
      <column name="email" type="varchar(250)">
        <constraints unique="true" uniqueConstraintName="clientes_email_unq" />
      </column>
      <column name="ativo" type="boolean" defaultValueBoolean="true"></column>
    </createTable>
  </changeSet>
</databaseChangeLog>
```

# Sintaxe Json
```json
{
  "databaseChangeLog": [
    {
      "changeSet": {
        "id": "1",
        "author": "Danilo",
        "changes": [
          {
            "createTable": {
              "tableName": "person",
              "columns": [
                {
                  "column": {
                    "name": "id",
                    "type": "int",
                    "autoIncrement": true,
                    "constraints": {
                      "primaryKey": true,
                      "nullable": false
                    }
                  }
                },
                {
                  "column": {
                    "name": "firstname",
                    "type": "varchar(50)"
                  }
                },
                {
                  "column": {
                    "name": "lastname",
                    "type": "varchar(50)",
                    "constraints": {
                      "nullable": false
                    }
                  }
                },
                {
                  "column": {
                    "name": "state",
                    "type": "char(2)"
                  }
                }
              ]
            }
          }
        ]
      }
    }
  ]
}
```

# Sintaxe Yaml
```yaml
databaseChangeLog:
  - changeSet:
     id: create-singers-table
     labels: example
     author: Danilo
     changes:
       - createTable:
          remarks:   Singer information
          tableName: Singers
          columns:
            -  column:
                name:    id
                type:    BIGINT
                constraints:
                  primaryKey: true
            -  column:
                name:    FirstName
                type:    VARCHAR(255)
            -  column:
                name:    LastName
                type:    VARCHAR(255)
                constraints:
                  nullable: false
            -  column:
                name:    SingerInfo
                type:    boolean
            -  column:
                name:    LastUpdateTime
                type:    TIMESTAMP
```

```yml
changeLogFile: db.changelog-master_include_rollback.xml
url: jdbc:mysql://localhost:3306/SpringLiquiBase?createDatabaseIfNotExist=true&useTimezone=true&serverTimezone=UTC
username: root
password: root
classpath: mysql-connector-java-8.0.28.jar
driver: com.mysql.cj.jdbc.Driver
logLevel: DEBUG
contexts: test # se produção ou teste
liquibase.hub.mode: off # modo online - https://docs.liquibase.com/tools-integrations/liquibase-hub/properties.html
# liquibaseProLicenseKey: <paste license key> # para acesso ao pago com mais funções
```

## Rodar update
```bash
cd test_exemplo_liquibase_comandline
vim liquibase.properties # configurar o arquivo
liquibase update
liquibase update --changelog-file=db.changelog-master.yml # roda arquivo isolado
liquibase --defaultsFile=liquibase.sql_server.properties update # aponta para o arquivo de config customizado
```

## Rodar rollback
```bash     
liquibase rollback v1  # faz rollback por tag
liquibase rollbackOneUpdate --deploymentId=7529231118 --force  # o ID 7529231118 é o valor referente ao campo deployment_id da tabela DATABASECHANGELOG
```

## Rodar export changlog de uma base existente
```bash
liquibase --changeLogFile=dbchangelog.json generateChangeLog
```

## Adicionando tag na última migração executada, caso queria mudar a versão da tag atrelada
```bash
liquibase tag v1 # Gera tag do ultimo changelog rodado
```

## Start app e aplicar o script liquibase em JavaSpring Boot e Gradle
```bash
gradle bootRun
```

# Modificar tabelas
- alterar o arquivo que está em src/resources/db/changelog

# Verificar mudanças 
- acessar o cliente do mysql
```bash
mysql -uroot -p'root'
show databases;
show tables;
desc clientes;
desc pedidos;
select * from clientes;
select * from pedidos;
```