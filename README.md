# Arandu Microverdes - E-commerce com Assinaturas

## 📖 Sobre o Projeto
O **Arandu Microverdes** é uma plataforma de e-commerce especializada na venda recorrente e avulsa de microverdes. O sistema foi projetado utilizando padrões de projeto consolidados (como Singleton, Factory, DAO, MVC e Observer) para garantir escalabilidade, gerenciamento automatizado de estoque, processamento de pagamentos estável e acompanhamento preciso do ciclo de vida de pedidos e assinaturas.

---

## 🏗️ Arquitetura e Engenharia do Sistema

Abaixo estão descritos sucintamente os diagramas que compõem a especificação técnica do sistema:

### 1. Modelo de Domínio e Arquitetura de Software
* **Código do Diagrama de Classes (`UML`):** Define a estrutura de entidades centrais como `Usuario`, `Cliente`, `Produto`, `Pedido` e `Assinatura`. O sistema adota padrões como **Singleton** (`EstoqueManager`, `APIPagamento`), **Factory** (`PagamentoFactory`) e **Observer** para desacoplar a lógica de negócio das notificações e baixas em estoque.

### 2. Fluxos de Interação (Diagramas de Sequência)
* **Diagrama_de_Sequencia_01.jpeg (Cliente Realiza uma Assinatura):** Demonstra o ciclo de contratação de um plano recorrente. A `AssinaturaController` aciona a `AssinaturaFactory` para instanciar o contrato, salva o registro via `AssinaturaDAO` e inscreve o cliente como observador do estoque para futuras entregas programadas.
* **Diagrama_de_Sequencia_02.jpeg (Cliente Pede um Produto):** Ilustra a jornada de compra avulsa. O fluxo valida o produto selecionado, orquestra a criação da entidade através da `ProdutoFactory` e persiste o novo pedido de forma segura no banco de dados usando `PedidoDAO` de forma transacional.
* **Diagrama_de_Sequencia_03.png & seq3_cadastro_bw.png (Admin Cadastra Novo Produto):** Apresenta o fluxo administrativo de abastecimento de catálogo. O administrador preenche os dados na interface, que passam pelo `ProdutoController` e utilizam a `ProdutoFactory` para validar e salvar o novo item via `ProdutoDAO`.

### 3. Infraestrutura (Diagrama de Implantação)
* **Diagrama_de_implantação.jpeg:** Mapeia a topologia física da aplicação. O ecossistema é dividido entre os clientes frontend (**App React** para smartphones e **Dashboard Admin** via Web), protegidos por um servidor de firewall, que se comunicam via HTTPS com uma API REST em **Node.js** com banco de dados **PostgreSQL**.

### 4. Ciclos de Vida (Diagramas de Estado)
* **Diagrama_de_Estado_Pedido.png:** Rastreia as transições físicas e financeiras de uma compra avulsa, partindo do `Carrinho` e `Checkout` para estados como `Aguardando Pagamento`, `Pago`, `Em preparo` (onde ocorre a baixa automática de estoque), `Em trânsito` e `Entregue`, cobrindo também cenários de `Devolução` e `Reembolso`.
* **Diagrama_Estado_Assinatura.png:** Gerencia o ciclo recorrente do cliente. Passa pelas fases de `Revisão do Pedido` e `Assinatura Ativa`. Contempla renovações automáticas, fluxos de falha financeira (`Assinatura Interrompida`) e políticas de encerramento programado ou imediato (`Cancelada`).

---

## 🛠️ Tecnologias Identificadas
* **Frontend:** React (Single Page Application - SPA) / Web Dashboard
* **Backend:** Node.js (API REST com arquitetura MVC)
* **Banco de Dados:** PostgreSQL (SGBD Relacional)
* **Protocolos & Segurança:** HTTPS, TCP/IP e Servidor Dedicado de Firewall

---

* 💻 **Contribuidores**
* Fellipe: Diagramas de Estado e Github
* Eduardo: Diagramas de Sequência e diagrama de Implantação
* Arthur: Diagrama de Classe com padrões de projeto(Singleton, DAO,Factory,Observer e MVC) e Prototipação com interfaces
