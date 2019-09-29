# Herramientas colaborativas en Unity

Git gestiona de forma eficiente el control de cambios en los ficheros de texto. Los ficheros binarios, y los de gran tamaño hacen crecer excesivamente el repositorio cada vez que se actualizan, lo que además provoca la ralentización de tareas de sincronización de los repositorios. Las actualizaciones de los ficheros binarios se interpretan como cambios completos de los archivos, mientras que en el caso de los ficheros de texto sólo se almacenan las diferencias.

## Git LFS

Git LFS es un proyecto open source que facilita la gestión en git de ficheros de gran tamaño y binarios. Podemos instalarlo en Linux, Windows, 
Git LFS usa **punteros** en lugar de los ficheros reales, cuando los ficheros (o tipos de ficheros) se marcan como **ficheros LFS**. Cuando un fichero se marca como LFS, en lugar de guardar grandes ficheros binarios en el repositorio Git, se escribe un puntero a un fichero. Por otra parte, los ficheros reales se almacenan en el repositorio remoto para ficheros LFS. En el repositorio local los ficheros reales se almacenan en una caché, fuera del repositorio git (en la carpeta .git en local). La ubicación de los archivos reales es transparente para el usuario. Cuando se requiere el fichero, los punteros se envían al repositorio local y se pasan a través de un filtro que reemplazará el puntero con el fichero real. 
Si los colaboradores del repositorio no tienen Git LFS instalado, no tendrán acceso al archivo de gran tamaño original. Si intentan clonar el repositorio, solo extraerán los archivos de punteros, y no tendrán acceso a los datos verdaderos.
### Arquitectura LFS
- El espacio de trabajo local está organizado en: Copia de trabajo, Caché LFS y Repositorio local. 
- El repositorio remoto se organiza en: Repositorio y repositorio de archivos LFS.
## Instalación de Git LFS
Es necesaria la descarga, y posteriormente ejecutar en Git: `git lfs instal`
Este paso sólo es necesario realizarlo una vez
### Instalación en Ubuntu
    curl -s https://packagecloud.io/install/repositories/github/git-lfs/script.deb.sh | sudo bash  
    sudo apt-get install git-lfs  
    git lfs install
### Instalación en Windows
[Descarga de Git LFS para Windows](https://git-lfs.github.com/)
### Instalación MAC

  `brew update`  
  `brew install git-lfs`  
  `git lfs install`  
## Uso de Git LFS
Cuando usamos Git LFS se debe especificar en el archivo .gitattributes los archivos que tendrán este seguimiento especial. Esto se hace en el fichero `.gitattributes`
- Marcar los ficheros para el seguimiento LFS `git lfs track "[patrón de fichero]"`  
Los patrones o ficheros especificados se registran en el archivo `.gitattributes`. Se añade la línea `*.jpg filter=lfs diff=lfs merge=lfs -text` 
- Listar los ficheros a los que se les está haciendo el seguimiento Git LFS `git lfs ls-files`
- Transformar un repositorio git convencional a uno con seguimiento LFS: `git lfs migrate import --include="[Lista de patrones de archivos]`  
Esto afecta a todo el histórico, por lo que hay que tener especial cuidado y todos los miembros del equipo deben llegar a cabo la misma operación, para que todos los repositorios estén configurados de forma similar.
- Podar la caché del repositorio local: `git lfs prune`
- Valorar si es estrictamente necesario realizar el seguimiento del fichero binario, cuando no lo sea agregarlo al fichero `.gitignore`
- Añadir el seguimiento LFS sólo cuando no haya posibilidad de generar versiones de texto del fichero y hacer el seguimiento en texto. (Por ejemplo, esto es posible en los ficheros Word).
## Git LFS desde Unity
[El paquete github for Unity] (https://unity.github.com/) es una extensión para utilizar Git LFS desde Unity. Cuando agregamos el paquete a nuestro proyecto configuramos la carpeta del proyecto como un repositorio Git LFS.  
- Windows --> GitHub podemos configurar un repositorio Git LFS sincronizado con un repositorio remoto en GitHub.
- Windows --> GitHub comand line console permite lanzar una consola bash de git
Podemos vincular nuestro proyecto con un repositorio Git LFS en GitHub. La extensión se encarga de configurar el archivo `.gitignore` y `.gitattribute`. 
Antes de hacer el push de nuestro proyecto es necesario hacer el pull del repositorio de Github Puede surgir un conflicto de discrepancias entre las historias de ambos repositorios. Esto lo resolvemos ejecutando en la consola bash el comando:  
`git pull origin master --allow-unrelated-histories`  
A partir de ahí, podemos operar desde Unity en la pestaña GitHub para mantener actualizado el repositorio remoto.  

## Collab de Unity



