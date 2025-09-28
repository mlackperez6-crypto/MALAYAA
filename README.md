# MALAYAA
PATA MALAYA MIKOA YOTE TZ
<!DOCTYPE html>
<html lang="sw">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>Mikoa ya Tanzania - Wilaya na Vijiji</title>
  <style>
    body {
      font-family: Arial, sans-serif;
      margin: 0;
      padding: 0;
      background-color: #f4f4f9;
    }
    header {
      background-color: #1e3d58;
      color: white;
      padding: 20px;
      text-align: center;
    }
    .region, .district, .village {
      margin: 10px;
      padding: 8px;
      background-color: #ffffff;
      border: 1px solid #ddd;
      border-radius: 5px;
      cursor: pointer;
      transition: background-color 0.3s;
    }
    .region:hover, .district:hover, .village:hover {
      background-color: #e0e0e0;
    }
    .districts, .villages {
      margin-left: 20px;
      display: none;
    }
    .message {
      display: none;
      margin: 20px;
      padding: 10px;
      background-color: #ffeb3b;
      border: 1px solid #fbc02d;
      border-radius: 5px;
      color: #f57c00;
    }
  </style>
</head>
<body>

<header>
  <h1>Mikoa ya Tanzania</h1>
  <p>Bonyeza mkoa, wilaya, au kijiji kwa maelezo zaidi</p>
</header>

<div id="regionsContainer"></div>

<div id="message" class="message">
  KAMA UNAHITAJI AGENT WA HAPAA NIPIGIE KWENYE NAMBA 0656104150
</div>

<script>
  const data = {
    "Pwani": {
      "Kibaha": ["Kibaha Kati", "Kibaha Vijijini"],
      "Chalinze": ["Chalinze Kati", "Chalinze Vijijini"]
    },
    "Dar es Salaam": {
      "Ilala": ["Gerezani", "Upanga"],
      "Kinondoni": ["Msasani", "Magomeni"]
    },
    // Ongeza mikoa mingine hapa kwa muundo huu
  };

  const regionsContainer = document.getElementById('regionsContainer');
  const message = document.getElementById('message');

  function createRegionElement(regionName) {
    const regionElement = document.createElement('div');
    regionElement.classList.add('region');
    regionElement.textContent = regionName;
    regionElement.addEventListener('click', () => toggleDistricts(regionName));
    return regionElement;
  }

  function createDistrictElement(regionName, districtName) {
    const districtElement = document.createElement('div');
    districtElement.classList.add('district');
    districtElement.textContent = districtName;
    districtElement.addEventListener('click', (event) => {
      event.stopPropagation();
      toggleVillages(regionName, districtName);
    });
    return districtElement;
  }

  function createVillageElement(regionName, districtName, villageName) {
    const villageElement = document.createElement('div');
    villageElement.classList.add('village');
    villageElement.textContent = villageName;
    villageElement.addEventListener('click', (event) => {
      event.stopPropagation();
      showMessage();
    });
    return villageElement;
  }

  function toggleDistricts(regionName) {
    const regionElement = document.getElementById(regionName);
    const districtsContainer = regionElement.querySelector('.districts');
    if (districtsContainer) {
      districtsContainer.style.display = districtsContainer.style.display === 'none' ? 'block' : 'none';
    }
  }

  function toggleVillages(regionName, districtName) {
    const regionElement = document.getElementById(regionName);
    const districtElement = regionElement.querySelector(`#${districtName}`);
    const villagesContainer = districtElement.querySelector('.villages');
    if (villagesContainer) {
      villagesContainer.style.display = villagesContainer.style.display === 'none' ? 'block' : 'none';
    }
  }

  function showMessage() {
    message.style.display = 'block';
    setTimeout(() => {
      message.style.display = 'none';
    }, 5000);
  }

  function buildRegions() {
    for (const regionName in data) {
      const regionElement = createRegionElement(regionName);
      regionElement.id = regionName;
      const districtsContainer = document.createElement('div');
      districtsContainer.classList.add('districts');
      for (const districtName in data[regionName]) {
        const districtElement = createDistrictElement(regionName, districtName);
        districtElement.id = districtName;
        const villagesContainer = document.createElement('div');
        villagesContainer.classList.add('villages');
        data[regionName][districtName].forEach(villageName => {
          const villageElement = createVillageElement(regionName, districtName, villageName);
          villagesContainer.appendChild(villageElement);
        });
        districtElement.appendChild(villagesContainer);
        districtsContainer.appendChild(districtElement);
      }
      regionElement.appendChild(districtsContainer);
      regionsContainer.appendChild(regionElement);
    }
  }

  buildRegions();
</script>

</body>
</html>
<!DOCTYPE html>
<html lang="sw">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>Delivery TZ - Dar es Salaam</title>
<style>
body {font-family:sans-serif; max-width:900px; margin:20px auto; padding:0 16px; background:#f9f9f9;}
h1{color:#1e3d58;}
ul {list-style:none; padding:0;}
li {padding:6px 10px; border-bottom:1px solid #ddd; cursor:pointer;}
li:hover {background:#e0e0e0;}
.intro {margin:10px 0; padding:10px; background:#f0f0f0; border-radius:8px; font-weight:bold;}
.popup {display:none; position:fixed; top:50%; left:50%; transform:translate(-50%,-50%); background:#fffae6; padding:20px; border:2px solid #f5c518; border-radius:10px; z-index:1000;}
.popup button {margin-top:10px; padding:5px 10px;}
</style>
</head>
<body>

<h1>Delivery Tanzania - Dar es Salaam</h1>
<p>Bonyeza mkoa kuendelea:</p>

<ul id="regionList">
  <li id="dar">Dar es Salaam</li>
</ul>

<div id="popup" class="popup">
  <div id="popupText"></div>
  <button onclick="closePopup()">Funga</button>
</div>

<script>
// Data
const data = {
  "Dar es Salaam": {
    "Ilala": ["Buguruni","Chanika","Gerezani","Gongo la Mboto","Ilala","Jangwani","Kariakoo","Kimanga","Kinyerezi","Kipawa","Kisutu","Kitunda","Kivukoni","Kivule","Kiwalani","Majohe","Mchafukoge","Mchikichini","Msongola","Pugu","Segerea","Tabata","Ukonga","Upanga Magharibi","Upanga Mashariki","Vingunguti"],
    "Kinondoni": ["Bunju","Hananasif","Kawe","Kigogo","Kijitonyama","Kinondoni","Kunduchi","Mabwepande","Magomeni","Makongo","Makumbusho","Mbezi Juu","Mbweni","Mikocheni","Msasani","Mwananyamala","Mzimuni","Ndugumbi","Tandale","Wazo"],
    "Temeke": ["Azimio","Buza","Chamazi","Chang'ombe","Charambe","Keko","Kibondemaji","Kiburugwa","Kijichi","Kilakala","Kilungule","Kurasini","Makangarawe","Mbagala","Mbagala Kuu","Mianzini","Miburani","Mtoni","Sandali","Tandika","Temeke","Toangoma","Yombo Vituka"],
    "Ubungo": ["Goba","Kibamba","Kimara","Kwembe","Mabibo","Makuburi","Makurumla","Manzese","Mbezi","Mburahati","Msigani","Saranga","Sinza","Ubungo"],
    "Kigamboni": ["Kibada","Kigamboni","Kimbiji","Kisarawe II","Mjimwema","Pembamnazi","Somangila","Tungi","Vijibweni"]
  }
};

const regionList = document.getElementById('regionList');
const popup = document.getElementById('popup');
const popupText = document.getElementById('popupText');

function clearOld(){
  const oldIntro = document.querySelectorAll('.intro');
  oldIntro.forEach(e=>e.remove());
  const oldWilaya = document.querySelectorAll('.wilayaList');
  oldWilaya.forEach(e=>e.remove());
  const oldKata = document.querySelectorAll('.kataList');
  oldKata.forEach(e=>e.remove());
}

// Show Wilaya
document.getElementById('dar').addEventListener('click',()=>{
  clearOld();
  const intro = document.createElement('div');
  intro.className = 'intro';
  intro.textContent = "JE UNAHITAJI WAKALA WETU WA WILAYA GANI KATIKA MKOA HUU WA DAR ES SALAAM?";
  regionList.appendChild(intro);

  const wList = document.createElement('ul');
  wList.className = 'wilayaList';
  Object.keys(data["Dar es Salaam"]).forEach(w=>{
    const li = document.createElement('li');
    li.textContent = w;
    li.addEventListener('click', e=>{
      e.stopPropagation();
      showKata("Dar es Salaam", w);
    });
    wList.appendChild(li);
  });
  regionList.appendChild(wList);
});

// Show Kata
function showKata(region, wilaya){
  clearOld();
  const intro = document.createElement('div');
  intro.className = 'intro';
  intro.textContent = `Kata zote za Wilaya ya ${wilaya} 🏙️`;
  regionList.appendChild(intro);

  const kList = document.createElement('ul');
  kList.className = 'kataList';
  data[region][wilaya].forEach(k=>{
    const li = document.createElement('li');
    li.textContent = k;
    li.addEventListener('click',()=>showPopup(k));
    kList.appendChild(li);
  });
  regionList.appendChild(kList);
}

// Popup
function showPopup(kata){
  popupText.textContent = `Kama unahitaji agent wa hapa lipia kwa namba hizi TIGOPESA 0652683080 JINA ASHURA (Kata: ${kata})`;
  popup.style.display='block';
}
function closePopup(){ popup.style.display='none'; }

</script>
</body>
</html>
