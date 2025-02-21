<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Motion Visualization</title>
    <script src="https://cdnjs.cloudflare.com/ajax/libs/p5.js/1.4.2/p5.min.js"></script>
    <style>
        body {
            font-family: -apple-system, BlinkMacSystemFont, 'Segoe UI', Roboto, sans-serif;
            margin: 0;
            padding: 20px;
            background-color: #f5f5f5;
        }
        .container {
            background-color: white;
            padding: 20px;
            border-radius: 10px;
            box-shadow: 0 2px 4px rgba(0,0,0,0.1);
            margin-bottom: 20px;
        }
        button {
            background-color: #007AFF;
            color: white;
            border: none;
            padding: 10px 20px;
            border-radius: 5px;
            font-size: 16px;
            cursor: pointer;
            margin: 10px 0;
        }
        button:disabled {
            background-color: #ccc;
        }
        .value-display {
            font-family: monospace;
            font-size: 16px;
            margin: 10px 0;
        }
        .status {
            margin-top: 20px;
            padding: 10px;
            border-radius: 5px;
        }
        .error {
            background-color: #ffebee;
            color: #c62828;
        }
        #canvas-container {
            width: 100%;
            display: flex;
            justify-content: center;
            margin-top: 20px;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Motion & Gyro Particles</h1>
        <button id="startBtn">Start Reading</button>
        <button id="stopBtn" disabled>Stop Reading</button>
        
        <div class="value-display">
            Acceleration:<br>
            X: <span id="xValue">0</span> m/s²<br>
            Y: <span id="yValue">0</span> m/s²<br>
            Z: <span id="zValue">0</span> m/s²<br>
            <br>
            Rotation:<br>
            α: <span id="alphaValue">0</span>°<br>
            β: <span id="betaValue">0</span>°<br>
            γ: <span id="gammaValue">0</span>°
        </div>

        <div id="status" class="status"></div>
    </div>
    <div id="canvas-container"></div>

    <script>
        class MotionStream {
            constructor() {
                this.isStreaming = false;
                this.motionListener = null;
                this.orientationListener = null;
            }

            async requestPermission() {
                if (typeof DeviceMotionEvent === 'undefined' || 
                    typeof DeviceOrientationEvent === 'undefined') {
                    throw new Error('Motion sensors not supported');
                }

                // Request motion permission (Safari)
                if (typeof DeviceMotionEvent.requestPermission === 'function') {
                    try {
                        const motionPermission = await DeviceMotionEvent.requestPermission();
                        if (motionPermission !== 'granted') {
                            throw new Error('Motion permission not granted');
                        }
                    } catch (error) {
                        throw new Error(`Motion permission error: ${error.message}`);
                    }
                }

                // Request orientation permission (Safari)
                if (typeof DeviceOrientationEvent.requestPermission === 'function') {
                    try {
                        const orientationPermission = await DeviceOrientationEvent.requestPermission();
                        if (orientationPermission !== 'granted') {
                            throw new Error('Orientation permission not granted');
                        }
                    } catch (error) {
                        throw new Error(`Orientation permission error: ${error.message}`);
                    }
                }
                
                return true;
            }

            start(callback) {
                if (this.isStreaming) return;
                
                this.motionListener = (event) => {
                    const motionData = {
                        x: event.accelerationIncludingGravity.x,
                        y: event.accelerationIncludingGravity.y,
                        z: event.accelerationIncludingGravity.z,
                        timestamp: event.timeStamp
                    };
                    callback(motionData, null);
                };

                this.orientationListener = (event) => {
                    const orientationData = {
                        alpha: event.alpha, // z-axis rotation [0,360)
                        beta: event.beta,   // x-axis rotation [-180,180]
                        gamma: event.gamma  // y-axis rotation [-90,90]
                    };
                    callback(null, orientationData);
                };

                window.addEventListener('devicemotion', this.motionListener);
                window.addEventListener('deviceorientation', this.orientationListener);
                this.isStreaming = true;
            }

            stop() {
                if (!this.isStreaming) return;
                
                window.removeEventListener('devicemotion', this.motionListener);
                window.removeEventListener('deviceorientation', this.orientationListener);
                this.isStreaming = false;
                this.motionListener = null;
                this.orientationListener = null;
            }
        }

        class Particle {
            constructor(p) {
                this.p = p;
                this.reset();
                this.rotation = 0;
                this.rotationSpeed = 0;
            }
            
            reset() {
                this.x = this.p.random(this.p.width);
                this.y = this.p.random(this.p.height);
                this.size = this.p.random(4, 12);
                this.baseColor = this.p.color(
                    this.p.random(100, 200),
                    this.p.random(100, 200),
                    255,
                    this.p.random(150, 200)
                );
                this.color = this.baseColor;
                this.speedX = 0;
                this.speedY = 0;
                this.rotation = this.p.random(360);
                this.rotationSpeed = 0;
            }
            
            update(accX, accY, gyroData) {
                // Update speed based on acceleration
                this.speedX += accX * 0.1;
                this.speedY += accY * 0.1;
                
                // Add some natural drift
                this.speedX += this.p.random(-0.1, 0.1);
                this.speedY += this.p.random(-0.1, 0.1);
                
                // Update rotation based on gyroscope
                if (gyroData) {
                    this.rotationSpeed += gyroData.gamma * 0.01;
                    this.rotation += this.rotationSpeed;
                    
                    // Change color based on orientation
                    const alphaInfluence = (gyroData.alpha / 360) * 255;
                    const betaInfluence = ((gyroData.beta + 180) / 360) * 255;
                    this.color = this.p.color(
                        alphaInfluence,
                        betaInfluence,
                        255,
                        this.p.alpha(this.baseColor)
                    );
                }
                
                // Apply friction
                this.speedX *= 0.95;
                this.speedY *= 0.95;
                this.rotationSpeed *= 0.95;
                
                // Update position
                this.x += this.speedX;
                this.y += this.speedY;
                
                // Wrap around edges
                if (this.x < 0) this.x = this.p.width;
                if (this.x > this.p.width) this.x = 0;
                if (this.y < 0) this.y = this.p.height;
                if (this.y > this.p.height) this.y = 0;
            }
            
            draw() {
                this.p.push();
                this.p.translate(this.x, this.y);
                this.p.rotate(this.p.radians(this.rotation));
                
                this.p.noStroke();
                this.p.fill(this.color);
                
                // Draw a more interesting shape
                this.p.beginShape();
                for (let i = 0; i < 3; i++) {
                    const angle = (i * 120) + this.rotation;
                    const x = this.p.cos(this.p.radians(angle)) * this.size;
                    const y = this.p.sin(this.p.radians(angle)) * this.size;
                    this.p.vertex(x, y);
                }
                this.p.endShape(this.p.CLOSE);
                
                this.p.pop();
            }
        }

        // p5.js sketch
        let sketch = function(p) {
            let particles = [];
            const numParticles = 100;
            let currentX = 0;
            let currentY = 0;
            let currentGyro = null;
            
            p.setup = function() {
                const canvas = p.createCanvas(340, 340);
                canvas.parent('canvas-container');
                
                // Create particles
                for (let i = 0; i < numParticles; i++) {
                    particles.push(new Particle(p));
                }
                
                p.background(20);
            };
            
            p.draw = function() {
                p.background(20, 20, 20, 10);
                
                // Update and draw all particles
                particles.forEach(particle => {
                    particle.update(currentX, currentY, currentGyro);
                    particle.draw();
                });
            };
            
            // Expose method to update motion values
            p.updateMotion = function(x, y, gyro) {
                currentX = x;
                currentY = y;
                currentGyro = gyro;
            };
        };

        // Create p5 instance
        let p5Instance = new p5(sketch);

        // UI Elements
        const startBtn = document.getElementById('startBtn');
        const stopBtn = document.getElementById('stopBtn');
        const xValue = document.getElementById('xValue');
        const yValue = document.getElementById('yValue');
        const zValue = document.getElementById('zValue');
        const alphaValue = document.getElementById('alphaValue');
        const betaValue = document.getElementById('betaValue');
        const gammaValue = document.getElementById('gammaValue');
        const status = document.getElementById('status');

        const motionSensor = new MotionStream();

        function updateStatus(message, isError = false) {
            status.textContent = message;
            status.className = 'status' + (isError ? ' error' : '');
        }

        function updateButtons(isReading) {
            startBtn.disabled = isReading;
            stopBtn.disabled = !isReading;
        }

        let currentGyroData = null;

        startBtn.addEventListener('click', async () => {
            try {
                await motionSensor.requestPermission();
                motionSensor.start((motionData, orientationData) => {
                    if (motionData) {
                        xValue.textContent = motionData.x?.toFixed(2) || 0;
                        yValue.textContent = motionData.y?.toFixed(2) || 0;
                        zValue.textContent = motionData.z?.toFixed(2) || 0;
                        
                        // Update p5 visualization with both motion and gyro data
                        p5Instance.updateMotion(
                            motionData.x || 0,
                            motionData.y || 0,
                            currentGyroData
                        );
                    }
                    if (orientationData) {
                        currentGyroData = orientationData;
                        alphaValue.textContent = orientationData.alpha?.toFixed(1) || 0;
                        betaValue.textContent = orientationData.beta?.toFixed(1) || 0;
                        gammaValue.textContent = orientationData.gamma?.toFixed(1) || 0;
                    }
                });
                updateButtons(true);
                updateStatus('Reading motion data...');
            } catch (error) {
                updateStatus(error.message, true);
            }
        });

        stopBtn.addEventListener('click', () => {
            motionSensor.stop();
            updateButtons(false);
            updateStatus('Stopped reading.');
        });

        // Initial status message
        updateStatus('Click "Start Reading" to begin');
    </script>
</body>
</html>
