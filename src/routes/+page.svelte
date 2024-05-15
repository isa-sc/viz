<script lang="ts">
    import Stickman from '../components/Stickman.svelte';

    let data = [
        { firstname: "T'avin", name: " T'soban", orders: 1, money: 1, adv: 1, comission: 1, luxury: 1 },
        { firstname: '', name: 'Bubbles', orders: 0.723, money: 0.745, adv: 0.813, comission: 0.422, luxury: 0.778 },
        { firstname: 'Kay', name: 'Glimshine', orders: 0.261, money: 0.263, adv: 0.494, comission: 0.011, luxury: 0.028 },
        { firstname: 'Bruno', name: 'Notlot', orders: 0.250, money: 0.239, adv: 0.280, comission: 0.06, luxury: 0.252 },
        ];
 
    let data2 = [
        { firstname: 'Balthazaar', name: 'Viscari', orders: 0.0748, money: 0.0732, adv: 0.123, comission: 0, luxury: 0.03 },
        { firstname: 'Lanec', name: 'Lot', orders: 0.096, money: 0.103, adv: 0.104, comission: 0.074, luxury: 0.1145 },
        { firstname: 'Shade', name: 'Tabaxii', orders: 0.118, money: 0.125, adv: 0.182, comission: 0, luxury: 0.092 },
        { firstname: 'Gudren', name: 'Rockseeker', orders: 0.076, money: 0.081, adv: 0.007, comission: 0.158, luxury: 0.159 }
    ];
</script>

<div class="stickmen-container">
    {#each data as dp}
        <div>
            <Stickman
                scaledMoney={dp.money}
                scaledOrders={dp.orders}
                scaledAdv={dp.adv}
                scaledCom={dp.comission}
                scaledLux={dp.luxury}
                firstname = {dp.firstname}
                lastname= {dp.name}
            />
            <p class="stickman" >
                Number of orders: {Math.round(dp.orders * 33790).toLocaleString()} <br>
                Money earned: {Math.round(dp.money * 910558306.7).toLocaleString()}$ <br>
                {#if dp.adv*465134305.8 > dp.comission*130412395.3}
                    {#if dp.adv*465134305.8 < dp.luxury*315011605.6}
                        most popular line: Luxury
                    {:else}
                        most popular line: Adventure
                    {/if}
                {:else if dp.comission*130412395.3 > dp.luxury*315011605.6}
                    most popular line: Commission
                {:else}
                    most popular line: Luxury
                {/if} <br>
                Luxury: {Math.round(dp.luxury * 315011605.6).toLocaleString()}$ <br>
                Adventure: {Math.round(dp.adv * 465134305.8).toLocaleString()}$ <br>
                Commission: {Math.round(dp.comission * 130412395.3).toLocaleString()}$
            </p>
        </div>
                
    {/each}
</div>

<div class="stickmen-container">
    {#each data2 as dp}
        <div>
            <Stickman
                scaledMoney={dp.money}
                scaledOrders={dp.orders}
                scaledAdv={dp.adv}
                scaledCom={dp.comission}
                scaledLux={dp.luxury}
                firstname = {dp.firstname}
                lastname= {dp.name}
            />
            <p class="stickman" >
                Number of orders: {Math.round(dp.orders * 33790).toLocaleString()} <br>
                Money earned: {Math.round(dp.money * 910558306.7).toLocaleString()}$ <br>
                {#if dp.adv*465134305.8 > dp.comission*130412395.3}
                    {#if dp.adv*465134305.8 < dp.luxury*315011605.6}
                        most popular line: Luxury
                    {:else}
                        most popular line: Adventure
                    {/if}
                {:else if dp.comission*130412395.3 > dp.luxury*315011605.6}
                    most popular line: Commission
                {:else}
                    most popular line: Luxury
                {/if} <br>
                Luxury: {Math.round(dp.luxury * 315011605.6).toLocaleString()}$ <br>
                Adventure: {Math.round(dp.adv * 465134305.8).toLocaleString()}$ <br>
                Commission: {Math.round(dp.comission * 130412395.3).toLocaleString()}$
            </p>
        </div>
    {/each}
</div>


<style>
    .stickmen-container {
        display: flex;
    }

    .stickman {
        opacity: 0;
    }

    .stickman:hover {
        opacity: 1; /* increase opacity when hovered over */
    }

    p {
        font-family: 'Courier New', Courier, monospace;
        font-size:x-small;
    }
</style>
