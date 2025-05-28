# 🐝 Beedoo SDK PHP

![PHP](https://img.shields.io/badge/PHP-777BB4?style=for-the-badge&logo=php&logoColor=white)
![Composer](https://img.shields.io/badge/Composer-885630?style=for-the-badge&logo=composer&logoColor=white)
![REST API](https://img.shields.io/badge/REST_API-009688?style=for-the-badge&logo=api&logoColor=white)
![JSON](https://img.shields.io/badge/JSON-000000?style=for-the-badge&logo=json&logoColor=white)

SDK oficial em PHP para integração com a API do Beedoo, desenvolvido para facilitar a comunicação com a plataforma de forma prática e eficiente.

## 📋 Sobre o Beedoo

O Beedoo é uma plataforma de gestão de conhecimento e engajamento corporativo que oferece recursos como wiki, grupos, gestão de usuários e muito mais. A API do Beedoo segue a arquitetura REST, adotando boas práticas, convenções e padrões como json:api e JSend.

## 🚀 Funcionalidades

Este SDK oferece acesso simplificado aos seguintes recursos da API Beedoo:

- **Gestão de Usuários**: Cadastro e atualização de usuários
- **Grupos**: Consulta e gerenciamento de grupos
- **Wiki**: Consulta de artigos, marcação de leitura
- **Times**: Consulta de avatares e identidade visual
- **Upload**: Geração de URLs pré-assinadas para upload no S3
- **Autenticação**: Obtenção de tokens de acesso

## 🛠️ Requisitos

- PHP 7.2 ou superior
- Composer
- Extensão cURL habilitada

## 📦 Instalação

Instale a biblioteca utilizando o Composer:

```bash
composer require beedooedtech/beedoo-sdk-php
```

## ⚙️ Configuração

Para incluir a biblioteca em seu projeto, basta fazer o seguinte:

```php
<?php

require __DIR__ . "/vendor/autoload.php";

// Inicialize o cliente com sua chave secreta
$beedoo = new Beedoo\Client("SUA_SECRET_KEY");
```

## 📚 Exemplos de Uso

### Autenticação - Obter Access Token

```php
<?php

$payloadAuth = [
    "clientId" => "n6XSN0o6FDQZQ4lmxb7P2"
];

$accessToken = $beedoo->accessToken()->get($payloadAuth);
```

### Consultar Grupos

```php
<?php

$params = [
  "id" => 1,
  "name" => "nome_do_grupo",
  "offset" => 5,
  "limit" => 20,
];

$groups = $beedoo->groups()->get($params);
```

### Consultar Artigos na Wiki

```php
<?php

$params = [
  "question" => "assunto_a_ser_pesquisado",
  "category" => 1,
  "tag" => 5,
  "offset" => 20,
  "limit" => 20,
];

$articles = $beedoo->wiki()->get($params);
```

### Verificar se um Artigo foi Lido

```php
<?php

$article = [
  'id' => 279
];

$result = $beedoo->wiki()->getIsReadArticle($article);
```

### Marcar um Artigo como Lido

```php
<?php

$article = [
  'id' => 279
];

$result = $beedoo->wiki()->saveArticleRead($article);
```

### Obter Avatares do Time

```php
<?php

$avatars = $beedoo->team()->getAvatar();
```

### Obter URL para Upload de Arquivos

```php
<?php

$uploadUrl = $beedoo->upload()->getUrl();
```

### Obter Identidade Visual do Time

```php
<?php

$visualIdentity = $beedoo->visualIdentity()->get();
```

### Cadastrar Novo Usuário

```php
<?php

/** Campos obrigatórios */
$userData = [
  "username" => "jhonsnow",
  "name" => "Jhon Snow",
  "login" => "jhonsnow",
  "password" => "123mudar",
  "status" => "Ativo",
  "typeUser" => "Usuário",
  "permission" => "Usuario",
  "groups" => "geral"
];

$user = $beedoo->user()->create($userData);
```

### Atualizar Usuário Existente

```php
<?php

$userData = [
  "username" => "jhonsnow",
  "name" => "Jhon Snow",
  "login" => "jhonsnow",
  "email" => "jhonsnow@gmail.com",
  "password" => "123mudar",
  "status" => "Ativo",
  "typeUser" => "Usuário",
  "permission" => "Usuario",
  "groups" => "geral, grupo_pela_api",
  "cpf_cnpj" => 46312127800,
  "dashboard" => [
    "agent_id" => 22032,
    "template" => "Template DEV"
  ],
  "hierarchy" => [
    "leader" => 77202,
    "level" => "Gerente" 
  ],
  "language" => "pt-BR",
  "leader" => true,
  "mention_feed" => false,
  "entrytime" => "18:45:00",
  "exittime" => "23:15:00",
  "customfields" => [
    "Login-SSO" => "jhonsnow",
    "Complementar Numero" => 12345
  ]
];

$user = $beedoo->user()->update($userData);
```

## 🔄 Tratamento de Erros

O SDK utiliza exceções para indicar erros de comunicação com a API. Recomenda-se utilizar blocos try/catch para capturar e tratar essas exceções:

```php
<?php

try {
    $groups = $beedoo->groups()->get($params);
} catch (\Exception $e) {
    // Tratar o erro
    echo "Erro na requisição: " . $e->getMessage();
}
```

## 📝 Parâmetros Comuns

Muitos métodos aceitam parâmetros de paginação:

- `offset`: Posição inicial para retorno dos registros (padrão: 0)
- `limit`: Quantidade máxima de registros a serem retornados (padrão: 20)

## 🔒 Segurança

- Nunca compartilhe sua SECRET_KEY
- Utilize HTTPS para todas as comunicações
- Armazene credenciais em variáveis de ambiente ou arquivos de configuração protegidos

## 🧪 Testes

O SDK inclui testes unitários que podem ser executados com PHPUnit:

```bash
./vendor/bin/phpunit
```

## 📄 Licença

Este projeto está licenciado sob a licença MIT - veja o arquivo LICENSE para detalhes.

## 🤝 Contribuição

Contribuições são bem-vindas! Sinta-se à vontade para abrir issues ou enviar pull requests.

## 📚 Recursos Adicionais

- [Documentação completa da API Beedoo](https://api.beedoo.io/docs)
- [Beedoo Website](https://www.beedoo.io)

---

⭐ Desenvolvido por [Beedoo EdTech](https://github.com/beedooedtech) e mantido por [Yan Policarpo](https://github.com/h4rd1ideveloper)
