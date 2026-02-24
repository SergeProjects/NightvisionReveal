Nightvision Reveal — Como configurar no mapa L_Overview
1) Abra o Level Blueprint do mapa

No Content Browser, abra o mapa:
Content/NightvisionReveal/Maps/L_Overview

Com o mapa aberto, vá em: Blueprints → Open Level Blueprint

Parte A — Criar a variável com os atores “Nightvision”
2) Copie o bloco do BeginPlay

No Level Blueprint, copie o primeiro bloco:

Event BeginPlay

Get All Actors With Tag (Tag: Nightvision)

3) Crie a variável “Nightvision Ref”

No node Get All Actors With Tag, pegue o pino azul Out Actors.

Clique com o botão direito nesse pino → Promote to Variable

Renomeie a variável criada para: NightvisionRef
(sem espaço, padrão mais profissional)

4) Use a variável no collision (se estiver no teu gráfico)

Conecte NightvisionRef no ForEachLoop (ou diretamente onde tu estiver usando array) e então no:

Set Actor Enable Collision (Target = Actor)

Se tu já tiver um loop no teu blueprint (ForEach), só troca o array antigo pela variável NightvisionRef.

Parte B — Toggle no “N” (FlipFlop) + Som + Colisão/Hidden
5) Copie o bloco do input

Agora copie a segunda parte do blueprint:

N (Pressed)

FlipFlop

Play Sound 2D

Set Actor Hidden In Game

Set Actor Enable Collision
(e o que mais tiver nessa parte de toggle)

Parte C — Post Process Volume (Nightvision verde)
6) Crie e configure o PostProcessVolume no mapa

No Level, adicione um Post Process Volume

No Details do volume:

Marque Infinite Extent (Unbound) ✅ (é “Unbound”, não “Bound”)

Em Misc:

Marque Scene Color Tint ✅

Ajuste a cor para verde

Dica: deixa o Blend Weight do volume em 0 pra começar normal.

Parte D — Criar referência do PostProcessVolume no Level Blueprint
7) Crie a referência do volume

Selecione o PostProcessVolume no level

Volte no Level Blueprint

Clique com o botão direito no gráfico → Create a Reference to PostProcessVolume

8) Conecte a referência nos nodes corretos

Agora, no teu bloco do N:

Remova qualquer node antigo “Post Process Volume” que esteja no gráfico (se for referência errada).

Nos dois nodes Set Blend Weight (os “Set” verdes):

Conecte a referência do PostProcessVolume no pino azul Target

Valores:

Nightvision ON → Blend Weight = 1.0

Nightvision OFF → Blend Weight = 0.0

Parte E — Ajustar os atores Nightvision no toggle
9) Troque os arrays “soltos” pela variável NightvisionRef

Se tu tiver nodes usando um array direto ou referências antigas:

Apague as referências antigas ligadas em Set Actor Hidden In Game / Set Actor Enable Collision

Arraste a variável NightvisionRef pro gráfico (Get)

Use ela no teu ForEachLoop para aplicar:

ON: Hidden In Game = false e Enable Collision = true

OFF: Hidden In Game = true e Enable Collision = false

Extra (opcional)
10) Trocar os sons

Nos nodes Play Sound 2D, tu pode trocar:

Som de ativar

Som de desativar