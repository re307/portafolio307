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
        }

        return esborde;
    }
    const celdaAccion = (infoCelda,id)=>{
        console.log(infoCelda);
        let celdaClick = document.getElementById(`ui${id}`);
        celdaClick.className = "celda_libre"
        if (infoCelda.isBoom) {
            displayBoom = "flex";
        }else{
            if (infoCelda.vecinas !== undefined ) {
                for (let index = 0; index < infoCelda.vecinas.length; index++) {
                    const idVecina = index;
                    document.getElementById(`ui${idVecina}`).click();
                }
            }
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
                ,aperturada:false
            }
            celdas.push(infoCelda);
        }
        for (let index = 0; index < celdasBombas.length; index++) {
            const value = celdasBombas[index];
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
            
        }
        const dataCelda = (value) =>{
            let arrayCeldas = new Array();
            let borde = isborde(value);
            let superior = ((value-largo)>0?false:true);
            let inferior = ((value+largo)<totalCeldas?false:true);
            arrayCeldas.push(borde,superior,inferior);
            return arrayCeldas;
        }
        const evaluaVecindad = (value)=>{
            let arrayCeldas = new Array();
            let borde = isborde(value);
            let superior = ((value-largo)>0?false:true);
            let inferior = ((value+largo)<totalCeldas?false:true);
            switch (borde) {
                case 0:
                    if (!superior) {
                        arrayCeldas.push(value-(largo-1));
                        arrayCeldas.push(value-largo);
                        arrayCeldas.push(value-(largo+1));
                    }
                    arrayCeldas.push(value+1);
                    if (!inferior) {
                        arrayCeldas.push(value+(largo-1));
                        arrayCeldas.push(value+largo);
                        arrayCeldas.push(value+(largo+1));
                    }
                    arrayCeldas.push(value-1);
                    break;
                case 1:
                    if (!superior) {
                        arrayCeldas.push(value-largo);
                        arrayCeldas.push(value-(largo+1));
                    }
                    arrayCeldas.push(value+1);
                    if (!inferior) {
                        arrayCeldas.push(value+largo);
                        arrayCeldas.push(value+(largo+1));
                    }
                    break;

                case 2:
                    if (!superior) {
                        arrayCeldas.push(value-(largo-1));
                        arrayCeldas.push(value-largo);
                    }
                    if (!inferior) {
                        arrayCeldas.push(value+(largo-1));
                        arrayCeldas.push(value+largo);
                    }
                    arrayCeldas.push(value-1);
                    break;
            
                default:
                    break;
            }
            return arrayCeldas;
        }
        for (let index = 0; index < celdas.length; index++) {
            const celda = celdas[index];
            celda.dataCelda = dataCelda(index);
            if (!celda.isBoom&&(celda.cercania == 0)) {
                celda.vecinas = evaluaVecindad(index);
            }
        }
    }
    ejecutaPrograma();
</script>
<div class="container juego_b">
    <div class="row marcador">
        macador
        <div class="btn btn-dark" on:click={()=>{ejecutaPrograma()}}>Clik</div>
    </div>
    <div id="tablero" class="row tablero">
        {#each celdas as celda,index }
            <div class="celda" id="ui{index}" on:click={()=>{celdaAccion(celda,index)}}>
                {#if celda.isBoom}
                    <div class="center" style="display:{displayBoom}"><img src="{boom}"/></div>
                {:else}
                    <p>{celda.cercania}</p>
                {/if}
            </div>
        {/each}
    </div>
</div>