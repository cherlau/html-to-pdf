# HTML → PDF

Ferramenta local para converter HTML em PDF via interface web. Cole seu HTML, clique no botão e o PDF é baixado automaticamente.

## Como funciona

- Interface web simples onde você cola o código HTML
- O servidor usa Puppeteer (Chromium headless) para renderizar o HTML e gerar o PDF
- O arquivo é devolvido como download direto (`documento.pdf`)
- Nenhum dado é enviado para servidores externos — tudo roda localmente

## Requisitos

- [Node.js](https://nodejs.org/) 18+

## Instalação

```bash
npm install
```

> Na primeira execução, o Puppeteer fará o download do Chromium automaticamente (~170 MB).

## Uso

```bash
npm start
```

Acesse [http://localhost:3000](http://localhost:3000) no navegador.

## API

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
