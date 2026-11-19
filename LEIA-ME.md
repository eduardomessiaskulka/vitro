# Site do Vitro

Páginas estáticas que os apps abrem no navegador. Hoje só tem `apoie/`, a página do "Apoie o criador".
A política de privacidade que a Store exige (veja `PUBLICAR-NA-STORE.md`, seção 4.2) pode morar aqui também.

## Página de apoio (`apoie/`)

O item "Apoie o criador" (menu da bandeja, painel de Ajustes e o aviso único) abre
`<PAGINA>?app=<id>&lang=<idioma>`. A página agradece pelo app certo, usa o idioma do app e mostra:

- **Pix**: QR Code e "copia e cola" gerados a partir da chave, sem valor fixo (quem paga escolhe). Vem primeiro em português.
- **Ko-fi** e **PayPal**: para quem está fora do Brasil. Vêm primeiro nos outros idiomas.

Forma sem dados no `config.js` não aparece. Sem nenhuma, a página diz que o apoio está sendo configurado.

### Antes de publicar

1. Crie as contas que for usar:
   - **Pix**: crie uma **chave aleatória** no app do banco. Ela fica dentro do QR Code e a página é pública,
     então é melhor não usar e-mail, celular nem CPF.
   - **Ko-fi** (ko-fi.com): não cobra taxa sobre doações; só o PayPal ou o Stripe cobram a deles. Conecte o PayPal
     para receber. Confira se o Stripe aceita conta do Brasil antes de contar com ele.
   - **PayPal.me** (opcional): paypal.me/<usuário>.
2. Preencha `apoie/config.js` (chave Pix, nome e cidade como no banco, usuário do Ko-fi e do PayPal).
3. Abra `apoie/index.html?lang=pt-BR&app=tasks` no navegador e pague um Pix de R$ 0,01 para você mesmo pelo QR Code,
   para ter certeza de que o código funciona no seu banco.

### Publicar no GitHub Pages (grátis)

1. Crie um repositório público, por exemplo `vitro`, e envie o conteúdo desta pasta `site/` para a raiz dele.
2. No repositório: Settings > Pages > Source: "Deploy from a branch", branch `main`, pasta `/ (root)`.
3. Em alguns minutos a página fica em `https://<seu-usuario>.github.io/vitro/apoie/`.
4. Ponha esse endereço em `PAGINA`, em `nucleo/src/apoio.rs`, e compile os apps de novo.
   O `empacotar-msix.js` recusa gerar pacotes enquanto `PAGINA` for o endereço de exemplo.

Depois disso, trocar a chave Pix ou o Ko-fi é só editar `config.js` e enviar de novo: os apps não mudam.

### Regras da Microsoft Store

- A doação **não pode liberar nada** no app (recurso, tema, tirar aviso, selo de apoiador). Só assim ela pode
  passar por Pix, Ko-fi ou PayPal (política 10.8.2). Se um dia liberar algo, tem que virar complemento da Store.
- Em cada envio, escreva nas **Notas para certificação** que o app tem um link opcional de doação para um site
  externo (Ko-fi, PayPal ou Pix) e que a doação não libera nada no app.

### Arquivos

- `apoie/index.html`: a página (textos nos 8 idiomas do Vitro, tema claro e escuro, cabe em celular).
- `apoie/config.js`: as formas de apoio.
- `apoie/qrcode.js`: [qrcode-generator](https://github.com/kazuhikoarase/qrcode-generator) 1.4.4 (licença MIT), copiado
  para a página não depender de outro site.
- `apoie/icones/`: ícones de 128 px de cada app (de `nucleo/icones/<id>/128.png`).
