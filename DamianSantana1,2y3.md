
def menu():
    print('Menú Mascotas')
    print('======================================================')
    print('1.- Ingresar mascota')
    print('2.- Buscar mascota')
    print('3.- Eliminar mascota')
    print('4.- Mostrar mascota registradas en un año especifico')
    print('5.- Salir')

def valida_fecha(fec):
    fecha_lista=fec.split('-')
    if len(fecha_lista)==3:
        if fecha_lista[0].isdigit() and fecha_lista[1].isdigit() and fecha_lista[2].isdigit():
            dd=int(fecha_lista[0])
            mm=int(fecha_lista[1])
            yyyy=int(fecha_lista[2])
            if 1<=dd<=31 and 1<=mm<=12 and 2000<=yyyy<=2025:
                return True
    return False

def ingresar():
    while True:
        nombre=input('Ingrese nombre de la mascota: ')
        if nombre.isalpha():
            if nombre in mascotas:
                print('Mascota ya existe')
            else:
                break
        else:
            print('Ingrese sólo letras')
    while True:
        tipo=input('Ingrese el tipo de mascota (P para Perro, G para Gato, A para Ave): ').upper()
        if tipo in ['P','G','A']:
            break
        else:
            print('Sólo P para Perro, G para Gato, A para Ave')
    while True:
        fecha=input('Ingrese fecha de registro (en formato DD-MM-AAAA): ')
        if valida_fecha(fecha):
            break
        else:
            print('Fecha incorrecta!!!')
    while True:
        try:
            edad=int(input('Ingrese edad (número entero positivo): '))
            if edad>=0:
                break
            else:
                print('La edad no puede ser un número negativo')
        except:
            print('Sólo número entero!!!')
    mascotas[nombre]=[tipo,fecha,edad]

def nombre_tipo(tipo):
    dicc={'P':'Perro', 'G':'Gato', 'A':'Ave'}
    nombre=dicc.get(tipo,'Desconocido')
    # nombre=dicc[tipo]
    return nombre

def buscar():
    nom=input('Ingrese nombre de la mascota: ')
    if nom in mascotas:
        tipo,fecha,edad=mascotas[nom]
        print('Tipo ',nombre_tipo(tipo))
        print('Fecha ',fecha)
        print('Edad ',edad)
        return
    else:
        print('Mascota NO encontrada')

def eliminar():
    print('Eliminar')
    nom=input('Ingrese Nombre de la Mascota: ')
    if nom in mascotas:
        del mascotas[nom]
        print('Mascota eliminada correctamente')
        return
    else:
        print('Mascota no encotrada')
        return

def mostrar():
    # print(mascotas)
    agnio=input('Ingrese año: ')
    if int(agnio)>=2000 and int(agnio)<=2025:
        encuentra=False
        for clave,valor in mascotas.items():
            fecha=valor[1].split('-')
            annio=fecha[2]
            if annio==agnio:
                encuentra=True
                nombre=clave
                tipo=valor[0]
                fecha=valor[1]
                edad=valor[2]
                print('============================')
                print('Nombre: ',nombre)
                print('Tipo: ',nombre_tipo(tipo))
                print('Fecha: ',fecha)
                print('Edad: ',edad)
        if not encuentra:
            print('No existen mascotas registradas en el año ',agnio)
    else:
        print('Año incorrecto')

# {'Dogui': ['P', '12-12-2020', 6], 'Tom': ['G', '05-18-2024', 12]}
# Editado el 15/07/25 por Damián Santana

# Programa Principal
mascotas={}
mascotas['Dogui']=['P', '12-12-2020',6]
mascotas['Tom']=['G', '05-11-2024',12]
mascotas['Pin']=['A', '03-01-2020',2]
while True:
    menu()
    opc=input('Ingrese Opción: ')
    if opc=='1':
        ingresar()
    elif opc=='2':
        buscar()
    elif opc=='3':
        eliminar()
    elif opc=='4':
        mostrar()
    elif opc=='5':
        break
    else:
        print('Opción Incorrecta!!!')
        
