<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <title>Juego 3D: Salto Espacial</title>
    <script src="https://code.playcanvas.com/playcanvas-stable.min.js"></script>
    <style>
        body { margin: 0; padding: 0; overflow: hidden; background-color: #000; }
        canvas { display: block; width: 100vw; height: 100vh; }
        #interfaz {
            position: absolute;
            top: 20px;
            left: 20px;
            color: white;
            font-family: system-ui, sans-serif;
            background: rgba(0, 0, 0, 0.8);
            padding: 15px;
            border-radius: 8px;
            border: 2px solid #56f5d2;
            box-shadow: 0 0 15px #56f5d244;
        }
        #puntos { color: #56f5d2; font-size: 24px; font-weight: bold; }
        #mensajeOver {
            position: absolute;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            font-family: system-ui, sans-serif;
            font-size: 32px;
            font-weight: bold;
            color: #ff4757;
            background: rgba(0, 0, 0, 0.9);
            padding: 30px;
            border-radius: 10px;
            border: 3px solid #ff4757;
            display: none;
            text-align: center;
            cursor: pointer;
        }
    </style>
</head>
<body>

    <div id="interfaz">
        Plataformas: <span id="puntos">0</span><br>
        <span style="font-size: 14px; color: #a2aec9;">Mover: Flechas | Saltar: ESPACIO</span>
    </div>

    <div id="mensajeOver" onclick="location.reload()">
        ¡CAÍSTE AL VACÍO!<br>
        <span style="font-size:16px; color:#fff;">Haz clic para reiniciar</span>
    </div>

    <canvas id="mundo3D"></canvas>

    <script>
        const canvas = document.getElementById('mundo3D');
        const spanPuntos = document.getElementById('puntos');
        const divMensaje = document.getElementById('mensajeOver');
        
        const app = new pc.Application(canvas, { keyboard: new pc.Keyboard(window) });
        app.start();
        app.setCanvasFillMode(pc.FILLMODE_FILL_WINDOW);
        app.setCanvasResolution(pc.RESOLUTION_AUTO);
        window.addEventListener('resize', () => app.resizeCanvas());

        // 1. ESCENARIO Y CÁMARA
        const camara = new pc.Entity();
        camara.addComponent('camera', { clearColor: new pc.Color(0.02, 0.05, 0.1) });
        camara.setPosition(0, 8, 12);
        camara.lookAt(0, 0, 0);
        app.root.addChild(camara);

        const luz = new pc.Entity();
        luz.addComponent('light', { type: 'directional', color: new pc.Color(1, 1, 1), intensity: 1.5 });
        luz.setEulerAngles(45, 30, 0);
        app.root.addChild(luz);

        // Materiales
        const matJugador = new pc.StandardMaterial();
        matJugador.diffuse.set(1, 0.2, 0.8); // Rosa fuerte
        matJugador.update();

        const matPlataforma = new pc.StandardMaterial();
        matPlataforma.diffuse.set(0.2, 0.8, 1); // Azul claro
        matPlataforma.update();

        // 2. JUGADOR
        const jugador = new pc.Entity();
        jugador.addComponent('render', { type: 'sphere' });
        jugador.setLocalScale(1, 1, 1);
        jugador.setPosition(0, 2, 0);
        jugador.render.material = matJugador;
        app.root.addChild(jugador);

        // 3. VARIABLES DE FÍSICA Y JUEGO
        let juegoActivo = true;
        let puntos = 0;
        
        let velY = 0; // Velocidad de caída/salto
        const gravedad = -25;
        const fuerzaSalto = 12;
        let enSuelo = false;
        
        const plataformas = [];
        let velocidadPlataformas = 5;

        // Función para crear plataformas infinitas
        function crearPlataforma(zPos, xPos) {
            const plat = new pc.Entity();
            plat.addComponent('render', { type: 'box' });
            plat.setLocalScale(4, 0.5, 4);
            plat.setPosition(xPos, 0, zPos);
            plat.render.material = matPlataforma;
            app.root.addChild(plat);
            plataformas.push(plat);
        }

        // Crear las primeras plataformas
        crearPlataforma(0, 0);
        crearPlataforma(-8, 2);
        crearPlataforma(-16, -2);
        crearPlataforma(-24, 0);

        // 4. BUCLE PRINCIPAL
        app.on('update', function (dt) {
            if (!juegoActivo) return;

            let posJugador = jugador.getPosition();

            // --- FÍSICAS DE SALTO Y GRAVEDAD ---
            velY += gravedad * dt; // Aplicar gravedad
            let nuevaY = posJugador.y + (velY * dt);
            enSuelo = false;

            // --- MOVER PLATAFORMAS (Efecto de avanzar) ---
            for (let i = plataformas.length - 1; i >= 0; i--) {
                let p = plataformas[i];
                p.translate(0, 0, velocidadPlataformas * dt);
                
                let posP = p.getPosition();
                
                // Comprobar si aterrizamos en esta plataforma
                // 1. Estamos cayendo (velY < 0)
                // 2. Nuestra Y anterior era mayor que la plataforma, y la nueva Y la atraviesa
                // 3. Estamos dentro de los límites X y Z de la plataforma
                if (velY < 0 && 
                    posJugador.y > 0 && nuevaY <= 0.5 &&
                    posJugador.x > posP.x - 2 && posJugador.x < posP.x + 2 &&
                    posJugador.z > posP.z - 2 && posJugador.z < posP.z + 2) {
                    
                    nuevaY = 0.5; // Ajustar posición encima de la plataforma
                    velY = 0;
                    enSuelo = true;
                }

                // Borrar plataformas que quedaron atrás y crear nuevas
                if (posP.z > 15) {
                    p.destroy();
                    plataformas.splice(i, 1);
                    puntos++;
                    spanPuntos.textContent = puntos;
                    
                    // Crear nueva plataforma a lo lejos (-32 aprox)
                    // con una pequeña variación en X para obligar a moverse
                    let ultimaZ = plataformas[0].getPosition().z;
                    let nuevoX = (Math.random() * 6) - 3;
                    crearPlataforma(ultimaZ - 8, nuevoX);
                    
                    if (puntos % 5 === 0) velocidadPlataformas += 1; // Aumentar dificultad
                }
            }

            jugador.setPosition(posJugador.x, nuevaY, posJugador.z);

            // --- CONTROLES DE MOVIMIENTO ---
            if (app.keyboard.isPressed(pc.KEY_LEFT) || app.keyboard.isPressed(pc.KEY_A)) {
                jugador.translate(-8 * dt, 0, 0);
            }
            if (app.keyboard.isPressed(pc.KEY_RIGHT) || app.keyboard.isPressed(pc.KEY_D)) {
                jugador.translate(8 * dt, 0, 0);
            }
            
            if (app.keyboard.wasPressed(pc.KEY_SPACE) && enSuelo) {
                velY = fuerzaSalto;
                enSuelo = false;
            }

            // --- GAME OVER ---
            // Si cae al vacío (Y es muy negativo)
            if (posJugador.y < -5) {
                juegoActivo = false;
                divMensaje.style.display = 'block';
            }
        });
    </script>
</body>
</html>