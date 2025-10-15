Crée le blueprint en json d'un **workflow n8n (v1.114+)** composé de 5 nœuds :

1. **Form node** en POST recevant un champ `password`.
2. **Set** contenant une variable `expectedPassword` = `"OpenSesame42"`.
3. **IF** comparant `{{$json["body"]["password"]}}` (depuis le webhook) avec `{{$json["expectedPassword"]}}` (du Set).
4. **Form Ending** sur la branche *true* :
   * Code 200
   * Type `text/html`
   * Corps : “✅ Accès autorisé ! Bienvenue dans la zone secrète.”
5. **Error** sur la branche *false* :
   * Code 401
   * Type `text/html`
   * Corps : “❌ Accès refusé. Mot de passe incorrect.”

Inclure les connexions entre nœuds, les expressions correctes, des commentaires d'expliction et un nom clair pour chaque nœud.
Résultat attendu : un JSON n8n complet prêt à importer.
