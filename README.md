# JosueSantosTech — Site de vídeos com IA

Versão completa atualizada em 9 de outubro de 2026.

Inclui vídeos com áudio e controles de volume, reprodução automática ao entrar na tela, preços recolhidos com botão Ver investimento, landing pages e sites como serviços, pacotes sob medida, links do Instagram e briefing enviado por e-mail. A confirmação de envio aparece em destaque e o formulário permanece habilitado.

Não foram adicionados depoimentos fictícios. O contato por WhatsApp depende do fornecimento do número pelo proprietário; os botões de conversa atuais direcionam ao Instagram.

Código-fonte da página de vendas, com vídeos, reprodução automática ao entrar na tela, controles de áudio, pacotes, Instagram e formulário de briefing.

## Subir no GitHub

1. Extraia este ZIP.
2. Crie um repositório no GitHub.
3. Envie o conteúdo da pasta `josuesantostech` para a raiz do repositório, preservando as subpastas e os arquivos ocultos `.gitignore`, `.npmrc` e `.openai/hosting.json`.
4. Não envie o ZIP como substituto do código: envie os arquivos extraídos. Para muitos arquivos, prefira Git ou GitHub Desktop.

Pelo terminal, dentro da pasta extraída:

```sh
git init
git add .
git commit -m "Site JosueSantosTech"
git branch -M main
git remote add origin URL_DO_SEU_REPOSITORIO
git push -u origin main
```

Substitua `URL_DO_SEU_REPOSITORIO` pelo endereço do repositório que você criar.

## Executar localmente

Requer Node.js 22.13 ou superior e npm.

```sh
npm run install:ci
npm run dev
```

Abra o endereço informado no terminal. Para gerar a versão de produção:

```sh
npm run build
```

## Formulário e hospedagem

Este projeto usa React, Vinext e um servidor compatível com Cloudflare Workers. Os briefings são gravados em Cloudflare D1, no binding `DB`.

O GitHub armazena o código. O GitHub Pages, sozinho, não executa este servidor e não salva o formulário. Para hospedar fora do site atual, configure uma implantação compatível com Workers, o banco D1 e as migrações da pasta `drizzle`. Subir os arquivos no GitHub não altera automaticamente o site atual.

A configuração `.openai/hosting.json` preserva a identidade do site existente. Não contém senha ou token. Ao criar uma implantação independente, sua configuração de hospedagem e os bindings precisarão ser ajustados.

Para testar o banco apenas localmente, depois de `npm run build`:

```sh
node --import ./scripts/sites-env.mjs ./node_modules/wrangler/bin/wrangler.js d1 execute DB --local --config dist/server/wrangler.json --persist-to .wrangler/state --file drizzle/0000_narrow_shotgun.sql
npm start
```

Aplique cada migração apenas uma vez em um banco local novo.

## Onde editar

- `app/page.tsx`: textos, serviços, preços e links.
- `app/globals.css`: cores, layout e adaptação para celular.
- `app/video-player.tsx`: reprodução automática e controles de áudio.
- `app/cinema.tsx`: passagem cinematográfica durante a rolagem.
- `app/briefing.tsx`: formulário.
- `app/api/briefing/route.ts`: validação e recebimento do briefing.
- `db/` e `drizzle/`: estrutura e acesso ao banco.
- `public/media/`: vídeos e imagens.

## Conteúdo do pacote

Inclui o código-fonte, mídias, dependências declaradas e migrações. Não inclui `node_modules`, histórico Git, credenciais, arquivos de ambiente, cache ou dados de clientes.

Os vídeos iniciam sem som pelas regras de reprodução dos navegadores. O visitante pode ativar o áudio. Preferências de movimento reduzido são respeitadas.

O briefing é salvo no banco e encaminhado pelo FormSubmit para josuedesigner04@gmail.com. O endereço foi ativado pelo proprietário e o serviço aceitou o teste de envio. Uma hospedagem em novo domínio pode exigir nova confirmação. A aceitação pelo serviço não comprova entrega na caixa de entrada. Falhas de envio não removem o briefing salvo. O encaminhamento usa lib/briefing-email.ts; ao mudar o domínio, revise o Referer desse arquivo e confirme eventual nova ativação. Não há integração de notificações por WhatsApp.


## Publicação e acesso

O ZIP contém o código para um repositório GitHub. Não contém credenciais, dados de clientes ou banco de produção. A publicação atual no Sites mantém acesso privado. Subir o código no GitHub não muda o acesso ao site nem publica automaticamente uma nova hospedagem.

Ajuste o destino de e-mail e o domínio de referência em `lib/briefing-email.ts` ao migrar. A configuração `.openai/hosting.json` identifica o site existente; não é uma configuração de GitHub Pages.
