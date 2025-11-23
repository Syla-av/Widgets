<!DOCTYPE html>
<html>
<head>
  <meta charset="UTF-8">
  <title>Racha Mágica</title>
  <style>
    @import url('https://fonts.googleapis.com/css2?family=Cinzel:wght@400;600&family=Crimson+Pro:wght@400;700&display=swap');

    body {
      font-family: 'Crimson Pro', serif;
      background: radial-gradient(circle at center, #1d1a2f, #0b0714 80%);
      color: #e6dff9;
      padding: 30px;
      text-align: center;
      overflow: hidden;
    }

    h2 {
      font-family: 'Cinzel', serif;
      font-size: 2.2rem;
      letter-spacing: 2px;
      margin-bottom: 10px;
      color: #d8caff;
      text-shadow: 0 0 8px #a487ff;
    }

    #days {
      font-size: 4.2rem;
      margin-bottom: 20px;
      font-family: 'Cinzel', serif;
      color: #fff2ff;
      text-shadow: 0 0 12px #c06bff;
    }

    button {
      background: rgba(90, 50, 150, 0.45);
      border: 1px solid #a87eff;
      padding: 12px 28px;
      border-radius: 10px;
      color: #e9d7ff;
      font-size: 1.1rem;
      font-family: 'Cinzel', serif;
      cursor: pointer;
      letter-spacing: 1px;
      backdrop-filter: blur(6px);
      transition: 0.25s ease;
      text-shadow: 0 0 6px #8f63f7;
      box-shadow: 0 0 12px rgba(162, 114, 255, 0.4);
    }

    button:hover {
      transform: scale(1.06);
      box-shadow: 0 0 18px rgba(200, 160, 255, 0.65);
      background: rgba(120, 70, 190, 0.55);
    }

    .calendar {
      display: flex;
      justify-content: center;
      gap: 8px;
      margin-top: 30px;
    }

    .day {
      width: 16px;
      height: 16px;
      border-radius: 4px;
      background: rgba(255,255,255,0.1);
      box-shadow: 0 0 6px rgba(255,255,255,0.08);
      transition: 0.3s ease;
    }

    .done {
      background: #9b6cff;
      box-shadow: 0 0 12px #b183ff;
    }

    .miss {
      background: #4b1d38;
      box-shadow: 0 0 8px #8b2e65;
    }

    /* Aura flotante mágica */
    .aura {
      position: absolute;
      width: 300px;
      height: 300px;
      top: -80px;
      left: 50%;
      transform: translateX(-50%);
      background: radial-gradient(circle, rgba(150,100,255,0.25), transparent 70%);
      filter: blur(40px);
      opacity: 0.7;
      animation: pulse 4s infinite ease-in-out;
      pointer-events: none;
    }

    @keyframes pulse {
      0% { transform: translateX(-50%) scale(1); opacity: 0.6; }
      50% { transform: translateX(-50%) scale(1.15); opacity: 0.9; }
      100% { transform: translateX(-50%) scale(1); opacity: 0.6; }
    }
  </style>
</head>

<body>

  <div class="aura"></div>

  <h2>✨ Racha Arcana</h2>
  <div id="days">0</div>

  <button onclick="markToday()">Activar ritual del día</button>

  <div class="calendar" id="calendar"></div>

  <script>
    function todayStr() {
      return new Date().toISOString().split("T")[0];
    }

    // Cargar datos
    let streak = parseInt(localStorage.getItem("streak") || "0");
    let dates = JSON.parse(localStorage.getItem("dates") || "[]");

    function render() {
      document.getElementById("days").innerText = streak;

      let cal = document.getElementById("calendar");
      cal.innerHTML = "";

      for (let i = 13; i >= 0; i--) {
        let d = new Date();
        d.setDate(d.getDate() - i);
        let ds = d.toISOString().split("T")[0];

        let div = document.createElement("div");
        div.classList.add("day");

        if (dates.includes(ds)) div.classList.add("done");
        else if (d < new Date()) div.classList.add("miss");

        cal.appendChild(div);
      }
    }

    function markToday() {
      let t = todayStr();

      if (dates.includes(t)) {
        alert("Hoy ya activaste tu ritual.");
        return;
      }

      streak += 1;
      dates.push(t);

      localStorage.setItem("streak", streak);
      localStorage.setItem("dates", JSON.stringify(dates));

      render();
    }

    render();
  </script>

</body>
</html>
