# Sistema de Gerenciamento de Pedidos em Java

Este projeto implementa um sistema simples de gerenciamento de pedidos em Java, demonstrando conceitos de **programação orientada a objetos**, **enumerações**, e **agregação de objetos**. O sistema permite registrar dados de um cliente, criar um pedido com um status específico e adicionar múltiplos itens a esse pedido. Ao final, ele gera um resumo detalhado do pedido, incluindo informações do cliente e o total dos itens.

---

## Estrutura do Projeto

O projeto é organizado em pacotes para melhor modularidade:

* `principal`: Contém a classe principal para a execução do programa (`Main`).
* `entities`: Contém as classes que representam as entidades do negócio (`Client`, `Product`, `OrderItem`, `Order`).
* `enums`: Contém a enumeração `OrderStatus` que define os possíveis estados de um pedido.

---

## Arquivos Incluídos

* `principal/Main.java`: O ponto de entrada da aplicação. Orquestra a entrada de dados do usuário e a criação e exibição do pedido.
* `enums/OrderStatus.java`: Define os status possíveis para um pedido (`PENDING_PAYMENT`, `PROCESSING`, `SHIPPED`, `DELIVERED`).
* `entities/Client.java`: Representa um cliente com nome, e-mail e data de nascimento.
* `entities/Product.java`: Representa um produto com nome e preço.
* `entities/OrderItem.java`: Representa um item dentro de um pedido, com quantidade, preço (no momento da compra) e uma referência ao produto. Inclui o método `subTotal()` para calcular o valor do item.
* `entities/Order.java`: Representa um pedido, contendo o momento da criação, status, informações do cliente e uma lista de `OrderItem`. Inclui métodos para adicionar/remover itens e calcular o valor total do pedido (`total()`).

---

## Como Usar

Para compilar e executar este projeto, siga os passos abaixo:

1.  **Organize os arquivos:**
    * Crie uma pasta raiz para o projeto (ex: `OrderManagement`).
    * Dentro dela, crie a pasta `principal` e coloque `Main.java`.
    * Crie a pasta `entities` e coloque `Client.java`, `Product.java`, `OrderItem.java`, e `Order.java`.
    * Crie a pasta `enums` (irmã de `entities`) e coloque `OrderStatus.java`.
    (A estrutura de pastas deve ser similar a: `OrderManagement/principal/Main.java`, `OrderManagement/entities/Client.java`, `OrderManagement/enums/OrderStatus.java`, etc.)

2.  **Compile o código:** Abra um terminal ou prompt de comando, navegue até a pasta raiz do seu projeto (`OrderManagement`) e execute o seguinte comando:

    ```bash
    javac principal/*.java entities/*.java enums/*.java
    ```

3.  **Execute o programa:** Após a compilação, execute a classe principal:

    ```bash
    java principal.Main
    ```

4.  **Interação com o Programa:**
    O programa solicitará dados em inglês (devido ao `Locale.setDefault(Locale.US)`):
    * **"Enter client data:"**
        * **"Name:"** Digite o nome do cliente.
        * **"Email:"** Digite o e-mail do cliente.
        * **"Birth date (DD/MM/YYYY):"** Digite a data de nascimento no formato `DD/MM/YYYY` (ex: `15/03/1990`).
    * **"Enter order data:"**
        * **"Status:"** Digite um dos status do pedido (sem espaços, em maiúsculas): `PENDING_PAYMENT`, `PROCESSING`, `SHIPPED`, ou `DELIVERED`.
    * **"How many items to this order?"** Digite a quantidade de itens que o pedido terá.
    * Para cada item, o programa pedirá:
        * **"Enter # X item data:"** (X é o número do item)
        * **"Product name:"** Digite o nome do produto.
        * **"Product price:"** Digite o preço do produto (use ponto `.` como separador decimal).
        * **"Quantity:"** Digite a quantidade do produto.

---

## Explicação Detalhada do Código

### `enums/OrderStatus.java`

Esta é uma **enumeração** simples que define um conjunto fixo de constantes para representar os estados possíveis de um pedido. Isso garante que o status do pedido seja sempre um dos valores válidos predefinidos, evitando erros e inconsistências de dados.

* **Constantes:** `PENDING_PAYMENT`, `PROCESSING`, `SHIPPED`, `DELIVERED`.

### `entities/Product.java`

Representa um **Produto** genérico.

* **Atributos:**
    * `name` (String): Nome do produto.
    * `price` (double): Preço unitário do produto.
* **Construtores:** Um construtor vazio e um construtor com `name` e `price`.
* **Getters e Setters:** Métodos para acessar e modificar os atributos.

### `entities/OrderItem.java`

Representa um **Item de Pedido**, ou seja, um produto específico dentro de um pedido. Ele **agrega** um `Product` e armazena o preço **no momento da venda** (pois o preço do produto pode mudar no futuro).

* **Atributos:**
    * `quantity` (Integer): Quantidade do produto neste item do pedido.
    * `price` (Double): Preço unitário do produto no momento em que foi adicionado ao pedido.
    * `product` (Product): Uma referência ao objeto `Product` correspondente.
* **Construtores:** Um construtor vazio e um construtor com `quantity`, `price` e `product`.
* **Getters e Setters:** Métodos para acessar e modificar os atributos.
* **`subTotal()`:** Método que calcula o valor total para este item (`price * quantity`).
* **`toString()`:** Sobrescreve o método para retornar uma representação textual formatada do item do pedido.

### `entities/Client.java`

Representa um **Cliente** no sistema.

* **Atributos:**
    * `name` (String): Nome completo do cliente.
    * `email` (String): Endereço de e-mail do cliente.
    * `birthDate` (Date): Data de nascimento do cliente.
* **Construtores:** Um construtor vazio e um construtor com `name`, `email` e `birthDate`.
* **Getters e Setters:** Métodos para acessar e modificar os atributos.
* **`toString()`:** Sobrescreve o método para retornar uma representação formatada do cliente, incluindo nome, data de nascimento e e-mail.

### `entities/Order.java`

Representa um **Pedido** principal, que **agrega** um cliente e uma lista de itens.

* **Atributos:**
    * `moment` (Date): O momento (data e hora) em que o pedido foi feito.
    * `status` (OrderStatus): O status atual do pedido, usando o enum `OrderStatus`.
    * `client` (Client): Uma referência ao objeto `Client` que fez o pedido.
    * `items` (List<OrderItem>): Uma lista dinâmica de objetos `OrderItem` que compõem o pedido.
* **Construtores:** Um construtor vazio e um construtor com `moment`, `status` e `client`.
* **Getters e Setters:** Métodos para acessar e modificar os atributos.
* **`addItem(OrderItem item)`:** Adiciona um `OrderItem` à lista de itens do pedido.
* **`removeItem(OrderItem item)`:** Remove um `OrderItem` da lista de itens do pedido.
* **`total()`:** Calcula e retorna o valor total do pedido, somando o `subTotal()` de cada `OrderItem` na lista.
* **`toString()`:** Sobrescreve o método para construir uma representação completa e formatada do pedido, incluindo o momento, status, dados do cliente, lista de itens e o preço total. Usa `StringBuilder` para construção eficiente da string.

### `principal/Main.java`

A classe principal que executa a lógica do programa.

* **`main(String[] args)`:**
    * Configura `SimpleDateFormat` para parsing de datas e `Locale.setDefault(Locale.US)` para garantir o formato de números decimais.
    * Solicita e lê os dados do cliente (nome, e-mail, data de nascimento), criando um objeto `Client`.
    * Solicita e lê o status do pedido, convertendo a string lida para um valor `OrderStatus` usando `OrderStatus.valueOf()`.
    * Cria um objeto `Order` com o momento atual, o status e o cliente recém-criado.
    * Solicita a quantidade de itens que serão adicionados ao pedido.
    * Em um loop, para cada item, solicita os dados necessários (nome do produto, preço do produto, quantidade):
        * Cria um objeto `Product` com nome e preço.
        * Cria um objeto `OrderItem` com a quantidade, o preço do produto (no momento da compra) e o objeto `Product`.
        * Adiciona o `OrderItem` ao `Order` usando `order.addItem()`.
    * Finalmente, imprime o resumo completo do pedido chamando `System.out.println(order.toString())`.

---

**Dica:** Ao executar, certifique-se de que os valores de **Status** inseridos (`PENDING_PAYMENT`, `PROCESSING`, `SHIPPED`, `DELIVERED`) estejam em maiúsculas e sem erros de digitação para que o `OrderStatus.valueOf()` funcione corretamente.

---

Espero que este README ajude a organizar seu repositório no GitHub! Se tiver mais alguma dúvida ou precisar de outro README, é só pedir.
