# Nunes Aquaworks — Website

Site institucional da **Nunes Aquaworks** — venda, instalação e manutenção de
equipamentos de piscina no Algarve. Site estático (HTML/CSS/JS), sem backend:
os pedidos de orçamento são encaminhados para WhatsApp através de um *deep link*.

## Estrutura

```
index.html              Página única (todas as secções)
app.js                  Comportamento: header, menu, idioma PT/EN, formulário→WhatsApp
manifest.webmanifest    Metadados PWA (ícone, nome, cores)
brand/                  Logótipo e ícones (gerados a partir do PDF da marca)
```

## Segurança

O site foi preparado como site estático seguro:

- **Content-Security-Policy** restritiva (`script-src 'self'`) — só corre JavaScript
  próprio; sem scripts remotos nem `eval`.
- **Sem dependências externas em runtime** — removido todo o scaffolding do editor
  (React/Babel via CDN) que existia na versão original.
- Todos os links externos usam `rel="noopener noreferrer"` e `referrer-policy`
  restritiva; imagens externas carregadas com `referrerpolicy="no-referrer"`.
- Email de contacto em `mailto:` direto (substituiu a ofuscação Cloudflare, que
  só funcionava atrás da Cloudflare).
- O formulário não envia nem guarda dados — abre o WhatsApp com a mensagem
  pré-preenchida.

> Nota: alguns controlos (ex.: `X-Frame-Options`, `Strict-Transport-Security`)
> só podem ser definidos por cabeçalhos de servidor. O GitHub Pages serve sempre
> por HTTPS, mas não permite cabeçalhos personalizados — para os adicionar, usar
> um host com configuração de cabeçalhos (ex.: Cloudflare Pages / Netlify).

## Publicar (GitHub Pages)

1. `Settings → Pages`
2. **Source:** `Deploy from a branch`
3. **Branch:** `main` / `/ (root)` → `Save`

O site fica disponível em `https://manuelmarrao0887.github.io/nunesaquaworks/`.

## Desenvolvimento local

É um site estático — basta servir a pasta:

```bash
python3 -m http.server 8000
# abrir http://localhost:8000
```

## Por preencher (`[CONFIRMAR: …]`)

Antes de divulgar publicamente, substituir os marcadores no `index.html`:

- Prazo de resposta ("Resposta em …")
- Marcas de equipamento representadas (+ logótipos na secção *Marcas*)
- Prazo de garantia de instalação
- Anos de atividade ("no Algarve desde …")
- Intervalo de preços do plano de manutenção
- Outros idiomas atendidos
- NIF e morada (rodapé)
- Testemunhos reais (os atuais são exemplos)
