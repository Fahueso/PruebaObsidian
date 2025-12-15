# Limpieza de commits


Esto deja deja todos como está en tu rama main, pero elimina todo el histórico de commits

```bash
# 1. Asegúrate de estar en main
git checkout main

# 2. Crear una rama temporal sin historial
git checkout --orphan temp

# 3. Añadir todos los archivos
git add .

# 4. Crear un commit inicial limpio
git commit -m "initial clean commit"

# 5. Borrar la rama main antigua
git branch -D main

# 6. Renombrar temp → main
git branch -m main

# 7. Forzar push al remoto
git push -f origin main
```
Además, si tenías un branch para tus desarrollos, deberías reiniciar tu rama
```bash
git branch -D nombreRama
git push origin --delete nombreRama
git checkout -b nombreRama
git push -u origin nombreRama
```