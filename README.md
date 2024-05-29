# Carrinho de Compras da Shopee com Node.js

## Introdução
Este artigo é um guia passo a passo para criar um sistema de carrinho de compras online, inspirado na interface da Shopee. Utilizando **Node.js**, vamos gerenciar o backend e sincronizar os estados do carrinho em tempo real. O sistema permitirá que os usuários adicionem, removam e modifiquem produtos em seus carrinhos, com atualizações instantâneas e cálculo automático dos totais.

## Módulo 1: Estruturação do Projeto

Primeiro, vamos configurar a estrutura básica do nosso projeto Node.js.

```javascript
// Instalação do Node.js
// Visite https://nodejs.org e instale o Node.js seguindo as instruções.

// Inicialização do projeto Node.js
const express = require('express');
const app = express();
const server = require('http').createServer(app);
const io = require('socket.io')(server);

// Configuração do servidor para aceitar conexões
server.listen(3000, () => {
  console.log('Servidor rodando na porta 3000');
});
```

## Módulo 2: Gerenciamento do Carrinho

Agora, vamos implementar a lógica para adicionar, remover e atualizar itens no carrinho.

```javascript
// Classe Carrinho para gerenciar os itens
class Carrinho {
  constructor() {
    this.itens = [];
  }

  // Adicionar item ao carrinho
  adicionarItem(item) {
    this.itens.push(item);
  }

  // Remover item do carrinho
  removerItem(itemId) {
    this.itens = this.itens.filter(item => item.id !== itemId);
  }

  // Atualizar quantidade de um item
  atualizarQuantidade(itemId, quantidade) {
    const item = this.itens.find(item => item.id === itemId);
    if (item) {
      item.quantidade = quantidade;
    }
  }

  // Calcular total do carrinho
  calcularTotal() {
    return this.itens.reduce((total, item) => total + (item.preco * item.quantidade), 0);
  }
}
```

## Módulo 3: Sincronização em Tempo Real

Para uma experiência de usuário fluida, implementaremos a sincronização do estado do carrinho em tempo real com Socket.io.

```javascript
// Configuração do Socket.io para comunicação em tempo real
io.on('connection', (socket) => {
  console.log('Usuário conectado');

  socket.on('adicionarAoCarrinho', (item) => {
    // Adiciona o item ao carrinho e emite o novo estado
  });

  socket.on('removerDoCarrinho', (itemId) => {
    // Remove o item do carrinho e emite o novo estado
  });

  socket.on('atualizarQuantidade', (dados) => {
    // Atualiza a quantidade de um item e emite o novo estado
  });

  socket.on('disconnect', () => {
    console.log('Usuário desconectado');
  });
});
```

## Conclusão

Com estes módulos, você construirá um sistema de carrinho de compras eficiente e interativo, similar ao da Shopee. Lembre-se de testar cada funcionalidade e garantir que a experiência do usuário seja a mais suave possível.
