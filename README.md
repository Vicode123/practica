# practica
Este código procesa datos de temperatura, humedad y presión de una cadena de texto y de un archivo CSV
from procesa_csv import extrae  

datos_str = ["2025/05/13 20:15:00,19.3,32,788.1"]

fecha = []
hora = []
temp = []
humedad = []
presion = []

for cadena in datos_str:
    valores = cadena.split(",")
    tiempos = valores[0].split(" ")

  numeros = [float(valor) for valor in valores[1:]]

  temp.append(numeros[0])
  humedad.append(numeros[1])
  presion.append(numeros[2])
  fecha.append(tiempos[0])
  hora.append(tiempos[1])

from matplotlib import pyplot as plt
import datetime
datos = extrae()  
x = datos["hora"]  
y = datos["T"]     


fechas_datetime = []
for time in x:
    tiempo = datetime.datetime.strptime(time, "%Y/%m/%d %H:%M:%S")
    fechas_datetime.append(tiempo)



plt.figure()
plt.plot(fechas_datetime, y, marker="o", color="blue")
plt.xlabel("Fecha y hora")
plt.ylabel("Temperatura (°C)")
plt.title("Temperatura en el tiempo")
plt.grid(True)
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()



print("Fecha:", fecha)
print("Hora:", hora)
print("Temperatura:", temp)
print("Humedad:", humedad)
print("Presión:", presion)

print("\n--- DATOS DEL CSV ---")
for i in range(len(datos["hora"])):
    print(f"{i+1}. Fecha y hora: {datos['hora'][i]}, "
          f"Temperatura: {datos['T'][i]} °C, "
          f"Humedad: {datos['H'][i]} %, "
          f"Presión: {datos['P'][i]} hPa")
