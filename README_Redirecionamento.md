
## 🚀 **Tutorial: Aplicação React com Nginx (macOS + Linux)**

### 🧰 **Pré-requisitos**

* Node.js e npm instalados
* Projeto React (aqui usei o `https://github.com/liviaflucena/cafeteria-web.git`)
* Nginx instalado

---

### ✅ **1. Instalar o Nginx**

#### 🔸 macOS (via Homebrew)

```bash
brew install nginx
```

#### 🔸 Linux (Debian/Ubuntu)

```bash
sudo apt update
sudo apt install nginx
```

---

### ✅ **2. Estrutura para Virtual Hosts**

#### Criar diretórios (iguais em ambos):

```bash
sudo mkdir -p /etc/nginx/sites-available
sudo mkdir -p /etc/nginx/sites-enabled
```

> 🔹 No **macOS (Homebrew)**, o caminho costuma ser:

```bash
sudo mkdir -p /opt/homebrew/etc/nginx/sites-available
sudo mkdir -p /opt/homebrew/etc/nginx/sites-enabled
```

---

### ✅ **3. Editar o `nginx.conf`**

#### Localizar o arquivo:

* **macOS:**
  `/opt/homebrew/etc/nginx/nginx.conf`
* **Linux:**
  `/etc/nginx/nginx.conf`

#### Editar:

```bash
sudo nano /CAMINHO/nginx.conf
```

🔧 Dentro do bloco `http { ... }`, adicione (ou descomente):

```nginx
include /CAMINHO/sites-enabled/*;
```

Substitua `/CAMINHO/` pelo caminho correto conforme seu sistema.

> ⚠️ Verifique se as chaves `{}` estão corretamente fechadas! Qualquer `}` extra gera erro.

---

### ✅ **4. Clonar e Buildar o Projeto React**

```bash
git clone https://github.com/liviaflucena/cafeteria-web.git
cd cafeteria-web
npm install
npm run build
```

---

### ✅ **5. Criar o diretório onde o Nginx vai servir os arquivos**

```bash
sudo mkdir -p /var/www/cafeteria
sudo cp -r dist/* /var/www/cafeteria/
```

> 🔸 **macOS (Homebrew):**

```bash
sudo mkdir -p /opt/homebrew/var/www/cafeteria
sudo cp -r dist/* /opt/homebrew/var/www/cafeteria/
```
Utilizo o  `dist` pois a aplicação React foi gerada com o VITE.
---

### ✅ **6. Criar o arquivo de configuração do site**

```bash
sudo nano /CAMINHO/sites-available/cafeteria.conf
```

📄 Conteúdo do arquivo:

```nginx
server {
    listen 8080;
    server_name localhost;

    root /CAMINHO/www/cafeteria;
    index index.html;

    location / {
        try_files $uri /index.html;
    }

    error_page 404 /index.html;
}
```

> Substitua `/CAMINHO/www/cafeteria` conforme o seu sistema:
>
> * **Linux:** `/var/www/cafeteria`
> * **macOS:** `/opt/homebrew/var/www/cafeteria`

---

### ✅ **7. Habilitar o site (link simbólico)**

```bash
sudo ln -s /CAMINHO/sites-available/cafeteria.conf /CAMINHO/sites-enabled/cafeteria.conf
```

Se já existir:

```bash
sudo rm /CAMINHO/sites-enabled/cafeteria.conf
sudo ln -s /CAMINHO/sites-available/cafeteria.conf /CAMINHO/sites-enabled/cafeteria.conf
```

---

### ✅ **8. Testar a configuração do Nginx**

```bash
sudo nginx -t
```

Saída esperada:

```
nginx: configuration file /.../nginx.conf test is successful
```

---

### ✅ **9. Reiniciar ou recarregar o Nginx**

#### 🔸 Linux:

```bash
sudo systemctl reload nginx
# ou
sudo systemctl restart nginx
```

#### 🔸 macOS:

```bash
sudo nginx -s reload
```

---

### ✅ **10. Acessar no navegador**

Abra:

```
http://localhost:8080
```

🎉 A aplicação React estará rodando via Nginx!

