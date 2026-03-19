# Taller_herencia_polimorfismo
class Animal:
    # Constructor: Inicializa los atributos del objeto al crearse
    def __init__(self, identificador, especie, peso):
        self.__identificador = identificador  # Atributo privado
        self.__especie = especie              # Atributo privado
        self.__peso = peso                    # Atributo privado

    # Getters (Consultores): Permiten leer el valor de forma segura
    def get_identificador(self):
        return self.__identificador

    def get_especie(self):
        return self.__especie

    def get_peso(self):
        return self.__peso
    def calcular_racion_diaria(self):
        return "Racion no definida"

    # Setters (Modificadores): Permiten cambiar el valor aplicando reglas o validaciones
    def set_peso(self, nuevo_peso):
        if nuevo_peso > 0:
            self.__peso = nuevo_peso
        else:
            print("Error: El peso de un animal no puede ser negativo o cero.")

    # Método general
    def mostrar_info(self):
        return f"[{self.__identificador}] Especie: {self.__especie} | Peso: {self.__peso}kg"

# --- PRUEBA DEL ENCAPSULAMIENTO ---
print("--- Creando Registro de Animal ---")
animal_generico = Animal("A001", "Desconocida", 50.5)
print(animal_generico.mostrar_info())

# Intentamos modificar el peso usando el Setter con una validación
animal_generico.set_peso(55.0)
print(f"Nuevo peso actualizado: {animal_generico.get_peso()}kg")

# Simulamos un error de digitación
animal_generico.set_peso(-10)
class Mamifero(Animal):
    def __init__(self, identificador, especie, peso, meses_gestacion, es_carnivoro):
        # Llamamos al constructor de la clase padre (Animal)
        super().__init__(identificador, especie, peso)
        # Atributo específico de la clase hija
        self.__meses_gestacion = meses_gestacion
        self.__es_carnivoro = es_carnivoro

    def get_meses_gestacion(self):
        return self.__meses_gestacion
    def calcular_racion_diaria(self):
        if self.__es_carnivoro:
          return self.get_peso() * 0.05
        return "No aplica"

class Reptil(Animal):
    def __init__(self, identificador, especie, peso, es_venenoso):
        super().__init__(identificador, especie, peso)
        self.__es_venenoso = es_venenoso # Booleano

    def get_es_venenoso(self):
        return "Sí" if self.__es_venenoso else "No"
    def calcular_racion_diaria(self):
        return "2 roedores por semana"
# --- PRUEBA DE HERENCIA ---
leon = Mamifero("M001", "León Africano", 190.0, 3.5,True)
cobra = Reptil("R001", "Cobra Real", 6.0, True)

print(leon.mostrar_info(), f"| Gestación: {leon.get_meses_gestacion()} meses")
print(cobra.mostrar_info(), f"| Venenoso: {cobra.get_es_venenoso()}")
