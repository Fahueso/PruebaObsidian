Git viene instalado de serie en Lliurex.

Sigue estos pasos para poner tu entorno de programación de DAW en marcha

* Registrate en Github, y crea un repositorio llamado ProgramacionDAW, usando tu cuenta institucional
* Abre un terminal en Lliurex y escribe los siguientes comandos

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
```