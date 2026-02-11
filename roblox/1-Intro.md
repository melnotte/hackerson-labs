# 🧪 Laboratorio de Roblox

Misión: Construir un juego funcional usando todas las herramientas del "Explorer" y entender las propiedades de la materia digital.

---

## 📑 1. Diccionario de Comandos (Cheat Sheet)
* local: Crea un nombre para guardar algo.
* task.wait(n): Pausa el código por n segundos.
* Connect(function() ... end): Escucha un evento (como un toque) y ejecuta una acción.
* Vector3.new(x, y, z): Posición en el espacio 3D.
* Parent: Es el "Padre" o contenedor de un objeto.

---

## 🏗️ 2. Fase de Construcción (Workspace)
El Workspace es el mundo físico.

1. Crea el suelo: Inserta una Part, cámbiale el nombre a SueloPeligroso.
2. Abre el Panel de Propiedades:
    * BrickColor: Naranja brillante.
    * Material: Neon.
    * Anchored: ✅ (Activado).



---

## 📦 3. Fase de Almacén (ReplicatedStorage)

1. Crea una esfera, llámala EsferaLava.
2. Arrastra EsferaLava dentro de ReplicatedStorage.

---

## 🧠 4. Fase de Lógica (ServerScriptService)

  * Ubicación: ServerScriptService -> Script
  * Función: Clona las esferas desde el almacenamiento y las lanza al mundo en posiciones aleatorias.

-- Referencias seguras a la API de Roblox
local ReplicatedStorage = game:GetService("ReplicatedStorage")
local debris = game:GetService("Debris")

-- Buscamos la esfera que guardamos en el almacén
local esferaOriginal = ReplicatedStorage:WaitForChild("EsferaLava")

-- Bucle infinito: esto se repite por siempre
while true do
    task.wait(1.5) -- Pausa de 1.5 segundos entre cada esfera
    
    -- Creamos una copia exacta de la esfera
    local copia = esferaOriginal:Clone()
    copia.Parent = game.Workspace
    
    -- La posicionamos en el cielo en un lugar aleatorio
    -- math.random(min, max) elige un número al azar
    local x = math.random(-30, 30)
    local z = math.random(-30, 30)
    copia.Position = Vector3.new(x, 50, z)
    
    -- Debris (Escombros): Borra la copia después de 4 segundos 
    -- Esto evita que el juego se ponga lento (Lag)
    debris:AddItem(copia, 4)
end

## 🎒 5. Fase de Equipo (StarterPack)

1. Busca una "Sword" en el Toolbox y arrástrala a StarterPack.

---

## 🖼️ 6. Fase de Interfaz (StarterGui)

1. Añade un ScreenGui y dentro un TextLabel.
2. Propiedades: Text = "¡ESQUIVA LAS ESFERAS!", TextScaled = ✅.

---

## 👤 7. Fase de Control (StarterPlayer)

  * Ubicación: StarterPlayer -> StarterPlayerScripts -> LocalScript
  * Función: Detecta si el jugador toca una esfera y avisa en la consola.

local jugador = game.Players.LocalPlayer
local personaje = jugador.Character or jugador.CharacterAdded:Wait()
local humanoide = personaje:WaitForChild("Humanoid")

-- Esta función se activa cuando el cuerpo del personaje toca algo
humanoide.Touched:Connect(function(objetoTocado)
    -- Verificamos si el objeto que tocamos es una de nuestras esferas
    if objetoTocado.Name == "EsferaLava" then
        print("¡AUCH! Te golpeó una esfera de lava.")
        
        -- Si quieres que el jugador pierda vida al contacto
        -- humanoide.Health = humanoide.Health - 10
    end
end)

## 🔥 RETO FINAL: ¡El Suelo es Lava!
En este desafío, haremos que el bloque SueloPeligroso que creamos al principio elimine al jugador si lo toca.

1. Selecciona tu pieza SueloPeligroso en el Workspace.
2. Asegúrate de que su propiedad Name sea exactamente SueloPeligroso.
* Ubicación: ServerScriptService -> Script
* Función: Elimina a cualquier jugador que toque la plataforma principal.

-- Buscamos el bloque que nombramos SueloPeligroso
local suelo = game.Workspace:WaitForChild("SueloPeligroso")

local function alTocarSuelo(objetoQueToco)
    -- Intentamos encontrar el personaje del jugador
    local modelo = objetoQueToco.Parent
    local humanoide = modelo:FindFirstChild("Humanoid")

    -- Si el objeto tiene un "Humanoide", significa que es un jugador
    if humanoide then
        humanoide.Health = 0 -- ¡Eliminación instantánea!
    end
end

-- Conectamos el evento "Touched" a nuestra función
suelo.Touched:Connect(alTocarSuelo)

## 🏆 ¡Misión Cumplida!
¡Felicidades! Has construido un juego que tiene:
* Física: Un suelo firme y esferas que caen.
* Memoria: Un almacén de esferas listas para ser usadas.
* Inteligencia: Scripts que clonan objetos y detectan peligros.
* Interfaz: Un mensaje en pantalla para el jugador.

**¿Qué sigue?** Intenta cambiar la propiedad Transparency de las esferas a 0.5 o cambia la velocidad del task.wait en el script de las esferas para que el juego sea más difícil.
