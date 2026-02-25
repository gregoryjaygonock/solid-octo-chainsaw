<!doctype html>
<html lang="en">
<head>
  <meta charset="utf-8" />
  <meta name="viewport" content="width=device-width,initial-scale=1" />
  <title>Buckeye Display</title>
  <style>
    :root{
      --bg:#050505;
      --gold:#d6b35a;
      --gold2:#b88a2a;
      --white:#f3f3f3;
      --muted:#b9b9b9;
      --shadow: 0 10px 30px rgba(0,0,0,.65);
    }
    html,body{height:100%; margin:0; background:var(--bg); font-family: system-ui, -apple-system, Segoe UI, Roboto, Arial, sans-serif;}
    .wrap{
      height:100%;
      display:flex;
      align-items:stretch;
      justify-content:center;
      overflow:hidden;
      position:relative;
      background:
        radial-gradient(900px 500px at 50% 50%, rgba(214,179,90,.10), transparent 60%),
        radial-gradient(700px 450px at 60% 40%, rgba(255,60,0,.08), transparent 60%),
        linear-gradient(180deg, #050505, #000);
    }

    /* Logo image (your artwork) */
    .art{
      position:absolute;
      inset:0;
      display:flex;
      align-items:center;
      justify-content:center;
      padding:2.5%;
      pointer-events:none;
      opacity:.92;
      filter: drop-shadow(0 25px 45px rgba(0,0,0,.75));
    }
    .art img{
      max-height:92%;
      max-width:92%;
      object-fit:contain;
    }

    /* UI overlay */
    .hud{
      position:absolute;
      inset:0;
      display:flex;
      flex-direction:column;
      justify-content:space-between;
      padding:24px 26px;
      pointer-events:none;
    }

    .topbar{
      display:flex;
      align-items:flex-start;
      justify-content:space-between;
      gap:16px;
    }

    .brand{
      display:flex;
      flex-direction:column;
      gap:6px;
      background:rgba(0,0,0,.35);
      border:1px solid rgba(214,179,90,.25);
      padding:12px 14px;
      border-radius:14px;
      box-shadow: var(--shadow);
      backdrop-filter: blur(6px);
      max-width: 60%;
    }
    .brand .title{
      font-weight:800;
      letter-spacing:.10em;
      text-transform:uppercase;
      color:var(--gold);
      font-size:18px;
      line-height:1.1;
    }
    .brand .subtitle{
      color:var(--muted);
      font-size:13px;
      letter-spacing:.05em;
      text-transform:uppercase;
    }

    .status{
      display:flex;
      flex-direction:column;
      align-items:flex-end;
      gap:8px;
      min-width: 220px;
    }

    .pill{
      background:rgba(0,0,0,.35);
      border:1px solid rgba(214,179,90,.22);
      padding:10px 12px;
      border-radius:14px;
      box-shadow: var(--shadow);
      backdrop-filter: blur(6px);
      color:var(--white);
      width:100%;
    }
    .pill .label{
      color:var(--muted);
      font-size:12px;
      letter-spacing:.08em;
      text-transform:uppercase;
      margin-bottom:4px;
    }

    .clock{
      font-weight:800;
      font-size:56px;
      letter-spacing:.02em;
      color:var(--white);
      text-shadow: 0 8px 22px rgba(0,0,0,.7);
      line-height:1.0;
    }
    .date{
      color:rgba(214,179,90,.95);
      font-weight:700;
      letter-spacing:.08em;
      text-transform:uppercase;
      font-size:13px;
      margin-top:6px;
    }

    .weatherLine{
      display:flex;
      justify-content:space-between;
      gap:12px;
      color:var(--white);
      font-size:16px;
      font-weight:650;
    }
    .weatherSmall{
      color:var(--muted);
      font-size:12px;
      margin-top:6px;
      letter-spacing:.04em;
    }

    .bottombar{
      display:flex;
      align-items:flex-end;
      justify-content:space-between;
      gap:16px;
    }

    .footerLeft{
      background:rgba(0,0,0,.35);
      border:1px solid rgba(214,179,90,.20);
      padding:10px 12px;
      border-radius:14px;
      box-shadow: var(--shadow);
      backdrop-filter: blur(6px);
      color:rgba(214,179,90,.95);
      font-weight:700;
      letter-spacing:.08em;
      text-transform:uppercase;
      font-size:12px;
    }

    .ticker{
      flex:1;
      background:rgba(0,0,0,.35);
      border:1px solid rgba(214,179,90,.20);
      padding:10px 12px;
      border-radius:14px;
      box-shadow: var(--shadow);
      backdrop-filter: blur(6px);
      overflow:hidden;
      color:var(--white);
      font-weight:650;
      letter-spacing:.02em;
      white-space:nowrap;
    }
    .ticker span{
      display:inline-block;
      padding-left:100%;
      animation: scroll 18s linear infinite;
    }
    @keyframes scroll{
      0%{transform:translateX(0);}
      100%{transform:translateX(-100%);}
    }

    /* Make it Echo-friendly */
    @media (max-width: 900px){
      .clock{font-size:48px;}
      .status{min-width: 200px;}
      .brand{max-width: 65%;}
    }
  </style>
</head>
<body>
  <div class="wrap">
    <div class="art">
      <img id="logo" alt="Buckeye Entertainment" />
    </div>

    <div class="hud">
      <div class="topbar">
        <div class="brand">
          <div class="title">Buckeye Entertainment</div>
          <div class="subtitle">Porterville • Command Display</div>
        </div>

        <div class="status">
          <div class="pill">
            <div class="label">Time</div>
            <div class="clock" id="clock">--:--</div>
            <div class="date" id="date">---</div>
          </div>

          <div class="pill">
            <div class="label">Weather</div>
            <div class="weatherLine">
              <div id="wTemp">--°</div>
              <div id="wCond">Loading…</div>
            </div>
            <div class="weatherSmall" id="wMeta">Porterville, CA</div>
          </div>
        </div>
      </div>

      <div class="bottombar">
        <div class="footerLeft">BUCKEYE • EST. 1985</div>
        <div class="ticker">
          <span id="tickerText">COPPER • BRASS • ALUMINUM • STEEL • KEEP IT MOVING •</span>
        </div>
      </div>
    </div>
  </div>

  <script>
    // 1) PASTE YOUR DIRECT IMAGE URL HERE (must end in .jpg/.png/.webp)
    const LOGO_URL = "PASTE_YOUR_DIRECT_IMAGE_URL_HERE";

    // Optional: 12-hour or 24-hour clock
    const USE_24H = false;

    // Porterville weather via Open-Meteo (no key)
    const CITY_QUERY = "Porterville, CA";

    const logoEl = document.getElementById("logo");
    logoEl.src = LOGO_URL;

    function pad(n){ return String(n).padStart(2,"0"); }

    function updateClock(){
      const now = new Date();
      let h = now.getHours();
      let ampm = "";
      if(!USE_24H){
        ampm = h >= 12 ? "PM" : "AM";
        h = h % 12; if(h === 0) h = 12;
      }
      const m = now.getMinutes();
      const clock = `${pad(h)}:${pad(m)}${USE_24H ? "" : " " + ampm}`;
      document.getElementById("clock").textContent = clock;

      const opts = { weekday:"short", month:"short", day:"2-digit" };
      document.getElementById("date").textContent = now.toLocaleDateString(undefined, opts).toUpperCase();
    }

    const WCODE = {
      0:"Clear",
      1:"Mostly Clear", 2:"Partly Cloudy", 3:"Overcast",
      45:"Fog", 48:"Rime Fog",
      51:"Light Drizzle", 53:"Drizzle", 55:"Heavy Drizzle",
      56:"Freezing Drizzle", 57:"Freezing Drizzle",
      61:"Light Rain", 63:"Rain", 65:"Heavy Rain",
      66:"Freezing Rain", 67:"Freezing Rain",
      71:"Light Snow", 73:"Snow", 75:"Heavy Snow",
      77:"Snow Grains",
      80:"Light Showers", 81:"Showers", 82:"Heavy Showers",
      85:"Snow Showers", 86:"Snow Showers",
      95:"Thunderstorm", 96:"T-storm + Hail", 99:"T-storm + Hail"
    };

    async function loadWeather(){
      try{
        // Geocode city -> lat/lon
        const gUrl = `https://geocoding-api.open-meteo.com/v1/search?name=${encodeURIComponent(CITY_QUERY)}&count=1&language=en&format=json`;
        const gRes = await fetch(gUrl);
        const g = await gRes.json();
        if(!g.results || !g.results.length) throw new Error("No geocode results");

        const { latitude, longitude, name, admin1 } = g.results[0];
        document.getElementById("wMeta").textContent = `${name}${admin1 ? ", " + admin1 : ""}`;

        // Current weather
        const wUrl = `https://api.open-meteo.com/v1/forecast?latitude=${latitude}&longitude=${longitude}&current=temperature_2m,weather_code,wind_speed_10m&temperature_unit=fahrenheit&wind_speed_unit=mph`;
        const wRes = await fetch(wUrl);
        const w = await wRes.json();

        const t = Math.round(w.current.temperature_2m);
        const code = w.current.weather_code;
        const wind = Math.round(w.current.wind_speed_10m);

        document.getElementById("wTemp").textContent = `${t}°F`;
        document.getElementById("wCond").textContent = WCODE[code] || `Code ${code}`;
        document.getElementById("wMeta").textContent = `${name}, ${admin1} • Wind ${wind} mph`;
      }catch(e){
        document.getElementById("wCond").textContent = "Offline";
        document.getElementById("wMeta").textContent = "Porterville, CA";
      }
    }

    updateClock();
    setInterval(updateClock, 1000 * 10);
    loadWeather();
    setInterval(loadWeather, 1000 * 60 * 10);
  </script>
</body>
</html>

