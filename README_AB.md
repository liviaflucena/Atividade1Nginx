
# Teste de Carga com Apache Bench na Aplicação React 🔋

Este tutorial detalha como configurar e usar o Apache Bench para realizar um teste de carga na página inicial da aplicação React, servida via Nginx, em sistemas Linux e macOS. Serve para testar a capacidade do seu servidor e a estabilidade da aplicação React sob carga simulada.

---

## 1. Pré-requisitos

- Servidor Nginx instalado e configurado para servir a aplicação React na porta 8080 (ex: http://localhost:8080)
- Apache Bench (`ab`) instalado

---

## 2. Instalando Apache Bench

### No macOS

O Apache Bench está incluso no pacote `httpd`. Para instalar via Homebrew:

```bash
brew install httpd
````

### No Linux (Debian/Ubuntu)

Para instalar o Apache Bench, que faz parte do pacote `apache2-utils`:

```bash
sudo apt update
sudo apt install apache2-utils
```

---

## 3. Verificando o servidor Nginx

Certifique-se que o Nginx está ativo e servindo a aplicação React corretamente.

Teste com:

```bash
curl -I http://localhost:8080/
```

Deve retornar `HTTP/1.1 200 OK` ou equivalente.

---

## 4. Executando um teste de carga com Apache Bench

Execute o seguinte comando para enviar 100 requisições com até 10 conexões simultâneas:

```bash
ab -n 100 -c 10 http://localhost:8080/
```

* `-n 100`: total de requisições.
* `-c 10`: requisições concorrentes (simultâneas).
* Ajuste a URL para o endereço correto da sua aplicação.

---

## 5. Interpretando os resultados 💡

Exemplo de saída simplificada:

```
Complete requests:      100
Failed requests:        0
Requests per second:    7620.79 [#/sec] (mean)
Time per request:       1.312 [ms] (mean)
Transfer rate:          4591.82 [Kbytes/sec] received
```

* **Complete requests**: número de requisições bem-sucedidas.
* **Failed requests**: requisições que falharam (ideal: 0).
* **Requests per second**: quantas requisições o servidor atende por segundo (performance).
* **Time per request**: tempo médio para responder uma requisição (latência).
* **Transfer rate**: taxa média de dados transferidos.

---

## 6. Dicas e comandos úteis ✍🏽

* Reiniciar o Nginx após alterar configurações:

```bash
sudo nginx -s reload
```

* Validar a configuração do Nginx:

```bash
sudo nginx -t
```

* Verificar processos Nginx rodando:

```bash
ps aux | grep nginx
```

* Verificar se a porta 8080 está em uso:

```bash
lsof -i :8080
```

