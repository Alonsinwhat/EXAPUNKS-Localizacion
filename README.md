Este es un proyecto de traducción no oficial para el juego EXAPUNKS, de Zachtronics, sin fines de lucro.

Este proyecto fue iniciado por el usuario chino None, dueño del repositorio original. Yo he tomado su trabajo y lo he adaptado de manera que pueda ser utilizado para traducir el juego al español.
Yo, Alonso, no poseo conocimientos de python ni de computación lo suficientemente buenos para entender al 100% lo que hace el código de la persona que creó el proyecto en un primer lugar, pero hago lo que puedo. Cuendo sea necesario, se indicará previamente lo que he aprendido de ciertos archivos en este mismo documento.

Sugiero que leas este documento en su totalidad antes de hacer cualquier cambio al juego.

# Cómo traducir
Primero que todo, debes poseer el juego; puedes comprarlo en [steam](https://store.steampowered.com/app/716490/EXAPUNKS/), [GOG](https://www.gog.com/game/exapunks) o la plataforma que desees.

Luego, deberás instalar los datos de este repositorio en tu computadora. Para ello, toca donde dice "<> Code" y luego en descargar .zip.
Esto descargará los datos que aparecen aquí en tu computadora para que puedas editar las traducciones o añadir alguna nueva, mientras esté dentro de las permitidas (Más sobre esto más adelante).

# Prepara tu entorno de trabajo
## 1. instala [python](https://www.python.org/) 3 y las librerías correspondientes.

* instala python desde [https://www.python.org/downloads/](https://www.python.org/downloads/). Debes poner la palomita en donde dice "Copy Python to PATH", o algo así.

Para instalar las dependencias, abre una consola del sistema con permisos de administrador y ejecuta los siguientes comandos (no es necesario descargar nada aparte, pip descargará todo por tí.):

* instala [pandas](https://pandas.pydata.org/)

    ```
    pip install pandas
    ```
* instala [openpyxl](https://openpyxl.readthedocs.io/en/stable/)
    ```
    pip install openpyxl
    ```
* instala [Pillow](https://python-pillow.org/)
    ```
    pip install pillow
    ```

* instala [python-lz4](https://github.com/python-lz4/python-lz4)
    ```
    pip install lz4
    ```

## 2. copia los archivos necesarios del juego al directorio de trabajo

Abre el directorio de instalación de EXAPUNKS, y luego:

* copia ``Content/descriptions/en/*`` a ``./export_txt/Content/descriptions/en/``
* copia ``Content/vignettes/*`` a ``./export_txt/Content/vignettes``
* copia ``PackedContent/fonts/*.packedfont`` a ``./font/fonts``
* copia ``PackedContent/*.tex`` a ``./images/PackedContent``
  
  Nota: **DEBES** arreglar los siguientes archivos; de lo contrario, los programas para traducir el juego no funcionarán correctamente:

  ``Content/vignettes/ember-7.csv`` faltan comillas en la línea 12

  ``Content/vignettes/nivas-3.csv`` faltan comillas en la línea 9  
  
## 3. instala fuentes (opcional) 
* install [Source Han Sans](https://github.com/adobe-fonts/source-han-sans)
* install [Source Han Mono](https://github.com/adobe-fonts/source-han-mono)

de lo contrario pon tu fuentes favoritas en ``import_txt/translation.py`` y ``font/gen.py``

ESTO sólo es necesario para tener las fuentes CHINAS, JAPONESAS, o de algún idioma que no utilice carácteres latinos.

# Traduce los textos
Hay tres archivos .json en ``import_txt``, deben ser traducidos.

Se recomienda mucho que utilices ``json2excel.py`` para generar archivos excel de los .json, para editarlos desde Excel, Google Sheets o un editor de hojas de cálculo que te guste.

En cuanto a lo de los IDIOMAS que aparecen arriba, se recomienda encarecidamente que leas la nota al final de este readme, para que sepas cómo funciona aquello.

* ``EXAPUNKS_descriptions.json``

    Se obtuvo de Content/descriptions/*.txt

    Hay que traducir todo en este archivo.

* ``EXAPUNKS_vignettes.json``

    Se obtuvo de Content/vignettes/*.csv

    Hay que traducir todo en este archivo.

* ``EXAPUNKS_exe.json``

    Se obtuvo directamente de EXAPUNKS.exe

    **No** todos los textos se deben traducir. 
    
    Traduce **sólo** aquellos textos que aparezcan visualmente en el juego.

  

## Cómo usar json2excel.py
Ejecutar ``json2excel.py`` hará que se dirija al directorio actual, y genere archivos .xlsx de todos los archivos .json.  

Una vez edites los archivos .xlsx, deben volver a ser .json; para ello, ejecuta ``excel2json.py``, que en esencia toma el camino contrario. 

Es posible que te aparezca una pregunta de confirmación en caso de que se intente sobreescribir un archivo más actualizado; en tal caso, debes escribir "Y" para sobreescribirlo o "N" para saltártelo.

# Modifica las texturas
Ejecuta ``images/export_imgs.py`` 

Viajará al directorio ``images/PackedContent``, convertirá todos los archivos .tex a .png en el directorio ``out``.

Elige las imágenes que modificarás. (Borra ``half``, se generará automáticamente luego.)

Pon las imágenes seleccionadas en el directorio ``new``, dentro de ``images`` (Debería quedar como se ve en el repositorio. SI vas a cambiar las imágenes, borra primero las que ya están, para que no haya ningún problema.)

# Edita los zines

Con tu editor de imágenes de preferencia, toma las imágenes en manual y editalas para que estén en el idioma que deseas. Luego, únelas en un mismo pdf. El dueño original del repositorio dejó un archivo ahí que se supone que junta todo, pero yo no me metí ahí, asi que puedes simplemente usar un unidor de pdfs online como ilovepdf.

# Genera el parche
Para generar el parche, necesitamos tener;
1. Los textos:
   Con los .json traducidos, vas a ejecutar ``import_text.py``. Esto creará los archivos necesarios en la carpeta ``/patch/Content``, en sus directorios correspondientes, y además creará un archivo llamado ``strings.csv`` en tu directorio actual. Debes mover ese archivo a ``/patch/Content``.

2. Las imágenes:
   Con tus imágenes editadas en /new, vas a ejecutar ``import_imgs.py``. Esto transformará las imágenes que hayas modificado de vuelta a .tex y las pondrá en ``/patch/PackedContent/``

3. Los zines:
   Una vez tengas el pdf listo, simplemente ponlo en ``/patch/Content/manual/``. Recuerda que debe tener el nombre de digital_en_1.pdf y digital_en_2.pdf. También puedes crear los zines para hoja tamaño carta (en cuyo caso, deben llamarse letter_en_1.pdf y letter_en_2.pdf) o A4 (metric_en_1.pdf y metric_en_2.pdf). Puedes encontrar esos otros documentos en la misma ruta, pero en la carpeta de instalación del juego.

# Aplica los cambios
Finalmente, has completado la traducción. Sólo debes modificar el nombre de EXAPUNKS_fixed.exe a EXAPUNKS.exe, y luego copia los contenidos de /patch a la carpeta de instalación del juego

Se recomienda que hagas copias tanto de los archivos del juego originales, como del parche, para que puedas probar y hacer cambios antes de todo.

# Cambia la configuración del juego
Ahora, debes poner el juego en Español!
Edita ``%USERPROFILE%\Documents\My Games\EXAPUNKS\xxxxxx\config.cfg``
```
Language = English
```
Cambia 'English' a 'German'

(¿Por qué German?)

# Nota final.

Entiendo que quien produjo esta traducción originalmente, es decir, la persona que intentó traducir al chino, utilizó un descompilador para acceder al código intermedio de EXAPUNKS.exe, lo limpió y luego extrajo los textos que encontramos en exapunks.json, además de editar el código (/exe/exe_patch.diff) para que así este acceda a distintas partes de los archivos dependiendo del idioma (es decir, en base a lo que dice en config.cfg, decidir qué carpeta abrir en /descriptions, y qué línea leer en /vignettes/*.csv y en /strings.csv). Es debido a esto que no podemos cambiar la palabra a Spanish/Español, en config.cfg, ni hacer que la carpeta en descriptions se llame "es", sólo puede ser "de". No sé editar los archivos internos del ejecutable, por lo que no sé cómo podría cambiarlo para que se puedan crear nuevos idiomas. Por ahora, tenemos que basarnos en lo que dice el archivo, es decir, estamos limitados a German, French, Russian, Japanese, Chinese; teniendo en cuenta que las imágenes y zines se mantendrán en un sólo idioma... pero invito a quien sepa hacerlo y esté interesado, a modificar el ejecutable del juego y a que añada la posibilidad de que existan nuevos idiomas. Por mientras, tendremos que quedarnos con simplemente sobreescribir German para el proyecto que quieras.
