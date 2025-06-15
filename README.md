<!DOCTYPE html>
<html lang="es">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Test - Control de Calidad</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }
          body {
            font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
            background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
            min-height: 100vh;
            padding: 20px;
        }
            .container {
            max-width: 800px;
            margin: 0 auto;
            background: white;
            border-radius: 20px;
            box-shadow: 0 20px 40px rgba(0,0,0,0.1);
            overflow: hidden;
        }
          .header {
            background: linear-gradient(135deg, #2c3e50, #34495e);
            color: white;
            padding: 30px;
            text-align: center;
        }
            .header h1 {
            font-size: 2.2em;
            margin-bottom: 10px;
        }
           .header p {
            opacity: 0.9;
            font-size: 1.1em;
        }
           .progress-container {
            background: #ecf0f1;
            padding: 20px;
        }
            .progress-bar {
            background: #bdc3c7;
            height: 10px;
            border-radius: 5px;
            overflow: hidden;
            margin-bottom: 10px;
        }
          .progress-fill {
            background: linear-gradient(90deg, #3498db, #2ecc71);
            height: 100%;
            width: 0%;
            transition: width 0.3s ease;
        }
           .progress-text {
            text-align: center;
            color: #2c3e50;
            font-weight: bold;
        }
            .question-container {
            padding: 30px;
            display: none;
        }
         .question-container.active {
            display: block;
            animation: fadeIn 0.5s ease;
        }
          @keyframes fadeIn {
            from { opacity: 0; transform: translateY(20px); }
            to { opacity: 1; transform: translateY(0); }
        }
          .question-number {
            color: #3498db;
            font-weight: bold;
            font-size: 1.1em;
            margin-bottom: 15px;
        }
         .question {
            font-size: 1.3em;
            color: #2c3e50;
            margin-bottom: 25px;
            line-height: 1.5;
        }   
        .options {
            list-style: none;
        }  
        .option {
            background: #f8f9fa;
            margin: 12px 0;
            padding: 18px;
            border-radius: 12px;
            cursor: pointer;
            transition: all 0.3s ease;
            border: 2px solid transparent;
            position: relative;
            overflow: hidden;
        }  
        .option::before {
            content: '';
            position: absolute;
            top: 0;
            left: -100%;
            width: 100%;
            height: 100%;
            background: linear-gradient(90deg, transparent, rgba(255,255,255,0.4), transparent);
            transition: left 0.5s;
        } 
        .option:hover {
            background: #e3f2fd;
            border-color: #3498db;
            transform: translateY(-2px);
            box-shadow: 0 8px 25px rgba(52, 152, 219, 0.15);
        } 
        .option:hover::before {
            left: 100%;
        } 
        .option.selected {
            background: #3498db;
            color: white;
            border-color: #2980b9;
        }   
        .option.correct {
            background: #27ae60;
            color: white;
            border-color: #229954;
        } 
        .option.incorrect {
            background: #e74c3c;
            color: white;
            border-color: #c0392b;
        }  
        .option.disabled {
            cursor: not-allowed;
            opacity: 0.7;
        } 
        .feedback {
            margin: 20px 0;
            padding: 20px;
            border-radius: 12px;
            display: none;
            animation: slideIn 0.5s ease;
        }
        @keyframes slideIn {
            from { opacity: 0; transform: translateX(-20px); }
            to { opacity: 1; transform: translateX(0); }
        } 
        .feedback.correct {
            background: #d5f4e6;
            border-left: 5px solid #27ae60;
            color: #155724;
        } 
        .feedback.incorrect {
            background: #f8d7da;
            border-left: 5px solid #e74c3c;
            color: #721c24;
        }
        .feedback.show {
            display: block;
        } 
        .controls {
            padding: 20px 30px;
            background: #f8f9fa;
            text-align: center;
        } 
        .btn {
            background: linear-gradient(135deg, #3498db, #2980b9);
            color: white;
            border: none;
            padding: 15px 30px;
            border-radius: 25px;
            cursor: pointer;
            font-size: 1.1em;
            font-weight: bold;
            transition: all 0.3s ease;
            margin: 0 10px;
            min-width: 120px;
        }
        .btn:hover {
            transform: translateY(-2px);
            box-shadow: 0 8px 25px rgba(52, 152, 219, 0.3);
        } 
        .btn:disabled {
            background: #bdc3c7;
            cursor: not-allowed;
            transform: none;
            box-shadow: none;
        }  
        .results {
            display: none;
            text-align: center;
            padding: 40px;
        } 
        .results.show {
            display: block;
            animation: fadeIn 0.8s ease;
        }
        .score-circle {
            width: 150px;
            height: 150px;
            border-radius: 50%;
            margin: 0 auto 30px;
            display: flex;
            align-items: center;
            justify-content: center;
            font-size: 2.5em;
            font-weight: bold;
            color: white;
            background: linear-gradient(135deg, #3498db, #2ecc71);
        } 
        .score-excellent {
            background: linear-gradient(135deg, #27ae60, #2ecc71);
        }  
        .score-good {
            background: linear-gradient(135deg, #f39c12, #e67e22);
        }
        .score-needs-improvement {
            background: linear-gradient(135deg, #e74c3c, #c0392b);
        }
        .results h2 {
            color: #2c3e50;
            margin-bottom: 20px;
            font-size: 2em;
        }
        .results p {
            color: #7f8c8d;
            font-size: 1.2em;
            margin-bottom: 30px;
        } 
        .restart-btn {
            background: linear-gradient(135deg, #9b59b6, #8e44ad);
        } 
        .topic-indicator {
            display: inline-block;
            background: #3498db;
            color: white;
            padding: 5px 12px;
            border-radius: 15px;
            font-size: 0.85em;
            margin-bottom: 15px;
        }
        @media (max-width: 600px) {
            .container {
                margin: 10px;
                border-radius: 15px;
            }
            .header {
                padding: 20px;
            }
            .header h1 {
                font-size: 1.8em;
            }
            .question-container {
                padding: 20px;
            }
            .question {
                font-size: 1.1em;
            }
            .option {
                padding: 15px;
            }
            .btn {
                padding: 12px 20px;
                margin: 5px;
                min-width: 100px;
            }
        }
    </style>
</head>
<body>
    <div class="container">
        <div class="header">
            <h1>🔬 Control de Calidad</h1>
            <p>Test sobre Diseño de Experimentos (DOE) y Control Estadístico de Procesos (SPC)</p>
        </div>
        <div class="progress-container">
            <div class="progress-bar">
                <div class="progress-fill" id="progressFill"></div>
            </div>
            <div class="progress-text" id="progressText">Pregunta 1 de 25</div>
        </div>
        <div id="questionsContainer"></div>
        <div class="controls">
            <button class="btn" id="prevBtn" onclick="previousQuestion()" disabled>⬅️ Anterior</button>
            <button class="btn" id="nextBtn" onclick="nextQuestion()" disabled>Siguiente ➡️</button>
        </div>
        <div class="results" id="results">
            <div class="score-circle" id="scoreCircle">0%</div>
            <h2 id="resultTitle">¡Resultado Final!</h2>
            <p id="resultMessage">Has completado el test</p>
            <button class="btn restart-btn" onclick="restartTest()">🔄 Reiniciar Test</button>
        </div>
    </div>
    <script>
        const questions = [
            {
                topic: "DOE - Conceptos Básicos",
                question: "¿Qué significa DOE en el contexto de control de calidad?",
                options: [
                    "Diseño de Operaciones Eficientes",
                    "Diseño de Experimentos",
                    "Desarrollo de Operaciones Especiales",
                    "Diagnóstico de Errores Operativos"
                ],
                correct: 1,
                explanation: "DOE significa 'Diseño de Experimentos' (Design of Experiments), una metodología estadística para planificar y analizar experimentos de manera eficiente."
            },
            {
                topic: "DOE - Principios",
                question: "¿Cuáles son los tres principios básicos del Diseño de Experimentos?",
                options: [
                    "Medición, análisis y mejora",
                    "Aleatorización, replicación y bloqueo",
                    "Planificación, ejecución y evaluación",
                    "Control, monitoreo y ajuste"
                ],
                correct: 1,
                explanation: "Los tres principios fundamentales del DOE son: aleatorización (para eliminar sesgos), replicación (para estimar el error experimental) y bloqueo (para controlar factores de ruido)."
            },
            {
                topic: "DOE - Factorial",
                question: "En un diseño factorial completo 2³, ¿cuántos experimentos se deben realizar?",
                options: [
                    "6 experimentos",
                    "8 experimentos", 
                    "9 experimentos",
                    "12 experimentos"
                ],
                correct: 1,
                explanation: "En un diseño factorial 2³ se tienen 3 factores con 2 niveles cada uno, por lo tanto 2³ = 8 experimentos diferentes."
            },
            {
                topic: "DOE - Factores",
                question: "¿Qué se entiende por 'factor' en el diseño de experimentos?",
                options: [
                    "El resultado del experimento",
                    "Una variable controlable que puede influir en la respuesta",
                    "El error experimental",
                    "La cantidad de repeticiones del experimento"
                ],
                correct: 1,
                explanation: "Un factor es una variable controlable e independiente que el experimentador puede manipular y que potencialmente afecta la variable de respuesta."
            },
            {
                topic: "DOE - Ventajas",
                question: "¿Cuál es la principal ventaja del diseño fraccionado sobre el diseño completo?",
                options: [
                    "Mayor precisión en los resultados",
                    "Menor costo y tiempo, manteniendo información relevante",
                    "Elimina completamente el error experimental",
                    "Permite usar más factores sin restricciones"
                ],
                correct: 1,
                explanation: "El diseño fraccionado reduce significativamente el número de experimentos necesarios (y por tanto costo y tiempo) mientras mantiene la información más importante sobre los efectos principales."
            },
            {
                topic: "DOE - Interacción",
                question: "¿Qué significa que dos factores tengan interacción en un experimento?",
                options: [
                    "Que ambos factores afectan por igual la respuesta",
                    "Que el efecto de un factor depende del nivel del otro factor",
                    "Que ambos factores son independientes",
                    "Que no se pueden medir simultáneamente"
                ],
                correct: 1,
                explanation: "La interacción significa que el efecto de un factor sobre la respuesta cambia dependiendo del nivel en que se encuentre el otro factor."
            },
            {
                topic: "DOE - Software",
                question: "¿Cuál es una ventaja de usar Minitab para el análisis de DOE?",
                options: [
                    "Solo puede analizar diseños simples",
                    "Automatiza cálculos complejos y genera gráficos interpretativos",
                    "No requiere conocimiento estadístico",
                    "Solo funciona con datos metalúrgicos"
                ],
                correct: 1,
                explanation: "Minitab facilita el análisis DOE automatizando cálculos estadísticos complejos, generando gráficos de efectos principales e interacciones, y proporcionando interpretaciones claras."
            },
            {
                topic: "SPC - Definición",
                question: "¿Qué significa SPC en control de calidad?",
                options: [
                    "Sistema de Producción Continua",
                    "Control Estadístico de Procesos",
                    "Supervisión de Procesos Críticos",
                    "Sistema de Prevención de Calidad"
                ],
                correct: 1,
                explanation: "SPC significa 'Control Estadístico de Procesos' (Statistical Process Control), una metodología para monitorear y controlar procesos usando técnicas estadísticas."
            },
            {
                topic: "SPC - Variación",
                question: "¿Cuáles son los dos tipos principales de causas de variación en SPC?",
                options: [
                    "Internas y externas",
                    "Controlables e incontrolables", 
                    "Comunes y especiales",
                    "Temporales y permanentes"
                ],
                correct: 2,
                explanation: "Las causas comunes son inherentes al proceso (variación natural), mientras que las causas especiales son eventos identificables que alteran el proceso de forma impredecible."
            },
            {
                topic: "SPC - Gráficos Variables",
                question: "¿Cuál es el gráfico de control más común para monitorear la media del proceso?",
                options: [
                    "Gráfico R",
                    "Gráfico X-barra",
                    "Gráfico S",
                    "Gráfico p"
                ],
                correct: 1,
                explanation: "El gráfico X-barra (X̄) se usa para monitorear la tendencia central (media) del proceso a través del tiempo."
            },
            {
                topic: "SPC - Gráficos Variables",
                question: "¿Qué gráfico se usa para controlar la variabilidad en muestras pequeñas (n<10)?",
                options: [
                    "Gráfico X-barra",
                    "Gráfico R (Rango)",
                    "Gráfico p",
                    "Gráfico c"
                ],
                correct: 1,
                explanation: "El gráfico R (Rango) es más eficiente para controlar la variabilidad cuando el tamaño de muestra es pequeño (menor a 10 observaciones)."
            },
            {
                topic: "SPC - Gráficos Atributos",
                question: "¿Qué tipo de datos se usa en los gráficos de control para atributos?",
                options: [
                    "Mediciones continuas como peso o temperatura",
                    "Datos de conteo o clasificación (defectuoso/no defectuoso)",
                    "Solo datos de tiempo",
                    "Únicamente porcentajes"
                ],
                correct: 1,
                explanation: "Los gráficos para atributos manejan datos discretos como número de defectos, proporción de unidades defectuosas, o clasificaciones del tipo pasa/no pasa."
            },
            {
                topic: "SPC - Gráfico p",
                question: "¿Para qué se utiliza el gráfico p en SPC?",
                options: [
                    "Para controlar el promedio del proceso",
                    "Para controlar la proporción de unidades defectuosas",
                    "Para controlar la variabilidad del proceso",
                    "Para controlar el número total de defectos"
                ],
                correct: 1,
                explanation: "El gráfico p controla la proporción (fracción) de unidades defectuosas en muestras de tamaño variable o constante."
            },
            {
                topic: "SPC - Límites Control",
                question: "¿Qué representan los límites de control en un gráfico SPC?",
                options: [
                    "Los valores mínimos y máximos permitidos por especificación",
                    "Los límites naturales de variación del proceso (±3σ)",
                    "Los objetivos de calidad de la empresa",
                    "Los rangos de medición del equipo"
                ],
                correct: 1,
                explanation: "Los límites de control (típicamente ±3σ de la línea central) representan la variación natural esperada del proceso cuando solo actúan causas comunes."
            },
            {
                topic: "SPC - Interpretación",
                question: "¿Qué indica un punto fuera de los límites de control?",
                options: [
                    "El proceso está funcionando perfectamente",
                    "Presencia probable de una causa especial de variación",
                    "Los límites están mal calculados",
                    "Se necesita cambiar el equipo de medición"
                ],
                correct: 1,
                explanation: "Un punto fuera de los límites de control sugiere que el proceso está siendo afectado por una causa especial que debe ser identificada y corregida."
            },
            {
                topic: "SPC - Patrones",
                question: "¿Cuál de estos patrones en un gráfico de control indica un problema?",
                options: [
                    "Puntos distribuidos aleatoriamente dentro de los límites",
                    "7 puntos consecutivos en el mismo lado de la línea central",
                    "Variación normal alrededor de la media",
                    "Puntos cerca de la línea central"
                ],
                correct: 1,
                explanation: "Siete o más puntos consecutivos en el mismo lado de la línea central indican una tendencia o cambio en el proceso, sugiriendo la presencia de causas especiales."
            },
            {
                topic: "Metalurgia - Aplicación DOE",
                question: "En metalurgia, ¿cuál sería un ejemplo típico de factor en un experimento DOE?",
                options: [
                    "El color del metal",
                    "La temperatura de tratamiento térmico",
                    "El nombre del operador",
                    "La fecha de producción"
                ],
                correct: 1,
                explanation: "La temperatura de tratamiento térmico es un factor controlable y relevante que puede afectar significativamente las propiedades mecánicas del metal."
            },
            {
                topic: "Metalurgia - Aplicación SPC",
                question: "¿En qué proceso metalúrgico sería más útil implementar gráficos de control?",
                options: [
                    "Almacenamiento de materias primas",
                    "Monitoreo continuo de composición química en fundición",
                    "Limpieza de equipos",
                    "Rotación de personal"
                ],
                correct: 1,
                explanation: "El monitoreo de composición química en fundición es crítico para la calidad y requiere control continuo, siendo ideal para SPC."
            },
            {
                topic: "DOE - Aleatorización",
                question: "¿Por qué es importante la aleatorización en el diseño de experimentos?",
                options: [
                    "Para hacer el experimento más complejo",
                    "Para eliminar sesgos y efectos de factores no controlados",
                    "Para usar menos materiales",
                    "Para acelerar el proceso experimental"
                ],
                correct: 1,
                explanation: "La aleatorización ayuda a eliminar sesgos sistemáticos y distribuye aleatoriamente los efectos de factores no controlados, aumentando la validez del experimento."
            },
            {
                topic: "SPC - Beneficios",
                question: "¿Cuál es el principal beneficio de implementar SPC en procesos metalúrgicos?",
                options: [
                    "Eliminar completamente los defectos",
                    "Detectar problemas antes de que produzcan productos no conformes",
                    "Reducir el costo de los materiales",
                    "Acelerar la producción"
                ],
                correct: 1,
                explanation: "SPC permite la detección temprana de cambios en el proceso, evitando la producción de material defectuoso y reduciendo costos de reproceso."
            },
            {
                topic: "DOE vs Tradicional",
                question: "¿Cuál es la principal diferencia entre DOE y las pruebas tradicionales de 'un factor a la vez'?",
                options: [
                    "DOE es más costoso",
                    "DOE permite estudiar interacciones entre factores eficientemente",
                    "Las pruebas tradicionales son más precisas",
                    "DOE solo funciona con software especializado"
                ],
                correct: 1,
                explanation: "DOE permite estudiar múltiples factores simultáneamente y detectar interacciones entre ellos, algo imposible con el enfoque tradicional de cambiar un factor a la vez."
            },
            {
                topic: "SPC - Gráfico c",
                question: "¿Para qué tipo de datos se utiliza el gráfico c en SPC?",
                options: [
                    "Proporción de defectuosos",
                    "Número de defectos por unidad de inspección constante",
                    "Media del proceso",
                    "Rango de las muestras"
                ],
                correct: 1,
                explanation: "El gráfico c se usa para controlar el número de defectos (conteos) cuando el tamaño o área de inspección es constante."
            },
            {
                topic: "Integración DOE-SPC",
                question: "¿Cómo se complementan DOE y SPC en el control de calidad?",
                options: [
                    "Son metodologías completamente independientes",
                    "DOE optimiza procesos y SPC los mantiene bajo control",
                    "Solo se puede usar una metodología a la vez",
                    "SPC reemplaza completamente a DOE"
                ],
                correct: 1,
                explanation: "DOE se usa para optimizar procesos identificando factores críticos y sus niveles óptimos, mientras que SPC mantiene el proceso optimizado bajo control estadístico."
            },
            {
                topic: "Aplicación Práctica",
                question: "¿Cuál sería la secuencia lógica para implementar mejoras en un proceso metalúrgico?",
                options: [
                    "SPC primero, luego DOE si se detectan problemas",
                    "DOE para optimizar, luego SPC para controlar",
                    "Solo DOE es suficiente",
                    "Solo SPC es necesario"
                ],
                correct: 1,
                explanation: "Primero se usa DOE para entender y optimizar el proceso, luego se implementa SPC para mantener el proceso optimizado bajo control estadístico continuo."
            },
            {
                topic: "Software y Herramientas",
                question: "¿Cuál de estos softwares mencionados es más especializado para análisis estadístico de calidad?",
                options: [
                    "Word",
                    "Minitab",
                    "PowerPoint", 
                    "Outlook"
                ],
                correct: 1,
                explanation: "Minitab es un software estadístico especializado que incluye herramientas específicas para DOE, SPC y análisis de calidad, siendo muy usado en la industria."
            }
        ];
        let currentQuestion = 0;
        let userAnswers = [];
        let score = 0;
        function initializeTest() {
            renderQuestion();
            updateProgress();
        }
        function renderQuestion() {
            const container = document.getElementById('questionsContainer');
            const question = questions[currentQuestion]; 
            container.innerHTML = `
                <div class="question-container active">
                    <div class="topic-indicator">${question.topic}</div>
                    <div class="question-number">Pregunta ${currentQuestion + 1} de ${questions.length}</div>
                    <div class="question">${question.question}</div>
                    <ul class="options">
                        ${question.options.map((option, index) => `
                            <li class="option" onclick="selectOption(${index})" data-index="${index}">
                                ${option}
                            </li>
                        `).join('')}
                    </ul>
                    <div class="feedback" id="feedback"></div>
                </div>
            `
            document.getElementById('prevBtn').disabled = currentQuestion === 0;
            document.getElementById('nextBtn').disabled = true;
        }
        function selectOption(selectedIndex) {
            const options = document.querySelectorAll('.option');
            const feedback = document.getElementById('feedback');
            const question = questions[currentQuestion]; 
            // Disable all options
            options.forEach(option => {
                option.classList.add('disabled');
                option.onclick = null;
            });  
            // Mark selected option
            options[selectedIndex].classList.add('selected');  
            // Show correct answer
            options[question.correct].classList.add('correct'); 
            // Mark incorrect if wrong selection
            if (selectedIndex !== question.correct) {
                options[selectedIndex].classList.add('incorrect');
            } 
            // Store answer
            userAnswers[currentQuestion] = selectedIndex; 
            // Show feedback
            const isCorrect = selectedIndex === question.correct;
            feedback.className = `feedback ${isCorrect ? 'correct' : 'incorrect'} show`;
            feedback.innerHTML = `
                <strong>${isCorrect ? '✅ ¡Correcto!' : '❌ Incorrecto'}</strong><br>
                ${question.explanation}
            `; 
            if (isCorrect) {
                score++;
            }  
            // Enable next button
            document.getElementById('nextBtn').disabled = false;
        }
        function nextQuestion() {
            if (currentQuestion < questions.length - 1) {
                currentQuestion++;
                renderQuestion();
                updateProgress();
            } else {
                showResults();
            }
        }
        function previousQuestion() {
            if (currentQuestion > 0) {
                currentQuestion--;
                renderQuestion();
                updateProgress();
                // If question was already answered, show the previous answer
                if (userAnswers[currentQuestion] !== undefined) {
                    const selectedIndex = userAnswers[currentQuestion];
                    selectOption(selectedIndex);
                }
            }
        }
        function updateProgress() {
            const progress = ((currentQuestion + 1) / questions.length) * 100;
            document.getElementById('progressFill').style.width = progress + '%';
            document.getElementById('progressText').textContent = `Pregunta ${currentQuestion + 1} de ${questions.length}`;
        }
        function showResults() {
            const percentage = Math.round((score / questions.length) * 100);
            const container = document.getElementById('questionsContainer');
            const controls = document.querySelector('.controls');
            const results = document.getElementById('results');
            const scoreCircle = document.getElementById('scoreCircle');
            const resultTitle = document.getElementById('resultTitle');
            const resultMessage = document.getElementById('resultMessage'); 
            container.style.display = 'none';
            controls.style.display = 'none';
            results.classList.add('show');
            scoreCircle.textContent = percentage + '%';
            if (percentage >= 90) {
                scoreCircle.className = 'score-circle score-excellent';
                resultTitle.textContent = '🏆 ¡Excelente!';
                resultMessage.textContent = `Obtuviste ${score} de ${questions.length} respuestas correctas. Dominas muy bien los conceptos de DOE y SPC.`;
            } else if (percentage >= 70) {
                scoreCircle.className = 'score-circle score-good';
                resultTitle.textContent = '👍 ¡Buen trabajo!';
                resultMessage.textContent = `Obtuviste ${score} de ${questions.length} respuestas correctas. Tienes una buena comprensión de los temas.`;
            } else {
                scoreCircle.className = 'score-circle score-needs-improvement';
                resultTitle.textContent = '📚 Sigue estudiando';
                resultMessage.textContent = `Obtuviste ${score} de ${questions.length} respuestas correctas. Te recomiendo revisar los conceptos de DOE y SPC.`;
            }
        }
        function restartTest() {
            currentQuestion = 0;
            userAnswers = [];
            score = 0; 
            const container = document.getElementById('questionsContainer');
            const controls = document.querySelector('.controls');
            const results = document.getElementById('results');
            container.style.display = 'block';
            controls.style.display = 'block';
            results.classList.remove('show');
            initializeTest();
        }
        // Initialize test when page loads
        window.onload = function() {
            initializeTest();
        };
    </script>
</body>
</html>
