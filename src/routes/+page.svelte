<script>
    import Stickman from '../components/Stickman.svelte';   
    let data = [
        {name: 'Balthazaar Viscari', orders:0.2, money: 0.0733, adv: 0.5, comission: 0.7, luxury: 0.3},
        {name: 'Bubbles',           orders:0.78, money: 0.33, adv: 0.6, comission: 0.3, luxury: 0.5},
        {name: 'Balthazaar Viscari', orders:0.48, money: 0.733, adv: 1, comission: 1, luxury: 0.1},
        {name: 'Balthazaar Viscari', orders:0.58, money: 0.43, adv: 1, comission: 1, luxury: 0.7},
        {name: 'Balthazaar Viscari', orders:0.68, money: 0.83, adv: 1, comission: 1, luxury: 0.3},
        {name: 'Balthazaar Viscari', orders:1, money: 1, adv: 0.1, comission: 0.2, luxury: 1},
        {name: 'Balthazaar Viscari', orders:0.28, money: 0.23, adv: 0.7, comission: 0.9, luxury: 0},
        {name: 'Balthazaar Viscari', orders:0.88, money: 0.13, adv: 0.5, comission: 0.1, luxury: 1}
    ];
 </script>


<style>
    .stickmen-container {
        display: flex;
    }
    .stickman{
        opacity: 0.5;
    }
    .stickman:hover {
        opacity: 1; /* increase opacity when hovered over */
    }
</style>

<div class="stickmen-container">
    {#each data as dp}
        <div class="stickman">
            <Stickman name = {dp.name} scaledMoney= {dp.money} scaledOrders = {dp.orders} scaledAdv = {dp.adv} scaledCom = {dp.comission} scaledLux= {dp.luxury}/>
        </div>
    {/each}
</div>

