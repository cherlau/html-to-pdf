# HTML → PDF

Ferramenta local/hospedada para converter HTML em PDF via interface web. Cole seu HTML, clique no botão e o PDF é baixado automaticamente.

> Web: https://html-to-pdf-p9p1.onrender.com/

---

## Como funciona

- Interface web onde você cola o código HTML
- O servidor usa Puppeteer (Chromium headless) para renderizar o HTML e gerar o PDF
- O arquivo é devolvido como download direto (`documento.pdf`)
- Nenhum dado é enviado para servidores externos — tudo roda no próprio servidor

## Requisitos

- [Node.js](https://nodejs.org/) 18+

## Instalação

```bash
npm install
```

> Na primeira execução, o Puppeteer fará o download do Chromium automaticamente (~170 MB).

## Uso local

```bash
npm start
```

Acesse [http://localhost:3000](http://localhost:3000) no navegador.

## Deploy no Render (gratuito)

1. Suba o projeto em um repositório no GitHub
2. Acesse [render.com](https://render.com) e crie um **Web Service** apontando para o repositório
3. Configure:
   - **Build command:** `npm install`
   - **Start command:** `npm start`
   - **Environment:** Node
4. Clique em **Deploy**

> **Atenção:** no plano gratuito do Render, o servidor hiberna após 15 minutos de inatividade e leva ~30 segundos para acordar na próxima requisição. A interface já lida com isso automaticamente — um banner de status aparece na página enquanto o servidor está acordando, some assim que estiver pronto, e exibe um botão para tentar novamente caso exceda o tempo de espera.

## API

### `GET /health`

Verifica se o servidor está no ar.

**Resposta:**

```json
{ "status": "ok" }
```

---

### `POST /generate-pdf`

Gera um PDF a partir de um HTML enviado no corpo da requisição.

**Body (JSON):**

```json
{
  "html": "<html><body><h1>Olá, mundo!</h1></body></html>"
}
```

**Resposta de sucesso:** arquivo PDF (`application/pdf`) como download.

**Resposta de erro:**

```json
{ "error": "Mensagem de erro" }
```

**Configurações do PDF gerado:**
- Formato: A4
- Margens: 15mm em todos os lados
- Background CSS incluído (`printBackground: true`)

## Stack

| | |
|---|---|
| Runtime | Node.js |
| Servidor | Express |
| Renderização | Puppeteer (Chromium headless) |
| Frontend | HTML + Tailwind CSS (CDN) |
