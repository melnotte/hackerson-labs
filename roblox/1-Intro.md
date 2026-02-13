# 🧪 Laboratorio de Roblox: Edición Espada y Puntos

## 📂 1. Mapa de Carpetas (Explorer)
Organiza tus objetos de la siguiente manera:

* Workspace 🌎
    * SueloPeligroso (Parte naranja Neon).
* ReplicatedStorage 📦
    * EsferaLava
    * DestruirEsferaEvent (Crea un RemoteEvent con este nombre).
* ServerScriptService ⚙️
    * GeneradorEsferas (Script).
    * GestionPuntos (Script).
    * LogicaSuelo (Script).
* StarterPack ⚔️
    * Sword (La espada).
        * ScriptPuntosEspada (LocalScript dentro de la espada).
* StarterPlayer 👤 -> StarterPlayerScripts
    * ControlDañoReaparicion (LocalScript).

---

## 🏗️ 2. Lógica del Servidor (ServerScriptService)

### A. Generador de Esferas (GeneradorEsferas)
lua local ReplicatedStorage = game:GetService("ReplicatedStorage") 
local debris = game:GetService("Debris") local esferaOriginal = ReplicatedStorage:WaitForChild("EsferaLava")  while true do     task.wait(1.5)     local copia = esferaOriginal:Clone()     copia.Name = "EsferaLava"     copia.Parent = game.Workspace          local x = math.random(-30, 30)     local z = math.random(-30, 30)     copia.Position = Vector3.new(x, 50, z)          debris:AddItem(copia, 4) end 

### B. Tabla de Puntos (GestionPuntos)
lua local ReplicatedStorage = game:GetService("ReplicatedStorage") local evento = ReplicatedStorage:WaitForChild("DestruirEsferaEvent")  game.Players.PlayerAdded:Connect(function(jugador)     local stats = Instance.new("Folder")     stats.Name = "leaderstats"     stats.Parent = jugador      local esferasDestruidas = Instance.new("IntValue")     esferasDestruidas.Name = "Esferas"     esferasDestruidas.Value = 0     esferasDestruidas.Parent = stats end)  evento.OnServerEvent:Connect(function(jugador)     jugador.leaderstats.Esferas.Value = jugador.leaderstats.Esferas.Value + 1 end) 

### C. El Suelo es Lava (LogicaSuelo)
lua local suelo = game.Workspace:WaitForChild("SueloPeligroso")  suelo.Touched:Connect(function(objeto)     local humanoide = objeto.Parent:FindFirstChild("Humanoid")     if humanoide then         humanoide.Health = 0      end end) 

---

## ⚔️ 3. Equipo y Combate (StarterPack)

### Script de la Espada (ScriptPuntosEspada)
lua local herramienta = script.Parent local ReplicatedStorage = game:GetService("ReplicatedStorage") local evento = ReplicatedStorage:WaitForChild("DestruirEsferaEvent")  local atacando = false  herramienta.Activated:Connect(function()     atacando = true     task.wait(0.6)     atacando = false end)  herramienta.Handle.Touched:Connect(function(objeto)     if atacando and objeto.Name == "EsferaLava" then         evento:FireServer()         objeto:Destroy()     end end) 

---

## 👤 4. Control del Jugador (StarterPlayerScripts)

### Daño por Esferas (ControlDañoReaparicion)
lua local jugador = game.Players.LocalPlayer  local function conectarDaño(personaje)     local humanoide = personaje:WaitForChild("Humanoid")          humanoide.Touched:Connect(function(objeto)         if objeto.Name == "EsferaLava" then             humanoide.Health = humanoide.Health - 20         end     end) end  if jugador.Character then conectarDaño(jugador.Character) end jugador.CharacterAdded:Connect(conectarDaño) 

---
