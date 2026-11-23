Voici l'ordre d'apprentissage recommandé pour les *Learning Paths* de PortSwigger, structuré pour progresser logiquement des fondamentaux vers les vecteurs d'attaques les plus récents et complexes.

### 1. Le point de départ (Niveau Apprentice)

C'est le seul parcours classé "Apprenti". Il est indispensable pour poser les bases avant d'attaquer les certifications.

* **Server-side vulnerabilities :** Vue d'ensemble des failles côté serveur pour comprendre la logique d'un attaquant dans un environnement réel.

### 2. Les classiques incontournables (Niveau Practitioner)

Ce sont les piliers de la sécurité web (souvent au sommet du Top 10 OWASP). Vous devez les maîtriser par cœur.

* **SQL injection :** La vulnérabilité historique et fondamentale pour extraire des données.
* **Authentication vulnerabilities :** Comprendre comment contourner les mécanismes de connexion et usurper des identités.
* **Path traversal :** Naviguer en dehors des répertoires prévus pour lire des fichiers sensibles du système.
* **File upload vulnerabilities :** Comment l'upload d'un simple fichier image peut mener à l'exécution de code à distance (RCE) et au contrôle du serveur.
* **Cross-site request forgery (CSRF) :** Forcer un utilisateur authentifié à exécuter des actions à son insu.

### 3. Architectures modernes et APIs

Une fois les bases acquises, passez aux vulnérabilités qui touchent les applications modernes, le Cloud et les micro-services.

* **API testing :** Apprendre à découvrir des paramètres cachés et la surface d'attaque non visible sur le front-end.
* **Server-side request forgery (SSRF) :** Failles extrêmement critiques aujourd'hui (surtout dans le Cloud) permettant de rebondir sur les réseaux internes.
* **Cross-origin resource sharing (CORS) :** Indispensable pour exploiter les mauvaises configurations de partage de ressources entre domaines.
* **NoSQL injection :** L'équivalent du SQLi mais pour les bases de données modernes comme MongoDB.
* **GraphQL API vulnerabilities :** Exploiter les endpoints GraphQL, de plus en plus utilisés pour remplacer les API REST classiques.

### 4. Mécaniques complexes et logiques avancées

Ces chemins demandent une compréhension plus pointue de l'infrastructure web et du comportement des navigateurs.

* **Clickjacking (UI redressing) :** Manipulation de l'interface client pour voler des clics.
* **WebSockets vulnerabilities :** Détecter et exploiter les failles dans les communications temps réel.
* **Prototype pollution :** Attaques très spécifiques à l'écosystème JavaScript / Node.js.
* **Race conditions :** Exploitation de failles logiques très avancées basées sur la concurrence et les millisecondes (nécessite l'extension *Turbo Intruder*).
* **Web cache deception :** Manipulation des serveurs de cache (CDN, reverse proxies) pour voler des données de session.

### 5. Les nouvelles frontières

* **Web LLM attacks :** Le parcours le plus récent. À garder pour la fin, car il se concentre sur l'exploitation et le vol de données via les modèles d'Intelligence Artificielle (LLMs) intégrés aux applications web.
