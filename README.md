![PHP](https://img.shields.io/badge/PHP-8.x-777BB4?logo=php)
![JavaScript](https://img.shields.io/badge/JavaScript-ES6-F7DF1E?logo=javascript)
![MySQL](https://img.shields.io/badge/MySQL-8.x-4479A1?logo=mysql)
![License](https://img.shields.io/badge/license-MIT-green)
![Status](https://img.shields.io/badge/status-concluído-brightgreen)

# user-registration-hybrid-crypto

Sistema de cadastro e login com criptografia híbrida ponta a ponta. Os dados do formulário são cifrados no front-end com AES (CryptoJS), a chave simétrica é então cifrada com RSA pública (JSEncrypt) e enviada ao back-end PHP, que usa OpenSSL para descriptografar a chave RSA, recuperar o AES e persistir os dados no MySQL.

---

## Fluxo de criptografia

```
Front-end
  1. Gera chave AES aleatória
  2. Cifra os dados do formulário com AES
  3. Cifra a chave AES com a chave pública RSA
  4. Envia { dados_cifrados, chave_cifrada } ao back-end

Back-end (PHP + OpenSSL)
  5. Descriptografa a chave AES com a chave privada RSA
  6. Descriptografa os dados com a chave AES recuperada
  7. Insere os dados no banco via MySQLi
```

## Tecnologias

| Camada | Tecnologia |
|--------|-----------|
| Front-end | HTML, CSS, JavaScript |
| Criptografia (cliente) | CryptoJS (AES), JSEncrypt (RSA) |
| Back-end | PHP + OpenSSL |
| Banco de dados | MySQL (MySQLi) |

## Pré-requisitos

- PHP 8+ com extensão OpenSSL habilitada
- MySQL 8+
- Servidor web (Apache/Nginx) ou `php -S` para desenvolvimento

## Instalação

```bash
git clone https://github.com/vMigliorini/Cadastro-hybrid-crypto.git
cd Cadastro-hybrid-crypto
```

1. Importe o schema do banco de dados:
```bash
mysql -u root -p < SQL/schema.sql
```

2. Configure a conexão com o banco e os caminhos das chaves RSA nos arquivos PHP da pasta `php/`.

3. Certifique-se de que as chaves RSA estão na pasta `chaves/`.

4. Suba o servidor:
```bash
php -S localhost:8000
```

5. Acesse `http://localhost:8000` no navegador.

## Estrutura do projeto

```
├── index.html            # Página de cadastro
├── pagina-login/         # Página de login
├── js/                   # Lógica de criptografia e requisições
├── css/                  # Estilos
├── php/                  # Back-end: descriptografia e acesso ao banco
├── chaves/               # Chaves RSA pública e privada
└── SQL/                  # Schema do banco de dados
```

---

Desenvolvido por [@vMigliorini](https://github.com/vMigliorini)
