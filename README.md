# Gestão de mesas — projeto Android

App de mesas com administrador e garçons. Todos os aparelhos compartilham as mesmas mesas em tempo real, usando o Firebase (plano gratuito).

## 1. Criar o banco (Firebase)
1. Acesse console.firebase.google.com e crie um projeto.
2. Em "Adicionar app", escolha **Web** (`</>`) e copie o `firebaseConfig`.
3. Cole os valores em `www/firebase-config.js`.
4. Em **Build > Firestore Database**, crie o banco (escolha a região mais próxima).
5. Na aba **Regras**, cole o conteúdo de `firestore.rules` e publique.

## 2. Gerar o APK
Requisitos: Node 18 ou mais novo e Android Studio.

```
npm install
npx cap add android
npx cap sync android
npx cap open android
```

No Android Studio: **Build > Build Bundle(s) / APK(s) > Build APK(s)**.
O arquivo fica em `android/app/build/outputs/apk/debug/app-debug.apk`. Envie para os celulares e permita a instalação de fontes desconhecidas.

## 3. Primeiro uso
Entre como **Administrador** com o PIN inicial **1234**, troque o PIN na aba Garçons e cadastre os garçons. As mesas e os produtos de exemplo são criados automaticamente na primeira abertura.

## Limitações
- O app precisa de internet para abrir (o Firebase é carregado da internet). Depois de aberto, pedidos feitos sem sinal são enviados quando a conexão volta.
- As regras acima deixam o banco aberto: quem tiver a configuração do Firebase consegue ler e gravar, inclusive os PINs. Serve para uso interno e testes; para uso sério, o próximo passo é ligar o Firebase Authentication.
- Se dois administradores editarem garçons ou produtos ao mesmo tempo, vale a última alteração. Os pedidos das mesas não sofrem isso.
