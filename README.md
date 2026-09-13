# Ataque de Força Bruta no DVWA - Login.php com Hydra

## Objetivo

Demonstrar um ataque de força bruta prático no formulário de login do DVWA utilizando a ferramenta Hydra.

## Ambiente

- Atacante: Kali Linux (Dualboot)
- Alvo: DVWA (VM)
- IP Alvo: 192.168.56.101
- Rede: Host-only
- Ferramenta: Hydra

## Resultados

Usuário: admin
Senha encontrada: password
Total de tentativas: 4
Tentativas até sucesso: 2
Tempo total: 1 min

## Comando Executado

```bash
hydra -l admin -P pass.txt 192.168.56.101 http-post-form "/dvwa/login.php:username=^USER^&password=^PASS^&Login=Login:Invalid username and/or password"
```

## Explicacao do Comando

- l admin: Define o usuario alvo
- P pass.txt: Arquivo com lista de senhas
- 192.168.56.101: IP do servidor
- http-post-form: Tipo de ataque (formulario POST)
- /dvwa/login.php: Caminho da pagina de login
- username=^USER^&password=^PASS^&Login=Login: Parametros do formulario
- Invalid username and/or password: Mensagem de erro detectada

## Como Funciona

O Hydra automatiza requisicoes POST ao formulario de login, testando cada combinacao de usuario e senha da wordlist. Quando a resposta nao contem a mensagem de erro, significa que o login foi bem-sucedido.

## Wordlist Utilizada

Arquivo: pass.txt
Senhas testadas:
- 123456
- password
- qwerty
- msfadmin

## Validacao

As credenciais encontradas foram validadas acessando manualmente o DVWA e realizando login com usuario admin e senha password. O acesso foi bem-sucedido.

## Vulnerabilidades Encontradas

- Sem rate limiting (sem limite de tentativas por segundo)
- Sem bloqueio de conta apos tentativas falhas
- Sem CAPTCHA
- Senhas fracas no banco de dados


## Referencias

- Hydra: https://github.com/vanhauser-thc/thc-hydra
- DVWA: http://www.dvwa.co.uk/
- OWASP Brute Force: https://owasp.org/www-community/attacks/Brute_force_attack
