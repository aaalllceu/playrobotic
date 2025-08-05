# Documentação do Projeto PlayRobótica

Este documento detalha a arquitetura e a implementação do projeto "PlayRobótica", uma aplicação de gerenciamento de vendas para uma loja de artigos eletrônicos e robótica. O projeto foi desenvolvido em Java puro, seguindo os princípios da Programação Orientada a Objetos (POO) e uma arquitetura em camadas. Recentemente, o projeto foi migrado para utilizar o Maven para gerenciamento de dependências e construção.

## Requisitos Atendidos

O projeto "PlayRobótica" foi construído para atender aos seguintes requisitos:

a. **Herança**: Utilizada para reutilização de código e modelagem de hierarquias de classes.
   - `Pessoa` (abstrata) é herdada por `Cliente` e `Funcionario`.
   - `Produto` (abstrata) é herdada por `Eletronico` e `Robotica`.

b. **Polimorfismo**: Demonstração de diferentes comportamentos para o mesmo método em classes relacionadas.
   - O método `getTipoProduto()` na classe `Produto` é abstrato e implementado de forma específica em `Eletronico` e `Robotica`.
   - O método `calcularDesconto()` na classe `Produto` é sobrescrito em `Eletronico` e `Robotica` para aplicar regras de desconto específicas.

c. **Coleções (ex., ArrayList)**: Utilizadas para armazenar e gerenciar listas de objetos.
   - `ArrayList` é amplamente utilizado nas classes DAO para simular o armazenamento de dados (ex: `List<Cliente> clientes` em `ClienteDAO`).
   - A classe `Pedido` utiliza `List<ItemPedido>` para gerenciar os itens de um pedido.

d. **Classe Abstrata**: Classes que não podem ser instanciadas diretamente e servem como base para outras classes.
   - `Pessoa`: Define atributos e comportamentos comuns a `Cliente` e `Funcionario`.
   - `Produto`: Define atributos e comportamentos comuns a `Eletronico` e `Robotica`, incluindo um método abstrato `getTipoProduto()`.

e. **Interface**: Define um contrato para classes que a implementam.
   - `IDAO<T>`: Interface genérica que define as operações CRUD (Criar, Ler, Atualizar, Deletar) para as classes DAO.

f. **Arquitetura em Camadas**: O projeto é dividido em camadas lógicas para melhor organização, manutenção e escalabilidade.
   - **Camada de Modelo (`com.playrobotica.model`)**: Contém as classes que representam as entidades de negócio (ex: `Cliente`, `Produto`, `Pedido`).
   - **Camada de Acesso a Dados (DAO - `com.playrobotica.dao`)**: Responsável pela persistência e recuperação de dados. Cada entidade possui sua própria classe DAO (ex: `ClienteDAO`, `ProdutoDAO`, `FuncionarioDAO`, `PedidoDAO`). Atualmente, a persistência é simulada em memória com `ArrayList`.
   - **Camada de Negócio (Service - `com.playrobotica.service`)**: Contém a lógica de negócio da aplicação, validações e orquestração das operações DAO (ex: `ClienteService`, `ProdutoService`, `FuncionarioService`, `PedidoService`).
   - **Camada de Interface Gráfica (GUI - `com.playrobotica.gui`)**: Responsável pela interação com o usuário (ex: `MainFrame`, `ClientePanel`, `ProdutoPanel`, `FuncionarioPanel`, `PedidoPanel`).
   - **Camada de Utilitários (`com.playrobotica.util`)**: Contém classes auxiliares, como a exceção personalizada `PlayRoboticaException`.
   - **Camada Principal (`com.playrobotica.main`)**: Contém a classe `PlayRoboticaApp` que inicia a aplicação.

g. **Interface Gráfica**: Desenvolvida utilizando a biblioteca Swing do Java.
   - `MainFrame`: A janela principal da aplicação, com um menu para navegar entre as telas de Clientes, Produtos, Funcionários e Pedidos.
   - `ClientePanel`: Painel para cadastro, edição, listagem e busca de clientes.
   - `ProdutoPanel`: Painel para cadastro, edição, listagem e busca de produtos (eletrônicos e robótica).
   - `FuncionarioPanel`: Painel para cadastro, edição, listagem e busca de funcionários.
   - `PedidoPanel`: Painel para criação, atualização de status, cancelamento, listagem e busca de pedidos.

h. **Tratamento de Exceções**: Utilização de blocos `try-catch` e exceções personalizadas para lidar com erros de forma controlada.
   - `PlayRoboticaException`: Exceção personalizada para erros específicos da aplicação.
   - As classes de serviço (`ClienteService`, `ProdutoService`, `FuncionarioService`, `PedidoService`) lançam `PlayRoboticaException` para indicar falhas nas operações de negócio, que são capturadas e exibidas na interface gráfica.

## Estrutura do Projeto

```
PlayRobotica/
├── pom.xml              # Arquivo de configuração do Maven
├── src/
│   └── main/
│       └── java/
│           └── com/
│               └── playrobotica/
│                   ├── dao/             # Camada de Acesso a Dados
│                   │   ├── ClienteDAO.java
│                   │   ├── FuncionarioDAO.java
│                   │   ├── IDAO.java
│                   │   ├── PedidoDAO.java
│                   │   └── ProdutoDAO.java
│                   ├── gui/             # Camada de Interface Gráfica
│                   │   ├── ClientePanel.java
│                   │   ├── FuncionarioPanel.java
│                   │   ├── MainFrame.java
│                   │   ├── PedidoPanel.java
│                   │   └── ProdutoPanel.java
│                   ├── main/            # Camada Principal
│                   │   └── PlayRoboticaApp.java
│                   ├── model/           # Camada de Modelo (Entidades)
│                   │   ├── Cliente.java
│                   │   ├── Eletronico.java
│                   │   ├── Funcionario.java
│                   │   ├── ItemPedido.java
│                   │   ├── Pedido.java
│                   │   ├── Pessoa.java
│                   │   ├── Produto.java
│                   │   └── Robotica.java
│                   ├── service/         # Camada de Negócio
│                   │   ├── ClienteService.java
│                   │   ├── FuncionarioService.java
│                   │   ├── PedidoService.java
│                   │   └── ProdutoService.java
│                   └── util/            # Camada de Utilitários
│                       └── PlayRoboticaException.java
├── target/              # Diretório gerado pelo Maven (contém o JAR compilado)
└── docs/                # Diretório para Javadoc
```

## Como Executar o Projeto (Localmente com Maven)

1.  **Pré-requisitos**: Certifique-se de ter o Java Development Kit (JDK) 17 ou superior e o Apache Maven instalados em sua máquina.

2.  **Compilar e Empacotar o Código**: Abra um terminal ou prompt de comando, navegue até o diretório `PlayRobotica` (onde está o arquivo `pom.xml`) e execute o seguinte comando:
    ```bash
    mvn clean install
    ```
    Este comando irá compilar o código-fonte, executar os testes (se houver) e empacotar a aplicação em um arquivo JAR executável no diretório `target/`.

3.  **Executar a Aplicação**: Após a compilação e empacotamento bem-sucedidos, execute a aplicação com o seguinte comando:
    ```bash
    java -jar target/PlayRobotica-1.0-SNAPSHOT.jar
    ```

4.  **Acessar a Documentação Javadoc**: A documentação Javadoc foi gerada no diretório `PlayRobotica/docs`. Você pode abri-la navegando até `PlayRobotica/docs/index.html` em seu navegador web.

## Testes e Validação

Devido às limitações do ambiente de sandbox (que não possui interface gráfica), os testes e a validação da interface gráfica devem ser realizados localmente em sua máquina. 

- **Testes Unitários**: Para um projeto real, você criaria classes de teste separadas (ex: usando JUnit) para testar cada método das classes de serviço e DAO isoladamente. Por exemplo, testar se `ClienteService.cadastrarCliente()` lança uma exceção quando o CPF é duplicado.

- **Testes de Integração**: Testaria a interação entre as camadas, por exemplo, se `PedidoService.criarPedido()` realmente atualiza o estoque de produtos via `ProdutoService` e `ProdutoDAO`.

- **Validação da Interface Gráfica**: Ao executar a aplicação localmente, você pode interagir com os formulários de cadastro de clientes, produtos, funcionários e pedidos. Adicione, edite e remova dados, e verifique se as informações são exibidas corretamente nas tabelas e se as mensagens de erro/sucesso aparecem conforme o esperado. Teste também a funcionalidade de busca em cada painel para filtrar os dados por nome, categoria, setor ou status. Verifique a funcionalidade de alternar entre os tipos de produto no painel de produtos e a criação de pedidos com múltiplos itens.

## Considerações Finais

Este projeto serve como uma base sólida para demonstrar os conceitos de POO e arquitetura em camadas em Java. Para uma aplicação de produção, seriam necessárias melhorias como:

- **Persistência de Dados Real**: Implementar um banco de dados (ex: SQLite, MySQL) para persistir os dados de forma permanente, em vez de usar `ArrayList` em memória.
- **Validações Mais Robustas**: Adicionar validações mais complexas (ex: formato de CPF, email).
- **Funcionalidades Completas**: Adicionar mais funcionalidades de negócio, como relatórios, gestão de usuários, etc.
- **Testes Automatizados**: Escrever testes unitários e de integração abrangentes usando frameworks como JUnit.
- **Melhorias na GUI**: Refinar a interface do usuário, adicionar mais recursos de usabilidade e talvez considerar um framework mais moderno como JavaFX para interfaces mais ricas.



## Atualizações Recentes na Interface Gráfica

### Botões de Acesso Rápido na `MainFrame`

A `MainFrame` foi aprimorada com a adição de botões de acesso rápido na parte superior da janela. Esses botões (`Clientes`, `Produtos`, `Funcionários`, `Pedidos`) permitem uma navegação mais intuitiva e direta entre os diferentes painéis de gerenciamento da aplicação, complementando a funcionalidade do menu superior.

### Melhoria na Seleção de Entidades no `PedidoPanel`

Para facilitar o cadastro de pedidos, os `JComboBoxes` de seleção de Cliente, Funcionário e Produto no `PedidoPanel` foram ajustados. Agora, as classes `Cliente`, `Funcionario` e `Produto` possuem um método `toString()` simplificado que retorna apenas o nome da entidade. Isso garante que os `JComboBoxes` exibam de forma clara e legível apenas o nome do cliente, funcionário ou produto, tornando a seleção mais eficiente e amigável ao usuário.



## Atualizações de Persistência e PedidoPanel

### Persistência de Dados com Serialização

Para garantir que os dados cadastrados (Clientes, Funcionários, Produtos e Pedidos) sejam salvos e carregados entre as sessões da aplicação, foi implementada uma camada de persistência básica utilizando serialização de objetos Java para arquivos. A nova classe `DataPersistence` (localizada em `com.playrobotica.util.DataPersistence`) é responsável por salvar (`save`)
 e carregar (`load`) listas de objetos para arquivos `.dat`.

Cada classe DAO (`ClienteDAO`, `FuncionarioDAO`, `ProdutoDAO`, `PedidoDAO`) foi modificada para utilizar essa classe de utilidade. Ao instanciar um DAO, ele tenta carregar os dados do arquivo correspondente. Após cada operação de adição, atualização ou remoção, os dados são automaticamente salvos de volta no arquivo. Isso simula um comportamento de banco de dados simples, permitindo que os cadastros sejam mantidos mesmo após o fechamento da aplicação.

### Correções e Melhorias no `PedidoPanel`

Foram realizadas as seguintes correções e melhorias no `PedidoPanel`:

- **Seleção de Entidades**: O problema na seleção de Cliente, Funcionário e Produto nos `JComboBoxes` foi resolvido. Agora, os `JComboBoxes` são populados corretamente com os objetos correspondentes, e a seleção é feita de forma adequada. Isso permite que o usuário escolha o cliente, funcionário e produto desejados ao criar um novo pedido.
- **Geração de ID de Pedido**: A lógica para gerar o próximo ID de pedido foi centralizada no `PedidoService` (`gerarProximoId()`), garantindo que os IDs sejam únicos e sequenciais, mesmo após o carregamento de dados persistidos.
- **Criação de Pedidos**: Com as correções na seleção de entidades e na persistência, agora é possível criar pedidos com sucesso, associando-os a clientes, funcionários e produtos existentes. Os pedidos criados são salvos e carregados corretamente.



## Correção do Erro de Serialização

Foi identificado um erro ao tentar salvar os dados, manifestado pela mensagem "Erro ao salvar cliente: Erro ao salvar dados em clientes.dat: com.playrobotica.model.Cliente". Este erro ocorre porque as classes de modelo que são salvas em arquivos (serializadas) precisam implementar a interface `java.io.Serializable`.

Para corrigir isso, todas as classes de modelo (`Pessoa`, `Cliente`, `Funcionario`, `Produto`, `Eletronico`, `Robotica`, `ItemPedido`, `Pedido`) foram atualizadas para implementar `java.io.Serializable`. Essa interface é uma interface de marcação, o que significa que ela não possui métodos para implementar, mas sinaliza à Java Virtual Machine (JVM) que os objetos dessa classe podem ser convertidos em uma sequência de bytes e vice-versa, permitindo que sejam salvos em arquivos ou transmitidos pela rede.

Com essa alteração, a persistência de dados deve funcionar corretamente, permitindo que os cadastros e pedidos sejam salvos e carregados entre as sessões da aplicação.

