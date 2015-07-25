[ Languages: [English](README.md), [Español](README-es.md), [한국어](README-ko.md), [Português](README-pt.md), [Русский](README-ru.md), [Slovenščina](README-sl.md), [中文](README-zh.md) ]


# El Arte del Terminal

[![Join the chat at https://gitter.im/jlevy/the-art-of-command-line](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/jlevy/the-art-of-command-line?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

- [Meta](#meta)
- [Fundamentos](#basics)
- [Uso diario](#everyday-use)
- [Procesamiento archivos y datos](#processing-files-and-data)
- [Depuración del sistema](#system-debugging)
- [One-liners](#one-liners)
- [Obscuro pero útil](#obscure-but-useful)
- [Solo para MacOS X](#macos-x-only)
- [Más recursos](#more-resources)
- [Advertencia](#disclaimer)


![curl -s 'https://raw.githubusercontent.com/jlevy/the-art-of-command-line/master/README.md' | egrep -o '`\w+`' | tr -d '`' | cowsay -W50](cowsay.png)

La fluidez en el terminal es una destreza a menudo abandonada y considerada arcaica, pero esta mejora su flexibilidad y productividad como ingeniero en formas obvia y sutil. Esta es una selección de notas y consejos al usar el terminal que encontré útiles al trabajar en Linux. Algunos consejos son elementales y algunos bastante específicos, sofisticados u oscuros. Esta página no es larga, pero si usa y recuerda todos los puntos aquí mostrados, usted sabrá un montón.

La mayor parte 
[originalmente](http://www.quora.com/What-are-some-lesser-known-but-useful-Unix-commands)
[apareció](http://www.quora.com/What-are-the-most-useful-Swiss-army-knife-one-liners-on-Unix)
en [Quora](http://www.quora.com/What-are-some-time-saving-tips-that-every-Linux-user-should-know),
pero debido al interés mostrado, parece que vale la pena usar Github, donde existen personas más talentosas que fácilmente pueden sugerir mejoras. Si ve un error o algo que podría ser mejor, por favor, cree un issue o PR! (Por supuesto revise la sección meta de PRs/issues primero.)


## Meta

Alcance:

- Esta guía es tanto para el principiante como para el experimentado. Los objetivos son *diversidad* (todo importa), *especificidad* (dar ejemplos concretos del caso más común), y *concisión* (evitar cosas que no son esenciales o insignificantes que pueda buscar en otro lugar fácilmente). Cada consejo es esencial en alguna situación o significativamente ahorra tiempo comparada con otras alternativas.
- Esta escrito para Linux, con excepción de la sección "[Solo para MacOS X](#macos-x-only)". Muchos de los otros puntos aplican o pueden ser instalados en otros Unices o MacOS (o incluso Cygwin).
- Se enfoca en Bash interactivo, aunque muchos de los consejos se aplican para otros shells y al Bash scripting por lo general.
- Esta incluye tanto comandos "estándar" Unix así como aquellos que requieren la instalación especial de un paquete -- siempre que sea suficientemente importante para ameritar su inclusión.

Notas:

- Para mantener esto en una página, el contenido está incluido implícitamente por referencia. Usted es suficientemente inteligente para ver profundamente los detalles en otros lugares, cuando conoce la idea o comando en Google. Usar `apt-get`/`yum`/`dnf`/`pacman`/`pip`/`brew` (según proceda) para instalar los nuevos programas.
- Usar [Explainshell](http://explainshell.com/) para obtener detalles de ayuda sobre que comandos, opciones, pipes, etc.


## Fundamentos

- Aprenda conocimientos básicos de Bash, de hecho, escriba `man bash` y al menos échele un vistazo a toda la cosa. Es bastante fácil de seguir y no es tan largo. Alternar entre shells puede ser agradable, pero Bash es poderoso y siempre está disponible (conocer *solo* zsh, fish, etc., aunque resulte tentador en tu propia laptop, le restringe en muchas situaciones, tales como el uso de servidores existentes).

- Aprenda bien al menos un editor de texto, idealmente Vim (`vi`), como no hay realmente una competencia para la edición aleatoria en un terminal (incluso si usa Emacs, un gran IDE, o un editor alternativo (hipster) moderno la mayor parte del tiempo).

- Conozca como leer la documentación con `man` (Para curiosos, `man man` lista las secciones enumeradas, ej. 1 es comandos "regulares", 5 son archivos/convenciones, y 8 para administración). Encuentra páginas de man con `apropos`. Sepa que alguno de los comandos no son ejecutables, sino Bash builtins, y que puede obtener ayuda sobre ellos con `help` y `help -d`.

- Aprenda sobre redirección de salida `>`, entrada `<` y pipes `|`. Sepa que `>` sobrescribe el archivo de salida y `>>` añade. Aprenda sobre stdout y stderr.

- Aprenda sobre expansión de archivos glob con `*` (y tal vez `?` y `{`...`}`) y quoting y la diferencia entre dobles `"` y simples `'` quotes. (Ver más en expansión de variables más abajo.)

- Familiarícese con la administración de trabajo en Bash: `&`, **ctrl-z**, **ctrl-c**, `jobs`, `fg`, `bg`, `kill`, etc.

- Conozca `ssh` y lo básico de autenticación sin contraseña, vía `ssh-agent`, `ssh-add`, etc.

- Administración de archivos básica: `ls` y `ls -l` (en particular, aprenda el significado de cada columna en `ls -l`), `less`, `head`, `tail` y `tail -f` (o mejor aun, `less +F`), `ln` y `ln -s` (aprenda las diferencias y ventajas entre enlaces hard y soft), `chown`, `chmod`, `du` (para un resumen rápido del uso del disco: `du -hs *`). Para administración de archivos de sistema, `df`, `mount`, `fdisk`, `mkfs`, `lsblk`.

- Administración básica de redes: `ip` o `ifconfig`, `dig`.

- Conozca bien las expresiones regulares y varias opciones (flags) para `grep`/`egrep`. Las opciones `-i`, `-o`, `-v`, `-A`, `-B` y `-C` son dignas de ser recordadas.

- Aprenda el uso de `apt-get`, `yum`, `dnf` o `pacman` (dependiendo de la distribución "distro") para buscar e instalar paquetes. Y asegúrate que tienes `pip` para instalar herramientas para la línea de comandos basadas en Python (un poco más abajo esta explicado como instalar vía `pip`).


## De uso diario

- En Bash, se usa **Tab** para completar los argumentos y **ctrl-r** para buscar, a través del historial de comandos.

- En Bash, se usa **ctrl-w** para borrar la última palabra, y **ctrl-u** para borrar todo el camino hasta el inicio de la línea. Se usa **alt-b** y **alt-f** para moverse entre letras, **ctrl-a** para mover el cursor al principio de la línea,  **ctrl-e** para mover el cursor al final de la línea,  **ctrl-k** para eliminar hasta el final de la línea, **ctrl-l** para limpiar la pantalla. Vea `man readline` para todos los atajos de teclado por defecto en Bash. Son una gran cantidad. Por ejemplo **alt-.** realiza un ciclo a través de los comandos previos, y **alt-*** expande un glob.

- Alternativamente, si ama los atajos de teclado vi-style, use `set -o vi`.

- Para ver los últimos comandos, `history`. También existen abreviaciones, tales como, `!$` (último argumento) y `!!` último comando, aunque son fácilmente remplazados con **ctrl-r** y **alt-.**.

- Para volver al directorio de trabajo previo: `cd -`

- Si está a mitad de camino de escribir un comando pero cambias de opinión, presiona **alt-#** para agregar un `#` al principio y lo agrega como comentario (o use **ctrl-a**, **#**, **enter**). Asi despues puede regresar al comando vía comando `history`.

- Se usa `xargs` (or `parallel`). Esto es muy poderoso. Nota: puede controlar muchos elementos ejecutados por línea (`-L`), también es conocido como paralelismo (`-P`). Si no está seguro de que este sea el camino correcto, use `xargs echo` primero. También, `-I{}` es cómodo. Ejemplos:
```bash
      find . -name '*.py' | xargs grep some_function
      cat hosts | xargs -I{} ssh root@{} hostname
```

- `pstree -p` es útil para mostrar el árbol de procesos.

- Se usa `pgrep` y `pkill` para encontrar o señalar procesos por su nombre (`-f` es de mucha ayuda).

- Conozca varias señales que pueda enviar a los procesos. Por ejemplo, para suspender un proceso, use `kill -STOP [pid]`. Para la lista completa, consultar `man 7 signal`.

- Use `nohup` o `disown` si quiere mantener un proceso de fondo corriendo para siempre.

- Verifique que procesos están escuchando vía `netstat -lntp` o `ss -plat` (para TCP; agrega `-u` para UDP).

- Consulte también `lsof` para abrir sockets y archivos.

- Consulta `uptime` o `w` para conocer cuánto tiempo el sistema ha estado corriendo.

- Usar `alias` para crear atajos para comandos comúnmente usados. Por ejemplo, `alias ll="las -latr"` crea un nuevo alias `ll`.

- En scripts Bash, use `set -x` para depurar la salida. Use el modo estricto cuando se posible. Use `set -e` para abortar en caso de errores. Use `set -o pipefail` también, para ser estrictos sobre los errores (aunque este tema es un poco delicado). Para scripts más complejos, también se puede utilizar `trap`.

- En scripts Bash, subshells (escritos con paréntesis) son maneras convenientes de agrupar los comandos. Un ejemplo común es para moverse temporalmente hacia un directorio diferente del de trabajo, Ej.
```bash
      # do something in current dir
      (cd /some/other/dir && other-command)
      # continue in original dir
```

- En Bash, considere que hay muchas formas de expansión de variables. Verificar la existencia de una variable: `${name:?error message}`. Por ejemplo, si un script Bash requiere un único argumento, solo escriba `input_file=${1:?usage: $0 input_file}`. Expansión aritmética: `i=$(( (i + 1) % 5 ))`. Secuencias: `{1..10}`. Reducción de strings: `${var%suffix}` y `${var#prefix}`. Por ejemplo si `var=foo.pdf`, entonces `echo ${var%.pdf}.txt` imprime `foo.txt`.

- La salida de un comando puede ser tratada como un archivo, vía `<(some command)`. Por ejemplo, comparar local `/etc/hosts` con uno remoto:
```sh
      diff /etc/hosts <(ssh somehost cat /etc/hosts)
```

- Conozca sobre los "here documents" en Bash, como también `cat <<EOF ...`.

- En Bash, redireccionar salida estándar y error estándar, vía: `some-command >logfile 2>&1`. Frecuentemente, para garantizar que un comando no haya dejado abierto un archivo para controlar la entrada estándar, vinculada al terminal en el que te encuentras, también es una buena práctica agregar `</dev/null`.

- Use `man ascii` para una buena tabla ASCII, con valores hexadecimal y decimales. Para información de codificación general, `man unicode`, `man utf-8`, y `man latin1` son de utilidad.

- Use `screen` o [`tmux`](https://tmux.github.io/) para multiplexar la pantalla, especialmente útil en sesiones ss remotas y para desconectar y reconectar a una sesión. Una alternativa más minimalista para persistencia de la sesión solo sería `dtach`.

- En ssh, saber cómo hacer un port tunnel con `-L` o `-D` (y de vez en cuando `-R`) es útil, Ej. para acceder sitio web desde un servidor remoto.

- Puede ser útil hacer algunas optimizaciones a su configuración ssh; por ejemplo, `~/.ssh/config`, contiene la configuración para evitar desconexiones en ciertos entornos de red, utiliza compresión (cual es útil con scp sobre conexiones con un ancho de banda pequeño), y la multiplexión de canales para el mismo servidor con un archivo de control local:
```
      TCPKeepAlive=yes
      ServerAliveInterval=15
      ServerAliveCountMax=6
      Compression=yes
      ControlMaster auto
      ControlPath /tmp/%r@%h:%p
      ControlPersist yes
```

- Unas pocas otras opciones relevantes para ssh son sensibles en cuanto a seguridad y deben ser usadas con cuidado, Ej. por subnet, host o en redes confiables: `StrictHostKeyChecking=no`, `ForwardAgent=yes`.

- Para obtener permiso sobre un archivo en forma octal, el cual es útil para la configuración del sistema pero no disponible con `ls` y fácil de estropear, use algo como
```sh
      stat -c '%A %a %n' /etc/timezone
```

- Para selección interactiva de valores desde la salida de otro comando, use [`percol`](https://github.com/mooz/percol) o [`fzf`](https://github.com/junegunn/fzf).

- Para la interacción con archivos basados en la salida de otro comando (como `git`), use `fpp` ([PathPicker](https://github.com/facebook/PathPicker)).

- Para un servidor web sencillo para todos los archivos en el directorio actual (y subdirectorios), disponible para cualquiera en tu red, use:
`python -m SimpleHTTPServer 7777` (para el puerto 7777 y Python 2) y `python -m http.server 7777` (para 7777 y Python 3).

- Para ejecutar un comando con privilegios, usando `sudo` (para root) o `sudo -u` (para otro usuario). Usar `su` o `sudo bash` para realmente ejecutar un shell como este usuario. Usar `su -` para simular un login fresco como root u otro usuario.


## Procesamiento de archivos y datos

- Para localizar un archivo por nombre en el directorio actual, `find . -iname '*something*'` (o similar). Para encontrar un archivo en cualquier lado por nombre, use `locate something` (pero tenga en mente que `updatedb` quizás no haya indexado recientemente los archivos creados).

- Para busqueda general sobre la fuente o archivos de datos (más avanzado que `grep -r`), use [`ag`](https://github.com/ggreer/the_silver_searcher).

- Para convertir HTML a texto: `lynx -dump -stdin`.

- Para Markdown, HTML, y todos los tipos de conversión de documentos, pruebe [`pandoc`](http://pandoc.org/).

- Si debe manipular XML, `xmlstarlet` es viejo pero bueno.

- Para JSON, use [`jq`](http://stedolan.github.io/jq/).

- Para archivos Excel o CSV, [csvkit](https://github.com/onyxfish/csvkit) provee `in2csv`, `csvcut`, `csvjoin`, `csvgrep`, etc.

- Para Amazon S3, [`s3cmd`](https://github.com/s3tools/s3cmd) es conveniente y [`s4cmd`](https://github.com/bloomreach/s4cmd) es el mas rápido. Hecho por Amazon [`aws`](https://github.com/aws/aws-cli) es esencial para otras tareas relacionadas al AWS.

- Conocer acerca de `sort` y `uniq`, incluyendo las opciones de uniq `-u` y `-d` -- ver [one-liners](https://github.com/jlevy/the-art-of-command-line/blob/master/README-es.md#one-liners) más abajo.

- Conocer acerca de `cut`, `paste` y `join` para manipular archivos de texto. Muchas personas usan `cut` pero se olvidan acerca de `join`.

- Conocer acerca de `wc` para contar saltos de línea (`-l`), caracteres (`-m`), palabras (`-w`) y bytes (`-c`).

- Conocer acerca de `tee` para copiar desde el stdin hacia un archivo y también hacia el stdout, así `ls -al | tee file.txt`.

- Sepa que `locale` afecta muchas herramientas de la línea de comandos en forma delicada, incluyendo el orden del ordenamiento (compaginación) y rendimiento. La mayoría de las instalaciones de Linux configuran `LANG` u otras variables de localización para la configuración local como US English. Pero tenga en cuenta que el ordenamiento va a cambiar si cambia `locale`. Y también las rutinas i18n pueden hacer que `sort` u otros comandos se ejecuten *muchas veces* más lentos. En algunas situaciones (tales como la realización de operaciones u operaciones singulares debajo) puede de forma segura ignorar las lentas rutinas i18n por completo y utilizar el sort tradicional basado en byte, usando `export LC_ALL=C`.

- Conozca los aspectos básicos de `awk` y `sed` para manejo de datos. Por ejemplo, sumar todos lo números en la tercera columna de un archivo de texto: `awk '{ x += $3 } END { print x }'`. Esto es probablemente 3 veces más rápido y 3 veces más corto que su equivalente en Python.

- Para reemplazar todas las ocurrencias de un string en su lugar, en uno o más archivos:
```sh
      perl -pi.bak -e 's/old-string/new-string/g' my-files-*.txt
```

- Para renombrar varios archivos a la vez de acuerdo a un patrón, usar `rename`. Para renombramientos complejos, [`repren`](https://github.com/jlevy/repren) puede ayudar.
```sh
      # Recuperar archivos de respaldo foo.bak -> foo:
      rename 's/\.bak$//' *.bak
      # Renombramiento completo de archivos, carpetas y contenidos foo -> bar:
      repren --full --preserve-case --from foo --to bar .
```

- Usar `shuf` para mezclar o seleccionar líneas aleatorias desde un archivo.

- Conozca las opciones de `sort`. Para números, use `-n`, o `-h` para manipulación de números humanamente leíbles (Ej. desde `du -h`). Conozca ecomo trabajan `-t` y `-k`. En particular, este atento a que necesitará escribir `-k1,1` para ordenar por solo el primer campo; `-k1` significa ordenar de acuerdo a toda la línea. Orden estable (`sort -s`) puede ser útil. Por ejemplo, para ordenar primero por el campo 2, luego secundariamente hacerlo por el campo 1, Puedes usar `sort -k1,1 | sort -s -k2,2`.

- Si alguna vez necesita escribir un tab literal en una línea de comandos en Bash (Ej. para el argumento -t para 'sort'), presione **ctrl-v** **[Tab]** o escriba `$'\t'` (el último es mejor porque puede copiarlo/pegarlo).

- Las herramientas estándar para reparar el código fuente son `diff` y `patch`. Ver también `diffstat` para resumen estadístico de una diff. Note que `diff -r` trabaja completamente con directorios. Usar`diff -r tree1 tree2 | diffstat` para un resumen de cambios.

- Para archivos binarios, usar `hd` para sencillos "hex dumps" y `bvi` para edición de binario.

- También para archivos binarios, `strings` (además de `grep`, etc.) permite encontrar fragmentos de texto.

- Para diffs binarias (delta compression), usar `xdelta3`.

- Para convertir la codificación del texto, probar `iconv`. O `uconv` para uso más avanzado; este soporta algunos elementos Unicode avanzados. Por ejemplo, este comando coloca en minúsculas y remueve todas los acentos (expandiéndolos y colocándolos):
```sh
      uconv -f utf-8 -t utf-8 -x '::Any-Lower; ::Any-NFD; [:Nonspacing Mark:] >; ::Any-NFC; ' < input.txt > output.txt
```

- Para dividir archivos en múltiples partes, consultar `split` (para dividir por tamaño) y `csplit` (para dividir por un patrón).

- Usar `zless`, `zmore`, `zcat`, y `zgrep` para operar sobre archivos comprimidos.


## Depuración del sistema

- Para depuración web, `curl` y `curl -I` son prácticos, o como sus equivalentes `wget`, o el más moderno [`httpie`](https://github.com/jakubroztocil/httpie).

- Para conocer el estado del disco/cpu/red, usar `iostat`, `netstat`, `top` (o el mejor `htop`), y (especialmente) `dstat`. Bueno para recibir una idea rápida de qué está pasando en un sistema.

- Para una visión general en mayor profundidad, usar [`glances`](https://github.com/nicolargo/glances). Este se presenta con varios niveles de estadística en un solo terminal. Muy útil para una verificación rápida de varios subsistemas.

- Para conocer el estado de la memoria, ejecutar y entender la salida de `free` y `vmstat`. En particular, tener en cuenta el valor "cached" es mantenido en memoria por el kernel Linux como un archivo de cache, por lo que efectivamente cuenta como valor para "free".

- El sistema de depuración de Java es harina de otro costal, pero un truco simple en las JSM de Oracle y otros consta en que puedes ejecutar `kill -3 <pid>` y una traza completa y un resumen del montículo "heap summary" (incluyendo del detalle de la colección de basura generacional, la cual puede ser altamente informativa) serán descargados al stderr/logs. Las herramientas `jps`, `jstat`, `jstack`, `jmap` del JDK son útiles. [SJK tools](https://github.com/aragozin/jvm-tools) son más avanzadas.

- Usar `mtr` como un mejor traceroute, para identificar los problemas en la red.

- Para examinar por qué el disco está lleno, `ncdu` ahorra tiempo sobre los comandos usuales como `du -sh *`.

- Para encontrar cual socket o proceso está utilizando el ancho de banda, pruebe `iftop` o `nethogs`.

- La herramienta `ab` (viene con Apache) es útil para una verificación "rápida y sucia" del rendimiento del servidor web. Para pruebas de carga más complejas, pruebe `siege`.

- Para una depuración mas seria de redes, `wireshark`, `tshark`, o `ngrep`.

- Conozca acerca de `strace` y `ltrace`. Estas puede ser de utilidad si un programa está fallando, está suspendido, o está "congelado/colgado/crasheado", y no sabe por qué, o si quieres tener una idea general del rendimiento. Note la opción de elaboración de perfiles, o "profiling", (`-c`), y la habilidad de adjuntar a un proceso en ejecución (`-p`).

- Conozca acerca de `ldd` para verificar librerías compartidas etc.

- Conozca como conectarse a un proceso en ejecución con `gdb` y obtener su traza de pilas.

- Usar `/proc`. Es extraordinariamente útil algunas veces cuando se depuran problemas en vivo. Ejemplos: `/proc/cpuinfo`, `/proc/xxx/cwd`, `/proc/meminfo`, `/proc/cmdline`, `/proc/xxx/exe`, `/proc/xxx/fd/`, `/proc/xxx/smaps` (donde `xxx` es el id o pid del proceso).

- Cuando se depura porque algo salió mal en el pasado, `sar` puede ser muy útil. Este muestra la estadística histórica en CPU, memoria, red, etc.

- Para análisis de sistemas y de rendimiento más profundos, vea `stap` ([SystemTap](https://sourceware.org/systemtap/wiki)), [`perf`](http://en.wikipedia.org/wiki/Perf_(Linux)), y [`sysdig`](https://github.com/draios/sysdig).

- Confirme en que OS se encuentra con `uname` o `uname -a` (información general en Unix/kernel) o `lsb_release -a` (información en Linux distro).

- Usar `dmesg` siempre que algo actúe raro (esto podría ser problemas con el hardware o driver).


## One-liners

Algunos ejemplos de comandos reunidos:

- Es notablemente útil en ocasiones que pueda realizar intersección, unión, y diferencia de conjuntos de archivos de texto vía `sort`/`uniq`. Suponga `a` y `b` como archivos de texto que son únicos. Esto es rápido, y trabaja con archivos de tamaño arbitrario, hasta varios gigabytes. (Sort no está limitado por la memoria, aunque quizás necesite utilizar la opción `-T` si `/tmp` está en una pequeña partición de raíz.) Vea también la nota acerca de `LC_ALL` y las opciones de `sort`, `-u` (dejado de lado para clarificar más abajo).
```sh
      cat a b | sort | uniq > c   # c es a unido con b
      cat a b | sort | uniq -d > c   # c es a intersectado con b
      cat a b b | sort | uniq -u > c   # c es el conjunto diferencia a - b
```

- Usar `grep . *` para examinar visualmente todos los contenidos de todos los archivos en un directorio, por ejemplo, para directorios llenos con parámetros de configuración, como `/sys`, `/proc`, `/etc`.


- Sumar todos los números en la tercera columna de un archivo de texto (esto es probablemente 3 veces más rápido y 3 veces menos código que el equivalente en Python):
```sh
      awk '{ x += $3 } END { print x }' myfile
```

- Si quiere ver tamaños/fechas en un árbol de archivos, esto es como hacer recursivo `ls -l` pero es más fácil de leer que `ls -lR`:
```sh
      find . -type f -ls
```

- Digamos que tiene un archivo de texto, como un log de un servidor web, y un cierto valor comienza a aparecer en algunas líneas, tales como un parámetro `acct_id` que está presente en la URL. Si quieres un recuento de cuantas peticiones ("request") hay por cada `acct_id`:
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

- `expr`: ejecuta operaciones aritméticas o booleanas, o evalúa expresiones regulares

- `m4`: procesador de macro sencillo 

- `yes`: imprime un string sin fin

- `cal`: lindo calendario

- `env`: ejecuta un comando (útil en scripts)

- `printenv`: imprime las variables del entorno (útil en depuración y scripts)

- `look`: buscar palabras en inglés (o líneas en un archivo) comenzando con un string

- `cut`, `paste` y `join`: manipulación de datos

- `fmt`: da formato a párrafos de texto

- `pr`: da formato al texto en páginas/columnas

- `fold`: envuelve líneas de texto

- `column`: da formato al texto en columnas o tablas

- `expand` y `unexpand`: conversión entre tabuladores y espacios

- `nl`: agrega números de línea

- `seq`: imprime números

- `bc`: calculadora

- `factor`: factorización de enteros

- [`gpg`](https://gnupg.org/): cifrado y firmas digitales

- `toe`: tabla de información de términos

- `nc`: depuración de la red y transferencia de datos

- `socat`: socket relay y redireccionador de puerto tcp (similar a `netcat`)

- [`slurm`](https://github.com/mattthias/slurm): visualización del tráfico de red

- `dd`: moviliza data entre archivos o dispositivos

- `file`: identifica el tipo de archivo

- `tree`: muestra directorios y subdirectorios como un árbol anidado; parecido a `ls` pero recursivo

- `stat`: información del archivo

- `time`: ejecuta y calcula el tiempo de ejecución de un comando

- `tac`: imprime archivos en forma inversa

- `shuf`: selección aleatoria de líneas de un archivo

- `comm`: compara archivos ordenados línea por línea

- `pv`: monitorea el progreso de datos a través de un tubo

- `hd` y `bvi`: descarga o edita archivos binarios

- `strings`: extrae texto desde archivos binarios

- `tr`: traducción o manipulación de caracteres

- `iconv` o `uconv`: conversión de codificaciones de texto

- `split` y `csplit`: división de archivos

- `sponge`: lee todas las entradas antes de escribirlo, útil para vista previa y posterior escritura sobre el mismo archivo, Ej., `grep -v something some-file | sponge some-file`

- `units`: unidades de conversión y cálculos; convierte furlongs por fortnight a twips por blink (ver también `/usr/share/units/definitions.units`)

- `7z`: compresión de archivos de alto nivel

- `ldd`: información de librería dinámica

- `nm`: símbolos de archvios objeto

- `ab`: benchmarking de servidores web

- `strace`: depuración de llamadas del sistema

- `mtr`: mejor traceroute para la depuración de la red

- `cssh`: shell concurrente visual

- `rsync`: sincronización de archivos y carpetas sobre SSH o en sistema de archivos locales

- `wireshark` y `tshark`: captura de paquetes y depuración de la red

- `ngrep`: grep para la capa de la red

- `host` y `dig`: consultas DNS

- `lsof`: descriptor de archivo de procesos e información de socket

- `dstat`: sistema de estadísticas útil

- [`glances`](https://github.com/nicolargo/glances): visión general de multi-subsistemas, de alto nivel

- `iostat`: estadísticas del uso del disco duro

- `mpstat`: estadísticas del uso del CPU

- `vmstat`: estadísticas del uso de la memoria

- `htop`: versión mejorada de top

- `last`: historial de login

- `w`: quién está autenticado

- `id`: información de identidad de usuario/grupo

- `sar`: estadísticas históricas del sistema

- `iftop` o `nethogs`: utilización de la red por un socket o proceso

- `ss`: estadísticas de socket

- `dmesg`: mensajes de error del arranque y del sistema 

- `hdparm`: manipulación/rendimiento de discos SATA/ATA

- `lsb_release`: información de la distribución de Linux

- `lsblk`: lista de dispositivos de bloque: una vista tipo arbol de sus discos y particiones de disco

- `lshw`, `lscpu`, `lspci`, `lsusb`, `dmidecode`: información de hardware, incluyendo CPU, BIOS, RAID, gráficos, dispositivos, etc
 
- `lsmod` y `modifno`: lista y muestra detalles de los módulos del kernel

- `fortune`, `ddate`, y `sl`: um, bien, depende de si considera las locomotoras de vapor y citas Zippy "útiles"


## Solo para MacOS X

Estos son puntos relevantes *solo* en MacOS.

- Administración de paquetes con `brew` (Homebrew) y/o `port` (MacPorts). Estos pueden ser utilizados para instalar en MacOS muchos de los comandos de arriba.

- Copie la salida de cualquier comando en una aplicación de escritorio con `pbcopy` y pegue una entrada con `pbpaste`.

- Para abrir un archivo con una aplicación de escritorio, use `open` o `open -a /Applications/Whatever.app`.

- Spotlight: Busque archivos con `mdfind` y liste metadata (tal como información de foto EXIF) con `mdls`.

- Tenga en cuenta que MacOS está basado en BSD Unix, y muchos comandos (por ejemplo `ps`, `ls`, `tail`, `awk`, `sed`) tienen muchas variaciones discretas respecto de Linux, que está en gran parte influenciado por el sistema Unix V-style y herramientas GNU. Comunmente puede diferenciar al notar que una página man tienen el encabezado "BSD General Commands Manual." En algunos casos versiones GNU pueden ser instaladas también (tales como `gawk` y `gsed` para GNU awk y sed). Si escribe scripts Bash multiplataforma, evite tales comandos (por ejemplo, considere Python o `perl`) o probar cuidadosamente.


## Más recursos

- [awesome-shell](https://github.com/alebcay/awesome-shell): Una lista curada de herramientas y recursos para la shell.
- [Strict mode](http://redsymbol.net/articles/unofficial-bash-strict-mode/) para escribir mejores scripts shell.


## Advertencia

Con la excepción de tareas muy pequeñas, el código está escrito para que otros puedan leerlo. Con el poder llega la responsabilidad. El hecho de que usted *puede* hacer algo en Bash no necesariamente significa que deba hacerlo! ;)


## Licencia

[![Creative Commons License](https://i.creativecommons.org/l/by-sa/4.0/88x31.png)](http://creativecommons.org/licenses/by-sa/4.0/)

Este trabajo está licenciado bajo [Creative Commons Attribution-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-sa/4.0/).
