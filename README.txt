Delícias Delivery - Firebase + Cloudinary

Arquivos:
- index.html
- README.txt

Antes de publicar:
1. Abra o arquivo HTML.
2. Procure a constante CONFIG.
3. Cole:
   - firebase.apiKey
   - firebase.authDomain
   - firebase.projectId
   - firebase.storageBucket
   - firebase.messagingSenderId
   - firebase.appId
   - cloudinary.cloudName
   - cloudinary.uploadPreset

Cloudinary:
- Crie um upload preset unsigned.

Firebase:
- Ative o Cloud Firestore.
- Crie as coleções/documentos automaticamente pelo site.
- Regras de produção devem ser configuradas no Firebase.

Publicação:
- Renomeie o HTML para index.html
- Netlify:
  - Base directory: vazio
  - Build command: vazio
  - Publish directory: .

Login admin do frontend:
- usuário: leane
- senha: 060923
