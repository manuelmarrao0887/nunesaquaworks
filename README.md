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

- **Cabeçalhos de segurança** (via [`vercel.json`](vercel.json)): `Content-Security-Policy`,
  `Strict-Transport-Security` (HSTS), `X-Frame-Options: DENY`, `X-Content-Type-Options: nosniff`,
  `Referrer-Policy` e `Permissions-Policy`. Definidos a nível de servidor pela Vercel.

## Publicar (Vercel)

O site está alojado na **Vercel** com domínio `www.nunesaquaworks.com` (apex
`nunesaquaworks.com` redireciona para `www`). A Vercel publica automaticamente
a cada `git push` para `main`. Os cabeçalhos de segurança são aplicados pelo
[`vercel.json`](vercel.json).

> O certificado é Let's Encrypt, renovado automaticamente pela Vercel. Logo após
> ligar o domínio, o browser pode mostrar "Não seguro" durante alguns minutos
> enquanto o DNS e o certificado propagam — depois disso fica com cadeado.

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
