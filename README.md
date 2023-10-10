# hyprland
Guía de hyprland base (Arch Linux)

### @nachoodubra ArchLinux 2023
### *hola perras malvadas, bueno aca voy a ir poniendo todo para el hyprland...*


### ¡¡¡aviso importante!!!, si tenes ya arch linux con hyprland, anda a configuracion con el entorno ya creado 



# primer arranque de hyprland

lo primero que hay que hacer, es activar el terminal kitty, (por lo general viene ya con la instalacion del entorno grafico.).
para activarlo, se usa la tecla win + q. 

con esto abriremos un terminal, (medio feo por cierto), que con este vamos a instalar los paquetes para instalar la personalizacion de hyprland

lo primero que instalaremos el el paquete de git. para ello en la terminal tipeamos esto:
    
###    sudo pacman -S git

luego, pedira la contraseña del sudo (superusuario). para poder instalar correctamente el paquete (te pedira si lo queres instalar, dale "s" y enter).

despues de esto, yo voy a dejar aca para que copien los archivos de personalizacion (llamados dotfiles), para  que los clonen (justamente para eso les hago instalar git).
(aviso, los dotfiles no son mios, no me maten xd).
para copiar los archivos, deben dejarlos en la carpeta /home/$su_nombre_de_usuario

### git clone https://gitlab.com/stephan-raabe/dotfiles.git

una vez halla terminado de pasar esos archivos (por sierto, no es mucho) vamos a entrar a la carpeta con el comando

### cd dotfiles/

cuando estemos en esta carpeta (obvio, toda la instalacion se hace por medio del terminal (por ahora kitty)) los que vamos a encontrar es un menjunje de carpetas (no le den pelota.) y un par de archivos, los que si nos importan
estos archivos, son los que van a hacer la instalacion mas facil (ya que son automaticos). los que usaremos de ahi seran estos:

### 1-install.sh

### 2-install-hyprland.sh

### 3-dotfiles.sh

el problema ahora, es que no vamos a poder iniciarlos, ya que le faltan un par de permisos, los cuales se los vamos a dar con el comando:

### sudo chmod +wxr nombre del archivo.sh

(cabe aclarar que esto hay que hacerlo con los 3 archivos, pero 1 sola vez).

luego de haber terminado eso, vamos a lo que nos importa, ejecutar los scripts de autoinstalacion. para ello, usaremos:

### ./nombre del archivo.sh

### ejemplo: ./1-install.sh

los ejecutaremos en orden 1, 2, 3. el primer script es el que mas va a tardar porque instalara las dependencias correspondientes para la personalizacion.

el segundo script te dara las opciones de acomodo de teclas y atajos del entorno (lo veremos mas abajo), y acomodara las dependencias para los dotfiles.

el tercer script va a crear un acceso directo a todas las configuraciones de los dotfiles(personalizacion) en la pc. (por eso es importante NO BORRAR DOTFILES).

#### ¡¡¡aviso!!!, una vez termine el primer script vamos a instalar el segundo, lo cual va a pedir que reiniciemos, reinicia y segui con la instalacion de los dotfiles.
en el tercer script, tambien vamos a reiniciar, para un mejor acomodo de archivos.

una vez terminemos esta parte, vamos por la mejoracion de la personalizacion, y mejorarlo a nuestro gusto:

# configuracion con el entorno ya creado...

okey, esta parte es la mejor, vamos a personalizar los atajos del teclado como se nos cante y acomodar la barrita de arriba o lo que quieran....

para ello, vamos a iniciar un terminal con las teclas "win + enter(el enter tambien se conoce como return)"

cuando iniciamos el terminal, ya no estaremos en kitty, sino en uno que instalamos al hacer la personalizacion, (llamado alacritty).
en este terminal, vamos a abrir, con nvim, vim, o nano,  el archivo hyprland.conf con este comando:

### nvim .config/hypr/hyprland.conf

en este encontraremos varias configuraciones importantes, pero aca lo unico que vamos a tocar es la configuracion del teclado.

### en la parte de $keyboardlayout, vamos a poner latam, para acomodar el teclado al español latino.
asi:
### $keyboardlayout = latam

luego de eso, vamos a guardar el archivo y vamos a abrir otro para ya configurar las teclas a nuestro modo. (para esto hay otros archivos).

### vamos a entrar al archivo keybindings.conf para poner nuestras combinaciones de teclas para abir programas.
asi: 
### nvim .config/hypr/conf/keybindings.conf

ahi vas a encontrar bastante para mover con el teclado, como??? bueno, vamos a crear lineas de codigo, en los lugares donde se ve algo asi:

### bind = $mainMod CTRL, Q, exec, wlogout


una vez encontremos algo asi, en la parte de abajo de ese parrafo, vamos a agregar atajos con este metodo:

### bind = $mainMod tecla, letra, exec, nombredelprograma


por ejemplo: 
### bind = $mainMod CTRL, Q, exec, wlogout ($mainMod, se llama a la tecla windows)

y con esa base, podemos poner las combinaciones que se nos canten, y obvio, los programas que nos guste linkear.


voy a poner ejemplos de los atajos standard que vienen:

### bind = $mainMod, 1, workspace, 1-10 (con esto, nos movemos entre escritorios virtuales, para manejar aplicaciones)


### bind = $mainMod CTRL, Q, exec, wlogout (esta se agrega con la personalizacion, pero nos da la posibilidad de un menu de inicio, para reiniciar, apagar o suspender el pc)


y aca dejo unas lineas que van debajo, (antes de #passthrough SUPER KEY...) para controlar el volumen y brillo con el teclado:

### binde = , XF86MonBrightnessUp, exec, brightnessctl set +10%

### binde = , XF86MonBrightnessDown, exec, brightnessctl set 10%-

### binde = , XF86AudioLowerVolume, exec, pactl set-sink-volume 0 -5%

### binde = , XF86AudioRaiseVolume, exec, pactl set-sink-volume 0 +5%

### binde = , XF86AudioMute, exec, pactl set-sink-volume 0 0%


metan mano, pero siempre hagan copias de seguridad de los archivos, para no perderlos en un cambio y tener que volver a instalar los scripts estos que son complicados.


# Wallpapers

bueno, para los fondos de pantalla, hay una carpeta en /home/$su_nombre_de_usuario que se llama Wallpapers.
aqui adentro, pueden poner mas fondos para el entorno, yo recomiendo que bajen un par y los metan, deben ser .jpg y cuanta mas resolucion, mejor.


# Decoration

hay un archivo en esta carpeta (.config/hypr/conf/) llamado decoration.conf con el cual podemos cambiar el blur de las ventanas abiertas (lo borroso y transparente que se ven) o el redondeo que se le da a las ventanas.

### la linea que esta en # que es blurls = waybar, activenla si quieren, le da un efecto de borrosidad a la barra superior pero no queda muy lindo.


# Window.conf

con este archivo (en la misma carpeta que el anterior.) podemos acomodar las ventanas abiertas como mas nos guste.
acomodar el borde, los margenes y los colores de los bordes.

para mejorar la experiencia, vamos a ir a la configuracion de la barra superior:

# Waybar

esta famosa barrita, nos va a dar una opcion inmensa de personalizacion, (utiliza un estilzador .css)

para arrancar con esto, vamos a la carpeta "/home/$su_nombre_de_usuario/.config/waybar" donde aca se va a ver toda la config de la barra

para cambiar la posicion, vamos a ir al archivo config, (logico, lo abrimos con nvim o vim o nano).

### si la queremos abajo, vamos a poner "//" en estas lineas

    // Position TOP
###     "layer": "top",

###     "margin-top": 2,

###     "margin-bottom": 0,


### para luego acomodar la parte de bottom sacando las "//"

y asi, vamos a guardar el archivo, cuando se guarde apretaremos win + shift + W para reiniciar el entorno y ver los cambios que hemos hecho.
ahora la barra esta en la parte de abajo.


y bueno, para los que saben .css, es mucho mas simple porque es eso nada mas, (la carga de modulos no lo vi, pero voy a ir actualizando esto).

### para acomodar el css... estando en la carpeta /home/$su_nombre_de_usuario/.config/waybar/

### vamos a usar nvim, vim o nano para abrir el archivo style.css donde esta lo que le da vida a la barra.


bueno, aca es solo cuestion de ver sus gustos y ver como les gusta a ustedes las modificaciones, prueben bastante.
apliquen los cambios y, reinicien el entorno (dije arriba como se hace).

### podemos modificar el color, los bordes de los botones, la opacidad, y obvio, agregar botones


por ahora no he tenido mucho mas, ya que recien arranco con esto, pero es muy buena opcion como entorno, ya que no consume nada de rercursos (500 mb de memoria ram, sin abrir nada).

mantenganme al tanto de cualquier cosa y lo agregare a esta pequeña guia.

@nachodubra ArchLinux 2023
