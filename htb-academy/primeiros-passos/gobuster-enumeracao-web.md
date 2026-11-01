# Gobuster - caminho da wordlist

## Objetivo

Praticar técnicas de enumeração web (Gobuster, leitura de robots.txt e código-fonte) para encontrar uma página de login escondida e capturar a flag.

## Antes de começar

Eu esperava que bastasse acessar o IP e a porta do alvo para já ver algo relevante. Não sabia ainda que seria preciso enumerar diretórios escondidos para achar o caminho certo.

## Passo a passo

1. Varredura de diretórios com Gobuster: 
`gobuster dir -u http://<IP>:<porta>/ -w /usr/share/seclists/Discovery/Web-Content/common.txt`  
Resultado: encontrados `/index.php`, `/robots.txt` (200) e `/wordpress` (301), entre outros com 403.

2. Leitura do `robots.txt` → achou `/admin-login-page.php`
 `curl http://<IP>:<porta>/robots.txt`  
 Resultado: revelou o caminho `/admin-login-page.php`, não encontrado na varredura do Gobuster.

3. Tentativa de login com credenciais do `my_credentials.txt` → falhou
 cat ~/Desktop/my_credentials.txt Username: htb-ac-1498319  Password: S6pszziG Login tentado com essas credenciais, mas o formulário não reagiu ao clique.

4. Inspeção do código-fonte → achou o comentário com credenciais de teste

```
- <!-- TODO: remove test credentials admin:password123 -->
```

5. Login bem-sucedido e captura da flag

- HTB{...}
## Onde travei

- Ponto em que emperrei: rodar o Gobuster 
- Quanto tempo tentei sozinha antes da dica: 2 minutos
- Dica que usei: “Tive apoio para entender a diferença entre `ls` e `cd` e a sintaxe do Gobuster; a descoberta da credencial no código-fonte foi minha.”

## O que aprendi

- Diferença entre `ls` e `cd`
- Como montar um comando do Gobuster corretamente
- O que significam os status 403, 200 e 301
- Que comentários no código-fonte podem vazar credenciais (_information disclosure_)

## Refazer sem consulta

Usei o código do Gobuster errado, onde uma parte do comando estava errado.  Usei ao comando LS errado com se fosse listar o diretório, já o comando Cd usei para atualizar. Corrigir isso é necessário.

## Para o portfólio

Revisado: IP, porta e flag ocultados antes da publicação. Nenhuma senha real exposta.
