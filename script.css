// Test questions
const questions = [
    { text: "We found your location near the spot, you have been gone there", type: "relevant" },
    { text: "Your phone records show calls to the victim before the incident", type: "relevant" },
    { text: "Witnesses saw you leaving the area around the time it happened", type: "relevant" },
    { text: "You were seen arguing with the victim earlier that day", type: "relevant" },
    { text: "Security footage shows your vehicle near the crime scene", type: "relevant" },
    { text: "Your alibi for that night has been verified by multiple sources", type: "relevant" },
    { text: "You had access to the location where the incident occurred", type: "relevant" },
    { text: "Your fingerprints were found on items related to the case", type: "relevant" },
    { text: "You have told us everything you know about this situation", type: "relevant" },
    { text: "You were at home alone during the entire time in question", type: "relevant" }
];

// Test state
let currentQuestion = 0;
let testResults = [];
let subjectName = "";
let testPurpose = "";
let graphIntervals = {};

// Show setup section
function showSetup() {
    document.getElementById('welcome').style.display = 'none';
    document.getElementById('setup').style.display = 'block';
}

// Handle setup form submission
document.getElementById('setupForm').addEventListener('submit', function(e) {
    e.preventDefault();
    subjectName = document.getElementById('subjectName').value;
    testPurpose = document.getElementById('testPurpose').value;
    
    document.getElementById('setup').style.display = 'none';
    document.getElementById('test').style.display = 'block';
    
    startTest();
});

// Start the test
function startTest() {
    currentQuestion = 0;
    testResults = [];
    showQuestion();
    startGraphs();
}

// Show current question
function showQuestion() {
    const question = questions[currentQuestion];
    document.getElementById('questionNumber').textContent = `Question ${currentQuestion + 1} of ${questions.length}`;
    document.getElementById('questionText').textContent = question.text;
    
    // Add recording animation
    document.querySelector('.question-box').classList.add('recording');
}

// Handle answer
function answerQuestion(answer) {
    const question = questions[currentQuestion];
    
    // Stop recording animation
    document.querySelector('.question-box').classList.remove('recording');
    
    // Simulate physiological response analysis
    const isDeceptive = simulateDeceptionDetection(question.type, answer);
    
    // Store result
    testResults.push({
        question: question.text,
        answer: answer,
        type: question.type,
        deceptive: isDeceptive
    });
    
    // Move to next question or show results
    currentQuestion++;
    if (currentQuestion < questions.length) {
        setTimeout(() => {
            showQuestion();
        }, 1000);
    } else {
        stopGraphs();
        showResults();
    }
}

// Simulate deception detection (random for demo)
function simulateDeceptionDetection(type, answer) {
    // For relevant questions, have a higher chance of showing deception
    return Math.random() < 0.4; // 40% chance
}

// Start graph animations
function startGraphs() {
    // Heart rate graph
    const heartCanvas = document.getElementById('heartRateCanvas');
    const heartCtx = heartCanvas.getContext('2d');
    heartCanvas.width = heartCanvas.offsetWidth;
    heartCanvas.height = heartCanvas.offsetHeight;
    
    let heartData = [];
    graphIntervals.heart = setInterval(() => {
        drawGraph(heartCtx, heartData, 60, 100, '#dc3545');
    }, 100);
    
    // Respiration graph
    const respCanvas = document.getElementById('respirationCanvas');
    const respCtx = respCanvas.getContext('2d');
    respCanvas.width = respCanvas.offsetWidth;
    respCanvas.height = respCanvas.offsetHeight;
    
    let respData = [];
    graphIntervals.respiration = setInterval(() => {
        drawGraph(respCtx, respData, 12, 20, '#007bff');
    }, 100);
    
    // Sweat graph
    const sweatCanvas = document.getElementById('sweatCanvas');
    const sweatCtx = sweatCanvas.getContext('2d');
    sweatCanvas.width = sweatCanvas.offsetWidth;
    sweatCanvas.height = sweatCanvas.offsetHeight;
    
    let sweatData = [];
    graphIntervals.sweat = setInterval(() => {
        drawGraph(sweatCtx, sweatData, 0, 10, '#6c757d');
    }, 100);
}

// Draw graph function
function drawGraph(ctx, data, min, max, color) {
    const width = ctx.canvas.width;
    const height = ctx.canvas.height;
    
    // Add new data point
    const value = min + Math.random() * (max - min);
    data.push(value);
    
    // Keep only last 50 points
    if (data.length > 50) {
        data.shift();
    }
    
    // Clear canvas
    ctx.clearRect(0, 0, width, height);
    
    // Draw grid
    ctx.strokeStyle = '#e9ecef';
    ctx.lineWidth = 1;
    for (let i = 0; i < 5; i++) {
        const y = (height / 5) * i;
        ctx.beginPath();
        ctx.moveTo(0, y);
        ctx.lineTo(width, y);
        ctx.stroke();
    }
    
    // Draw graph
    if (data.length > 1) {
        ctx.strokeStyle = color;
        ctx.lineWidth = 2;
        ctx.beginPath();
        
        const xStep = width / (data.length - 1);
        data.forEach((value, index) => {
            const x = index * xStep;
            const y = height - ((value - min) / (max - min)) * height;
            
            if (index === 0) {
                ctx.moveTo(x, y);
            } else {
                ctx.lineTo(x, y);
            }
        });
        
        ctx.stroke();
    }
}

// Stop graph animations
function stopGraphs() {
    Object.values(graphIntervals).forEach(interval => {
        clearInterval(interval);
    });
    graphIntervals = {};
}

// Show results
function showResults() {
    document.getElementById('test').style.display = 'none';
    document.getElementById('results').style.display = 'block';
    
    // Calculate overall deception score
    const relevantQuestions = testResults.filter(r => r.type === 'relevant');
    const deceptiveCount = relevantQuestions.filter(r => r.deceptive).length;
    const deceptionScore = deceptiveCount / relevantQuestions.length;
    
    // Determine overall result
    let resultClass, resultText, description;
    if (deceptionScore < 0.3) {
        resultClass = 'truthful';
        resultText = 'No Deception Detected';
        description = 'Physiological responses indicate truthful answers to relevant questions.';
    } else if (deceptionScore < 0.7) {
        resultClass = 'inconclusive';
        resultText = 'Inconclusive Results';
        description = 'Mixed physiological responses. Further examination may be required.';
    } else {
        resultClass = 'deceptive';
        resultText = 'Deception Detected';
        description = 'Significant physiological responses suggest deception in relevant questions.';
    }
    
    const indicator = document.getElementById('deceptionIndicator');
    indicator.className = `deception-indicator ${resultClass}`;
    indicator.textContent = resultText;
    
    document.getElementById('resultDescription').textContent = description;
    
    // Show question-by-question results
    const resultsContainer = document.getElementById('questionResults');
    resultsContainer.innerHTML = '';
    
    testResults.forEach(result => {
        const resultItem = document.createElement('div');
        resultItem.className = 'question-result-item';
        
        const badgeClass = result.deceptive ? 'deceptive' : 'truthful';
        const badgeText = result.deceptive ? 'Deception' : 'Truthful';
        
        resultItem.innerHTML = `
            <div class="question-text">
                <strong>${result.question}</strong><br>
                <span style="color: var(--dark-gray);">Answer: ${result.answer.toUpperCase()}</span>
            </div>
            <span class="result-badge ${badgeClass}">${badgeText}</span>
        `;
        
        resultsContainer.appendChild(resultItem);
    });
}

// Reset test
function resetTest() {
    document.getElementById('results').style.display = 'none';
    document.getElementById('welcome').style.display = 'block';
    
    // Reset form
    document.getElementById('setupForm').reset();
    
    // Clear canvases
    const canvases = document.querySelectorAll('.graph-canvas');
    canvases.forEach(canvas => {
        const ctx = canvas.getContext('2d');
        ctx.clearRect(0, 0, canvas.width, canvas.height);
    });
}

// Handle window resize
window.addEventListener('resize', () => {
    const canvases = document.querySelectorAll('.graph-canvas');
    canvases.forEach(canvas => {
        canvas.width = canvas.offsetWidth;
        canvas.height = canvas.offsetHeight;
    });
});
