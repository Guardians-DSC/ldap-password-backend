# Reset Password LDAP LCC - Backend

Esse repositório contém o código-fonte de uma aplicação web que altera a senha de usuários em um servidor LDAP. Se você quer reutilizar esse sistema fora dos LCCs, altere as variáveis presentes no <code>lcc_ldap.py</code>, para incluir o domain, server e outras variáveis baseado nas suas configurações, e também altere a verificação do host em <code>main.py</code>.

## Importante

- É necessário um arquivo .env com uma variável "KEY". Ela vai ser usada por questões de segurança. Então, na requisição, inclua um campo "key" no JSON do corpo da requisição.
- Além da KEY, inclua no arquivo .env a variável "LDAP_PASS" com a senha do seu servidor LDAP.
- Quando um usuário tenta alterar sua senha, com sucesso ou sem sucesso, um log é gerado e salvo em <code>reset.log</code>

## Run

Para rodar a aplicação e instalar as dependências

```sh
python3.11 -m venv .venv
source .venv/bin/activate
pip install -r requirements.txt
uvicorn main:app --port 5000
```

Copie o `.env.sample` para o `.env` configurando suas variáveis de ambiente:

```sh
cp .env.sample .env
```

### Com Docker

#### Pré-requisitos

- Docker

1. Faça o build da imagem:

```sh
make build
```

2. Rode o container:

```sh
make run # rodar em foreground
# or
make rund # rodar em background
```

3. Parar o container (background) após o uso:

```sh
make stop
```
## Rotas

Quando a aplicação estiver rodando, você pode acessar a rota única do sistema: <code>localhost:5000/reset-password</code>. Sua requisição deve ser POST e deve incluir uma campo "email" (ex: fulano.silva@ccc.ufcg.edu.br) e uma campo "key" com o valor do arquivo .env.
