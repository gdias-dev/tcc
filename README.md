# DevClub Café — Sistema de Pedidos Online

Sistema de pedidos para cafeteria, com catálogo de produtos, carrinho de compras, controle de estoque e painel administrativo. Desenvolvido como trabalho de conclusão de curso.

## O que faz

**Para o cliente**
- Catálogo de produtos com preço, imagem e disponibilidade em estoque
- Cadastro e login
- Carrinho de compras
- Fechamento de pedido

**Para o administrador**
- Cadastro, edição e exclusão de produtos
- Atualização de estoque por produto
- Consulta de usuários e pedidos

## Endpoints

| Método | Rota | O que faz |
|---|---|---|
| `GET` | `/product` | Lista produtos com o estoque disponível |
| `GET` | `/product/:id` | Detalha um produto |
| `POST` | `/product` | Cadastra produto |
| `PUT` | `/product/:id` | Atualiza produto |
| `DELETE` | `/product/:id` | Remove produto |
| `PUT` | `/stock/:product_id` | Atualiza o estoque |
| `POST` | `/users` | Cadastra usuário |
| `GET` | `/users` | Lista usuários |
| `POST` | `/login` | Autentica e devolve o token |
| `POST` | `/cart-products` | Adiciona item ao carrinho |
| `GET` | `/cart-products/:cart_id` | Lista os itens do carrinho |
| `DELETE` | `/cart/item/:id` | Remove item do carrinho |
| `POST` | `/orders` | Fecha o pedido |

O estoque não fica em uma coluna do produto: a listagem faz `LEFT JOIN` com a tabela `stock` e usa `COALESCE(s.amount, 0)`, então um produto recém-cadastrado aparece com estoque zero em vez de sumir da consulta.

## Stack

- **Back-end:** Node.js, Express, PostgreSQL (driver `pg`)
- **Front-end:** HTML, CSS e JavaScript
- **Autenticação:** JWT, com senhas em hash bcrypt
- **Imagens:** Cloudinary

## Estrutura

```
api/
├── server.js       # Express e rotas
├── db.js           # pool de conexão PostgreSQL
├── auth.js         # registro, login e emissão de JWT
├── cloudinary.js   # upload de imagens
└── script.js
tcc/
├── produtos.html   # catálogo
├── admin.html      # painel administrativo
├── login.html
├── cadastro.html
└── sobre.html
```

## Como rodar

```bash
cd api
npm install
cp .env.example .env   # DATABASE_URL, JWT_SECRET e credenciais do Cloudinary
node server.js
```

## Melhorias planejadas

- [ ] Mover as credenciais do Cloudinary para variáveis de ambiente
- [ ] Middleware de autenticação nas rotas de administração
- [ ] Validação de entrada nos endpoints de escrita
- [ ] Testes de integração
