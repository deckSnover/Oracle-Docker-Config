### Documentação: Configuração Oracle em Docker

#### Objetivo
O objetivo deste documento é guiar na configuração de um ambiente de desenvolvimento local do Oracle Database utilizando Docker. Este ambiente é útil para desenvolvimento, testes e aprendizado de Oracle Database sem a necessidade de configuração manual complexa.

#### Pré-requisitos
Antes de começar, certifique-se de ter os seguintes pré-requisitos instalados e configurados em seu sistema:

- Docker: Verifique se o Docker está instalado e funcionando corretamente na sua máquina. Consulte a documentação oficial do Docker para instalação específica para o seu sistema operacional.

#### Passo a Passo

**1. Download da Imagem do Oracle Database:**

Para começar, baixe a imagem do Oracle Database Enterprise Edition 19c do Docker Hub. Esta imagem será usada para configurar o Oracle Database dentro de um contêiner Docker.

```bash
docker pull store/oracle/database-enterprise:19.3.0.0
```

**2. Execução do Contêiner Oracle:**

Agora, vamos executar o contêiner Oracle Database com configurações básicas, como SID (System Identifier), PDB (Pluggable Database) e senha para o usuário SYS e SYSTEM.

```bash
docker run -d --name oracle-db \
  -p 1521:1521 -p 5500:5500 \
  -e ORACLE_SID=ORCLCDB \
  -e ORACLE_PDB=ORCLPDB1 \
  -e ORACLE_PWD=password \
  store/oracle/database-enterprise:19.3.0.0
```

- `-d`: Executa o contêiner em segundo plano.
- `--name oracle-db`: Nome do contêiner como `oracle-db`.
- `-p 1521:1521 -p 5500:5500`: Mapeamento das portas do contêiner para o host para acesso ao Oracle Database (1521 para listener e 5500 para Enterprise Manager Express).
- `-e ORACLE_SID=ORCLCDB`: SID do Oracle Database.
- `-e ORACLE_PDB=ORCLPDB1`: PDB do Oracle Database.
- `-e ORACLE_PWD=password`: Senha para os usuários SYS e SYSTEM.

**3. Verificação e Acesso ao Oracle:**

Após a execução bem-sucedida do contêiner, verifique se ele está em execução:

```bash
docker ps
```

Para conectar-se ao Oracle Database dentro do contêiner, você pode usar ferramentas como SQL*Plus. Por exemplo:

```bash
# Conectar-se como usuário SYS (DBA)
sqlplus sys/password@//localhost:1521/ORCLCDB as sysdba

# Conectar-se como usuário SYSTEM
sqlplus system/password@//localhost:1521/ORCLCDB
```

**4. Parada e Remoção do Contêiner:**

Quando você terminar de usar o Oracle Database no Docker, você pode parar e remover o contêiner:

```bash
docker stop oracle-db
docker rm oracle-db
```

#### Considerações Finais

- **Ambiente de Desenvolvimento:** Este ambiente Docker é adequado para desenvolvimento e testes locais. Para ambientes de produção, consulte as diretrizes da Oracle para implantação adequada do Oracle Database.

- **Personalização:** Você pode ajustar as configurações, como portas mapeadas, variáveis de ambiente (como senha e nomes de SID/PDB), conforme necessário para o seu ambiente específico.

- **Documentação Adicional:** Para mais informações sobre configurações avançadas, consulte a documentação oficial do Oracle Database e do Docker.
