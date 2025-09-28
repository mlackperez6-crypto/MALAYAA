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
