[ Languages: [English](README.md), [Español](README-es.md), [한국어](README-ko.md), [Português](README-pt.md), [Русский](README-ru.md), [Slovenščina](README-sl.md), [中文](README-zh.md) ]


# El Arte del Terminal

[![Join the chat at https://gitter.im/jlevy/the-art-of-command-line](https://badges.gitter.im/Join%20Chat.svg)](https://gitter.im/jlevy/the-art-of-command-line?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge&utm_content=badge)

- [Meta](#meta)
- [Fundamentos](#basics)
- [De uso diario](#everyday-use)
- [Procesamiento de archivos y datos](#processing-files-and-data)
- [Depuración del sistema](#system-debugging)
- [One-liners](#one-liners)
- [Obscuro pero útil](#obscure-but-useful)
- [Solo para MacOS X](#macos-x-only)
- [Más recursos](#more-resources)
- [Advertencia](#disclaimer)


![curl -s 'https://raw.githubusercontent.com/jlevy/the-art-of-command-line/master/README.md' | egrep -o '`\w+`' | tr -d '`' | cowsay -W50](cowsay.png)

La fluidez en la terminal es una destreza a menudo abandonada y considerada arcaica, pero ésta ayuda a mejorar tu flexibilidad y productividad como ingeniero en formas obvias y sutiles. Esta guía es una selección de notas y consejos para usar la terminal que encontré útiles al trabajar en Linux. Algunos consejos son elementales y otros bastante específicos, sofisticados u oscuros. Esta guía no es larga, pero si usas y recuerdas todos los puntos aquí mostrados, aprenderás un montón.

Gran parte está en
[originally](http://www.quora.com/What-are-some-lesser-known-but-useful-Unix-commands)
[appeared](http://www.quora.com/What-are-the-most-useful-Swiss-army-knife-one-liners-on-Unix)
en [Quora](http://www.quora.com/What-are-some-time-saving-tips-that-every-Linux-user-should-know),
pero debido al interés mostrado, parece que vale la pena usar Github, donde existen personas más talentosas, que fácilmente pueden sugerir mejoras. Si ves un error o algo que podría ser mejor, por favor, crea un issue o PR (Por supuesto primero revisa la sección meta de PRs/issues.)


## Meta

Alcance:

- Esta guía está enfocada tanto para principiantes como para experimentados. Los objetivos son *diversidad* (todo importa), *especificidad* (dar ejemplos concretos del caso más común), y *concisión* (evitar cosas que no son esenciales o insignificantes que puedas buscar fácilmente en otro lugar). Cada tip es esencial en alguna situación o puede ayudarte a ahorrar tiempo significativo comparado con otras alternativas
- Esta escrito para Linux, con excepción de la sección "[Solo para MacOS X](#macos-x-only)". Muchos de los otros puntos aplican o pueden ser instalados en otros Unices o MacOS (o incluso Cygwin).
- Se enfoca en Bash interactivo, aunque muchos de los consejos se aplican para otros shells y al Bash scripting por lo general.
- Incluye comandos "estándar" Unix, así como aquellos que requieren la instalación especial de un paquete (siempre que sea suficientemente importante para ameritar su inclusión).

Notas:

- Para mantener esto en una página, el contenido está organizado por referencia. Una vez que conozcas la idea básica, puedes verificar o buscar más información en otros lugares (como Google). Usa `apt-get`/`yum`/`dnf`/`pacman`/`pip`/`brew` (según proceda) para instalar  nuevos programas.
- Usa [Explainshell](http://explainshell.com/) para obtener ayuda acerca de un comando, opción o pipes.


## Fundamentos

- Aprende conocimientos básicos de Bash, de hecho escribe `man bash` y verifica el contenido, es bastante fácil de seguir y no es tan largo. Alternar entre shells puede ser agradable, pero Bash es poderoso y siempre está disponible (conocer *solo* zsh, fish, etc., aunque resulte tentador en tu propia laptop, te restringe en muchas situaciones, tales como el uso de servidores existentes).

- Aprende bien al menos un editor de texto. Idealmente Vim (`vi`), pues realmente no tiene competencia cuando de editar en una termianal se trata (incluso si usas Emacs, un IDE, o un editor alternativo (hipster) moderno la mayor parte del tiempo).

- Conoce como leer la documentación con `man` (Para curiosos, `man man` lista las secciones enumeradas, ej. 1 es comandos "regulares", 5 son archivos/convenciones, y 8 para administración). Encuentra las páginas de man con `apropos`. Fíjate que alguno de los comandos no son ejecutables, pero son "Bash builtins", y puedes aprender de ellos con `help` y `help -d`.

- Aprende sobre redirección de salida `>`, entrada `<` y pipes utilizando `|`. `>` sobrescribe el archivo de salida y `>>` añade. Aprenda sobre stdout y stderr.

- Aprende sobre expansión de archivos glob con `*` (y tal vez `?` y `{`...`}`) y "quoting" y la diferencia entre comillas dobles `"` y simples `'`. (Ver más sobre expansión de variables en las siguientes secciones.)

- Familiarízate con la administración de trabajo en Bash: `&`, **ctrl-z**, **ctrl-c**, `jobs`, `fg`, `bg`, `kill`, etc.

- Conoce `ssh` y lo básico de autenticación sin contraseña, vía `ssh-agent`, `ssh-add`, etc.

- Administración de archivos básica: `ls` y `ls -l` (en particular, aprende el significado de cada columna en `ls -l`), `less`, `head`, `tail` y `tail -f` (o incluso mejor, `less +F`), `ln` y `ln -s` (aprende las diferencias y ventajas entre enlaces hard y soft), `chown`, `chmod`, `du` (para un resumen rápido del uso del disco: `du -hs *`). Para administración de archivos de sistema, `df`, `mount`, `fdisk`, `mkfs`, `lsblk`.

- Administración básica de redes: `ip` o `ifconfig`, `dig`.

- Conoce bien las expresiones regulares y varias opciones (flags) para `grep`/`egrep`. Las opciones `-i`, `-o`, `-v`, `-A`, y `-B` son dignas de ser recordadas.

- Aprende el uso de `apt-get`, `yum`, `dnf` o `pacman` (dependiendo del "distro" que uses) para buscar e instalar paquetes. Y asegúrate que tienes `pip` para instalar la herramienta de línea de comando basada en Python (abajo se explica cómo instalar vía `pip`).


## De uso diario

- En Bash, se usa **Tab** para completar los argumentos y **ctrl-r** para buscar a través del historial de comandos.

- En Bash, se usa **ctrl-w** para borrar la última palabra, y **ctrl-u** para borrar todo hasta el inicio de una línea. Se usa **alt-b** y **alt-f** para moverse una palabra, **ctrl-a** para mover el cursor al principio de la línea,  **ctrl-e** para mover el cursor al final de la línea,  **ctrl-k** para eliminar hasta el final de la línea, **ctrl-l** para limpiar la pantalla. `man readline` muestra todos los atajos del teclado que Bash trae integrado por default, son una gran cantidad. Por ejemplo **alt-.** realiza un ciclo a través de los comandos previos, y **alt-*** expande un glob.

- Alternativamente si amas los atajos de teclado "vi-style", usa `set -o vi`.

- `history` muestra los últimos comandos. También existen abreviaciones, tales como, `!$` (último argumento) y `!!` último comando, aunque son fácilmente remplazados con **ctrl-r** y **alt-.**.

- Para volver al directorio de trabajo previo: `cd -`

- Si estás a mitad de camino de escribir un comando pero cambias de opinión, presiona **alt-#** para agregar un `#` al principio, agregándolo como comentario al historial(o usar **ctrl-a**, **#**, **enter**). Luego puedes regresar a este comando vía `history`.

- Usa `xargs` (or `parallel`), son muy poderosos. Nota: puedes controlar cuantos elementos son ejecutados por línea (`-L`), e incluso el paralelismo (`-P`). Si no estás seguro de que estás haciendo las cosas correctamente, primero usa `xargs echo`, (`-I{}` también es práctico). Ejemplos:
```bash
      find . -name '*.py' | xargs grep some_function
      cat hosts | xargs -I{} ssh root@{} hostname
```

- `pstree -p` es útil para mostrar el árbol de procesos.

- Usa `pgrep` y `pkill` para encontrar o señalar procesos por su nombre (`-f` es de mucha ayuda).

- Conoce las señales que puedes enviar a los procesos. Por ejemplo, para suspender un proceso usa `kill -STOP [pid]`. Con `man 7 signal` puedes ver la lista completa

- Usa `nohup` o `disown` para mantener un proceso corriendo en "background"

- Verifica que procesos están escuchando con `netstat -lntp` o `ss -plat` (para TCP; para UDP agrega `-u`).

- Consulta también `lsof` para abrir sockets y archivos.

- Usa `alias` para crear atajos para comandos comúnmente usados. Por ejemplo, `alias ll="las -latr"` crea el alias `ll`

- En scripts Bash, usa `set -x` para depurar la salida. Utiliza el modo estricto cuando se posible. Utiliza `set -e` para abortar en errores. Para ser estrictos sobre los errores utiliza `set -o pipefail` también, (aunque este tema es un poco delicado). Para scripts más complejos, también se puede utilizar `trap`.

- En scripts Bash, subshells (escritos con paréntesis) son maneras convenientes de agrupar comandos. Un ejemplo común es moverse temporalmente hacia un directorio diferente, ejemplo:
```bash
      # do something in current dir
      (cd /some/other/dir && other-command)
      # continue in original dir
```

- En Bash, nota que hay muchas formas de expansión de variables. Para verificar la existencia de una variable: `${name:?error message}`. Por ejemplo, si un script Bash requiere un único argumento, solo escribe `input_file=${1:?usage: $0 input_file}`. Expansión aritmética: `i=$(( (i + 1) % 5 ))`. Secuencias: `{1..10}`. Reducción de strings: `${var%suffix}` y `${var#prefix}`. Por ejemplo si `var=foo.pdf`, entonces `echo ${var%.pdf}.txt` imprime `foo.txt`.

- La salida de un comando puede ser tratado como un archivo con `<(some command)`. Por ejemplo, comparar local `/etc/hosts` con uno remoto:
```sh
      diff /etc/hosts <(ssh somehost cat /etc/hosts)
```

- Conoce acerca "here documents" en Bash, como `cat <<EOF ...`.

- En Bash, redirecciona salidas y errores estándar con: `some-command >logfile 2>&1`. Frecuentemente, para garantizar que un comando no haya dejado abierto un archivo para controlar la entrada estándar vinculada a la terminal en que te encuentras, es una buena práctica puedes agregar `</dev/null`.

- Usa `man ascii` para una buena tabla ASCII con valores hexadecimal y decimales. Para información de codificación general, `man unicode`, `man utf-8`, y `man latin1` son de utilidad.

- Use `screen` o [`tmux`](https://tmux.github.io/) para multiplexar la pantalla, especialmente útil en sesiones ssh remotas y para desconectar y reconectar a una sesión. Una alternativa más minimalista para persistencia de la sesión solo sería `dtach`.

- En ssh conocer cómo hacer un port tunnel con `-L` o `-D` (y de vez en cuando `-R`) es útil, por ejemplo para acceder sitio web desde un servidor remoto.

- Puede ser útil hacer algunas configuraciones a tu conexión de ssh; por ejemplo `~/.ssh/config` contiene la configuración para evitar desconexiones en ciertos entornos de red, utiliza compresión (lo cual es útil con scp sobre conexiones con un bajo ancho de banda), y la multiplexión de los canales para el mismo servidor con un archivo de control local:
```
      TCPKeepAlive=yes
      ServerAliveInterval=15
      ServerAliveCountMax=6
      Compression=yes
      ControlMaster auto
      ControlPath /tmp/%r@%h:%p
      ControlPersist yes
```

- Otras opciones relevantes a ssh son sensitivas a la seguridad y deben ser activadas con cuidado, por ejemplo "per subnet", "host" o "in trusted networks: `StrictHostKeyChecking=no`, `ForwardAgent=yes`

- Para obtener permiso sobre un archivo en forma octal, lo cual es útil para la configuración del sistema pero está disponible con `ls` y es fácil de estropear, usa  algo como
```sh
      stat -c '%A %a %n' /etc/timezone
```

- Para selección interactiva de valores desde la salida de otro comando, usa [`percol`](https://github.com/mooz/percol) o [`fzf`](https://github.com/junegunn/fzf).

- Para la interacción con archivos basados en la salida de otro comando (como `git`), usa `fpp` ([PathPicker](https://github.com/facebook/PathPicker)).

- Para un servidor web sencillo para todos los archivos en el directorio actual (y subdirectorios) disponibles para cualquiera en tu red, usa:
`python -m SimpleHTTPServer 7777` (para el puerto 7777 y Python 2) y `python -m http.server 7777` (para 7777 y Python 3).

- Para ejecutar un comando con privilegios, usa `sudo` (para root) o `sudo -u` (para otro usuario). Usa `su` o `sudo bash` para realmente ejecutar un shell como este usuario. Usa `su -` para simular un login nuevo como root u otro usuario.


## Procesamiento de archivos y datos

- Para localizar un archivo por nombre en el directorio actual usa `find . -iname '*something*'` (o similar). Para encontrar un archivo por nombre en cualquier otro lado usa `locate something` (pero ten en mente que `updatedb` quizás no haya indexado los archivos que han sido recientemente creados).

- Para una búsqueda general de archivos fuente o de datos (más avanzado que `grep -r`), usa [`ag`](https://github.com/ggreer/the_silver_searcher).

- Para convertir HTML a texto: `lynx -dump -stdin`

- Para Markdown, HTML, y todos los tipos de conversión de documentos prueba con [`pandoc`](http://pandoc.org/).

- Si debes manipular XML, `xmlstarlet` es viejo pero bueno.

- Para JSON usa [`jq`](http://stedolan.github.io/jq/).

- Para archivos Excel o CSV, [csvkit](https://github.com/onyxfish/csvkit) proporciona `in2csv`, `csvcut`, `csvjoin`, `csvgrep`, etc.

- Para Amazon S3, [`s3cmd`](https://github.com/s3tools/s3cmd) es conveniente y [`s4cmd`](https://github.com/bloomreach/s4cmd) es el mas rápido. [`aws`](https://github.com/aws/aws-cli) de Amazon es esencial para otras tareas relacionadas al AWS.

- Conoce acerca `sort` y `uniq`, incluyendo opciones de uniq `-u` y `-d` (ver unas líneas más abajo).

- Conoce acerca `cut`, `paste` y `join` para manipular archivos de texto. Muchas personas usan `cut` pero se olvidan acerca de `join`.

- Conoce acerca `wc` para contar nuevas líneas (`-l`), caracteres (`-m`), palabras (`-w`) y bytes (`-c`).

- Conoce acerca `tee` para copiar desde el stdin hacia un archivo y también hacia el stdout, como `ls -al | tee file.txt`.

- Conoce que la localización afecta muchas herramientas de línea de comando en forma delicada, incluyendo el ordenamiento (compaginación) y rendimiento. La mayoría de las instalaciones de Linux configuran `LANG` u otras variables de localización para la configuración local como US English. Pero ten en mente que el ordenamiento puede cambiar si cambia la localización. Y también las rutinas i18n pueden hacer que `sort` u otros comandos se ejecuten más lentamente. En algunas situaciones (tales como la realización de operaciones u operaciones singulares descritas más abajo) puedes ignorar las rutinas i18n por completo y utilizar el sort tradicional basado en bytes, usando `export LC_ALL=C`.

- Conozca aspectos básicos de `awk` y `sed` para manejo de datos. Por ejemplo, sumar todos lo números en la tercera columna de un archivo de texto: `awk '{ x += $3 } END { print x }'`. Esto es probablemente 3X más rápido y 3X más corto que su equivalente en Python.

- Para reemplazar todas las ocurrencias de un string en su lugar, en uno o más archivos:
```sh
      perl -pi.bak -e 's/old-string/new-string/g' my-files-*.txt
```

- Para renombrar varios archivos a la vez de acuerdo a un patrón usa `rename`. Para renombramientos complejos, [`repren`](https://github.com/jlevy/repren) puede ayudar.
```sh
      # Recover backup files foo.bak -> foo:
      rename 's/\.bak$//' *.bak
      # Full rename of filenames, directories, and contents foo -> bar:
      repren --full --preserve-case --from foo --to bar .
```

- Usa `shuf` para mezclar o seleccionar líneas aleatorias de un archivo.

- Conoce las opciones de `sort`. Para números usa `-n`, o `-h` para manipulación de números humanamente leíbles (Ej. desde `du -h`). Conoce el trabajo principal de (`-t` y `-k`). En particular, verifica que necesitas  escribir `-k1,1` para ordenar solo por el primer campo; `-k1` significa ordenar de acuerdo a toda la línea. Orden estable (`sort -s`) puede ser útil. Por ejemplo, para ordenar primero por el campo 2, y luego secundariamente por el campo 1, puedes usar `sort -k1,1 | sort -s -k2,2`.

- Si alguna vez necesitas escribir un tab literal en una línea de comandos en Bash (por ejemplo para el argumento -t de ordenar), presiona **ctrl-v** **[Tab]** o escribe `$'\t'` (El último es mejor porque puedes copiarlo/pegarlo).

- Las herramientas estándar para reparar el código fuente son `diff` y `patch`. Checa también `diffstat` para un resumen estadístico de un diff. Nota que `diff -r` trabaja con directorios por completo. Usa `diff -r tree1 tree2 | diffstat` para el resumen de cambios.

- Para archivos binarios usa `hd` para sencillos "hex dumps" y `bvi` para edición de binario.

- También para archivos binarios, `strings` (además de `grep`, etc.) te permite encontrar "bits" de texto.

- Para diffs binarios (delta compression), usa `xdelta3`.

- Para convertir la codificación del texto, prueba con `iconv` o `uconv` para un uso avanzado, éste soporta algunas cosas de Unicode avanzadas. Por ejemplo, coloca minúsculas y remueve todos los acentos (por expansión y colocándolos a ellos):
```sh
      uconv -f utf-8 -t utf-8 -x '::Any-Lower; ::Any-NFD; [:Nonspacing Mark:] >; ::Any-NFC; ' < input.txt > output.txt
```

- Para dividir archivos en múltiples partes, consulta `split` (para dividir por tamaño) y `csplit` (para dividir por un patrón).

- Usa `zless`, `zmore`, `zcat`, y `zgrep` para operar sobre archivos comprimidos.


## Depuración del sistema

- Para depuración web, `curl` y `curl -I` son prácticos, o sus equivalentes `wget`, o el más moderno [`httpie`](https://github.com/jakubroztocil/httpie).

- Para el estado del disco/cpu/red, usa `iostat`, `netstat`, `top` (o el mejor `htop`), y (especialmente) `dstat`. Es bueno para dar un vistazo rápido de lo que está pasando en tu sistema.

- Para una resumen más profundo usa [`glances`](https://github.com/nicolargo/glances). Éste presenta varios niveles de estadística en un solo terminal. Muy útil para una verificación rápida de varios subsistemas.

- Para conocer el estado de la memoria, ejecuta y entiende la salida de `free` y `vmstat`. En particular, ten en cuenta que el valor "cached" es memoria mantenida por el kernel Linux como un archivo de cache, entonces efectivamente cuenta como valor para "free".

- El sistema de depuración de Java es harina de otro costal, pero un truco simple en las JSM de Oracle y de otros consta en que puedes ejecutar `kill -3 <pid>` y una traza completa y un resumen del montículo "heap summary" (incluyendo del detalle de la colección de basura generacional, la cual puede ser altamente informativa) serán descargados al stderr/logs. Las herramientas `jps`, `jstat`, `jstack`, `jmap` del JDK son útiles. [SJK tools](https://github.com/aragozin/jvm-tools) son más avanzadas.

- Usa `mtr` como un mejor traceroute para identificar los problemas en la red.

- Para mirar porque el disco está lleno, `ncdu` ahorra tiempo en comparación con los comandos usuales como `du -sh *`.

- Para encontrar cual socket o proceso está utilizando el ancho de banda, prueba `iftop` o `nethogs`.

- La herramienta `ab` (viene con Apache) es útil para una verificación rápida del rendimiento de un servidor web. Para pruebas de carga más complejas prueba `siege`.

- Para depuración de redes más serias, `wireshark`, `tshark`, o `ngrep`.

- Conoce acerca `strace` y `ltrace`. Estas son de utilidad si un programa está fallando, se queda colgado y no conoces por qué, o si quieres tener una idea general acerca del rendimiento. Nota la opción de elaboración de perfiles (`-c`), y la habilidad de adjuntar a un proceso en ejecución (`-p`).

- Conoce acerca `ldd` para verificar librerías compartidas etc.

- Conoce como conectarse a un proceso en ejecución con `gdb` y obtener su traza de pilas.

- Usa `/proc`. Este es extraordinariamente útil para depurar problemas "en vivo". Ejemplos: `/proc/cpuinfo`, `/proc/xxx/cwd`, `/proc/xxx/exe`, `/proc/xxx/fd/`, `/proc/xxx/smaps`.

- Cuando se depura porque algo salió mal en el pasado, `sar` puede ser muy útil. Éste muestra la estadística histórica en CPU, memoria, red, etc.

- Para sistemas y análisis de rendimiento de mayor profundidad, checa `stap` ([SystemTap](https://sourceware.org/systemtap/wiki)), [`perf`](http://en.wikipedia.org/wiki/Perf_(Linux)), y [`sysdig`](https://github.com/draios/sysdig).

- Verifica que OS te encuentras con `uname` o `uname -a` (información general Unix/kernel) o `lsb_release -a` (Linux distro info).

- Usa `dmesg` siempre que algo actúe raro (esto podría ser problemas con el hardware o driver).


## One-liners

Algunos ejemplos de comandos reunidos:

- Es bastante útil que en ocasiones realices intersecciones, unión, y diferencies el texto de los archivos con `sort`/`uniq`. Supon que `a` y `b` son archivos de texto únicos. Es rápido y se puede trabajar con archivos de tamaño arbitrario hasta varios gigabytes. (Sort no está limitado por memoria, aunque quizás necesites utilizar la opción `-T` si `/tmp` está en una pequeña partición raíz.) Ver también la nota acerca `LC_ALL` y las opciones de `sort`, `-u` (dejado de lado para clarificar más abajo).
```sh
      cat a b | sort | uniq > c   # c is a union b
      cat a b | sort | uniq -d > c   # c is a intersect b
      cat a b b | sort | uniq -u > c   # c is set difference a - b
```

- Usa `grep . *` para visualizar el contenido de todos los archivos en un directorio, por ejemplo para directorios llenos de parámetros con configuración, como `/sys`, `/proc`, `/etc`.


- Sumar todos los números en la tercera columna de un archivo de texto (esto es probablemente 3 veces más rápido y 3 veces menor código que la equivalencia en Python):
```sh
      awk '{ x += $3 } END { print x }' myfile
```

- Si quieres ver tamaños/fechas en un árbol de archivos, el siguiente comando es como hacer un `ls -l` recursivo, pero es más fácil de leer que `ls -lR`:
```sh
      find . -type f -ls
```

- Digamos que tienes un archivo de texto, como un log de un servidor web, y un cierto valor comienza a aparecer en algunas líneas, tales como un parámetro `acct_id` que está presente en el URL. Si quieres un recuento de cuantas peticiones existen por cada `acct_id`:
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

- `m4`: procesador de macro sencillo 

- `yes`: imprime un string sin fin

- `cal`: lindo calendario

- `env`: ejecuta un comando (útil en scripts)

- `printenv`: imprime las variables del ambiente (útil en depuración y scripts)

- `look`: buscar palabras en inglés (o líneas en un archivo) comenzando con un string

- `cut`, `paste` y `join`: manipulación de datos

- `fmt`: Formatea párrafos de texto

- `pr`: Formatea texto en páginas/columnas

- `fold`: Ajusta de líneas de texto

- `column`: Formatea texto en columnas o tablas

- `expand` y `unexpand`: convertidor entre tabuladores y espacios

- `nl`: agrega números de línea

- `seq`: imprime números

- `bc`: calculadora

- `factor`: factorización de enteros

- [`gpg`](https://gnupg.org/): encripta y firma archivos

- `toe`: tabla de información de términos

- `nc`: depuración del entorno de red y transferencia de datos

- `socat`: socket relay y redireccionador de puerto tcp (similar a `netcat`)

- [`slurm`](https://github.com/mattthias/slurm): visualización del tráfico de red

- `dd`: moviliza data entre archivos y dispositivos

- `file`: identifica el tipo de archivo

- `tree`: muestra directorios y subdirectorios como un árbol anidado; parecido a `ls` pero recursivo

- `stat`: información del archivo

- `tac`: imprime archivos en forma inversa

- `shuf`: selecciona líneas de forma aleatoria en un archivo

- `comm`: compara archivos ordenados línea por línea

- `pv`: monitor del progreso de datos, a través, de un tubo

- `hd` y `bvi`: descarga o edita archivos binarios

- `strings`: extrae textos de archivos binarios

- `tr`: traducción y manipulación de caracteres

- `iconv` o `uconv`: conversión de codificaciones de texto

- `split` y `csplit`: división de archivos

- `sponge`: lee todas las entradas antes de escribirlo, útil para vista previa y posterior escritura hacia el mismo archivo, Ej., `grep -v something some-file | sponge some-file`

- `units`: unidades de conversión y calculaciones; convierte furlongs por fortnight para twips por blink (ver también `/usr/share/units/definitions.units`)

- `7z`: compresión de archivos de alto nivel

- `ldd`: información de librería dinámica

- `nm`: archivo de objeto de símbolos

- `ab`: benchmarking de servidores web

- `strace`: depuración de llamadas del sistema

- `mtr`: mejor traceroute para la depuración de la red

- `cssh`: shell concurrent visual

- `rsync`: sincronización de archivos y carpetas sobre SSH o en sistemas de archivos locales

- `wireshark` y `tshark`: captura de paquetes y depuración de la red

- `ngrep`: grep para la capa de la red

- `host` y `dig`: consulta DNS

- `lsof`: descriptor de archivo de procesos y información de socket

- `dstat`: sistema de estadísticas útil

- [`glances`](https://github.com/nicolargo/glances):vistazo de multi-subsistemas de alto nivel

- `iostat`: estadísticas del CPU y uso del disco

- `htop`: versión mejorada de top

- `last`: historial de login

- `w`: Muestra quien está autenticado

- `id`: información de identidad de usuario/grupo

- `sar`: sistema de estadísticas histórico

- `iftop` o `nethogs`: utilización de la red por un socket o process

- `ss`: estadísticas de socket

- `dmesg`: arranque y sistema de mensajes de error

- `hdparm`: manipulación/rendimiento de discos SATA/ATA

- `lsb_release`: información de la distribución de Linux

- `lsblk`: lista de bloques de dispositivos: un árbol de vista de sus discos y particiones de disco

- `lshw`, `lscpu`, `lspci`, `lsusb`, `dmidecode`: información de hardware, incluyendo CPU, BIOS, RAID, gráficos, dispositivos, etc.

- `fortune`, `ddate`, y `sl`: um, bien, este depende si tiene la consideración de locomotoras de vapor y citas Zippy "práctico"


## Solo para MacOS X

Estos son puntos relevantes *únicamente* para MacOS.

- Administración de paquetes con `brew` (Homebrew) y/o `port` (MacPorts). Estos pueden ser utilizados para instalar en MacOS muchos de los comandos de arriba.

- Copiar la salida de cualquier comando para una aplicación desktop con `pbcopy` y pegar desde una entrada con `pbpaste`.

- Para abrir un archivo con una aplicación desktop, usar `open` o `open -a /Applications/Whatever.app`.

- Spotlight: Busca archivos con `mdfind` y listar metadata (como información de foto EXIF) con `mdls`.

- Ten en cuenta que MacOS está basado en BSD Unix y cualquier comando (por ejemplo `ps`, `ls`, `tail`, `awk`, `sed`) tiene sutiles variaciones en comparación con Linux, que está en gran parte influenciado por el sistema Unix V-style y herramientas GNU. Puedes notar la diferencia en las páginas man que tienen el encabezado "BSD General Commands Manual." En algunos casos versiones GNU también pueden ser instaladas, (tales como `gawk` y `gsed` para awk y sed del GNU). Si escribe cross-platform scripts Bash, evita tales comandos (por ejemplo, considera Python o `perl`) o prueba con mucho cuidado.


## Más recursos

- [awesome-shell](https://github.com/alebcay/awesome-shell): Una amplia lista de herramientas shell y recursos.
- [Strict mode](http://redsymbol.net/articles/unofficial-bash-strict-mode/) para escribir mejores script shell.


## Advertencia

Con excepción de pequeñas tareas, el código está escrito para que otros puedan leerlo. Con el poder llega la responsabilidad. El hecho de que *puedes* hacer algo en Bash no necesariamente significa que debas hacerlo! ;)


## Licencia

[![Creative Commons License](https://i.creativecommons.org/l/by-sa/4.0/88x31.png)](http://creativecommons.org/licenses/by-sa/4.0/)

Este trabajo esta licenciado bajo [Creative Commons Attribution-ShareAlike 4.0 International License](http://creativecommons.org/licenses/by-sa/4.0/).
