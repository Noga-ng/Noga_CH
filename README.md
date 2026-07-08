# Noga_CH

Client HTTP léger en TypeScript/JavaScript fourni sous forme de fichier unique (Noga_Http.ts / Noga_Http.js). Fournit un singleton `http` avec gestion des timeouts, retries, cache GET, interceptors et support d'AbortSignal.

## Prérequis
- Node.js 18+ (fetch, AbortController et structuredClone natifs) ou un navigateur moderne
- Si vous utilisez Node < 18, polyfill `fetch`, `AbortController` et `structuredClone` ou build pour le navigateur.

## Installation
Cloner le dépôt et importer le fichier dans votre projet :

```bash
git clone https://github.com/Noga-ng/Noga_CH.git
cd Noga_CH
```

Il n'y a pas de package.json ni d'installation npm dans ce dépôt ; importez directement `Noga_Http.ts` (TypeScript) ou `Noga_Http.js` (JavaScript) dans votre projet.

## Usage
Exemples d'utilisation simples :

- En JavaScript (ESM) :
```js
import http from './Noga_Http.js';

async function main() {
  try {
    const res = await http.get('/api/users', { cache: true });
    if (res.ok) console.log(res.data);
    else console.error('Erreur', res.status, res.data);
  } catch (e) {
    console.error('Requête échouée', e);
  }
}

main();
```

- En TypeScript :
```ts
import http from './Noga_Http';

(async () => {
  const r = await http.post('/api/login', { username: 'u', password: 'p' });
  console.log(r);
})();
```

## API rapide
- `http.get<T>(link, opts?)` — GET (opts: cache, timeout, retries, signal, expectJson...)
- `http.post<T>(link, data, opts?)` — POST
- `http.put<T>(link, data, opts?)` — PUT
- `http.delete<T>(link, data?, opts?)` — DELETE
- `http.setBaseUrl(url)` — définir la base pour tous les appels
- `http.setToken(token)` — ajouter automatiquement l'en-tête Authorization
- `http.useReq(interceptor)` — ajouter un intercepteur de requête
- `http.useRes(interceptor)` — ajouter un intercepteur de réponse
- `http.clearCache()` — vider le cache GET

Les options de requête supportées (extraits) : `link`, `method`, `data`, `headers`, `timeout`, `retries`, `retryDelay`, `cache`, `signal`, `expectJson`.

## Notes
- Le client ne dépend d'aucune librairie externe ; il utilise l'API Fetch native.
- Le code TypeScript est fourni (Noga_Http.ts) ainsi que la version compilée JS (Noga_Http.js).
- Si tu veux, je peux :
  - ajouter un package.json avec des scripts (build/test),
  - ajouter des exemples plus complets ou des tests unitaires,
  - publier le paquet sur npm.

## Licence
À préciser (ex : MIT).
