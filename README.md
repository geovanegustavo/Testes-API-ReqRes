# Testes-API-ReqRes

## Ajustar o arquivo ReqRes-env.json

Abra o arquivo ReqRes-env.json no seu repositório e adicione a URL base diretamente no campo "value" da chave url_base.

O campo da api_key nós vamos deixar em branco de propósito por segurança. O arquivo deve ficar assim:

```bash
{
	"id": "d52e6311-a94f-4b64-ab9e-bb5a4de310e1",
	"name": "ReqRes",
	"values": [
		{
			"key": "url_base",
			"value": "https://reqres.in/api",
			"type": "default",
			"enabled": true
		},
		{
			"key": "api_key",
			"value": "",
			"type": "default",
			"enabled": true
		},
		{
			"key": "token_autenticacao",
			"value": "",
			"type": "any",
			"enabled": true
		}
...
```

## Cadastrar sua API Key nos Secrets do GitHub

Nunca coloque chaves de API diretamente em arquivos de texto no GitHub. Para protegê-la:

1. No seu repositório no GitHub, clique na aba Settings (Configurações).
2. Na barra lateral esquerda, clique em Secrets and variables -> Actions.
3. Clique no botão verde New repository secret.
4. No campo Name, digite exatamente: REQRES_API_KEY
5. No campo Secret, cole a sua chave do ReqRes (aquela do x-api-key).
6. Clique em Add secret.

## Atualizar o arquivo github-ci.yml

Alterar o Step 4 da sua Action para fazer duas coisas:

1. Injetar a chave secreta que você guardou no GitHub diretamente na execução do Newman usando o parâmetro --env-var.
2. Adicionar o parâmetro --suppress-exit-code para garantir que o fluxo gere o relatório HTML mesmo se algum teste falhar.
3. Substitua o trecho do Step 4 no seu arquivo .yml por este:

```bash
# Runs a set of commands using the runners shell
      - name: Step 4 Execute collection
        run: newman run ./ReqRes-ci.json -e ./ReqRes-env.json --env-var "api_key=${{ secrets.REQRES_API_KEY }}" --reporters cli,htmlextra --reporter-htmlextra-export ./results/Report.html --suppress-exit-code
```