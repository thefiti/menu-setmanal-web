# Menú Setmanal — web pública

Còpia de la mateixa app que tens com a Claude Artifact, pensada per publicar-se
a GitHub Pages i funcionar sense necessitat d'iniciar sessió a Claude.
Fa servir Firebase (Firestore + Storage) com a base de dades.

No està connectada encara a cap projecte Firebase real — `firebase-config.js`
no existeix fins que el crees (pas 2 d'aquí sota).

## Posada en marxa

1. **Firebase**
   - Crea un projecte a https://console.firebase.google.com
   - Activa **Firestore Database** (mode producció) i **Storage**.
   - A "Configuració del projecte" → "Els teus apps" → afegeix una app Web (`</>`).
   - A "Firestore Database" → pestanya "Regles", enganxa el contingut de
     `firestore.rules` d'aquesta carpeta i publica-ho.
   - A "Storage" → pestanya "Regles", enganxa el contingut de `storage.rules`
     i publica-ho.

2. **Configuració local**
   - Copia `firebase-config.example.js` com a `firebase-config.js`.
   - Enganxa-hi els valors reals que et dona la consola de Firebase.

3. **Provar en local**
   - Obre `index.html` directament al navegador (o amb un servidor estàtic
     qualsevol, p. ex. `npx serve`).
   - La primera vegada estarà buit: cal migrar les dades (pas 5).

4. **Publicar a GitHub Pages**
   - Crea un repositori nou (públic) i puja-hi tot el contingut d'aquesta
     carpeta (`git init`, `git add .`, `git commit`, `git push`).
   - A la configuració del repositori → "Pages" → activa-ho des de la branca
     principal, carpeta arrel.
   - La URL pública quedarà del tipus `https://<el-teu-usuari>.github.io/<repo>/`.

5. **Migrar les dades actuals de l'Artifact de Claude**
   - Això ho fa Claude: demana-li que copiï les receptes, el menú i la llista
     de la compra actuals cap a aquest Firebase.

6. **Tasca pont (sincronització bidireccional)**
   - Un cop migrat, Claude pot crear una tasca programada que cada 5 minuts
     copiï els canvis nous en tots dos sentits entre l'Artifact de Claude i
     aquest Firebase. Necessitarà la clau del compte de servei (pas següent).

## Compte de servei (només per a la tasca pont de sincronització)

Aquesta clau dona accés total d'escriptura al projecte — **no es puja mai a
git** (ja està al `.gitignore`), i Claude no l'exposa enlloc, només la fa
servir localment des de la tasca programada.

- Consola de Firebase → "Configuració del projecte" → "Comptes de servei" →
  "Generar nova clau privada".
- Guarda el `.json` descarregat en una carpeta d'aquest ordinador (fora
  d'aquest repositori, o dins seguint que el `.gitignore` el cobreix) i dona
  la ruta a Claude.
