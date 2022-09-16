# JDBC
Repositório com exemplos de utilização da API de conectividade com banco de dados JDBC

## Drivers de Conexões

| Banco de Dados | Maven |
|----------------|-------|
| SQLite         |  https://mvnrepository.com/artifact/org.xerial/sqlite-jdbc     |
| MySql          |   https://mvnrepository.com/artifact/mysql/mysql-connector-java     |
| Postgree       |  https://mvnrepository.com/artifact/org.postgresql/postgresql    |

## Strings de Conexões

| Banco de Dados | Maven |
|----------------|-------|
| SQLite         |  ```jdbc:sqlite:nome_do_banco.db``` |
| MySql          |  ```jdbc:mysql://<database_host>:<port>/<database_name> ``` |
| Postgree       |  ```jdbc:postgresql://<database_host>:<port>/<database_name> ``` |


## Fábrica de conexões

```mermaid
classDiagram
class ConnectionFactory{
    -ConnectionFactory instancia$
    -ConnectionFactory()
    +obterInstancia()$ ConnectionFactory
    +obterConexao() Connection
}

```

```java
class ConnectionFactory {

    private  static ConnectionFactory instancia;

    private ConnectionFactory(){

    }

    public static ConnectionFactory obterInstancia(){
        if(instancia == null){
            instancia = new ConnectionFactory();
        }
        return instancia;
    }

    public Connection obterConexao(){
        try{
            Connection conn = DriverManager.getConnection("jdbc:sqlite:meu_banco_de_dados.db");
            return conn;
        }catch (Exception e){
            e.printStackTrace();
        }
        throw new RuntimeException("Não foi possível conectar ao banco de dados.");
    }


}
```

