Git viene instalado de serie en Lliurex.

Sigue estos pasos para poner tu entorno de programación de DAW en marcha

* Abre un terminal y escribe los siguientes comandos

```bash
git config --global user.name "Nombre"
git config --global user.email "tu-email@dominio.com"
```

* Os recomiendo gastar los siguientes Alias:
```bash
git config --global color.ui auto
git config --global alias.s "status -s"
git config --global alias.lg "log --oneline --graph --decorate --all"
git config --global alias.a "add ."
git config --global alias.c "commit -m"
git config --global alias.p "push"
```
* Para evitar problemas con saltos de línea en Linux:

```bash
git config --global core.autocrlf input
```
* Para evitar problemas con saltos de línea en Windows:

```bash
git config --global core.autocrlf true
```
* Para asegurarnos que la rama inicial se llame `main` en lugar de `master`:

```bash
git config --global init.defaultBranch main
```
