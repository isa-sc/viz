
<body>
    <div id="stickman-con">
        
        <svg width={widthx} height= {heighty}>
            <image class="crown" href="crown.png" x= {crownstartx} y = {crownstarty} 
                width ={crownsize} height={crownsize}/>
            <image class= "backpack" href="backpack.png" x="{backpackx}" y="{backpacky}" 
                width="{backpacksize}" height={backpacksize}/>
            <image class= "potion" href="potion.png" x={potionx} y={potiony} 
                width={potionsize} height={potionsize}/>
            <circle cx="{startx}" cy="{headcenter}" r="{headsize}"/>
            <path d="M {startx},{starty} l -10,10 l 10, -10 l 10, 10"/>
            <path d="M {startx},{starty} l 0,-{stickheight}" />
            <path d="M {startx}, {armheight} l -15, 10 l 15, -10 l 15, 10"/>
            
        </svg>
        <p>{firstname} {lastname}</p>
 </div>
</body>

<script>
    export let scaledOrders;
    export let scaledMoney;
    export let scaledLux;
    export let scaledAdv;
    export let scaledCom;
    export let firstname;
    export let lastname;
    let widthx = 100;
    let heighty = (scaledMoney + scaledOrders < 0.25) ? 190 * 0.22 : 190;
    let stickheight = scaledOrders * 100;
    let headsize = scaledMoney * 20
    let crownsize = scaledLux * 40;
    let backpacksize = scaledAdv * 40;
    let potionsize = scaledCom * 40;
    let startx = widthx / 2
    let starty = heighty - 10
    let armheight = starty - (stickheight * 2) / 3
    let headcenter = starty - stickheight - headsize
    let crownstarty = headcenter - headsize - crownsize * 0.85
    let crownstartx = startx - (crownsize * 0.5)
    let backpackx = startx - 10 - backpacksize
    let backpacky = armheight + 10
    let potionx = startx + 10 - (potionsize / 8)
    let potiony = armheight + 10 
</script>

   
<style> 
    circle , path{
        fill: none;
        stroke: black;
    }
    
</style>
