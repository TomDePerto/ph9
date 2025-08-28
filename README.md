[beta9.html](https://github.com/user-attachments/files/22031399/beta9.html)
<!DOCTYPE html>
<html lang="pt-BR">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Horário Escolar</title>
    <style>
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
            font-family: Arial, sans-serif;
        }
        
        body {
            background: #2a5298;
            color: #fff;
            min-height: 100vh;
            padding: 20px;
            text-align: center;
        }
        
        .container {
            max-width: 600px;
            margin: 0 auto;
            background-color: rgba(255, 255, 255, 0.1);
            border-radius: 10px;
            padding: 20px;
            position: relative;
        }
        
        h1 {
            font-size: 24px;
            margin-bottom: 10px;
        }
        
        .school-selector {
            margin-bottom: 15px;
        }
        
        .school-btn {
            background-color: rgba(255, 255, 255, 0.1);
            border: none;
            border-radius: 5px;
            padding: 8px 15px;
            color: white;
            cursor: pointer;
            margin: 0 5px;
        }
        
        .school-btn.active {
            background-color: rgba(255, 255, 255, 0.3);
            font-weight: bold;
        }
        
        .current-time {
            font-size: 16px;
            margin-bottom: 20px;
        }
        
        .class-info {
            background-color: rgba(255, 255, 255, 0.15);
            border-radius: 10px;
            padding: 20px;
            margin-bottom: 20px;
        }
        
        .status {
            font-size: 18px;
            margin-bottom: 10px;
            font-weight: bold;
        }
        
        .class-details {
            font-size: 24px;
            font-weight: bold;
            margin: 10px 0;
            padding: 10px;
            border-radius: 8px;
        }
        
        .time-range {
            font-size: 16px;
        }
        
        .next-class-btn {
            background-color: rgba(255, 255, 255, 0.2);
            border: none;
            border-radius: 50%;
            width: 50px;
            height: 50px;
            color: white;
            font-size: 18px;
            cursor: pointer;
            position: fixed;
            bottom: 20px;
            right: 20px;
            z-index: 100;
        }
        
        .config-btn {
            background-color: rgba(255, 255, 255, 0.2);
            border: none;
            border-radius: 50%;
            width: 40px;
            height: 40px;
            color: white;
            font-size: 16px;
            cursor: pointer;
            position: fixed;
            bottom: 80px;
            right: 20px;
            z-index: 100;
        }
        
        .next-class-panel {
            background-color: rgba(255, 255, 255, 0.15);
            border-radius: 10px;
            padding: 15px;
            margin-top: 15px;
            display: none;
        }
        
        .next-class-panel.show {
            display: block;
        }
        
        .day-navigation {
            display: flex;
            justify-content: center;
            margin-top: 15px;
            gap: 5px;
        }
        
        .day-btn {
            background-color: rgba(255, 255, 255, 0.1);
            border: none;
            border-radius: 5px;
            padding: 5px 10px;
            color: white;
            cursor: pointer;
        }
        
        .day-btn.active {
            background-color: rgba(255, 255, 255, 0.3);
        }
        
        /* Cores para cada sala */
        .class-1A { background-color: rgba(255, 204, 204, 0.5); }
        .class-1B { background-color: rgba(204, 229, 255, 0.5); }
        .class-2A { background-color: rgba(204, 255, 204, 0.5); }
        .class-2B { background-color: rgba(255, 255, 204, 0.5); }
        .class-2C { background-color: rgba(255, 204, 255, 0.5); }
        .class-2D { background-color: rgba(204, 255, 255, 0.5); }
        .class-3A { background-color: rgba(229, 204, 255, 0.5); }
        .class-3B { background-color: rgba(255, 217, 179, 0.5); }
        .class-4A { background-color: rgba(179, 255, 217, 0.5); }
        .class-4B { background-color: rgba(217, 179, 255, 0.5); }
        .class-5A { background-color: rgba(255, 179, 217, 0.5); }
        .class-5B { background-color: rgba(179, 217, 255, 0.5); }
        .class-6A { background-color: rgba(217, 255, 179, 0.5); }
        .class-6B { background-color: rgba(255, 255, 179, 0.5); }
        .class-7A { background-color: rgba(255, 204, 153, 0.5); }
        .class-7B { background-color: rgba(204, 255, 153, 0.5); }
        .class-8A { background-color: rgba(153, 204, 255, 0.5); }
        .class-8B { background-color: rgba(255, 153, 204, 0.5); }
        .class-9A { background-color: rgba(204, 153, 255, 0.5); }
        .class-9B { background-color: rgba(153, 255, 204, 0.5); }
        .class-ATPCA { background-color: rgba(255, 204, 153, 0.7); }
        .class-ATPCG { background-color: rgba(153, 204, 255, 0.7); }
        .class-ELETIVA { background-color: rgba(204, 255, 153, 0.7); }
        .class-EXTRA { background-color: rgba(255, 204, 153, 0.7); }
        
        /* Painel de configuração */
        .config-panel {
            background-color: rgba(0, 0, 0, 0.9);
            border-radius: 10px;
            padding: 20px;
            position: fixed;
            top: 50%;
            left: 50%;
            transform: translate(-50%, -50%);
            width: 90%;
            max-width: 400px;
            z-index: 1000;
            display: none;
        }
        
        .config-panel.show {
            display: block;
        }
        
        .config-panel h2 {
            margin-bottom: 15px;
        }
        
        .close-btn {
            position: absolute;
            top: 10px;
            right: 10px;
            background: none;
            border: none;
            color: white;
            font-size: 20px;
            cursor: pointer;
        }
        
        .form-group {
            margin-bottom: 15px;
            text-align: left;
        }
        
        .form-group label {
            display: block;
            margin-bottom: 5px;
        }
        
        .form-group input, .form-group select {
            width: 100%;
            padding: 8px;
            border-radius: 5px;
            border: 1px solid rgba(255, 255, 255, 0.2);
            background-color: rgba(255, 255, 255, 0.1);
            color: white;
        }
        
        .btn {
            background-color: rgba(255, 255, 255, 0.2);
            border: none;
            border-radius: 5px;
            padding: 8px 12px;
            color: white;
            cursor: pointer;
            margin-top: 10px;
        }
        
        .btn-primary {
            background-color: rgba(76, 175, 80, 0.7);
        }
        
        .btn-danger {
            background-color: rgba(244, 67, 54, 0.7);
        }
        
        .extra-classes-list {
            margin-top: 20px;
            text-align: left;
        }
        
        .extra-class-item {
            background-color: rgba(255, 255, 255, 0.1);
            border-radius: 5px;
            padding: 10px;
            margin-bottom: 10px;
        }
        
        .overlay {
            display: none;
            position: fixed;
            top: 0;
            left: 0;
            width: 100%;
            height: 100%;
            background-color: rgba(0, 0, 0, 0.7);
            z-index: 999;
        }
        
        .overlay.show {
            display: block;
        }
    </style>
</head>
<body>
    <div class="container">
        <h1>Horário Escolar</h1>
        
        <div class="school-selector">
            <button class="school-btn active" data-school="PS">Paulo Silva</button>
            <button class="school-btn" data-school="CSM">São Matheus</button>
        </div>
        
        <div class="current-time" id="current-time">Carregando...</div>
        
        <div class="class-info">
            <div class="status" id="status">Verificando...</div>
            <div class="class-details" id="class-details">-</div>
            <div class="time-range" id="time-range">-</div>
        </div>
        
        <div class="day-navigation">
            <button class="day-btn" data-day="0">Seg</button>
            <button class="day-btn" data-day="1">Ter</button>
            <button class="day-btn" data-day="2">Qua</button>
            <button class="day-btn" data-day="3">Qui</button>
            <button class="day-btn" data-day="4">Sex</button>
        </div>
        
        <div class="next-class-panel" id="next-class-panel">
            <h3>Próxima Aula</h3>
            <div id="next-class-details">-</div>
            <div class="time-range" id="next-time-range">-</div>
        </div>
    </div>
    
    <button class="next-class-btn" id="next-class-btn">
        →
    </button>
    
    <button class="config-btn" id="config-btn">
        ⚙
    </button>
    
    <div class="overlay" id="overlay"></div>
    
    <div class="config-panel" id="config-panel">
        <h2>Configurações</h2>
        <button class="close-btn" id="close-config">×</button>
        
        <h3>Adicionar Aula Extra</h3>
        <div class="form-group">
            <label for="extra-school">Escola:</label>
            <select id="extra-school">
                <option value="PS">Paulo Silva</option>
                <option value="CSM">São Matheus</option>
            </select>
        </div>
        
        <div class="form-group">
            <label for="extra-day">Dia da Semana:</label>
            <select id="extra-day">
                <option value="0">Segunda-feira</option>
                <option value="1">Terça-feira</option>
                <option value="2">Quarta-feira</option>
                <option value="3">Quinta-feira</option>
                <option value="4">Sexta-feira</option>
            </select>
        </div>
        
        <div class="form-group">
            <label for="extra-time">Horário (ex: 08:00 - 09:00):</label>
            <input type="text" id="extra-time" placeholder="08:00 - 09:00">
        </div>
        
        <div class="form-group">
            <label for="extra-class">Sala/Turma:</label>
            <input type="text" id="extra-class" placeholder="Ex: 8ºA">
        </div>
        
        <button class="btn btn-primary" id="add-extra-class">
            Adicionar Aula
        </button>
        
        <div class="extra-classes-list">
            <h3>Aulas Extras</h3>
            <div id="extra-classes-container">
                <!-- Aulas extras serão adicionadas aqui -->
            </div>
        </div>
    </div>

    <script>
        // Dados do horário da Escola Paulo Silva (PS)
        var schedulePS = {
            name: "Paulo Silva",
            days: ["Seg", "Ter", "Qua", "Qui", "Sex"],
            periods: [
                { name: "1ª AULA", time: "7:00 - 7:50", classes: ["9ºA", "1º A", "", "", ""] },
                { name: "2ª AULA", time: "7:50 - 8:40", classes: ["9ºB", "8ºA", "9ºB", "", ""] },
                { name: "INTER", time: "8:40 - 14:15", classes: ["", "", "", "", ""], isBreak: true },
                { name: "3ª AULA", time: "8:50 - 9:40", classes: ["6ºB", "9ºA", "8ºA", "", ""] },
                { name: "4ª AULA", time: "9:40 - 10:30", classes: ["7ºA", "6ºB", "7ºB", "", ""] },
                { name: "5ª AULA", time: "10:30 - 11:20", classes: ["", "1º B", "1º A", "", ""] },
                { name: "ALMOÇO", time: "11:20 - 16:55", classes: ["", "", "", "", ""], isBreak: true },
                { name: "6ª AULA", time: "12:20 - 13:10", classes: ["8ºB", "7ºA", "8ºB", "", "1º B"] },
                { name: "7ª AULA", time: "13:10 - 14:00", classes: ["6ºA", "7ºB", "", "", "6ºA"] },
                { name: "TP", time: "14:00 - 19:35", classes: ["", "", "", "", ""], isBreak: true },
                { name: "1ª AULA", time: "14:15 - 15:05", classes: ["", "ATPCA", "ATPCG", "", ""] },
                { name: "2ª AULA", time: "15:05 - 15:55", classes: ["", "ATPCA", "ATPCG", "", ""] },
                { name: "INTERVALO", time: "15:55 - 17:00", classes: ["", "", "", "", ""], isBreak: true },
                { name: "3ª AULA", time: "16:05 - 16:55", classes: ["", "", "", "", ""] },
                { name: "4ª AULA", time: "16:55 - 17:45", classes: ["", "", "", "ELETIVA", "2ªD"] },
                { name: "5ª AULA", time: "17:45 - 18:35", classes: ["", "", "", "", "3ª A"] },
                { name: "JANTAR", time: "20:45 - 19:35", classes: ["", "", "", "", ""], isBreak: true },
                { name: "6ª AULA", time: "19:35 - 20:25", classes: ["", "", "2ªA", "2ªB", ""] },
                { name: "7ª AULA", time: "20:25 - 21:15", classes: ["", "", "3ª B", "2ªC", ""] }
            ]
        };

        // Dados do horário do Colégio São Matheus (CSM)
        var scheduleCSM = {
            name: "São Matheus",
            days: ["Seg", "Ter", "Qua", "Qui", "Sex"],
            periods: [
                { name: "1ª AULA", time: "7:30 - 8:20", classes: ["", "", "", "", "4º ano"] },
                { name: "2ª AULA", time: "8:20 - 9:10", classes: ["", "", "", "", "4º ano"] },
                { name: "3ª AULA", time: "9:10 - 10:00", classes: ["", "", "", "5º ano", ""] },
                { name: "4ª AULA", time: "10:20 - 11:10", classes: ["", "", "", "5º ano", "7º ano"] },
                { name: "5ª AULA", time: "11:10 - 12:00", classes: ["1º ano", "2º/3º ano", "2º/3º ano", "6º ano", "8º ano"] },
                { name: "ALMOÇO", time: "12:00 - 13:30", classes: ["", "", "", "", ""], isBreak: true },
                { name: "6ª AULA", time: "13:30 - 14:20", classes: ["", "", "", "", ""] },
                { name: "7ª AULA", time: "14:20 - 15:10", classes: ["", "", "", "", ""] },
                { name: "8ª AULA", time: "15:30 - 16:20", classes: ["", "", "", "", ""] },
                { name: "9ª AULA", time: "16:40 - 17:30", classes: ["1º ano", "2º/3º ano", "2º/3º ano", "", ""] }
            ]
        };

        // Mapeamento de classes para CSS
        var classToCssMap = {
            "1º A": "class-1A", "1º B": "class-1B", "2ªA": "class-2A", "2ªB": "class-2B",
            "2ªC": "class-2C", "2ªD": "class-2D", "3ª A": "class-3A", "3ª B": "class-3B",
            "4º ano": "class-4A", "5º ano": "class-5A", "6º ano": "class-6A", 
            "7º ano": "class-7A", "8º ano": "class-8A", "9ºA": "class-9A", "9ºB": "class-9B",
            "1º ano": "class-1A", "2º/3º ano": "class-2A",
            "ATPCA": "class-ATPCA", "ATPCG": "class-ATPCG", "ELETIVA": "class-ELETIVA"
        };

        // Variáveis globais
        var currentDayIndex = new Date().getDay() - 1;
        if (currentDayIndex < 0 || currentDayIndex > 4) currentDayIndex = 0;
        
        var currentSchool = "PS";
        var extraClasses = JSON.parse(localStorage.getItem('extraClasses')) || [];

        // Elementos DOM
        var currentTimeEl = document.getElementById('current-time');
        var statusEl = document.getElementById('status');
        var classDetailsEl = document.getElementById('class-details');
        var timeRangeEl = document.getElementById('time-range');
        var nextClassBtn = document.getElementById('next-class-btn');
        var nextClassPanel = document.getElementById('next-class-panel');
        var nextClassDetailsEl = document.getElementById('next-class-details');
        var nextTimeRangeEl = document.getElementById('next-time-range');
        var dayButtons = document.querySelectorAll('.day-btn');
        var schoolButtons = document.querySelectorAll('.school-btn');
        var configBtn = document.getElementById('config-btn');
        var configPanel = document.getElementById('config-panel');
        var overlay = document.getElementById('overlay');
        var closeConfigBtn = document.getElementById('close-config');
        var addExtraClassBtn = document.getElementById('add-extra-class');
        var extraClassesContainer = document.getElementById('extra-classes-container');

        // Função para obter o horário atual baseado na escola selecionada
        function getCurrentSchedule() {
            return currentSchool === "PS" ? schedulePS : scheduleCSM;
        }

        // Função para atualizar o horário atual
        function updateCurrentTime() {
            var now = new Date();
            var timeString = now.toLocaleTimeString('pt-BR', { 
                hour: '2-digit', 
                minute: '2-digit'
            });
            var dateString = now.toLocaleDateString('pt-BR', {
                weekday: 'long',
                day: 'numeric',
                month: 'long'
            });
            currentTimeEl.textContent = dateString + ' - ' + timeString;
        }

        // Função para converter hora para minutos
        function timeToMinutes(timeStr) {
            var parts = timeStr.split(':');
            return parseInt(parts[0]) * 60 + parseInt(parts[1] || '0');
        }

        // Função para verificar qual aula está no momento
        function findCurrentClass() {
            var now = new Date();
            var currentMinutes = now.getHours() * 60 + now.getMinutes();
            var currentDay = currentDayIndex;
            var schedule = getCurrentSchedule();
            
            var currentClass = null;
            var nextClass = null;
            
            // Verificar aulas padrão
            for (var i = 0; i < schedule.periods.length; i++) {
                var period = schedule.periods[i];
                if (period.isBreak) continue;
                
                var timeParts = period.time.split(' - ');
                var startMinutes = timeToMinutes(timeParts[0]);
                var endMinutes = timeToMinutes(timeParts[1]);
                
                if (currentMinutes >= startMinutes && currentMinutes <= endMinutes) {
                    currentClass = {
                        class: period.classes[currentDay],
                        period: period.name,
                        time: period.time
                    };
                } else if (currentMinutes < startMinutes && !nextClass) {
                    nextClass = {
                        class: period.classes[currentDay],
                        period: period.name,
                        time: period.time
                    };
                }
            }
            
            // Verificar aulas extras para a escola atual
            for (var i = 0; i < extraClasses.length; i++) {
                var extra = extraClasses[i];
                if (extra.day != currentDay || extra.school != currentSchool) continue;
                
                var timeParts = extra.time.split(' - ');
                var startMinutes = timeToMinutes(timeParts[0]);
                var endMinutes = timeToMinutes(timeParts[1]);
                
                if (currentMinutes >= startMinutes && currentMinutes <= endMinutes) {
                    currentClass = {
                        class: extra.class,
                        period: "AULA EXTRA",
                        time: extra.time,
                        isExtra: true
                    };
                } else if (currentMinutes < startMinutes && !nextClass) {
                    nextClass = {
                        class: extra.class,
                        period: "AULA EXTRA",
                        time: extra.time,
                        isExtra: true
                    };
                }
            }
            
            return { currentClass: currentClass, nextClass: nextClass };
        }

        // Função para obter a classe CSS com base no nome da sala
        function getClassCss(className) {
            return classToCssMap[className] || 'class-EXTRA';
        }

        // Função para atualizar a exibição
        function updateDisplay() {
            var result = findCurrentClass();
            var currentClass = result.currentClass;
            var nextClass = result.nextClass;
            
            classDetailsEl.className = 'class-details';
            nextClassDetailsEl.className = '';
            
            if (currentClass && currentClass.class) {
                statusEl.textContent = "AULA EM ANDAMENTO";
                classDetailsEl.textContent = currentClass.class;
                classDetailsEl.classList.add(getClassCss(currentClass.class));
                if (currentClass.isExtra) {
                    classDetailsEl.classList.add('class-EXTRA');
                }
                timeRangeEl.textContent = currentClass.period + ' • ' + currentClass.time;
            } else {
                statusEl.textContent = "SEM AULA NO MOMENTO";
                classDetailsEl.textContent = "-";
                timeRangeEl.textContent = "Fora do horário de aula";
            }
            
            if (nextClass && nextClass.class) {
                nextClassDetailsEl.textContent = nextClass.class;
                nextClassDetailsEl.classList.add(getClassCss(nextClass.class));
                if (nextClass.isExtra) {
                    nextClassDetailsEl.classList.add('class-EXTRA');
                }
                nextTimeRangeEl.textContent = nextClass.period + ' • ' + nextClass.time;
            } else {
                nextClassDetailsEl.textContent = "Não há mais aulas hoje";
                nextTimeRangeEl.textContent = "";
            }
            
            for (var i = 0; i < dayButtons.length; i++) {
                if (i === currentDayIndex) {
                    dayButtons[i].classList.add('active');
                } else {
                    dayButtons[i].classList.remove('active');
                }
            }
            
            // Atualizar botões da escola
            for (var i = 0; i < schoolButtons.length; i++) {
                if (schoolButtons[i].getAttribute('data-school') === currentSchool) {
                    schoolButtons[i].classList.add('active');
                } else {
                    schoolButtons[i].classList.remove('active');
                }
            }
        }

        // Função para renderizar a lista de aulas extras
        function renderExtraClasses() {
            extraClassesContainer.innerHTML = '';
            
            var schoolExtras = extraClasses.filter(function(extra) {
                return extra.school === currentSchool;
            });
            
            if (schoolExtras.length === 0) {
                extraClassesContainer.innerHTML = '<p>Nenhuma aula extra adicionada.</p>';
                return;
            }
            
            var dayNames = ['Segunda', 'Terça', 'Quarta', 'Quinta', 'Sexta'];
            
            for (var i = 0; i < schoolExtras.length; i++) {
                var extra = schoolExtras[i];
                var item = document.createElement('div');
                item.className = 'extra-class-item';
                item.innerHTML = `
                    <div><strong>${dayNames[extra.day]} - ${extra.time}</strong></div>
                    <div>${extra.class}</div>
                    <button class="btn btn-danger delete-extra" data-index="${i}">Remover</button>
                `;
                extraClassesContainer.appendChild(item);
            }
            
            // Adicionar event listeners aos botões de deletar
            var deleteButtons = document.querySelectorAll('.delete-extra');
            for (var i = 0; i < deleteButtons.length; i++) {
                deleteButtons[i].addEventListener('click', function() {
                    var index = parseInt(this.getAttribute('data-index'));
                    deleteExtraClass(index);
                });
            }
        }

        // Função para adicionar uma aula extra
        function addExtraClass() {
            var school = document.getElementById('extra-school').value;
            var day = parseInt(document.getElementById('extra-day').value);
            var time = document.getElementById('extra-time').value;
            var classValue = document.getElementById('extra-class').value;
            
            // Validação básica
            if (!time || !classValue) {
                alert('Por favor, preencha o horário e a sala/turma.');
                return;
            }
            
            // Validar formato do horário
            var timeRegex = /^([0-1]?[0-9]|2[0-3]):[0-5][0-9] - ([0-1]?[0-9]|2[0-3]):[0-5][0-9]$/;
            if (!timeRegex.test(time)) {
                alert('Por favor, use o formato HH:MM - HH:MM para o horário.');
                return;
            }
            
            // Adicionar à lista de aulas extras
            extraClasses.push({
                school: school,
                day: day,
                time: time,
                class: classValue
            });
            
            // Salvar no localStorage
            localStorage.setItem('extraClasses', JSON.stringify(extraClasses));
            
            // Atualizar a interface
            updateDisplay();
            renderExtraClasses();
            
            // Limpar o formulário
            document.getElementById('extra-time').value = '';
            document.getElementById('extra-class').value = '';
            
            alert('Aula extra adicionada com sucesso!');
        }

        // Função para deletar uma aula extra
        function deleteExtraClass(index) {
            if (confirm('Tem certeza que deseja remover esta aula extra?')) {
                extraClasses.splice(index, 1);
                localStorage.setItem('extraClasses', JSON.stringify(extraClasses));
                updateDisplay();
                renderExtraClasses();
            }
        }

        // Inicializar
        function init() {
            updateCurrentTime();
            updateDisplay();
            renderExtraClasses();
            
            setInterval(function() {
                updateCurrentTime();
                updateDisplay();
            }, 60000);
            
            nextClassBtn.addEventListener('click', function() {
                nextClassPanel.classList.toggle('show');
            });
            
            for (var i = 0; i < dayButtons.length; i++) {
                dayButtons[i].addEventListener('click', function() {
                    currentDayIndex = parseInt(this.getAttribute('data-day'));
                    updateDisplay();
                });
            }
            
            for (var i = 0; i < schoolButtons.length; i++) {
                schoolButtons[i].addEventListener('click', function() {
                    currentSchool = this.getAttribute('data-school');
                    updateDisplay();
                    renderExtraClasses();
                });
            }
            
            configBtn.addEventListener('click', function() {
                configPanel.classList.add('show');
                overlay.classList.add('show');
            });
            
            closeConfigBtn.addEventListener('click', function() {
                configPanel.classList.remove('show');
                overlay.classList.remove('show');
            });
            
            overlay.addEventListener('click', function() {
                configPanel.classList.remove('show');
                overlay.classList.remove('show');
            });
            
            addExtraClassBtn.addEventListener('click', addExtraClass);
        }

        // Iniciar
        init();
    </script>
</body>
</html>
