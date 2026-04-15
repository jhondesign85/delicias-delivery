DELÍCIAS DELIVERY - SITE HÍBRIDO LOCAL + FIREBASE

Arquivos:
- index.html
- README.txt

==================================================
COMO FUNCIONA
==================================================

1. MODO LOCAL
- O site funciona sem Firebase.
- Os dados ficam salvos no navegador/celular via localStorage.
- Serve para testar rápido ou usar em apenas um aparelho.

2. MODO FIREBASE
- Depois de preencher a CONFIG no painel admin, o site pode sincronizar:
  - produtos
  - preços
  - imagens dos itens
  - banner
  - logo/banner
  - WhatsApp
- Assim, todos que abrirem o site verão os mesmos dados.

==================================================
LOGIN ADMIN
==================================================

Usuário: leane
Senha: 060923

Observação importante:
Como este projeto está em HTML puro no front-end, esse login é apenas visual/local.
Para segurança real de produção, o ideal é usar Firebase Authentication e regras no Firestore.

==================================================
ITENS INICIAIS
==================================================

- Arroz com Galinha
- Vatapá
- Lasanha
- Torta Salgada
- Refrigerante

Todos os itens já vêm com imagem inicial.

==================================================
COMO USAR
==================================================

1. Abra o arquivo index.html no navegador.
2. Toque em "Admin".
3. Entre com:
   - usuário: leane
   - senha: 060923
4. Edite:
   - logo/banner
   - WhatsApp
   - banner
   - produtos, preços e imagens
5. Clique em "Salvar dados" para usar localmente.
6. Clique em "Salvar e sincronizar" para enviar ao Firebase.

==================================================
IMAGENS E LOGO
==================================================

- Cada produto tem um campo de URL da imagem no painel admin.
- A logo do topo também usa um campo de URL.
- Você pode usar links de imagens públicas da internet.
- Se quiser algo mais profissional, pode hospedar as imagens no Cloudinary ou no Firebase Storage.

==================================================
COMO CONFIGURAR FIREBASE
==================================================

1. Crie um projeto no Firebase.
2. Ative o Firestore Database.
3. Vá em Configurações do projeto.
4. Adicione um app Web.
5. Copie os dados de configuração.
6. No painel admin do site, preencha:
   - apiKey
   - authDomain
   - projectId
   - storageBucket
   - messagingSenderId
   - appId
7. Salve a configuração Firebase.
8. Depois clique em "Sincronizar" ou "Salvar e sincronizar".

==================================================
ESTRUTURA USADA NO FIRESTORE
==================================================

Coleção:
- delivery_data

Documento:
- app

==================================================
REGRAS DE TESTE DO FIRESTORE
==================================================

Para testes simples, você pode usar regras temporárias como estas:

rules_version = '2';
service cloud.firestore {
  match /databases/{database}/documents {
    match /delivery_data/{document=**} {
      allow read, write: if true;
    }
  }
}

ATENÇÃO:
Essas regras são abertas e servem só para teste.
Para colocar no ar de verdade, proteja com autenticação.

==================================================
VISUAL
==================================================

- Site pensado para celular
- Cores em roxo claro e escuro
- Layout moderno e simples
- Cards com imagem dos produtos
- Banner superior com área para logo
- Botão direto para pedido no WhatsApp

==================================================
PUBLICAR
==================================================

Você pode publicar este index.html em:
- Netlify
- Firebase Hosting
- Vercel
- qualquer hospedagem estática

Se quiser, basta enviar o arquivo index.html.
