# Controle diário de inadimplência

Dashboard de uma página (HTML + Chart.js) com 7 cidades e 5 faixas de parcelas vencidas. Versão zerada: você lança os dias pelo próprio app.

## Arquivos
- `index.html`: o app inteiro.
- `firestore.rules`: regras de segurança do banco (Firebase).

## Dois modos de uso

**Modo local (padrão):** `FIREBASE_CONFIG = null`. Funciona sem configurar nada, mas os dados lançados ficam só no navegador de quem lançou. A gerência não vê.

**Modo compartilhado:** com o Firebase configurado, você faz login, lança o dia e a gerência vê a atualização ao abrir o mesmo link.

## Publicar no GitHub Pages
1. Crie um repositório e envie `index.html`, `firestore.rules` e este `README.md`.
2. Em **Settings → Pages**, escolha **Deploy from a branch**, branch `main`, pasta `/ (root)`.
3. O endereço será `https://SEU-USUARIO.github.io/NOME-DO-REPOSITORIO/`.

## Ativar o modo compartilhado (Firebase, plano gratuito)
1. Em https://console.firebase.google.com, crie um projeto.
2. **Build → Firestore Database → Criar banco** (modo produção).
3. Aba **Regras**: cole o conteúdo de `firestore.rules` e publique.
4. **Build → Authentication → Método de login**: ative **E-mail/senha**. Em **Usuários**, adicione o seu e-mail e uma senha.
5. Em **Authentication → Configurações → Domínios autorizados**, adicione `SEU-USUARIO.github.io`.
6. **Configurações do projeto → Seus apps → Web (</>)**: registre o app e copie o objeto `firebaseConfig`.
7. No `index.html`, troque `const FIREBASE_CONFIG=null;` por `const FIREBASE_CONFIG={ ...cole aqui... };` e envie de novo ao GitHub.

A configuração do Firebase não é segredo: quem protege os dados são as regras do passo 3.

## Privacidade (importante)
- O GitHub Pages é público: qualquer pessoa com o link abre o dashboard, e em repositório público o código fica visível.
- Esta versão começa **sem nenhum dado** dentro do código. Em modo compartilhado, os números ficam no Firebase e não no repositório.
- Em modo local, os dados ficam só no navegador de quem lançou.
- O arquivo tem `noindex`, então buscadores não devem listar a página, mas isso não impede o acesso por quem tem o link.
- Se a gerência também precisar de login para ver, use `allow read: if request.auth != null;` nas regras e crie um usuário para cada pessoa.

## Datas aceitas
O app aceita datas de `MIN` (no `index.html`, hoje `2026-10-01`) até amanhã. Para começar em outra data, mude a constante `MIN`.

## Apagar ou corrigir dados
- Para corrigir um dia, escolha a data, edite os valores e clique em **Salvar dia** (ele pede confirmação).
- Modo local: limpe os dados do site no navegador (chave `inadimp2026`).
- Modo compartilhado: exclua o documento da data em Firestore Database → coleção `dias` no Console do Firebase.

## Uso diário
1. Abra o link e entre com e-mail e senha.
2. Em **Lançar dados do dia**, a data já vem no dia seguinte ao último lançado. Preencha as 35 células e clique em **Salvar dia**.
3. Compartilhe o link com a gerência.
