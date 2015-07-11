[ Languages: [English](README.md), [Español](README-es.md), [한국어](README-ko.md), [Português](README-pt.md), [Русский](README-ru.md), [中文](README-zh.md) ]


# El Arte del Terminal

[![Join the chat at https://gitter.im/jlevy/the-art-of-command-line](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/jlevy/the-art-of-command-line?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

- [Meta](#meta)
- [Fundamentos](#basics)
- [De uso diario](#everyday-use)
- [Procesamiento de archivos y datos](#processing-files-and-data)
- [Depuración del sistema](#system-debugging)
- [One-liners](#one-liners)
- [Obscuro pero útil](#obscure-but-useful)
- [Solo para MacOS](#macos-only)
- [Más recursos](#more-resources)
- [Advertencia](#disclaimer)


![curl -s 'https://raw.githubusercontent.com/jlevy/the-art-of-command-line/master/README.md' | egrep -o '`\w+`' | tr -d '`' | cowsay -W50](cowsay.png)

La fluidez en el terminal es una destreza a menudo abandonada y considerada arcaica, pero esta mejora su flexibilidad y productividad como ingeniero en formas obvia y sutil. Esta es una selección de notas y consejos al usar el terminal que encontré útiles al trabajar en Linux. Algunos consejos son elementales y algunos bastante específicos, sofisticados u oscuros. Esta página no es larga, pero si usa y recuerda todos los puntos aquí mostrados, ustedes sabrán un montón.

Gran parte está en
[originally](http://www.quora.com/What-are-some-lesser-known-but-useful-Unix-commands)
[appeared](http://www.quora.com/What-are-the-most-useful-Swiss-army-knife-one-liners-on-Unix)
en [Quora](http://www.quora.com/What-are-some-time-saving-tips-that-every-Linux-user-should-know),
pero debido al interés mostrado, parece que vale la pena usar Github, donde existen personas más talentosas, que fácilmente pueden sugerir mejoras. Si ve un error o algo que podría ser mejor, por favor, cree un issue o PR! (Por supuesto revise la sección meta de PRs/issues primero.)


## Meta

Alcance:

- Esta guía es tanto para el principiante como para el experimentado. Los objetivos son *diversidad* (todo importa), *especificidad* (dar ejemplos concretos del caso más común), y *concisión* (evitar cosas que no son esenciales o insignificantes que puedas buscar fácilmente en otro lugar). Cada consejo es esencial en alguna situación o significativamente ahorra tiempo comparada con otras alternativas.
- Esta escrito para Linux, con excepción de la sección "[Solo para MacOS](#macos-only)". Muchos de los otros puntos aplican o pueden ser instalados en otros Unices o MacOS (o incluso Cygwin).
- Se enfoca en Bash interactivo, aunque muchos de los consejos se aplican para otros shells y al Bash scripting por lo general.
- Esta incluye ambos comandos "estándar" Unix, así como aquellos que requieren la instalación especial de un paquete -- siempre que sea suficientemente importante para ameritar su inclusión.

Notas:

- Para mantener esto en una página, el contenido esta incluido implícitamente por referencia. Usted es suficientemente inteligente para ver profundamente los detalles en otros lugares, cuando conoces la idea o comando en Google. Usar `apt-get`/`yum`/`dnf`/`pacman`/`pip`/`brew` (según proceda) para instalar los nuevos programas.
- Usar [Explainshell](http://explainshell.com/) para obtener detalles de ayuda sobre que comandos, opciones, pipes, etc.


## Fundamentos

- Aprenda conocimientos básicos de Bash, de hecho, escriba `man bash` y al menos échele un vistazo a toda la cosa. Es bastante fácil de seguir y no es tan largo. Alternar entre shells puede ser agradable, pero Bash es poderoso y siempre esta disponible (conocer *solo* zsh, fish, etc., aunque resulte tentador en tu propia laptop, los restringe en muchas situaciones, tales como el uso de servidores existentes).

- Aprenda bien al menos un editor de texto, idealmente Vim (`vi`), como no hay realmente una competencia para la edición aleatoria en un terminal (incluso si usa Emacs, un gran IDE, o un editor alternativo (hipster) moderno la mayor parte del tiempo).

- Conozca como leer la documentación con `man` (Para curiosos, `man man` lista las secciones enumeradas, ej. 1 es comandos "regulares", 5 son archivos/convenciones, y 8 are para administración). En en las páginas de man `apropos`. Conozca que alguno de los comandos no son ejecutables, pero son Bash builtins, y que puede obtener ayuda sobre ellos con `help` y `help -d`.

- Aprenda sobre redirección de salida >, entrada < y pipes utilizando `|`. Conozca que `>` sobrescribe el archivo de salida y `>>` añade. Aprenda sobre stdout y stderr.

- Aprenda sobre expansión de archivos glob con `*` (y tal vez `?` y `{`...`}`) y quoting y la diferencia entre doble `"` y simple `'` quotes. (Ver más en expansión de variables más abajo.)

- Familiarízate con la administración de trabajo en Bash: `&`, **ctrl-z**, **ctrl-c**, `jobs`, `fg`, `bg`, `kill`, etc.

- Conoce `ssh` y lo básico de autenticación sin contraseña, vía `ssh-agent`, `ssh-add`, etc.

- Administración de archivos básica: `ls` y `ls -l` (en particular, aprenda el significado de cada columna en `ls -l`), `less`, `head`, `tail` y `tail -f` (o incluso mejor, `less +F`), `ln` y `ln -s` (aprenda las diferencias y ventajas entre enlaces hard y soft), `chown`, `chmod`, `du` (para un resumen rápido del uso del disco: `du -hs *`). Para administración de archivos de sistema, `df`, `mount`, `fdisk`, `mkfs`, `lsblk`.

- Administración básica de redes: `ip` o `ifconfig`, `dig`.

- Conozca bien las expresiones regulares y varias opciones (flags) para `grep`/`egrep`. Las opciones `-i`, `-o`, `-A`, y `-B` son dignas de ser recordadas.

- Aprenda el uso de `apt-get`, `yum`, `dnf` o `pacman` (dependiendo de la distribución "distro") para buscar e instalar paquetes. Y asegúrate que tienes `pip` para instalar la herramienta de línea de comando basada en Python (un poco más abajo esta explicado como instalar vía `pip`).


## De uso diario

- En Bash, se usa **Tab** para completar los argumentos y **ctrl-r** para buscar, a través del historial de comandos.

- En Bash, se usa **ctrl-w** para borrar la última palabra, y **ctrl-u** para borrar todo el camino hasta el inicio de la línea. Se usa **alt-b** y **alt-f** para moverse entre letras, **ctrl-a** para mover el cursor al principio de la línea,  **ctrl-e** para mover el cursor al final de la línea,  **ctrl-k** para eliminar hasta el final de la línea, **ctrl-l** para limpiar la panatalla. Ver `man readline` para todos los atajos de teclado por defecto en Bash. Son una gran cantidad. Por ejemplo **alt-.** realiza un ciclo a través de los comandos previos, y **alt-*** expande un glob.

- Alternativamente, si amas los atajos de teclado vi-style, usa `set -o vi`.

- Para ver los últimos comandos, `history`. También existen abreviaciones, tales como, `!$` (último argumento) y `!!` último comando, auque sin facílmente remplazados con **ctrl-r** y **alt-.**.

- Para volver al diretorio de trabajo previo: `cd -`

- Si estas a mitad de camino de escritura de un comando pero cambias de opinión, presiona **alt-#** para agregar un `#` al principio y lo agrega como comentario (o usar **ctrl-a**, **#**, **enter**). Para que puedas entonces regresar a este luego vía comando `history`.

- Se usa `xargs` (or `parallel`). Esto es muy poderoso. Nota: puedes controlar muchos items ejecutados por línea (`-L`), tamabién es conocido como paralelismo (`-P`). Si no estas seguro, este puede ser el camino correcto, usa `xargs echo` primero. También, `-I{}` es comodo. Ejemplos:
```bash
      find . -name '*.py' | xargs grep some_function
      cat hosts | xargs -I{} ssh root@{} hostname
```

- `pstree -p` es útil para mostrar el árbol de procesos.

- Se usa `pgrep` y `pkill` para encontrar o señalar procesos por su nombre (`-f` es de mucha ayuda).

- Conocer varias señales que puedes enviar a los procesos. Por ejemplo, para suspender un proceso, usa `kill -STOP [pid]`. Para la lista completa, consultar `man 7 signal`

- Usa `nohup` o `disown` si quieres mantener un proceso de fondo corriendo para siempre.

- Verifica que procesos esta escuchando via `netstat -lntp` o `ss -plat` (para TCP; agrega `-u` para UDP).

- Consulta también `lsof` para abrir sockets y archivos.

- Usar `alias` para crear atajos para comandos comúnmente usados. Por ejemplo, `alias ll="las -latr"` crea un nuevo alias `ll`

- En scripts Bash, usa `set -x` para depurar la salida. Utiliza el modo estricto cuando se posible. Utiliza `set -e` para abortar en errores. Utiliza `set -o pipefail` también, para ser estrictos sobre los errores (aunque este tema es un poco delicado). Para scripts más complejos, también se puede utilizar `trap`.

- En scripts Bash, subshells (escritos con parentesís) son maneras convenientes para agrupar los comandos. Un ejemplo común es para moverse temporalmente hacia un directorio diferente del de trabajo, Ej.
```bash
      # do something in current dir
      (cd /some/other/dir && other-command)
      # continue in original dir
```

- En Bash, considere que hay muchas formas de expansión de variables. Verificar la existencia de una variable: `${name:?error message}`. Por ejemplo, si un script Bash requiere un único argumento, solo escriba `input_file=${1:?usage: $0 input_file}`. Expansión arítmetica: `i=$(( (i + 1) % 5 ))`. Secuencias: `{1..10}`. Reducción de strings: `${var%suffix}` y `${var#prefix}`. Por ejemplo si `var=foo.pdf`, entonces `echo ${var%.pdf}.txt` imprime `foo.txt`.

- La salida de un comando puede ser tratado como un archivo, vía `<(some command)`. Por ejemplo, compare local `/etc/hosts` con uno remoto:
```sh
      diff /etc/hosts <(ssh somehost cat /etc/hosts)
```

- Conocer acerca "here documents" en Bash, así también `cat <<EOF ...`.

- En Bash, redireccionar salida estándar y error estándar, via: `some-command >logfile 2>&1`. Frecuentemente, para garantizar que un comando no haya dejado abierto un archivo para controlar la entrada estándar vinculada al terminal en el que te encuentras y también como buena practica puedes agregar `</dev/null`.

- Use `man ascii` para una buena tabla ASCII, con valores hexadecimal y decimales. Para información de codificación general, `man unicode`, `man utf-8`, y `man latin1` son de utilidad.

- Use `screen` o [`tmux`](https://tmux.github.io/) para multiplexar la pantalla, especialmente útil en sesiones ss remotas y para desconectar y reconectar a una sesión. Una alternativa más minimalista para persistencia de la sesión solo sería `dtach`.

- En ssh, conocer como hacer un port tunnel con `-L` o `-D` (y de vez en cuando `-R`) es útil, Ej. para acceder sitio web desde un servidor remoto.

- esto puede ser útil para hacer algunas optimizaciones para su configuración ssh; por ejemplo, Este, `~/.ssh/config` contiene la configuracion para evitar desconexiones en ciertos entornos de red, usar comprensión (la cual es muy útil con scp sobre conexiones con un ancho de banda pequeño), y multiplexar canales para el mismo servidor con un archivo de control local:
```
      TCPKeepAlive=yes
      ServerAliveInterval=15
      ServerAliveCountMax=6
      Compression=yes
      ControlMaster auto
      ControlPath /tmp/%r@%h:%p
      ControlPersist yes
```

- Unas pocas otras opciones relevantes para ssh son are sensitivas a la seguridad y deben ser activadas con cuidado, Ej. "per subnet", "host" o "in trusted networks: `StrictHostKeyChecking=no`, `ForwardAgent=yes`

- Para obtener permiso sobre un archivo en forma octal form, el cual es útil para la configuración del sistema pero no disponible con `ls` y fácil de estropear, usando algo como
```sh
      stat -c '%A %a %n' /etc/timezone
```

- Para selección interactiva de valores desde la salida de otro comando, usa [`percol`](https://github.com/mooz/percol) o [`fzf`](https://github.com/junegunn/fzf).

- Para la interacción con archivos basados en la salida de otro comando (como `git`), usa `fpp` ([PathPicker](https://github.com/facebook/PathPicker)).

- Para un servidor web sencillo para todos los archivos en el directorio actual (y subdirectorios), disponible para cualquiera en tu red, usa:
`python -m SimpleHTTPServer 7777` (para el puerto 7777 y Python 2) y `python -m http.server 7777` (para 7777 y Python 3).

- Para ejecutar un comando con privilegios, usando `sudo` (para root) o `sudo -u` (para otro usuario). Usar `su` o `sudo bash` para realmente ejecutar un shell como este usuario. Usar `su -` para simular un login fresco como root u otro usuario.


## Procesamiento de archivos y datos

- Para localizar un archivo por nombre en el directorio actual, `find . -iname '*something*'` (o similar). Para encontrar un archivo en cualquier lado por nombre, usar `locate something` (pero tenga en mente `updatedb` quizas no haya indexado recientement los archivos creados).

- Por lo general buscar por la fuente o archivos de datos (más avanzado que `grep -r`), usar [`ag`](https://github.com/ggreer/the_silver_searcher).

- Para convertir HTML a text: `lynx -dump -stdin`

- Para Markdown, HTML, y todos los tipos de conversión de documentos, probar [`pandoc`](http://pandoc.org/).

- Si debes manipular XML, `xmlstarlet` es viejo pero bueno.

- Para JSON, usa `jq`.

- Para archivos Excel o CSV, [csvkit](https://github.com/onyxfish/csvkit) provee `in2csv`, `csvcut`, `csvjoin`, `csvgrep`, etc.

- Para Amazon S3, [`s3cmd`](https://github.com/s3tools/s3cmd) es conveniente y [`s4cmd`](https://github.com/bloomreach/s4cmd) es el mas rápido. Hecho por Amazon [`aws`](https://github.com/aws/aws-cli) es esencial para otras tareas relacionadas al AWS.

- Conocer acerca `sort` y `uniq`, incluyendo opciones de uniq `-u` y `-d` -- ver unas lineas mas abajo.

- Conocer acerca `cut`, `paste`, y `join` para manipular archivos de texto. Muchas personas usan `cut` pero se olvidan acerca de `join`.

- Conocer acerca `wc` para contar nuevas líneas (`-l`), caractéres (`-m`), palabras (`-w`) y bytes (`-c`).

- Conocer acerca `tee` para copiar desde el stdin hacia un archivo y también hacia el stdout, así `ls -al | tee file.txt`.

- Conocer que `locale` afecta muchas herramientas de línea de comando en forma delicada, incluyendo el orden del ordenamiento (compaginación) y rendimiento. La mayoría de las instalaciones de Linux configuran `LANG` u otras variables de localización para la configuración local como US English. Pero esté alerta, el ordenamiento puede cambiar si cambia la localización. Y también las rutinas i18n pueden hacer que `sort` u otros comandos se ejecuten **muchas veces** más lentos. En algunas situaciones (tales como la realización de operaciones u operaciones singulares debajo) puede de forma segura ignorar las turinas lentas i18n por completo y utilizar el sort tradicional basado en byte, usando `export LC_ALL=C`.

- Conozca aspectos básicos de `awk` y `sed` para manejo de datos. Por ejemplo, sumar todos lo números en la tercera columna de un archivo de texto: `awk '{ x += $3 } END { print x }'`. Esto es probablemente 3X más rápido y 3X más corto que su equivalente en Python.

- Para remplazar todas las ocurrencias de un string en su lugar, en uno o más archivos:
```sh
      perl -pi.bak -e 's/old-string/new-string/g' my-files-*.txt
```

- Para renombrar varios archivos a la vez de acuerdo a un patrón, usar `rename`. Para renombramientos complejos, [`repren`](https://github.com/jlevy/repren) may help.
```sh
      # Recover backup files foo.bak -> foo:
      rename 's/\.bak$//' *.bak
      # Full rename of filenames, directories, and contents foo -> bar:
      repren --full --preserve-case --from foo --to bar .
```

- Usar `shuf` para mezclar o seleccionar líneas aleatorias desde un archivo.

- Conozca las opciones de `sort`. Para números, use `-n`, o `-h` para manipulación de números humanamente leíbles (Ej. desde `du -h`). Conozca el trabajo principal de (`-t` y `-k`). En particular, este atento que lo necesitara para escribir`-k1,1` para ordenar por solo el primer campo; `-k1` significa ordenar de acuerdo a toda la línea. Orden estable (`sort -s`) puede ser útil. Por ejemplo, para organizar el primer por el campo 2, entonces secundariamente hacerlo por el campo 1, Puedes usar `sort -k1,1 | sort -s -k2,2`.

- Si necesitas siempre escribir un tab literal en una línea de comandos en Bash (Ej. para el argumento -t de ordenar), presione **ctrl-v** **[Tab]** o escriba `$'\t'` (El último es mejor porque puedes copiarlo/pegarlo).

- Las herramientas estándar para reparar el código fuente son `diff` y `patch`. Ver también `diffstat` para resumen estadístico de una diff. Nota `diff -r` trabaja con directorios por completo. Usar`diff -r tree1 tree2 | diffstat` para el resumen de cambios.

- Para archivos binarios, usar `hd` para sencillos "hex dumps" y `bvi` para edición de binario.

- También para archivos binarios, `strings` (además de `grep`, etc.) permite encontrar en el texto bits.

- Para diffs binaria (delta compression), usar `xdelta3`.

- Para convertir la codificación del texto, probar `iconv`. O `uconv` para el uso avanzado; este soporta este soporta algunos elementos Unicode avanzados. Por ejemplo, este coloca en minúsculas y remueve todos los acentos (por expanción y colocandolos a ellos):
```sh
      uconv -f utf-8 -t utf-8 -x '::Any-Lower; ::Any-NFD; [:Nonspacing Mark:] >; ::Any-NFC; ' < input.txt > output.txt
```

- Para dividir archivos en multiples partes, consultar `split` (para dividir por tamaño) y `csplit` (para dividir por un patrón).

- Usar `zless`, `zmore`, `zcat`, y `zgrep` para operar sobre archivos comprimidos.


## Depuración del sistema

- Para depuración web, `curl` y `curl -I` son prácticos, o sus equivalentes `wget`, o el más moderno [`httpie`](https://github.com/jakubroztocil/httpie).

- Para el estado del disco/cpu/red, usar `iostat`, `netstat`, `top` (o el mejor `htop`), y (especialmente) `dstat`. Bueno para recibir una idea rápida de lo que esta pasando en tu sistema.

- Para una resumen en mayor profundidad, usar [`glances`](https://github.com/nicolargo/glances). Este se presenta con varios niveles de estadística en un solo terminal. Muy útil para una verificación rápida de vaios subsistemas.

- Para conocer el estado de la memoria, ejecutar y entender la salida de `free` y `vmstat`. En particular, tener en cuenta el valor "cached" es memoria mantenida por el kernel Linux como un archivo de cache, entonces efectivamente cuenta como valor para "free".

- El sistema de depuración de Java es harina de otro costal, pero un truco simple en las JSM de Oracle y de otros consta en que puedes ejecutar `kill -3 <pid>` y una traza completa y un resumen del montículo "heap summary" (incluyendo del detalle de la colección de basura generacional, la cual puede ser altamente informativa) serán descargados al stderr/logs.

- Usar `mtr` como un mejor traceroute, para identificar los problemas en la red.

- Para mirara porque el disco esta lleno, `ncdu` ahorra tiempo sobre los comandos usual como `du -sh *`.

- Para encontrar cual socket o proceso  esta utilizando el ancho de banda, prueba `iftop` o `nethogs`.

- La herramienta `ab` (viene con Apache) es útil para una verificación rápida y sucia del rendimiento del servidor web. Para pruebas de carga más complejas, prueba `siege`.

- Para depuración de redes más serias, `wireshark`, `tshark`, o `ngrep`.

- Conozca acerca `strace` y `ltrace`. Estas son de utilidad si un programa esta fallando, guindando, o estrellando, y no conoces por qué?, o si quieres tener una idea general del rendimiento. Note la opción de elaboración de perfiles (`-c`), y la habilidad de adjuntar a un proceso en ejecución (`-p`).

- Conozca acerca `ldd` para verificar librerías compartidas etc.

- Conozca como conectarse a un proceso en ejecución con `gdb` y obtener su traza de pilas.

- Usar `/proc`. Este es extraordinariamente útil algunas veces cuando hay problemas de depuración en vivo. Ejemplos: `/proc/cpuinfo`, `/proc/xxx/cwd`, `/proc/xxx/exe`, `/proc/xxx/fd/`, `/proc/xxx/smaps`.

- Cuando se depura porque algo salio más en el pasado, `sar` puede ser muy útil. Este muestra la estadistica historica en CPU, memoria, red, etc.

- Para sistemas y análisis de rendimiento de mayor profundidad, ver `stap` ([SystemTap](https://sourceware.org/systemtap/wiki)), [`perf`](http://en.wikipedia.org/wiki/Perf_(Linux)), y [`sysdig`](https://github.com/draios/sysdig).

- Confirmar que OS te encuentras con `uname` o `uname -a` (información general Unix/kernel) o `lsb_release -a` (Linux distro info).

- Usar `dmesg` siempre que algo actúe raro (esto podría ser problemas con el hardware o driver).


## One-liners

Algunos ejemplos de comandos reunidos:

- Este es notablemente útil en ocasiones que hay que realizar intersección, unión, y diferencia de archivos de texto vía `sort`/`uniq`. Considere `a` y `b` como archivos de texto que son únicos. Esto es rápido, y trabaja con archivos de tamaño arbitrario, hasta varios gigabytes. (Sort no esta limitado por la memoria, aunque quizás necesites utilizar la opción `-T` si `/tmp` esta en una pequeña partición raíz.) Ver también la nota acerca `LC_ALL` y las opciones de `sort`, `-u` (dejado de lado para clarificar mas abajo).
```sh
      cat a b | sort | uniq > c   # c is a union b
      cat a b | sort | uniq -d > c   # c is a intersect b
      cat a b b | sort | uniq -u > c   # c is set difference a - b
```

- Usar `grep . *` para visualmente examinar todo el contenido de todos los archivos de un directorio, Ej. para directorios llenos con parametros de configuración, como `/sys`, `/proc`, `/etc`.


- Sumar todos os números en la tercera columna de un archivo de texto (esto es probablemente 3X más rápido 3X menor código que el equivalente en Python):
```sh
      awk '{ x += $3 } END { print x }' myfile
```

- Si quiere ver tamaños/fechas en un árbol de archivos, esto es como hacer recursivo `ls -l` pero es mas facil de leer que `ls -lR`:
```sh
      find . -type f -ls
```

- Usar `xargs` o `parallel` cuando pueda. Considere que puede controlar algunos elementos ejecutados por línea (`-L`) así como paralelismo (`-P`). Si no esta seguro de estar haciendo la cosa correcta, use primero xargs echo. También, `-I{}` es práctico. Ejemplos:
```sh
      find . -name '*.py' | xargs grep some_function
      cat hosts | xargs -I{} ssh root@{} hostname
```

- Digamos que tiene un archivo de texto, como un log de un servidor web, y un cierto valor comienza a aparecer en algunas líneas, tales como un parametro `acct_id` que esta presente en el URL. Si quieres un recuento de cuantas peticiones ""request hay por cada `acct_id`:
```sh
      cat access.log | egrep -o 'acct_id=[0-9]+' | cut -d= -f2 | sort | uniq -c | sort -rn
```

- Ejecuta esta función para obtener un consejo aleatorio desde este documento (analiza el Markdown y extrae un elemento):
```sh
      function taocl() {
        curl -s https://raw.githubusercontent.com/jlevy/the-art-of-command-line/master/README.md |
          pandoc -f markdown -t html |
          xmlstarlet fo --html --dropdtd |
          xmlstarlet sel -t -v "(html/body/ul/li[count(p)>0])[$RANDOM mod last()+1]" |
          xmlstarlet unesc | fmt -80
      }
```


## Oscuro pero útil

- `expr`: ejecuta operaciones aritméticas o booleanas o evalúa expresiones regulares

- `m4`: macro procesador sencillo

- `yes`: imprime un string sin fin

- `cal`: lindo calendario

- `env`: ejecuta un comando (útil en scripts)

- `printenv`: imprime las variables del ambiente (útil en depuración y scripts)

- `look`: buscar palabras en English (o líneas en un archivo) comenzando con un string

- `cut`, `paste` y `join`: manipulación de datos

- `fmt`: formato de texto de parrafo

- `pr`: formato de texto en páginas/columnas

- `fold`: envolturas de líneas de texto

- `column`: formato de texto en columnas o tablas

- `expand` y `unexpand`: convertidor entre tabs y espacios

- `nl`: agrega números de línea

- `seq`: imprime números

- `bc`: calculadora

- `factor`: factorización de enteros

- `gpg`: cifrado y firmas digitales

- `toe`: tabla de información de términos

- `nc`: depuración del entorno de red y transferencia de datos

- `socat`: socket relay y redireccionador de puerto tcp (similar a `netcat`)

- `slurm`: visualización del tráfico de red

- `dd`: moviliza data entre archivos y dispositivos

- `file`: identifica el typo de archivo

- `tree`: muestra directorios y subdirectorios como un árbol anidado; parecido a `ls` pero recursivo

- `stat`: información del archivo

- `tac`: imprime archivos en forma inversa

- `shuf`: selección de líneas de un archivo de forma aleatorea

- `comm`: compara archivos ordenados línea por línea

- `pv`: monitor del progreso de datos, a través, de un tubo

- `hd` y `bvi`: descarga o edita archivos binarios

- `strings`: extrae textos de archivos binarios

- `tr`: traducción y manipulación de caracter

- `iconv` o `uconv`: conversión de codificaciones de texto

- `split` y `csplit`: división de archivos

- `sponge`: lee todas las entradas antes de escribirlo, útil para vista previa y posterior escritura hacia el mismo archivo, Ej., `grep -v something some-file | sponge some-file`

- `units`: unidades de conversión y calculaciones; convierte furlongs por fortnight para twips por blink (ver también `/usr/share/units/definitions.units`)

- `7z`: compresión de archivos de alto nivel

- `ldd`: información de librería dinámica

- `nm`: archivo de objeto de simbolos

- `ab`: benchmarking de servidores web

- `strace`: depuración de llamadas del sistema

- `mtr`: mejor traceroute para la depuración de la red

- `cssh`: shell concurrent visual

- `rsync`: sincronización de archivos y carpetas sobre SSH

- `wireshark` y `tshark`: captura de paquetes y depuración de la red

- `ngrep`: grep para la capa de la red

- `host` y `dig`: consulta DNS

- `lsof`: descriptor de archivo de procesos y información de socket

- `dstat`: sistema de estadísticas útil

- [`glances`](https://github.com/nicolargo/glances):vistazo de multi-subsistemas, de alto nivel

- `iostat`: estadísticas del CPU y uso del disco

- `htop`: versión mejorada de top

- `last`: historial de login

- `w`: quien esta autenticado?

- `id`: información de identidad de usuario/grupo

- `sar`: sistema de estadísticas histórico

- `iftop` o `nethogs`: utilización de la red por un socket o process

- `ss`: estadísticas de socket

- `dmesg`: arranque y sistema de mensajes de error

- `hdparm`: manipulación/rendimiento de discos SATA/ATA

- `lsb_release`: información de la distribución de Linux

- `lsblk`: Lista de bloques de dispositivos: un árbol de vista de sus discos y particiones de disco

- `lshw`, `lscpu`, `lspci`, `lsusb`, `dmidecode`: información de hardware, incluyendo CPU, BIOS, RAID, grafícos, dispositivos, etc.

- `fortune`, `ddate`, y `sl`: um, bien, este depende si tiene la consideración de locomotoras de vapor y citas Zippy "práctico"


## Solo para MacOS

Estos son puntos relevantes *solo* en MacOS.

- Administración de paquetes con `brew` (Homebrew) y/o `port` (MacPorts). Estos pueden ser utilizados para instalar en MacOS muchos de los comandos de arriba.

- Copiar la salida de cualquier comando para una aplicación desktop con `pbcopy` y pegar desde una entrada con `pbpaste`.

- Para abrir un archivo con una aplicación desktop, usar `open` o `open -a /Applications/Whatever.app`.

- Spotlight: Busca archivos con `mdfind` y listar metadata (como información de foto EXIF) con `mdls`.

- Tenga encuenta que MacOS esta basado en BSD Unix, y cualquier comando (por ejemplo `ps`, `ls`, `tail`, `awk`, `sed`) tiene variaciones discretas variaciones por cada Linux, que esta en gran parte influenciado por el sistema Unix V-style y herramientas GNU. Puedes frecuentemente decirme la diferencia por señalar unas páginas man que tienen el encabezado "BSD General Commands Manual." En algunos casos versiones GNU pueden ser instalados, también (tales como `gawk` y `gsed` para awk y sed del GNU). Si escribe cross-platform scripts Bash, evita tales comandos (por ejemplo, considerando Python o `perl`) o probar con mucho cuidado.


## Más recursos

- [awesome-shell](https://github.com/alebcay/awesome-shell): Una lista curada de herramientas shell y recursos.
- [Strict mode](http://redsymbol.net/articles/unofficial-bash-strict-mode/) para escribir mejores script shell.


## Advertencia

Con excepción de pequeñas tareas, el código está escrito para que otros puedan leerlo. Con el poder llega la responsabilidad. El hecho de que tú *puedes* hacer algo en Bash no necesaria mente significa que debas hacerlo! ;)


## Licencia

[![Creative Commons License](https://i.creativecommons.org/l/by-sa/4.0/88x31.png)](http://creativecommons.org/licenses/by-sa/4.0/)

Este trabajo esta licenciado bajo [Creative Commons Attribution-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-sa/4.0/).
