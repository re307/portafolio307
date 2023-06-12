<script>
    import './buscaminas.css'
    import boom from '../../assets/boom.png'
    export let recarga;
    let largo = 18;
    let ancho = largo;
    let totalCeldas = largo * 18;
    let celdas = new Array();
    let celdasBombas = new Array();
    let vecinasBombas = new Array();
    let displayBoom = "none";
    let htmlHijo = null;
    // @ts-ignore
    let conunt = 0;
    let determinaColor = (cercania)=>{
        let color = "";
        switch (cercania) {
            case 0:
                color = "black";
                break;
            case 1:
                color = "blue";
                break;
            case 2:
                color = "green";
                break;
            case 3:
                color = "yellow";
                break;
            case 4:
                color = "red";
                break;
            default:
                break;
        }
        return color;
    }
    const isborde = (celda)=>{
        let esborde = 0;

        if ((celda%largo === 0)) {
            esborde = 1;
        } else {
            if (celda%largo === (largo-1)) {
                esborde = 2;
            }
            //console.log(`la celda: ${celda} es una bomba fuera de los laterales`);
        }

        return esborde;
    }
    const celdaAccion = (infoCelda)=>{
        console.log(infoCelda);
        if (infoCelda.isBoom) {
            displayBoom = "flex";
        }
    }
    const ejecutaPrograma = ()=>{
        celdas = new Array();
        celdasBombas = new Array();
        vecinasBombas = new Array();
        displayBoom = "none";
        let totalBombas = Math.round(totalCeldas / 8);
        for (let index = 1; index <= totalBombas; index++) {
            let celdaBomba = Math.floor(Math.random() * totalCeldas) + 1;
            celdasBombas.push(celdaBomba);
        }
        console.log(celdasBombas);
        for (let index = 0; index < totalCeldas; index++) {
            let isBoom = celdasBombas.includes(index);
            let cercania = 0;
            let infoCelda = {
                isBoom:isBoom
                ,cercania:cercania
            }
            celdas.push(infoCelda);
        }
        celdasBombas.forEach((value)=>{
            let borde = isborde(value);
            let superior = ((value-largo)>0?false:true);
            let inferior = ((value+largo)<totalCeldas?false:true);
            switch (borde) {
                case 0:
                    if (!superior) {
                        celdas[value-(largo-1)].cercania = celdas[value-(largo-1)].cercania+1
                        celdas[value-largo].cercania = celdas[value-largo].cercania+1
                        celdas[value-(largo+1)].cercania = celdas[value-(largo+1)].cercania+1
                    }
                    celdas[value+1].cercania = celdas[value+1].cercania+1
                    if (!inferior) {
                        celdas[value+(largo-1)].cercania = celdas[value+(largo-1)].cercania+1
                        celdas[value+largo].cercania = celdas[value+largo].cercania+1
                        celdas[value+(largo+1)].cercania = celdas[value+(largo+1)].cercania+1
                    }
                    celdas[value-1].cercania = celdas[value-1].cercania+1
                    break;
                case 1:
                    if (!superior) {
                        celdas[value-largo].cercania = celdas[value-largo].cercania+1
                        celdas[value-(largo+1)].cercania = celdas[value-(largo+1)].cercania+1
                    }
                    celdas[value+1].cercania = celdas[value+1].cercania+1
                    if (!inferior) {
                        celdas[value+largo].cercania = celdas[value+largo].cercania+1
                        celdas[value+(largo+1)].cercania = celdas[value+(largo+1)].cercania+1
                    }
                    break;
                case 2:
                    if (!superior) {
                        celdas[value-(largo-1)].cercania = celdas[value-(largo-1)].cercania+1
                        celdas[value-largo].cercania = celdas[value-largo].cercania+1
                    }
                    if (!inferior) {
                        celdas[value+(largo-1)].cercania = celdas[value+(largo-1)].cercania+1
                        celdas[value+largo].cercania = celdas[value+largo].cercania+1
                    }
                    celdas[value-1].cercania = celdas[value-1].cercania+1
                    break;
            
                default:
                    break;
            }
        });
    }
    ejecutaPrograma();
</script>
<div class="container juego_b">
    <div class="row marcador">
        macador
        <div class="btn btn-dark" on:click={()=>{ejecutaPrograma()}}>Clik</div>
    </div>
    <div id="tablero" class="row tablero">
        {#each celdas as celda }
            <div class="celda" on:click={()=>{celdaAccion(celda)}}>
                {#if celda.isBoom}
                    <div class="center" style="display:{displayBoom}"><img src="{boom}"/></div>
                {:else}
                    <p>{celda.cercania}</p>
                {/if}
            </div>
        {/each}
    </div>
</div>