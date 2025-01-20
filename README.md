# ENVIRONMENTS_CONDA
yml files from environments conda for INSTITUTO NACIONAL DE SALUD PUBLICA - MÉXICO

### EXPORTACIÓN DE AMBIENTES CONDA
Para exportar un ambiente conda uso el comando:

1. Activo el ambiente que quiero exportar
$ conda activate mi_ambiente

2. Exporto el ambiente a un archivo .yml
$ conda env export > mi_ambiente.yml

3. Una vez que tengamos el archivo.yml lo copiamos al servidor al que queremos exportarlo
$ scp mi_archivo.yml user@remote_server:path
$ rsync -avzh mi_archivo.yml user@remote_server:path

### IMPORTACIÓN  DE AMBIENTES CONDA
4. En el servidor “nuevo” y como “usuario root” ejecutamos el comando:
$ conda env  create --prefix /usr/local/share/conda_envs_all/bwa_qc -f /home/leslie/bwa_multiqc.yml

Donde:
-- prefix → ruta del directorio para ambientes compartidos 
bwa_qc → nombre del nuevo ambiente
-f → ruta o nombre del archivo.yml de donde se importará el nuevo ambiente

El directorio /usr/local/share/conda_envs_all/ debe:
 - Estar creado previamente por el usuario root
 - Contar con los permisos 755 para que todos los usuarios puedan acceder a él pero solo el root pueda escribir

### VARIABLES DE AMBIENTE
5. Para que los ambientes puedan verse desde el comando:
 “conda env list” , se debe agregar una variable de ambiente para que se reconozca en todos los shells.

 Para ello creamo en el directorio /etc/profile.d/ un archivo llamado envs_for_all.sh, este archivo contiene la variable CONDA_ENVS_PATH:
CONDA_ENVS_PATH=/usr/local/share/conda_envs_all/
PATH=$CONDA_ENVS_PATH:$PATH
export CONDA_ENVS_PATH PATH
