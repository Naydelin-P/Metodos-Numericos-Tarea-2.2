#   Codigo que implementa el esquema numerico 
#   de punto fijo para determinar la raiz de
#   una ecuacion
# 
#           Autor:
#  Naydelin Palomo Martinez
#   naydelin.palomo@gmail.com
#   
#

import numpy as np
import matplotlib.pyplot as plt

#Definir la función g(x) para el método de punto fijo
def g(x):
    return np.sqrt(3*x - 1)

#Criterio de convergencia
def g_prime(x):
    return (3/2) * (3*x - 1)**(-1/2)

#Error absoluto
def error_absoluto(x_new, x_old):
    return abs(x_new - x_old)

#Error relativo
def error_relativo(x_new, x_old):
    return abs((x_new - x_old) / x_new)

#Error cuadrático
def error_cuadratico(x_new, x_old):
    return (x_new - x_old)**2

#metodo de punto fijo
def punto_fijo(x0, tol=1e-5, max_iter=100):
    iteraciones = []
    errores_abs = []
    errores_rel = []
    errores_cuad = []

    x_old = x0
    for i in range(max_iter):
        x_new = g(x_old)
        e_abs = error_absoluto(x_new, x_old)
        e_rel = error_relativo(x_new, x_old)
        e_cuad = error_cuadratico(x_new, x_old)

        iteraciones.append((i+1, x_new, e_abs, e_rel, e_cuad))
        errores_abs.append(e_abs)
        errores_rel.append(e_rel)
        errores_cuad.append(e_cuad)

        if e_abs < tol:
            break

        x_old = x_new

    return iteraciones, errores_abs, errores_rel, errores_cuad

#Parámetros 
x0 = 1.5
iteraciones, errores_abs, errores_rel, errores_cuad = punto_fijo(x0)

#tabla de iteraciones
print("Iteración | x_n      | Error absoluto | Error relativo | Error cuadrático")
print("-----------------------------------------------------------------------")
for it in iteraciones:
    print(f"{it[0]:9d} | {it[1]:.6f} | {it[2]:.6e} | {it[3]:.6e} | {it[4]:.6e}")

#grafica de convergencia
x_vals = np.linspace(1, 4, 100)
y_vals = g(x_vals)

plt.figure(figsize=(8, 5))
plt.plot(x_vals, y_vals, label=r"$g(x) = \sqrt{3x-1}$", color="green")
plt.plot(x_vals, x_vals, linestyle="dashed", color="purple", label="y = x")

#grafica de las iteraciones
x_points = [it[1] for it in iteraciones]
y_points = [g(x) for x in x_points]
plt.scatter(x_points, y_points, color="orange", zorder=3)
plt.plot(x_points, y_points, linestyle="dotted", color="brown", label="Iteraciones")

plt.xlabel("x")
plt.ylabel("g(x)")
plt.legend()
plt.grid(True)
plt.title("Método de Punto Fijo")
plt.savefig("punto_fijo_convergencia.png")
plt.show()

#grafica de los errores
plt.figure(figsize=(8, 5))
plt.plot(range(1, len(errores_abs) + 1), errores_abs, marker="o", color="blue", label="Error absoluto")
plt.plot(range(1, len(errores_rel) + 1), errores_rel, marker="s", color="red", label="Error relativo")
plt.plot(range(1, len(errores_cuad) + 1), errores_cuad, marker="^", color="green", label="Error cuadrático")

plt.xlabel("Iteración")
plt.ylabel("Error")
plt.yscale("log")
plt.legend()
plt.grid(True)
plt.title("Evolución de los Errores")
plt.savefig("errores_punto_fijo.png")
plt.show()
