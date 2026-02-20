# Landing Page Estática

Projeto de landing page estática com foco em SEO e segurança. Sem dependências externas, sem backend.

## 📁 Estrutura do Projeto

```
/
├── index.html              # Página principal com SEO completo
├── robots.txt              # Configuração para search engines
├── sitemap.xml             # Mapa do site
├── manifest.webmanifest    # PWA manifest
├── .gitignore              # Arquivos ignorados pelo Git
├── README.md               # Este arquivo
├── assets/
│   ├── css/
│   │   └── style.css       # Estilos CSS (CSS Grid, Flexbox)
│   ├── js/
│   │   └── main.js         # JavaScript principal
│   ├── img/                # Imagens (JPG, PNG, SVG, WebP)
│   └── fonts/              # Fontes locais (opcional)
└── favicon/                # Ícones do site
    ├── favicon.ico
    ├── apple-touch-icon.png
    ├── icon-192x192.png
    ├── icon-512x512.png
    └── icon-maskable.png
```

## 🚀 Como Começar

### 1. Clonar o repositório
```bash
git clone <seu-repositorio>
cd PersonalLP
```

### 2. Estrutura de desenvolvimento
A página está pronta para edição. Substitua os comentários `<!-- COLE SEU CONTEÚDO AQUI -->` pelo seu HTML.

### 3. Personalizar
- **index.html**: Atualize as meta tags, title, description, Open Graph, Twitter Card
- **assets/css/style.css**: Atualize cores, tipografia, layout conforme seu design
- **assets/js/main.js**: Adicione suas funkcionalidades (scroll, eventos, etc)

## 🔍 SEO - Checklist

- [x] Title e meta description (placeholder)
- [x] Canonical URL
- [x] Open Graph meta tags
- [x] Twitter Card meta tags
- [x] Idioma (pt-BR) definido
- [x] Viewport meta tag
- [x] Charset UTF-8
- [x] Estrutura semântica (header, main, section, footer)
- [x] Um único H1 na página
- [x] robots.txt
- [x] sitemap.xml
- [ ] Gerar favicons e colocá-los em `/favicon/`
- [ ] Atualizar URLs canônicas com seu domínio real
- [ ] Substituir placeholders de meta tags

## 🔐 Segurança - Headers de Segurança

Os headers abaixo **DEVEM ser configurados no seu provedor** (Netlify, Vercel, Cloudflare, etc):

### Content-Security-Policy (CSP)
Para landing page estática **sem scripts externos**:
```
default-src 'self'; 
script-src 'self'; 
style-src 'self' 'unsafe-inline'; 
img-src 'self' data: https:; 
font-src 'self'; 
connect-src 'self'
```

**Se usar Google Fonts ou Analytics**, afrouxe assim:
```
default-src 'self'; 
script-src 'self' https://cdn.jsdelivr.net https://www.googletagmanager.com https://www.google-analytics.com; 
style-src 'self' 'unsafe-inline' https://fonts.googleapis.com; 
font-src 'self' https://fonts.gstatic.com; 
img-src 'self' data: https:; 
connect-src 'self' https://www.google-analytics.com
```

### Outros Headers
- **X-Frame-Options**: `SAMEORIGIN` (previne clickjacking)
- **X-Content-Type-Options**: `nosniff` (previne MIME sniffing)
- **Referrer-Policy**: `strict-origin-when-cross-origin` (controla referrer)
- **Permissions-Policy**: `geolocation=(), microphone=(), camera=(), payment=()` (desativa features não necessárias)
- **Strict-Transport-Security**: `max-age=31536000; includeSubDomains; preload` (force HTTPS)

### Configuração por Provedor

#### 🔷 **Netlify** (netlify.toml)
```toml
[[headers]]
  for = "/*"
  [headers.values]
    X-Frame-Options = "SAMEORIGIN"
    X-Content-Type-Options = "nosniff"
    Referrer-Policy = "strict-origin-when-cross-origin"
    Permissions-Policy = "geolocation=(), microphone=(), camera=(), payment=()"
    Strict-Transport-Security = "max-age=31536000; includeSubDomains; preload"
    Content-Security-Policy = "default-src 'self'; script-src 'self'; style-src 'self' 'unsafe-inline'; img-src 'self' data: https:; font-src 'self'; connect-src 'self'"
```

#### 🔶 **Vercel** (vercel.json)
```json
{
  "headers": [
    {
      "source": "/(.*)",
      "headers": [
        { "key": "X-Frame-Options", "value": "SAMEORIGIN" },
        { "key": "X-Content-Type-Options", "value": "nosniff" },
        { "key": "Referrer-Policy", "value": "strict-origin-when-cross-origin" },
        { "key": "Permissions-Policy", "value": "geolocation=(), microphone=(), camera=(), payment=()" },
        { "key": "Strict-Transport-Security", "value": "max-age=31536000; includeSubDomains; preload" },
        { "key": "Content-Security-Policy", "value": "default-src 'self'; script-src 'self'; style-src 'self' 'unsafe-inline'; img-src 'self' data: https:; font-src 'self'; connect-src 'self'" }
      ]
    }
  ]
}
```

#### ☁️ **Cloudflare**
- **Opção 1**: Dashboard → Security → Headers (visual)
- **Opção 2**: Cloudflare Worker para mais controle:
```javascript
export default {
  async fetch(request) {
    const response = await fetch(request);
    const newResponse = new Response(response.body, response);
    newResponse.headers.set('X-Frame-Options', 'SAMEORIGIN');
    newResponse.headers.set('X-Content-Type-Options', 'nosniff');
    newResponse.headers.set('Content-Security-Policy', "default-src 'self'; ...");
    return newResponse;
  }
}
```

## 🎨 Customização

### Cores
No `assets/css/style.css`, modifique as variáveis CSS:
```css
:root {
  --color-primary: #007bff;
  --color-secondary: #6c757d;
  --color-background: #ffffff;
  --color-text: #212529;
}
```

### Tipografia
```css
:root {
  --font-family-base: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
  --font-size-base: 16px;
}
```

### Responsividade
O CSS já inclui breakpoints:
- Mobile: < 576px
- Tablet: < 768px
- Desktop: >= 992px

## 📱 PWA (Progressive Web App)

O projeto inclui `manifest.webmanifest` para instalação como app nativa. Você precisa:

1. Gerar ícones em `/favicon/`:
   - favicon.ico (32x32)
   - apple-touch-icon.png (180x180)
   - icon-192x192.png (para Android)
   - icon-512x512.png (para Android splash)
   - icon-maskable.png (192x192, para Android Adaptive Icons)
   - Opcionais: screenshots (540x720 e 1280x720)

[Usar gerador online](https://realfavicongenerator.net/)

## 🚀 Deploy

### Netlify
```bash
npm i -g netlify-cli
netlify deploy --prod
```

### Vercel
```bash
npm i -g vercel
vercel --prod
```

### GitHub Pages
```bash
git push origin main
# Enable GitHub Pages nas Settings do repositório
```

### Cloudflare Pages
1. Conecte seu repositório Git
2. Cloudflare Pages detectará automaticamente

## ✅ Boas Practices

- ✅ HTML semântico
- ✅ CSS responsivo (mobile-first)
- ✅ AccessibilityHTML (WCAG 2.1)
- ✅ Meta tags SEO completas
- ✅ Headers de segurança configuráveis
- ✅ PWA ready
- ✅ Sem dependências externas
- ✅ Sem backend
- ✅ Performance otimizada

## 📝 Licença

MIT - Use livremente

## 📧 Suporte

Para mais informações sobre SEO e segurança:
- [Google Search Central](https://search.google.com/search-console)
- [Mozilla MDN Web Docs](https://developer.mozilla.org/)
- [OWASP Security Headers](https://owasp.org/www-project-secure-headers/)
