<script>
    import { onMount, onDestroy } from 'svelte';
  
    let year = 2019; // Default year
    let showMostPopular = false; // Toggle for showing most popular product images
    let showLeastPopular = false; // Toggle for showing least popular product images
    let showDeliveryTimes = false; // Toggle for showing delivery times

    
    // Define delivery colors for regions
    const deliveryColors = {
      "Western Empire": "white",
      "United Moonshae Empire": "lightgreen",
      "None Empire": "darkblue",
      "Waterdhavian Empire": "lightgrey",
      "Dwarven Empire": "darkgreen",
      "Purple Dragon Empire": "purple",
      "Amnian Empire": "lightsalmon",
      "Calim Empire": "pink",
      "Halruaan Empire": "lightblue",
      "Bloodlands Empire": "brown",
      "Thayan Empire": "red",
      "Old Empire": "yellow",
      "Southern Empire": "lightskyblue",
      "Eastern Empire": "darkred",
      "New Neverwinter Empire": "lightcoral"
    };
  
    // Delivery times data for each region and year
    const deliveryTimes = {
      "Western Empire": {
        2019: 6.96449904968775,
        2020: 7.13362770160353,
        2021: 24.4720855196689,
        2022: 6.97607263327133,
        2023: 7.02663026019916
      },
      "United Moonshae Empire": {
      2019: 6.94136249835288,
      2020: 7.08744229611293,
      2021: 23.8503172588832,
      2022: 7.02887170814206,
      2023: 7.10324280248385
    },
    "None Empire": {
      2019: 6.91329639889197,
      2020: 7.19482014388489,
      2021: 25.5950883498053,
      2022: 7.0171461784365,
      2023: 6.94921985815603
    },
    "Waterdhavian Empire": {
      2019: 7.15853137896684,
      2020: 7.02346385100455,
      2021: 24.557157569516,
      2022: 7.04897494305239,
      2023: 6.96975142258161
    },
    "Dwarven Empire": {
      2019: 7.05152671755725,
      2020: 7.00484148055599,
      2021: 22.16862607475,
      2022: 7.00916921367046,
      2023: 7.06394557823129
    },
    "Purple Dragon Empire": {
      2019: 6.97466208032557,
      2020: 7.04276432894268,
      2021: 25.0990963326899,
      2022: 7.08327433628319,
      2023: 6.94572258208622
    },
    "Amnian Empire": {
      2019: 6.96449904968775,
      2020: 7.13362770160353,
      2021: 24.4720855196689,
      2022: 6.97607263327133,
      2023: 7.02663026019916
    },
    "Calim Empire": {
      2019: 7.04501346339481,
      2020: 7.02821229050279,
      2021: 24.4040712954556,
      2022: 6.99845886154611,
      2023: 7.09593604263824
    },
    "Halruaan Empire": {
      2019: 7.01675257731959,
      2020: 6.98810200985969,
      2021: 25.0441505216095,
      2022: 6.99583851525878,
      2023: 7.04268758596098
    },
    "Bloodlands Empire": {
      2019: 7.05620087639981,
      2020: 6.95808023496429,
      2021: 23.2490584807788,
      2022: 6.9447666195191,
      2023: 7.05151774262505
    },
    "Thayan Empire": {
      2019: 7.09419402905646,
      2020: 6.87296322999279,
      2021: 24.693011360842,
      2022: 7.01091049531718,
      2023: 7.06494845360825
    },
    "Old Empire": {
      2019: 7.01962410171365,
      2020: 7.12823974082073,
      2021: 21.9789007554051,
      2022: 7.04047976011994,
      2023: 6.93429981492906
    },
    "Southern Empire": {
      2019: 7.14272970561998,
      2020: 6.75238095238095,
      2021: 30.0246406570842,
      2022: 7.16346153846154,
      2023: 6.76830318690784
    },
    "Eastern Empire": {
      2019: 6.90087764584409,
      2020: 7.05185865075723,
      2021: 21.4747039827772,
      2022: 6.74231557377049,
      2023: 7.05935162094763
    },
    "New Neverwinter Empire": {
      2019: 7.0279771765139,
      2020: 6.9127051260362,
      2021: 23.8945007476325,
      2022: 7.16970003370408,
      2023: 7.1070599933709
    },
  };
  
    // Popular and least popular products data for each region and year
    const popularProducts = {
      "Western Empire": {
        mostPopularProducts: {
          2019: ["magic_utility", "martial_melee_weapon", "tools"],
          2020: ["magic_utility", "tools", "martial_melee_weapon"],
          2021: ["magic_utility", "martial_melee_weapon", "tools"],
          2022: ["magic_utility", "martial_melee_weapon", "tools"],
          2023: ["magic_utility", "tools", "martial_melee_weapon"]
        },
        leastPopularProducts: {
          2019: ["vehicle", "bracers", "percussion_instrument"],
          2020: ["vehicle", "percussion_instrument", "weapon_other"],
          2021: ["vehicle", "percussion_instrument", "belt_girdle"],
          2022: ["vehicle", "belt_girdle", "percussion_instrument"],
          2023: ["vehicle", "percussion_instrument", "gauntlets_gloves"]
        }
      },
      "Amnian Empire": {
        mostPopularProducts: {
          2019: ["magic_utility", "martial_melee_weapon", "tools"],
          2020: ["magic_utility", "martial_melee_weapon", "tools"],
          2021: ["magic_utility", "martial_melee_weapon", "simple_melee_weapon"],
          2022: ["martial_melee_weapon", "magic_utility", "simple_melee_weapon"],
          2023: ["magic_utility", "martial_melee_weapon", "tools"]
        },
        leastPopularProducts: {
          2019: ["vehicle", "percussion_instrument", "bracers"],
          2020: ["vehicle", "percussion_instrument", "bracers"],
          2021: ["vehicle", "percussion_instrument", "bracers"],
          2022: ["vehicle", "percussion_instrument", "boots"],
          2023: ["vehicle", "percussion_instrument", "weapon_other"]
        }
      },
      "Bloodlands Empire": {
        mostPopularProducts: {
          2019: ["martial_melee_weapon", "magic_utility", "simple_melee_weapon"],
          2020: ["martial_melee_weapon", "magic_utility", "simple_melee_weapon"],
          2021: ["martial_melee_weapon", "magic_utility", "simple_melee_weapon"],
          2022: ["martial_melee_weapon", "magic_utility", "simple_melee_weapon"],
          2023: ["magic_utility", "martial_melee_weapon", "simple_melee_weapon"]
        },
        leastPopularProducts: {
          2019: ["vehicle", "percussion_instrument", "bracers"],
          2020: ["vehicle", "percussion_instrument", "bracers"],
          2021: ["vehicle", "percussion_instrument", "brass_instrument"],
          2022: ["vehicle", "percussion_instrument", "bracers"],
          2023: ["vehicle", "bracers", "percussion_instrument"]
        }
      },
      "Calim Empire": {
        mostPopularProducts: {
          2019: ["magic_utility", "martial_melee_weapon", "tools"],
          2020: ["martial_melee_weapon", "magic_utility", "tools"],
          2021: ["magic_utility", "martial_melee_weapon", "tools"],
          2022: ["magic_utility", "martial_melee_weapon", "tools"],
          2023: ["magic_utility", "martial_melee_weapon", "tools"]
        },
        leastPopularProducts: {
          2019: ["vehicle", "percussion_instrument", "bracers"],
          2020: ["vehicle", "percussion_instrument", "belt_girdle"],
          2021: ["vehicle", "percussion_instrument", "bracers"],
          2022: ["vehicle", "percussion_instrument", "bracers"],
          2023: ["vehicle", "percussion_instrument", "bracers"]
        }
      },
      "Dwarven Empire": {
        mostPopularProducts: {
          2019: ["magic_utility", "martial_melee_weapon", "tools"],
          2020: ["magic_utility", "martial_melee_weapon", "tools"],
          2021: ["magic_utility", "tools", "light_armour"],
          2022: ["martial_melee_weapon", "wand", "magic_utility"],
          2023: ["martial_melee_weapon", "heavy_armour", "simple_melee_weapon"]
        },
        leastPopularProducts: {
          2019: ["vehicle", "percussion_instrument", "weapon_other"],
          2020: ["vehicle", "percussion_instrument", "bracers"],
          2021: ["vehicle", "weapon_other", "percussion_instrument"],
          2022: ["vehicle", "percussion_instrument", "bracers"],
          2023: ["vehicle", "percussion_instrument", "bracers"]
        }
      },
      "Eastern Empire": {
        mostPopularProducts: {
          2019: ["magic_utility", "tools", "martial_melee_weapon"],
          2020: ["magic_utility", "martial_melee_weapon", "scroll"],
          2021: ["magic_utility", "martial_melee_weapon", "tools"],
          2022: ["magic_utility", "martial_melee_weapon", "tools"],
          2023: ["magic_utility", "tools", "martial_melee_weapon"]
        },
        leastPopularProducts: {
          2019: ["vehicle", "belt_girdle", "boots"],
          2020: ["vehicle", "percussion_instrument", "wind_instrument"],
          2021: ["percussion_instrument", "vehicle", "weapon_other"],
          2022: ["vehicle", "belt_girdle", "gaming_set"],
          2023: ["vehicle", "percussion_instrument", "bracers"]
        }
      },
      "Halruaan Empire": {
        mostPopularProducts: {
          2019: ["magic_utility", "martial_melee_weapon", "tools"],
          2020: ["martial_melee_weapon", "magic_utility", "simple_melee_weapon"],
          2021: ["martial_melee_weapon", "magic_utility", "simple_melee_weapon"],
          2022: ["magic_utility", "martial_melee_weapon", "simple_melee_weapon"],
          2023: ["magic_utility", "martial_melee_weapon", "tools"]
        },
        leastPopularProducts: {
          2019: ["vehicle", "percussion_instrument", "bracers"],
          2020: ["vehicle", "percussion_instrument", "bracers"],
          2021: ["vehicle", "percussion_instrument", "bracers"],
          2022: ["vehicle", "percussion_instrument", "bracers"],
          2023: ["vehicle", "percussion_instrument", "bracers"]
        }
      },
      "New Neverwinter Empire": {
        mostPopularProducts: {
          2019: ["magic_utility", "martial_melee_weapon", "tools"],
          2020: ["magic_utility", "tools", "potions_alchemy"],
          2021: ["magic_utility", "martial_melee_weapon", "simple_melee_weapon"],
          2022: ["magic_utility", "martial_melee_weapon", "simple_melee_weapon"],
          2023: ["magic_utility", "martial_melee_weapon", "tools"]
        },
        leastPopularProducts: {
          2019: ["vehicle", "percussion_instrument", "gauntlets_gloves"],
          2020: ["vehicle", "bracers", "boots"],
          2021: ["vehicle", "bracers", "gauntlets_gloves"],
          2022: ["vehicle", "percussion_instrument", "weapon_other"],
          2023: ["vehicle", "percussion_instrument", "boots"]
        }
      },
      "None Empire": {
        mostPopularProducts: {
          2019: ["magic_utility", "simple_melee_weapon", "martial_melee_weapon"],
          2020: ["magic_utility", "martial_melee_weapon", "simple_melee_weapon"],
          2021: ["magic_utility", "martial_melee_weapon", "simple_melee_weapon"],
          2022: ["magic_utility", "tools", "martial_melee_weapon"],
          2023: ["magic_utility", "martial_melee_weapon", "scroll"]
        },
        leastPopularProducts: {
          2019: ["vehicle", "percussion_instrument", "bracers"],
          2020: ["vehicle", "percussion_instrument", "weapon_other"],
          2021: ["vehicle", "percussion_instrument", "bracers"],
          2022: ["vehicle", "weapon_other", "bracers"],
          2023: ["vehicle", "weapon_other", "percussion_instrument"]
        }
      },
      "Old Empire": {
        mostPopularProducts: {
          2019: ["magic_utility", "tools", "martial_melee_weapon"],
          2020: ["magic_utility", "tools", "simple_melee_weapon"],
          2021: ["magic_utility", "simple_melee_weapon", "martial_melee_weapon"],
          2022: ["magic_utility", "martial_melee_weapon", "scroll"],
          2023: ["martial_melee_weapon", "heavy_armour", "magic_utility"]
        },
        leastPopularProducts: {
          2019: ["vehicle", "percussion_instrument", "bracers"],
          2020: ["vehicle", "percussion_instrument", "bracers"],
          2021: ["vehicle", "percussion_instrument", "boots"],
          2022: ["percussion_instrument", "belt_girdle", "livestock"],
          2023: ["vehicle", "bracers", "boots"]
        }
      },
      "Purple Dragon Empire": {
        mostPopularProducts: {
          2019: ["martial_melee_weapon", "magic_utility", "simple_melee_weapon"],
          2020: ["martial_melee_weapon", "simple_melee_weapon", "magic_utility"],
          2021: ["martial_melee_weapon", "simple_melee_weapon", "magic_utility"],
          2022: ["martial_melee_weapon", "simple_melee_weapon", "magic_utility"],
          2023: ["martial_melee_weapon", "magic_utility", "simple_melee_weapon"]
        },
        leastPopularProducts: {
          2019: ["vehicle", "bracers", "percussion_instrument"],
          2020: ["vehicle", "percussion_instrument", "brass_instrument"],
          2021: ["vehicle", "percussion_instrument", "bracers"],
          2022: ["vehicle", "percussion_instrument", "bracers"],
          2023: ["vehicle", "percussion_instrument", "bracers"]
        }
      },
      "Southern Empire": {
        mostPopularProducts: {
          2019: ["magic_utility", "tools", "potions_alchemy"],
          2020: ["magic_utility", "tools", "martial_melee_weapon"],
          2021: ["magic_utility", "martial_melee_weapon", "potions_alchemy"],
          2022: ["magic_utility", "martial_melee_weapon", "scroll"],
          2023: ["magic_utility", "tools", "martial_melee_weapon"]
        },
        leastPopularProducts: {
          2019: ["percussion_instrument", "vehicle", "bracers"],
          2020: ["brass_instrument", "boots", "belt_girdle"],
          2021: ["percussion_instrument", "boots", "vehicle"],
          2022: ["vehicle", "bracers", "percussion_instrument"],
          2023: ["vehicle", "belt_girdle", "ammunition"]
        }
      },
      "Thayan Empire": {
        mostPopularProducts: {
          2019: ["magic_utility", "martial_melee_weapon", "tools"],
          2020: ["martial_melee_weapon", "magic_utility", "simple_melee_weapon"],
          2021: ["martial_melee_weapon", "magic_utility", "simple_melee_weapon"],
          2022: ["martial_melee_weapon", "magic_utility", "simple_melee_weapon"],
          2023: ["magic_utility", "martial_melee_weapon", "tools"]
        },
        leastPopularProducts: {
          2019: ["vehicle", "bracers", "percussion_instrument"],
          2020: ["vehicle", "percussion_instrument", "boots"],
          2021: ["vehicle", "percussion_instrument", "boots"],
          2022: ["vehicle", "percussion_instrument", "bracers"],
          2023: ["vehicle", "percussion_instrument", "bracers"]
        }
      },
      "United Moonshae Empire": {
        mostPopularProducts: {
          2019: ["magic_utility", "tools", "martial_melee_weapon"],
          2020: ["magic_utility", "tools", "martial_melee_weapon"],
          2021: ["magic_utility", "martial_melee_weapon", "tools"],
          2022: ["magic_utility", "martial_melee_weapon", "tools"],
          2023: ["martial_melee_weapon", "magic_utility", "tools"]
        },
        leastPopularProducts: {
          2019: ["vehicle", "weapon_other", "percussion_instrument"],
          2020: ["vehicle", "percussion_instrument", "bracers"],
          2021: ["vehicle", "percussion_instrument", "bracers"],
          2022: ["vehicle", "weapon_other", "bracers"],
          2023: ["vehicle", "percussion_instrument", "weapon_other"]
        }
      },
      "Waterdhavian Empire": {
        mostPopularProducts: {
          2019: ["magic_utility", "tools", "martial_melee_weapon"],
          2020: ["magic_utility", "tools", "martial_melee_weapon"],
          2021: ["magic_utility", "martial_melee_weapon", "tools"],
          2022: ["magic_utility", "tools", "martial_melee_weapon"],
          2023: ["magic_utility", "martial_melee_weapon", "tools"]
        },
        leastPopularProducts: {
          2019: ["vehicle", "percussion_instrument", "bracers"],
          2020: ["vehicle", "percussion_instrument", "bracers"],
          2021: ["vehicle", "percussion_instrument", "weapon_other"],
          2022: ["vehicle", "percussion_instrument", "bracers"],
          2023: ["vehicle", "percussion_instrument", "bracers"]
        }
      },
    };
  
    // Mapping of product names to image file paths
    const productImageMap = {
        "magic_utility": "magic_utility.png",
      "martial_melee_weapon": "martial_melee_weapon.png",
      "tools": "tools.png",
      "vehicle": "vehicle.png",
      "belt_girdle": "belt_girdle.png",
      "bracers": "bracers.png",
      "gauntlets_gloves": "gauntlets_gloves.png",
      "weapon_other": "weapon_other.png",
      "percussion_instrument": "percussion_instrument.png",
      "ammunition": "ammunition.png",
      "boots": "boots.png",
      "brass_instrument": "brass_instrument.png",
      "livestock": "livestock.png",
      "potions_alchemy": "potions_alchemy.png",
      "scroll": "scroll.png",
      "simple_melee_weapon": "simple_melee_weapon.png",
      "wand": "wand.png", 
      "light_armour": "light_armour.png",
      "heavy_armour": "heavy_armour.png",
      "wind_instrument": "wind_instrument.png",
      "gaming_set": "gaming_set.png",
    };
  
    let timeoutId;
  
    onMount(() => {
      calculateTextCoordinates();
      calculateImageCoordinates();
      updateTextContent();
      updateImages();
    });
  
    onDestroy(() => {
      clearTimeout(timeoutId);
    });
  
    const calculateTextCoordinates = () => {
        Object.keys(deliveryColors).forEach(region => {
            const fillColor = deliveryColors[region];
            const path = document.querySelector(`path[fill="${fillColor}"]`);
            if (path) {
                const centroid = calculatePathCentroid(path);
                let textX = centroid.x;
                let textY = centroid.y;

                const textElement = document.createElementNS("http://www.w3.org/2000/svg", "text");
                textElement.setAttribute("class", "region-label");
                textElement.setAttribute("id", `text-${region}`);
                textElement.setAttribute("x", textX);
                textElement.setAttribute("y", textY);
                textElement.textContent = deliveryTimes[region][year].toFixed(2) + " days";

                const svg = document.querySelector('svg');
                svg.appendChild(textElement);

                // Conditionally hide or show the text element
                textElement.style.display = showDeliveryTimes ? 'block' : 'none';
            } else {
                console.warn(`Path not found for fill color: ${fillColor}`);
            }
        });
    };
  
    const calculatePathCentroid = (path) => {
      const length = path.getTotalLength();
      let x = 0, y = 0, n = 0;
      const numPoints = 100; 
      for (let i = 0; i < numPoints; i++) {
        const point = path.getPointAtLength((i / numPoints) * length);
        x += point.x;
        y += point.y;
        n++;
      }
      return { x: x / n, y: y / n };
    };
  
    const calculateImageCoordinates = () => {
      Object.keys(deliveryColors).forEach(region => {
        const fillColor = deliveryColors[region];
        const path = document.querySelector(`path[fill="${fillColor}"]`);
        if (path) {
          const bbox = path.getBBox();
          const centerX = bbox.x + bbox.width / 2;
          const centerY = bbox.y + bbox.height / 2;
  
          const container = document.createElementNS("http://www.w3.org/2000/svg", "g");
          container.setAttribute("id", `images-${region}`);
          container.setAttribute("transform", `translate(${centerX}, ${centerY})`);
  
          const svg = document.querySelector('svg');
          svg.appendChild(container);
        } else {
          console.warn(`Path not found for fill color: ${fillColor}`);
        }
      });
    };
  
    const updateTextContent = () => {
    Object.keys(deliveryColors).forEach(region => {
        const textElement = document.getElementById(`text-${region}`);
        if (textElement && deliveryTimes[region] && deliveryTimes[region][year]) {
            textElement.textContent = deliveryTimes[region][year].toFixed(2) + " days";
            // Set the display property based on the showDeliveryTimes variable
            textElement.style.display = showDeliveryTimes ? 'block' : 'none';
        }
    });
};

    function toggleDeliveryTimes(event) {
        showDeliveryTimes = event.target.checked;
        updateTextContent();
    }
  
    const updateImages = () => {
      Object.keys(deliveryColors).forEach(region => {
        const imageContainer = document.getElementById(`images-${region}`);
        if (imageContainer) {
          imageContainer.innerHTML = ''; // Clear previous images
          let products = [];
          if (showMostPopular) {
            products = products.concat(popularProducts[region]?.mostPopularProducts[year] || []);
          }
          if (showLeastPopular) {
            products = products.concat(popularProducts[region]?.leastPopularProducts[year] || []);
          }
          products.forEach((productName, index) => {
            const imgSrc = productImageMap[productName];
            if (imgSrc) {
              const img = document.createElementNS("http://www.w3.org/2000/svg", "image");
              img.setAttributeNS("http://www.w3.org/1999/xlink", "href", imgSrc);
              img.setAttribute("width", "50");
              img.setAttribute("height", "50");
  
              const path = document.querySelector(`path[fill="${deliveryColors[region]}"]`);
              if (path) {
                const bbox = path.getBBox();
                let centerX = bbox.x + bbox.width / 2;
                let centerY = bbox.y + bbox.height / 2;

                // Special adjustments for Amnian Empire and Southern Empire
                if (region === "Amnian Empire") {
                    centerX += 20; // Adjust this value as needed
                    centerY -= 80; // Adjust this value as needed
                } else if (region === "Halruaan Empire") {
                    centerX -= 40; // Adjust this value as needed
                    centerY += 60; // Adjust this value as needed
                }
  
                img.setAttribute("transform", `translate(${centerX - 25 + index * 55 - (products.length - 1) * 55 / 2}, ${centerY - 25})`);
              }
              imageContainer.appendChild(img);
            } else {
              console.warn(`Image not found for product
              productName}`);
          }
        });
      }
    });
  };

  // Event handler for slider input
  function handleSliderInput(event) {
    year = parseInt(event.target.value, 10);
    updateTextContent();
    updateImages();
  }

  // Event handler for checkbox changes
  function handleCheckboxChange(event) {
    const { name, checked } = event.target;
    if (name === 'mostPopular') {
      showMostPopular = checked;
    } else if (name === 'leastPopular') {
      showLeastPopular = checked;
    }
    updateImages();
  }

</script>

<style>
  /* Add any custom styles here */
  text.region-label {
    font-size: 20px; /* Increase font size for better visibility */
    fill: black;
    text-anchor: middle; /* Center text horizontally */
    dominant-baseline: middle; /* Center text vertically */
  }
</style>

<div>
  <input type="checkbox" id="showMostPopularCheckbox" name="mostPopular" bind:checked={showMostPopular} on:change={handleCheckboxChange} />
  <label for="showMostPopularCheckbox">Show most popular products</label>

  <input type="checkbox" id="showLeastPopularCheckbox" name="leastPopular" bind:checked={showLeastPopular} on:change={handleCheckboxChange} />
  <label for="showLeastPopularCheckbox">Show least popular products</label>

  <label for="delivery-times">
    <input type="checkbox" id="delivery-times" bind:checked={showDeliveryTimes} on:change={toggleDeliveryTimes}>
    Show Delivery Times
</label>

  <svg width="800" height="600" viewBox="-250 300 1600 1">
    <!-- SVG paths for regions -->
    <!-- Western Empire -->
    <path id="region-western" d="M -85 51 L -147 176 L -238 114 L -220 18 Z" stroke="black" fill="white" />

    <!-- Region 2: United Moonshae Empire -->
    <path id="region-moonshae" d="M 2 259 L 62 185 L 70 63 L -19 6 L -86 153 L -101 231 L 2 259" stroke="black" fill="lightgreen" />

    <!-- Region 3: None Empire -->
    <path id="region-none" d="M 36 -167 L 59 -69 L 221 -69 L 218 -151 L 113 -211 L 36 -167" stroke="black" fill="darkblue" />
    
    <!-- Region 4: Waterdhavian Empire -->
    <path id="region-waterdhavian" d="M 108 155 L 116 90 L 193 39 L 216 75 L 188 143 L 108 155" stroke="black" fill="lightgrey" />
    
    <!-- Region 5: Dwarven Empire -->
    <path id="region-dwarven" d="M 198 -305 C 145 -257 139 -242 199 -197 C 339 -180 343 -168 529 -203 C 598 -214 580 -276 521 -304 Z" stroke="black" fill="darkgreen" />
    
    <!-- Region 6: Purple Dragon Empire -->
    <path id="region-purpledragon" d="M 269 -103 L 255 81 L 230 110 C 230 120 240 130 260 130 L 330 130 L 340 110 C 370 110 370 90 400 90 L 400 60 C 400 40 470 -20 380 -112 Z " stroke="black" fill="purple" />
    
    <!-- Region 7: Amnian Empire -->
    <path id="region-amnian" d="M 140 190 L 100 210 C 70 270 70 330 100 390 C 110 413.333 100 450 130 460 C 170 470 190 410 220 420 C 260 400 240 360 250 330 C 260 300 236.667 276.667 230 250 C 270 260 280 250 320 220 C 350 250 380 240 410 230 C 450 210 460 190 500 200 C 380 140 210 150 140 190 " stroke="black" fill="lightsalmon" />

    <!-- Region 8: Calim Empire -->
    <path id="region-calim" d="M 320 330 L 300 370 L 298 422 L 404 420 L 458 366 L 437 288 C 390 280 350 300 320 330 " stroke="black" fill="pink" />
    
    <!-- Region 9: Halruaan Empire -->
    <path id="region-halruaan" d="M 280 480 C 260 490 230 490 200 520 L 210 570 L 353 617 L 459 589 C 602 557 649 504 660 420 L 647 356 L 617 286 L 541 281 L 520 326 L 517 408 L 440 460 C 393.3333 473.3333 340 450 280 480 " stroke="black" fill="lightblue" />
    
    <!-- Region 10: Bloodlands Empire -->
    <path id="region-bloodlands" d="M 516 -29 L 469 47 L 509 115 L 624 45 L 691 -104 L 585 -169 L 470 -126 L 515 -29 " stroke="black" fill="brown" />
    
    <!-- Region 11: Thayan Empire -->
    <path id="region-thayan" d="M 634 104 L 600 150 L 600 210 L 690 220 L 760 200 L 780 150 L 789 69 L 686 -4 L 632 107" stroke="black" fill="red" />
    
    <!-- Region 12: Old Empire -->
    <path id="region-old" d="M 710 265 L 697 344 L 750 392 L 844 380 L 882 300 L 849 245 L 783 236 L 710 265" stroke="black" fill="yellow" />
    
    <!-- Region 13: Southern Empire -->
    <path id="region-southern" d="M 774 693 L 845 667 L 826 570 L 762 537 L 691 571 L 691 648 L 774 693" stroke="black" fill="lightskyblue" />
    
    <!-- Region 14: Eastern Empire -->
    <path id="region-eastern" d="M 953 338 L 906 404 L 875 488 L 944 521 L 1049 476 L 1042 371 Z" stroke="black" fill="darkred" />
    
    <!-- Region 15: New Neverwinter Empire -->
    <path id="region-neverwinter" d="M 92 -46 L 76 -4 L 102 62 L 231 -5 L 162 -48 L 92 -46" stroke="black" fill="lightcoral" />

    <!-- Example Image container within a region -->
    <g id="images-Western Empire"></g>
    <g id="images-Amnian Empire"></g>
    <g id="images-Bloodlands Empire"></g>
    <g id="images-Calim Empire"></g>
    <g id="images-Dwarven Empire"></g>
    <g id="images-Eastern Empire"></g>
    <g id="images-Halruaan Empire"></g>
    <g id="images-New Neverwinter Empire"></g>
    <g id="images-None Empire"></g>
    <g id="images-Old Empire"></g>
    <g id="images-Purple Dragon Empire"></g>
    <g id="images-Southern Empire"></g>
    <g id="images-Thayan Empire"></g>
    <g id="images-United Moonshae Empire"></g>
    <g id="images-Waterdhavian Empire"></g>
  
</svg>

  <input type="range" min="2019" max="2023" step="1" value={year} on:input={handleSliderInput}>
  <span>{year}</span> <!-- Display the selected year next to the slider -->
  
</div>







  
