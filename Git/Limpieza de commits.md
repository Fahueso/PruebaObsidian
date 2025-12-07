
## Limpiar mi repositorio de commits basura, sin reiniciar el repositorio

Esto deja deja todos como está en tu rama master, pero elimina todo el histórico de commits

```bash
# 1. Asegúrate de estar en master
git checkout master

# 2. Crear una rama temporal sin historial
git checkout --orphan temp

# 3. Añadir todos los archivos
git add .

# 4. Crear un commit inicial limpio
git commit -m "initial clean commit"

# 5. Borrar la rama master antigua
git branch -D master

# 6. Renombrar temp → master
git branch -m master

# 7. Forzar push al remoto
git push -f origin master
```
Además, si tenías un branch para tus desarrollos, deberías reiniciar tu rama
```bash
git branch -D autosync
git push origin --delete autosync
git checkout -b autosync
git push -u origin autosync
```