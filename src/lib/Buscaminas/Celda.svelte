<script>
    import boom from '../../assets/boom.png'
    export let data;
    let vecinas = data.vecinas;
    let liberada = false;
    let cercania = 0;
    let destapaVecinas = ()=>{
        if (!liberada&&!data.isBomba) {
            let celda = document.getElementById(`celda${data.numero}`);
            celda.className = "celda_libre";
            let hijo = celda.childNodes[0].childNodes[0];
            // console.log(hijo);
            liberada = true;
            if (hijo.innerText == "") {
                vecinas.forEach(element => {
                    setTimeout(()=>{
                        document.getElementById(`celda${element}`).click();
                    },1);
                });
            }
        }
        if (data.isBomba) {
            data.bombas.forEach(element => {
                let celda = document.getElementById(`celda${data.numero}`);
                celda.className = "celda_libre";
                liberada = true;
                setTimeout(()=>{
                    document.getElementById(`celda${element}`).click();
                },1);
            });
        }
    }
</script>
<!-- svelte-ignore a11y-click-events-have-key-events -->
<div class="celda" id="celda{data.numero}"
    on:click={destapaVecinas}
>
    <div style="display: {liberada?'block':'none'};">
        {#if data.isBomba}
            <img src="{boom}" class="logo" alt="Vite logo" />
        {:else}
            <p id="cercania{data.numero}">{cercania>0?cercania:""}</p>
        {/if}
    </div>
</div>