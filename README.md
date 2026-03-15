# Arquitetura de Software — Resumo



# O que é Arquitetura de Software

Arquitetura de software é a **estrutura fundamental de um sistema**, definindo:

- Organização dos componentes
- Comunicação entre partes do sistema
- Regras e diretrizes de evolução do software

Um dos principais desafios é **dividir o sistema em módulos pequenos e bem definidos**, com responsabilidades claras.

---

# Arquitetura em Camadas

Uma arquitetura comum organiza o sistema em camadas:


Apresentação → Negócios → Persistência → Banco de Dados


### Benefícios

- Separação de responsabilidades
- Melhor manutenção
- Maior testabilidade
- Escalabilidade

### Anti-pattern

Quando a camada de apresentação acessa diretamente o banco de dados ocorre o **Architecture Sinkhole**, causando:

- Alto acoplamento
- Dificuldade de testes
- Código difícil de manter

---

# Evolução das Arquiteturas de Software

## Mainframe

- Sistema centralizado
- Tudo rodava em um único computador
- Baixa flexibilidade

---

## Cliente-Servidor

Separação entre cliente e servidor.


Cliente → Requisição
Servidor → Resposta


Mais flexibilidade e escalabilidade.

---

## Arquitetura 2-Tier


[Cliente (UI + Regras)] ↔ [Banco de Dados]


### Problema
Atualizações exigiam reinstalar o sistema em todos os computadores.

---

## Arquitetura 3-Tier


Cliente (UI)
↓
Servidor de Aplicação
↓
Banco de Dados


### Benefícios

- Regras de negócio centralizadas
- Atualizações mais simples
- Manutenção mais barata

---

## Arquitetura 4-Tier


Browser
↓
Servidor Web
↓
Servidor de Aplicação
↓
Banco de Dados


### Benefícios

- Interface via navegador
- Atualizações centralizadas
- Nenhuma instalação no cliente
- Maior desacoplamento

---

# Estilos vs Padrões Arquiteturais

## Estilos Arquiteturais

Definem a **estrutura geral do sistema**.

Exemplos:

- Monolítico
- Cliente-Servidor
- Arquitetura em Camadas
- Microsserviços
- Event-Driven
- Peer-to-Peer
- Pipe and Filter

---

## Padrões Arquiteturais

São **soluções reutilizáveis para organizar o código**.

Exemplos:

- MVC
- MVVM
- Clean Architecture
- Hexagonal
- Onion Architecture
- Microkernel
- N-Tier

---

# MVC (Model-View-Controller)

Separação entre:

- **Model** → Dados e acesso ao banco
- **View** → Interface com o usuário
- **Controller** → Processa requisições

Fluxo:


Usuário → Controller → Model → Banco
Controller → View → Usuário


### Limitações

- Regras de negócio misturadas nos controllers
- Baixa reutilização
- Testes difíceis
- Escalabilidade limitada

---

# Princípios Fundamentais

## Alta Coesão

Cada componente possui **uma responsabilidade clara**.

Benefícios:

- Código mais simples
- Fácil manutenção
- Melhor testabilidade

---

## Baixo Acoplamento

Componentes devem depender o mínimo possível uns dos outros.

Benefícios:

- Mudanças isoladas
- Código mais flexível
- Facilita evolução do sistema

---

# Princípios SOLID

Conjunto de boas práticas para design de software.

Principais ideias:

- Responsabilidade única
- Programar contra abstrações
- Inversão de dependência
- Código modular e testável

---

# Arquitetura em 4 Camadas Lógicas

Estrutura moderna:


Apresentação
↓
Aplicação
↓
Domínio
↓
Infraestrutura


### Responsabilidades

**Apresentação**
Interface com o usuário.

**Aplicação**
Coordena os casos de uso.

**Domínio**
Regras de negócio puras.

**Infraestrutura**
Banco de dados, APIs externas, serviços.

---

# Inversão de Dependência

O núcleo do sistema **não deve depender de detalhes externos**.

Dependências passam a apontar para dentro:


Apresentação → Aplicação → Domínio ← Infraestrutura


Benefícios:

- Testes mais fáceis
- Troca de tecnologias sem impactar o núcleo
- Código mais flexível

---

# Deploy e Infraestrutura

Para colocar um sistema em produção são usados:

### Docker
Containers para padronizar ambientes.

### VPS
Servidor virtual na nuvem.

### Nginx
Servidor web e proxy reverso.

Fluxo típico:


Browser → Nginx → Backend → Banco de Dados


---

# Arquitetura de Produção

Componentes comuns em sistemas reais:

- Load Balancer
- API Gateway
- Backend Services
- Cache (Redis)
- Filas de Mensagem
- Workers / Processamento em background
- Banco de dados
- Object Storage
- Serviços externos

---

# Arquitetura Hexagonal (Ports and Adapters)

Objetivo: **proteger o núcleo da aplicação**.

Estrutura:


Adaptadores → Portas → Núcleo (Domínio + Casos de Uso)


### Benefícios

- Independência de frameworks
- Alta testabilidade
- Facilidade de trocar tecnologias

---

# Clean Architecture

Organiza o sistema em camadas concêntricas:


Frameworks / Infraestrutura
Interfaces / Adaptadores
Casos de Uso
Entidades


### Regra principal

As dependências **sempre apontam para o centro**.

Benefícios:

- Domínio protegido
- Testes independentes
- Longa vida útil do sistema

---

# Microserviços

Divide o sistema em **serviços independentes**.

Características:

- Cada serviço possui seu próprio banco
- Deploy independente
- Escalabilidade individual

### Vantagens

- Escalabilidade
- Resiliência
- Times independentes

### Desafios

- Complexidade de infraestrutura
- Observabilidade
- Testes distribuídos

---

# Comunicação entre Serviços

## REST APIs

Comunicação síncrona via HTTP.

Vantagens:

- Simples
- Amplamente suportado

Desvantagens:

- Dependência direta entre serviços

---

## GraphQL

Permite ao cliente solicitar **apenas os dados necessários**.

Benefícios:

- Redução de overfetching
- Mais flexibilidade no frontend

---

## Comunicação Assíncrona

Uso de **Message Brokers** como:

- RabbitMQ
- Kafka

Fluxo:


Serviço → Broker → Consumidor


Benefícios:

- Desacoplamento
- Escalabilidade
- Resiliência

---

# Event-Driven / Publish-Subscribe

Serviços publicam eventos e outros serviços reagem.

Exemplo:


Evento: UsuarioCadastrado

→ Serviço de Email
→ Serviço de CRM
→ Serviço de Log


Benefícios:

- Alta modularidade
- Extensibilidade
- Baixo acoplamento

---

# SOA (Service Oriented Architecture)

Arquitetura baseada em **serviços corporativos reutilizáveis**.

Exemplos de serviços:

- Pagamento
- Autenticação
- Recomendações

Vantagens:

- Integração com sistemas legados
- Reutilização

Desvantagens:

- Governança complexa
- Possível gargalo no ESB

---

# CQRS

Separação entre **leitura e escrita**:


Commands → Escrita
Queries → Leitura


Benefícios:

- Melhor desempenho
- Escalabilidade
- Modelos otimizados para cada operação

---

# Conclusão

Uma boa arquitetura de software:

- Separa responsabilidades
- Protege o domínio do sistema
- Facilita testes e manutenção
- Permite evolução tecnológica
- Escala conforme o crescimento do sistema

Arquitetura não é apenas código — envolve **design, infraestrutura, comunicação e deploy**.
