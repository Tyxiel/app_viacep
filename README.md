# tyxiel-app_viacep

> 📮 Buscador de CEPs brasileiro utilizando a API pública ViaCEP. Aplicação web estática que preenche automaticamente endereço, bairro, cidade e estado a partir de um CEP informado.

[🇧🇷 Português](#-visão-geral-pt) | [🇺🇸 English](#-overview-en)

---

## 📋 Table of Contents

- [Visão Geral (PT)](#-visão-geral-pt)
- [Overview (EN)](#-overview-en)
- [Tech Stack](#-tech-stack)
- [Prerequisites](#-prerequisites)
- [Getting Started](#-getting-started)
- [Architecture](#-architecture)
- [Environment Variables](#-environment-variables)
- [Available Scripts](#-available-scripts)
- [Testing](#-testing)
- [Deployment](#-deployment)
- [Troubleshooting](#-troubleshooting)
- [Contributing](#-contributing)
- [License](#-license)

---

## 🇧🇷 Visão Geral (PT)

Aplicação web estática para consulta de endereços brasileiros via CEP (Código de Endereçamento Postal). O usuário digita um CEP válido e o sistema busca automaticamente os dados na API pública [ViaCEP](https://viacep.com.br/), preenchendo os campos de endereço, bairro, cidade e estado.

### Principais Funcionalidades

- ✅ Consulta de CEP via API ViaCEP (gratuita, sem autenticação)
- ✅ Preenchimento automático de campos: logradouro, bairro, localidade, UF
- ✅ Interface simples e responsiva com CSS Flexbox
- ✅ Zero dependências externas (apenas navegador moderno)
- ✅ Código em português para fácil compreensão
- ✅ License AGPL v3 para software livre

### Limitações Conhecidas

| Limitação | Impacto | Workaround |
|-----------|---------|------------|
| CEPs inválidos retornam `{ "erro": true }` | Campos não são preenchidos | Validar formato do CEP antes de buscar |
| API ViaCEP tem rate limit não documentado | Requisições em massa podem falhar | Implementar debounce ou cache local |
| Sem tratamento de erros na UI | Usuário não vê feedback de falha | Adicionar mensagens de erro (sugestão de melhoria) |
| CEPs sem bairro retornam campo vazio | Campo "bairro" fica em branco | Exibir "Não informado" quando vazio |

---

## 🇺🇸 Overview (EN)

Static web application for looking up Brazilian addresses via CEP (Postal Code). Users enter a valid CEP and the system automatically fetches data from the public [ViaCEP API](https://viacep.com.br/), populating fields for street, neighborhood, city, and state.

### Key Features

- ✅ CEP lookup via ViaCEP API (free, no authentication required)
- ✅ Auto-fill fields: street, neighborhood, city, state
- ✅ Simple, responsive UI with CSS Flexbox
- ✅ Zero external dependencies (modern browser only)
- ✅ Portuguese code for easy understanding
- ✅ AGPL v3 license for free software

### Known Limitations

| Limitation | Impact | Workaround |
|------------|--------|------------|
| Invalid CEPs return `{ "erro": true }` | Fields remain empty | Validate CEP format before fetching |
| ViaCEP API has undocumented rate limits | Bulk requests may fail | Implement debounce or local caching |
| No error handling in UI | Users see no feedback on failure | Add error messages (improvement suggestion) |
| CEPs without neighborhood return empty | "Bairro" field stays blank | Display "Not provided" when empty |

---

## 🛠 Tech Stack

| Category | Technology | Version/Purpose |
|----------|-----------|-----------------|
| **Markup** | HTML5 | Semantic structure, form inputs |
| **Styling** | CSS3 | Flexbox layout, custom properties, responsive design |
| **Logic** | Vanilla JavaScript (ES6+) | Fetch API, DOM manipulation, async/await |
| **External API** | ViaCEP | `https://viacep.com.br/ws/{cep}/json/` |
| **Hosting** | Any static host | GitHub Pages, Netlify, Vercel, or local file |
| **License** | GNU AGPL v3 | Copyleft license for network software |

### Why This Stack?

- **Zero build step**: Edit `.html`/`.js`/`.css` and refresh — no compilation.
- **Maximum compatibility**: Works in any browser with ES6+ support (Chrome 55+, Firefox 52+, Edge 15+).
- **Lightweight**: ~1KB JS + ~1KB CSS = instant load times.
- **Educational**: Demonstrates `fetch()`, `async/await`, and DOM manipulation in pure JS.

---

## 📦 Prerequisites

| Tool | Version | Purpose | Install Command |
|------|---------|---------|----------------|
| **Web Browser** | Chrome 55+, Firefox 52+, Edge 15+, Safari 10+ | Render and execute JavaScript | [Download](https://www.google.com/chrome/) |
| **Text Editor** | Any (VS Code recommended) | Edit source files | [VS Code](https://code.visualstudio.com/) |
| **Git** | 2.30+ (optional) | Clone repo and manage versions | `sudo apt install git` / `brew install git` |
| **Node.js** | Not required | — | — |

> 💡 **No package manager, bundler, or runtime needed.** This is a pure static site.

### CEP Format Reference

```
Brazilian CEP format: XXXXX-XXX or XXXXXXXX
Examples: 
  - 01001-000 (Praça da Sé, São Paulo-SP)
  - 20040-020 (Centro, Rio de Janeiro-RJ)
  - 70040-010 (Asa Sul, Brasília-DF)
```

---

## 🚀 Getting Started

### 1. Clone the Repository

```bash
git clone https://github.com/tyxiel/tyxiel-app_viacep.git
cd tyxiel-app_viacep
```

### 2. Open Locally

**Option A: Direct file open (quick test)**
```bash
# macOS
open index.html

# Linux
xdg-open index.html

# Windows
start index.html
```

**Option B: Local server (recommended for accurate testing)**
```bash
# Python 3
python3 -m http.server 8000
# Then open: http://localhost:8000

# Or with Node.js (if installed)
npx serve .
```

> ⚠️ **Note**: Some browsers restrict `fetch()` calls when opening files via `file://`. Use a local server for reliable testing.

### 3. Using the Application

1. Enter a valid Brazilian CEP in the "CEP" field (format: `12345-678` or `12345678`)
2. Click **"Enviar"** or press Enter
3. Wait ~1-2 seconds for the API response
4. Fields will auto-fill with:
   - **Endereço**: Street name (logradouro)
   - **Bairro**: Neighborhood
   - **Cidade**: City name (localidade)
   - **Estado**: State abbreviation (UF)

### 4. Test CEPs (Valid Examples)

| CEP | Expected Result |
|-----|----------------|
| `01001-000` | Praça da Sé, Sé, São Paulo, SP |
| `20040-020` | Rua do Ouvidor, Centro, Rio de Janeiro, RJ |
| `70040-010` | Esplanada dos Ministérios, Zona Cívico-Administrativa, Brasília, DF |
| `88010-400` | Rua Felipe Schmidt, Centro, Florianópolis, SC |

### 5. Customize (Optional)

**Update styles** in `style.css`:
```css
/* Change primary colors */
body {
    background-color: #f0f0f0; /* Instead of gray */
}

.inputs {
    background-color: #ffffff; /* Instead of darkgray */
    border: 2px solid #007bff; /* Add border */
}
```

**Add error handling** in `App.js`:
```javascript
async function BuscarDados(cep){
    try {
        const response = await fetch(`https://viacep.com.br/ws/${cep}/json/`);
        const dados = await response.json();
        
        if (dados.erro) {
            alert('CEP não encontrado. Verifique o número e tente novamente.');
            return;
        }
        dadosNaTela(dados);
    } catch (error) {
        console.error('Erro na requisição:', error);
        alert('Erro de conexão. Verifique sua internet e tente novamente.');
    }
}
```

---

## 🏗 Architecture

### Directory Structure

```
tyxiel-app_viacep/
├── index.html    # Main entry point: HTML structure + form
├── App.js        # Application logic: fetch, DOM manipulation
├── style.css     # Visual styling: layout, colors, responsiveness
├── LICENSE       # GNU AGPL v3 license text
└── README.md     # This documentation
```

### File Responsibilities

#### `index.html`
- **Structure**: Semantic HTML5 form with labeled inputs
- **Inputs**:
  ```html
  <input type="text" id="cep">        <!-- User input: CEP -->
  <input type="text" id="endereco">   <!-- Output: street (readonly visual) -->
  <input type="text" id="bairro">     <!-- Output: neighborhood -->
  <input type="text" id="cidade">     <!-- Output: city -->
  <input type="text" id="estado">     <!-- Output: state (UF) -->
  <input type="submit" onclick="CliqueBotao()"> <!-- Trigger search -->
  ```
- **Script Loading**: `<script src="App.js"></script>` in `<head>` (executes on load)

#### `App.js` — Core Logic Flow

```javascript
// 1. Event handler: button click
function CliqueBotao(){
    var cep = document.querySelector('#cep').value;  // Get CEP value
    BuscarDados(cep);  // Call async fetch function
}

// 2. Async API call via Fetch API
async function BuscarDados(cep){
    var dados = await fetch(`https://viacep.com.br/ws/${cep}/json/`)
        .then(x => x.json());  // Parse JSON response
    dadosNaTela(dados);  // Populate DOM with results
}

// 3. DOM update: fill form fields
function dadosNaTela(dados){
    document.querySelector('#endereco').value = dados.logradouro;
    document.querySelector('#bairro').value = dados.bairro;
    document.querySelector('#cidade').value = dados.localidade;
    document.querySelector('#estado').value = dados.uf;
}
```

#### `style.css` — Design System

```css
/* Reset and base typography */
* {
    padding: 0;
    margin: 0;
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
}

/* Centered layout with full viewport */
body {
    display: flex;
    height: 100vh;
    width: 100vw;
    align-items: center;
    justify-content: center;
    background-color: gray;
}

/* Form container styling */
.inputs {
    background-color: darkgray;
    display: flex;
    flex-direction: column;
    padding: 1rem;
    border-radius: 5px;
    margin: 0 auto;
}

/* Input field consistency */
.inputs input {
    margin: 5px;
    border-radius: 5px;
    border: none;
    outline: none;
    padding: 8px;
}

/* Submit button accent */
.inputs input.enviar {
    background-color: white;
    cursor: pointer;
    transition: background-color 0.2s;
}

.inputs input.enviar:hover {
    background-color: #e0e0e0;
}
```

### Request Flow Diagram

```
User enters CEP → Clicks "Enviar"
       ↓
CliqueBotao() reads #cep value
       ↓
BuscarDados(cep) calls ViaCEP API
       ↓
fetch() → HTTPS GET https://viacep.com.br/ws/XXXXX-XXX/json/
       ↓
API responds with JSON:
{
  "cep": "01001-000",
  "logradouro": "Praça da Sé",
  "bairro": "Sé",
  "localidade": "São Paulo",
  "uf": "SP",
  ...
}
       ↓
dadosNaTela(dados) updates DOM:
#endereco.value = "Praça da Sé"
#bairro.value = "Sé"
#cidade.value = "São Paulo"
#estado.value = "SP"
       ↓
User sees auto-filled form
```

### ViaCEP API Reference

| Endpoint | Method | Response Format | Rate Limit |
|----------|--------|----------------|------------|
| `https://viacep.com.br/ws/{cep}/json/` | GET | JSON | Undocumented (be respectful) |

**Success Response (200 OK)**:
```json
{
  "cep": "01001-000",
  "logradouro": "Praça da Sé",
  "complemento": "lado ímpar",
  "bairro": "Sé",
  "localidade": "São Paulo",
  "uf": "SP",
  "ibge": "3550308",
  "gia": "1004",
  "ddd": "11",
  "siafi": "7107"
}
```

**Error Response (CEP not found)**:
```json
{
  "erro": true
}
```

---

## 🔐 Environment Variables

**None required.** This is a fully static, client-side application with no backend, server-side rendering, or sensitive configuration.

> ⚠️ **Security Note**: The ViaCEP API is public and does not require authentication. However, avoid sending sensitive user data in URL parameters. This app only transmits the CEP (public information).

---

## ⚙️ Available Scripts

| Command | Description | Use Case |
|---------|-------------|----------|
| `python3 -m http.server 8000` | Start local dev server | Test without CORS/file:// restrictions |
| `npx serve .` | Alternative local server (Node) | Quick preview with clean URLs |
| `open index.html` | Open file directly in browser | Fastest local testing (may have fetch limitations) |
| `git add . && git commit -m "msg"` | Stage and commit changes | Version control workflow |
| `git push origin main` | Deploy to GitHub Pages | Trigger auto-deploy (if configured) |

### GitHub Pages Deployment Workflow

```bash
# 1. Ensure you're on the main branch
git checkout main

# 2. Commit your changes
git add .
git commit -m "feat: add error handling for invalid CEP"

# 3. Push to trigger deployment
git push origin main

# 4. Wait ~1-2 minutes, then visit:
# https://tyxiel.github.io/tyxiel-app_viacep/
```

> 🔄 **Auto-deploy**: GitHub Pages rebuilds automatically on push to `main`. No build step required.

---

## 🧪 Testing

### Manual Testing Checklist

```markdown
## Functional Tests
- [ ] Enter valid CEP `01001-000` → Fields fill correctly
- [ ] Enter invalid CEP `99999-999` → No crash, fields stay empty
- [ ] Enter malformed CEP `abc` → Graceful handling (no JS error)
- [ ] Click button multiple times rapidly → No duplicate requests (debounce recommended)
- [ ] Copy-paste CEP with hyphen `01001-000` → Works
- [ ] Copy-paste CEP without hyphen `01001000` → Works

## UI/UX Tests
- [ ] Layout centers on desktop (≥1024px)
- [ ] Layout adapts to mobile (≤480px) — inputs stack vertically
- [ ] Input fields have visible focus states
- [ ] Submit button has hover feedback
- [ ] Text is readable (contrast ratio ≥ 4.5:1)

## Network Tests
- [ ] App works offline? → No (requires API) — expected behavior
- [ ] Slow network: loading state? → No (improvement opportunity)
- [ ] API down: error message? → No (improvement opportunity)
```

### Automated Testing (Optional)

Since this is a simple static app, automated tests are optional. If desired:

```bash
# Install Playwright for E2E testing
npm init -y
npm install -D @playwright/test

# Create test: tests/cep-search.spec.js
import { test, expect } from '@playwright/test';

test('preenche campos com CEP válido', async ({ page }) => {
  await page.goto('http://localhost:8000');
  await page.fill('#cep', '01001-000');
  await page.click('.enviar');
  
  await expect(page.locator('#endereco')).toHaveValue('Praça da Sé');
  await expect(page.locator('#cidade')).toHaveValue('São Paulo');
  await expect(page.locator('#estado')).toHaveValue('SP');
});
```

### Accessibility Audit (Optional)

```bash
# Install Lighthouse CLI
npm install -g @lhci/cli

# Run audit
lhci autorun --collect.url=http://localhost:8000
```

Or use Chrome DevTools → Lighthouse tab → Generate report.

---

## 🌍 Deployment

### GitHub Pages (Recommended)

**Automatic Setup**:
1. Go to repo **Settings** → **Pages**
2. Set **Source** to `Deploy from branch`
3. Select branch: `main`, folder: `/ (root)`
4. Save → Wait for deployment URL

**No configuration files needed** — pure static site.

### Alternative: Netlify (Drag & Drop)

```bash
# 1. Build (no build step needed)
# 2. Drag the entire folder to Netlify Drop
# 3. Site is live instantly
```

### Alternative: Vercel

```bash
# Install Vercel CLI
npm i -g vercel

# Deploy
vercel --prod
```

### Alternative: Self-Hosted (Any Web Server)

```bash
# Copy files to your web root
cp -r tyxiel-app_viacep/* /var/www/html/cep-busca/

# Ensure web server serves .html, .css, .js with correct MIME types
# Apache/Nginx default configs usually handle this automatically
```

### Custom Domain (Optional)

1. Add `CNAME` file to repo root:
   ```
   cep.seudominio.com.br
   ```
2. Configure DNS with your registrar:
   ```
   Type: CNAME
   Name: cep
   Value: tyxiel.github.io
   ```

---

## 🔧 Troubleshooting

### ❌ "CORS error" or "fetch failed" when opening via `file://`

**Cause**: Browsers restrict `fetch()` calls from `file://` protocol for security.

**Solution**:
```bash
# Use a local server instead of direct file open
python3 -m http.server 8000
# Then visit http://localhost:8000
```

### ❌ Campos não preenchem com CEP válido

**Cause**: API ViaCEP retornou `{ "erro": true }` ou problema de rede.

**Solution**:
1. Verifique o formato do CEP (8 dígitos, com ou sem hífen)
2. Teste o CEP diretamente na API:  
   `https://viacep.com.br/ws/01001-000/json/`
3. Verifique console do navegador (F12 → Console) para erros de rede

### ❌ Layout quebrado no mobile

**Cause**: CSS não está sendo carregado ou cache antigo.

**Solution**:
```bash
# Hard refresh
Ctrl+F5 (Windows) / Cmd+Shift+R (macOS)

# Ou verifique o caminho do CSS no HTML:
<link rel="stylesheet" type="text/css" href="style.css">
# Deve estar relativo, não absoluto
```

### ❌ Botão "Enviar" não funciona

**Cause**: JavaScript não carregou ou erro de sintaxe.

**Solution**:
1. Abra o Console do Desenvolvedor (F12)
2. Verifique se há erros em vermelho
3. Confirme que `App.js` está sendo carregado (aba Network)
4. Teste a função manualmente no Console:
   ```javascript
   CliqueBotao(); // Deve ler o valor do #cep
   ```

### ❌ API ViaCEP fora do ar ou lenta

**Cause**: Serviço de terceiros indisponível ou sobrecarregado.

**Solution**:
1. Implemente cache local simples:
   ```javascript
   const cache = {};
   async function BuscarDados(cep){
       if (cache[cep]) {
           dadosNaTela(cache[cep]);
           return;
       }
       // ... fetch normal, depois:
       cache[cep] = dados;
   }
   ```
2. Adicione fallback ou mensagem de "Tente novamente mais tarde"

### ❌ CEP com hífen não funciona

**Cause**: API ViaCEP aceita ambos os formatos, mas validação prévia pode ajudar.

**Solution**:
```javascript
// Normalizar CEP antes de buscar
function normalizarCep(cep){
    return cep.replace(/\D/g, ''); // Remove tudo que não é dígito
}

// Em CliqueBotao():
var cepLimpo = normalizarCep(document.querySelector('#cep').value);
BuscarDados(cepLimpo);
```

---

## 🤝 Contributing

Contributions are welcome! This project follows the [GNU AGPL v3](LICENSE) license.

### How to Contribute

1. Fork the repository
2. Create a feature branch: `git checkout -b feat/add-cep-mask`
3. Commit changes: `git commit -m 'feat: add CEP input mask (XXX.XXX-XXX)'`
4. Push to branch: `git push origin feat/add-cep-mask`
5. Open a Pull Request

### Contribution Guidelines

- ✅ Keep changes focused and atomic (one feature/fix per PR)
- ✅ Test manually in at least 2 browsers before submitting
- ✅ Follow existing code style:
  - JS: No semicolons, `var` (legacy), functions declarations
  - CSS: No preprocessors, mobile-first approach
  - HTML: Semantic tags, `id` selectors for JS hooks
- ✅ Add Portuguese comments for new logic
- ✅ Update this README if adding user-facing features

### Suggested Improvements

```markdown
✨ Features
- [ ] Máscara de entrada para CEP (XXX.XXX-XXX)
- [ ] Validação em tempo real (formato, dígitos)
- [ ] Feedback visual de carregamento (spinner)
- [ ] Mensagens de erro amigáveis na UI
- [ ] Cache local de consultas recentes (localStorage)
- [ ] Botão "Limpar" para resetar o formulário
- [ ] Suporte a busca por endereço (reverse geocoding)

🔧 Technical
- [ ] Migrar `var` para `const`/`let` (ES6+)
- [ ] Adicionar tratamento de erros com try/catch
- [ ] Extrair seleção de elementos para constantes
- [ ] Adicionar testes unitários simples (Jest + jsdom)
- [ ] Configurar ESLint + Prettier para consistência

♿ Accessibility
- [ ] Adicionar `aria-live` para feedback de carregamento
- [ ] Garantir contraste de cores ≥ 4.5:1
- [ ] Adicionar labels visíveis ou `aria-label` em inputs
- [ ] Suporte a navegação por teclado (Enter no CEP)
```

### Reporting Issues

Use the [GitHub Issues](https://github.com/tyxiel/tyxiel-app_viacep/issues) tab with:

- 🐛 **Bug Report**: Steps to reproduce, browser/OS, CEP tested, expected vs actual
- 💡 **Feature Request**: Use case, proposed solution, priority (low/medium/high)
- ❓ **Question**: Clear description of what you're trying to achieve

---

## 📜 License

Distributed under the **GNU Affero General Public License v3.0**. See [`LICENSE`](LICENSE) for full text.

### What This Means

| You Can | You Must |
|---------|----------|
| ✅ Use commercially | 🔓 Disclose source code if modified and served over network |
| ✅ Modify and distribute | 🔗 Provide source to network users of modified version |
| ✅ Patent use | 📝 Include license and copyright notices |
| ✅ Private use | 🔄 Share improvements under same license |

> ℹ️ **AGPL Specific**: If you host a modified version on a server and users interact with it over a network (e.g., deploy to Vercel), you **must** make the source code of your modifications available to those users.

### Quick Start with License Compliance

```bash
# When forking/modifying:
# 1. Keep LICENSE file intact
# 2. Add your copyright to modified files:
// Copyright (C) 2026 Your Name

# 3. If deploying modified version publicly:
#    - Add a "Source" link in footer pointing to your fork
#    - Or include a modal with source code download option

# Example footer addition in index.html:
<footer>
  <small>
    Código fonte: 
    <a href="https://github.com/seu-usuario/tyxiel-app_viacep" target="_blank">
      GitHub
    </a>
    | Licença: AGPL-3.0
  </small>
</footer>
```

---

## 🙏 Acknowledgments

- [ViaCEP](https://viacep.com.br/) — For the free, reliable Brazilian CEP API
- [freeCodeCamp](https://www.freecodecamp.org/) — For foundational web development education
- [MDN Web Docs](https://developer.mozilla.org/) — For reliable JavaScript and Fetch API documentation
- [GitHub Pages](https://pages.github.com/) — For hassle-free static hosting

---

> 💡 **Pro Tip**: Always test with real Brazilian CEPs from different regions (SP, RJ, DF, AM) — some have quirks like missing neighborhoods or special characters in street names. When in doubt, check the raw API response in browser DevTools → Network tab.

*Built with ❤️ by [Tyxiel](https://github.com/tyxiel)*
