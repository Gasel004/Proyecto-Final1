#Basicamente se trata de crear un editor de texto.
#Teniendo las siguientes opciones en la barr opciones de; Abrir, Guardar y Guardar Como.
#Editar; Deshacer (Control +a superior; 
#Archivo: debe desplegar las Z) y Rehacer (Control + Y).
#Ayuda; Información, Manual de usuario y integrantes.

#Importamos las diferentes librerias y modulos que usaremos a lo largo de nuestro programa.

#Importamos "Tkinter" la cual contiene elementos basicos ya incluidos para crear X programa en este caso un editos basico de texto.
from tkinter import *
#Impotamos el modulo "Filedialog" el cual ya viene incluido en la libreria tkinter y nos ayuda a abrir varias ventanas a la vez.
from tkinter import filedialog
#Importamos el modulo "Webbrowser" el cual nos ayudara para abrir enlaces a paginas o archivos online.
import webbrowser
#Iniciamos nuestra función abrir la cual tiene como función abrir el documento que el usuario desee.
def abrir():
    #Asignamos los tipos de archivo que nuestro programa podra manejar en nuestro caso son los siguientes:
    tipos_archivo = [("Todos los archivos", "*.*"), ("Archivos de texto", "*.txt"), ("C++", "*.cpp"), ("C#", "*.cs"), ("Py", "*.py"), ("JV", "*.jar"), ("JavaScrip", "*js")]
    #Aplicamos el módulo "filedialog" para poder manejar varias ventanas a la vez de nuestro editor de texto.
    archivo = filedialog.askopenfile(filetypes=tipos_archivo)
    #El programa leera el arhivo que desee el usuario y lo agregara.
    if archivo:
        contenido = archivo.read()
        archivo.close()
        crear_nueva_ventana(contenido)
#Iniciamos nuestra función guardar la cual nos ayudara para hacer un guardado rapido si nuestro documento ya esta previamente guardado
def guardar():
    documento = texto.get("1.0", "end-1c")
    if archivo_actual:
#guardamos nuestro arhivo por ello la letra"W"
        with open(archivo_actual, "w") as archivo:
#sobreescrimis en nuestro archivo los nuevos caracteres
            archivo.write(documento)
#Iniciamos nuestra función "guardar_como" que nos serivira para que el usario seleccine la ruta en donde se guardara su archivo y el tipo que quiera darle al mismo.
def guardar_como():
    #Insertamos los tipos de arhivo que nuestro editor soportará los cuales son los siguientes:
    tipos_archivo = [("Archivos de texto", "*.txt"), ("C++", "*.cpp"), ("C#", "*.cs"), ("Py", "*.py"),("JV", "*.jar"), ("JavaScrip", "*js")]
    #hacemos uso del modúlo filedialog para que podamos hacerlo en varias ventanas a la vez
    archivo = filedialog.asksaveasfile(filetypes=tipos_archivo, defaultextension=".txt")
    if archivo:
        documento = texto.get("1.0", "end-1c")
        #sobreescribios si ya existe un archivo con dicho nombre.
        archivo.write(documento)
#Iniciamos nuestra función para abrir una nueva ventana para abrir varios archivos a la vez:
def crear_nueva_ventana(contenido):
    nueva_ventana = Toplevel(root)
#Le damos nombre a nustra nueva ventana
    nueva_ventana.title("Editor")
#Definimos los valores predeterminados que tendra nuestro archivo nuevo.
    texto_nueva_ventana = Text(nueva_ventana)
    texto_nueva_ventana.grid(row=1, columnspan=5)
    texto_nueva_ventana.config(font=('arial', 10, 'normal'))
    texto_nueva_ventana.insert(INSERT, contenido)
#Iniciamos nuestra función para aplicar formato que tiene como función poder modificar el tipo de letra y su tamaño según los deseos del usuario.
def aplicar_formato():
    estilo = formato_fuente.get()
    inicio, fin = texto.tag_ranges("sel")
#Iniciamos un if para aplicar los cambios en el texto que el usario decida hacer y que puedan ser lo mas independientes posibles
    if inicio and fin:
        texto.tag_add(estilo, inicio, fin)
        texto.tag_configure(estilo, font=(fuente.get(), tamano_fuente.get(), estilo))
    #En caso el usuario aplique cambios a una linea vacía se le mostrar el siguiente mensaje:
    else:
        messagebox.showinfo("Error","\nSelecciona un rango donde se encuentre algún texto para aplicar el formato.")
#Iniciamos nuestra función "Informació" la cual contendra datos sonbre nuestra aplicación.
def información():
    webbrowser.open("https://drive.google.com/file/d/1wj_iwJoqrzcWWd6z9MVsQFMO5fWowpsC/view?usp=drive_link")
#Inciamos nuestra función "Manueal_De_usario" la cual nos abrira el siguiente link; con el manual respectivo de nuestra aplicación.
def Manual_usuario():
    webbrowser.open("https://drive.google.com/file/d/16xSVOq7w172nKruh6VRs7EEoBtzr4ZXH/view?usp=drive_link")
#Definimos nuestra función "Integrantes" la cual se encarga de mostrar los nombre de los integrantes y su respectivo grupo.
def Integrantes():
    print("Integrantes Grupo#3\n", "\n1. ELmer Yovani Rodríguez de Paz 7690-22-11804\n2. Erasmo Raul Garcia Tambito\n3. Marco Tulio De leon Rivera")

root = Tk()
root.title("Editor")

# Variable para almacenar el archivo actual
archivo_actual = None

#Creamos nuetra barra de opciones con los datos de la libreria tkinter. 
barra_opciones = Menu(root)

#Creamos nuestra barra superior con nuestras opciones
#Agregamos la opción "Archivo" a nuestra barra superior la cual tendra las siguientes opciones y sera la primera opción:
menu_archivo = Menu(barra_opciones, tearoff=0)
#Agregamos la función abrir y le asignamos el comando previamente creado el cual es "Abrir"
menu_archivo.add_command(label="Abrir", command=abrir)
#Agregamos la función guardar y le asignamos el comando previamente creado el cual es "Guardar"
menu_archivo.add_command(label="Guardar", command=guardar)
#Agregamos la función guardar como y le asignamos el comando previamente creado el cual es "Guardar como" la opción cual le permitira al usaurio selecciónar la ruta y el tipo de arhivo que querra para su documento.
menu_archivo.add_command(label="Guardar como", command=guardar_como)
barra_opciones.add_cascade(label="Archivo", menu=menu_archivo)

#Creamos nuestra opción "Editar" en nuestra barra superior el cual servira para deshacer y rehacer acciónes dentro de nuestro documento.
menu_editar = Menu(barra_opciones, tearoff=0)
#Asiganmos el nombre y le agregamos nuestra función editar previamente iniciada.
barra_opciones.add_cascade(label="Editar", menu=menu_editar)

#Iniciamos las funciones Deshacer y Rehacer para usarlas en nuestro editor.
def deshacer():
    texto.edit_undo()

def rehacer():
    texto.edit_redo()
#agregamos las opcines deshacer y rehacer a nuestro menu y le asignamos el comando requerido, ademas le asignamos las respectivas combinaciones en el teclado utilizadas y conocidas para mayor comodidad del ususario.
menu_editar.add_command(label="Deshacer", command=deshacer, accelerator="Ctrl+Z")
menu_editar.add_command(label="Rehacer", command=rehacer, accelerator="Ctrl+Y")

#Creamos nuestra opción "Ayuda" y la agregamos a nuestra barra superior de accines;
menu_ayuda = Menu(barra_opciones, tearoff=0)
#Le asignamos el nombre y la agregamos al menu
barra_opciones.add_cascade(label="Ayuda", menu=menu_ayuda)
#le agregamos la acción "Información" y le asignamos la funcion abrir_información anteriormente iniciada.
menu_ayuda.add_command(label="Información", command=información)
#Le agregamos la acción "Manual de usuario" la cual dirigira al usuari a un link en donde estara el manual para uso del editor de texto.
menu_ayuda.add_command(label="Manual de usuario", command=Manual_usuario)
#Le agregamos la opción "Integrantes" y le asignamos la función "Mostrar_integrantes" que creamos anteriormente.
menu_ayuda.add_command(label="Integrantes", command=Integrantes)

# Asignamos la barra de opciones al widget raíz
root.config(menu=barra_opciones)
#lo editamos a nuestro gusto;
texto = Text(root)
texto.grid(row=1, columnspan=5)
texto.config(font=('arial', 12, 'normal'))

#Creamos nuestro menú de formatos y le damos forma
formato_fuente = StringVar()
formato_fuente.set("normal")
fuente = StringVar()
fuente.set("Arial")
tamano_fuente = IntVar()
tamano_fuente.set(10)

#Creamos nuestro menu de formato para que el usuario escoja la que mas le guste
menu_formato_fuente = OptionMenu(root, formato_fuente, "normal", "bold", "italic", "underline", "overstrike")
#le asignamos la posición
menu_formato_fuente.grid(row=1, column=5)
#Le agregamos las diferentes fuentes para el texto.
menu_fuente = OptionMenu(root, fuente, "Arial", "Times", "Courier")
#y le asignmos la posición deseada
menu_fuente.grid(row=1, column=6)
#asi mismo creamos los diferentes tamaños para la letra y que el usuario escoja el que mas le guste.
tamano_fuente = OptionMenu(root, tamano_fuente, 8,10, 12, 14, 16, 18, 20)
#le asigamos posición;
tamano_fuente.grid(row=1, column=7)
#creamos la opción de "aplicar formato" para aplicar los cambios que el usuario desee hace a su texto.
#y le asignamos la función "aplicar_formato" que iniciamos antes.
aplicar_formato_button = Button(root, text="Aplicar formato", command=aplicar_formato)
#le damos la posición que querramos.
aplicar_formato_button.grid(row=1, column=8)

#Creamos los atajos del teclado para Deshacer y Rehacer
root.bind('<Control-z>', lambda event=None: deshacer())
root.bind('<Control-y>', lambda event=None: rehacer())
#Ejecutamos
root.mainloop()
#Ya no hay más codigo.
#ಥ⁠‿⁠ಥ
