<script>
    import './buscaminas.css'
    import Celda from './Celda.svelte'
    export let recarga;
    let largo = 18;
    let totalCeldas = largo * 18;
    let filas = new Array(totalCeldas);
    let celdasBombas = new Array();
    let vecinasBombas = new Array();
    // @ts-ignore
    let conunt = 0;

    if (recarga) {
        let totalBombas = Math.round(totalCeldas / 8);
        celdasBombas = new Array();
        for (let index = 1; index <= totalBombas; index++) {
            let celdaBomba = Math.floor(Math.random() * totalCeldas) + 1;
            celdasBombas.push(celdaBomba);
        } 
        //this.ejecutaCreacion();
    }
    // recarga = false;
    let isBorde = (celda) =>{
        let result = false;
        if (celda%largo<2) {
            result = true;
        }
        return result;
    }
    let isBordeIzquierdo = (celda) =>{
        let result = false;
        if (celda%largo == 1) {
            result = true;
        }
        return result;
    }
    let isBordeDerecho = (celda) =>{
        let result = false;
        if (celda%largo == 0) {
            result = true;
        }
        return result;
    }
    let isBordeSuperior = (celda)=>{
        let result = false;
        if ((celda-largo)<1) {
            result = true;
        }
        return result
    }
    let isBordeInferior = (celda)=>{
        let result = false;
        if ((largo+celda)>totalCeldas) {
            result = true;
        }
        return result
    }
    let vecindad = (Celda)=>{
        let vecinas;
        if (isBorde(Celda)) {
            if (isBordeIzquierdo(Celda)) {
                if (isBordeSuperior(Celda)) {
                    vecinas = [(Celda+1),(Celda+(largo+1)),Celda+largo];
                }else
                    if (isBordeInferior(Celda)) {
                        vecinas = [(Celda+1),(Celda-largo),(Celda-(largo+1))];
                    }else{
                        vecinas = [(Celda+1),(Celda+(largo+1)),Celda+largo,(Celda-largo),((Celda-largo)+1)];
                    }
                
            }else
                if (isBordeDerecho(Celda)) {
                    if (isBordeSuperior(Celda)) {
                        vecinas = [(Celda+largo),((Celda+largo)-1),(Celda-1)]
                    }else
                        if (isBordeInferior(Celda)) {
                            vecinas = [(Celda-1),((Celda-largo)-1),(Celda-largo)]
                        }else{
                            vecinas = [(Celda+largo),((Celda+largo)-1),(Celda-1),((Celda-largo)-1),(Celda-largo)]
                        }
                    
                }
        }else{
            if (isBordeSuperior(Celda)) {
                    vecinas = [(Celda+1),((Celda+largo)+1),(Celda+largo),((Celda+largo)-1),(Celda-1)]
            }else
                if (isBordeInferior(Celda)) {
                    vecinas = [(Celda+1),(Celda-1),((Celda-largo)-1),(Celda-largo),((Celda-largo)+1)]
                }else{
                    vecinas = [(Celda+1),((Celda+largo)+1),(Celda+largo),((Celda+largo)-1),(Celda-1),((Celda-largo)-1),(Celda-largo),((Celda-largo)+1)]
                }
        }
        if (celdasBombas.includes(Celda)) {
            vecinasBombas[Celda]=vecinas;
        }
        return vecinas;
    }
    let ejecutaCreacion = ()=>{
        setTimeout(()=>{
            console.log(celdasBombas);
            console.log(vecinasBombas);
            vecinasBombas.forEach((vecinas)=>{
                vecinas.forEach((vecina)=>{
                        if (!celdasBombas.includes(vecina)) {
                            let celdaCercania = document.getElementById(`cercania${vecina}`);
                            // console.log(celdaCercania);
                            let cercania = celdaCercania.innerText;
                            let cantidad = Number(cercania);
                            cantidad = cantidad+1;
                            celdaCercania.innerText = `${cantidad}`;
                            celdaCercania.style.color = determinaColor(cantidad);
                        }
                });
            });
        },1000);
    }
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
    let reinicio = ()=>{
        recarga = false;
        setTimeout(()=>{
            recarga = true;
            // ejecutaCreacion();
        },1000);
    }
</script>
<div class="container juego_b">
    <div class="row marcador">
        macador
        <div class="btn btn-dark" on:click={()=>{reinicio()}}>Clik</div>
    </div>
    <div id="tablero" class="row tablero">
        {#if recarga}
            {#each filas as fila,i }
                <Celda data={{
                    "numero":i+1,
                    "largo":largo,
                    "ancho":totalCeldas,
                    "vecinas":vecindad(i+1),
                    "isBomba":celdasBombas.includes(i+1),
                    "bombas":celdasBombas
                }}>
                </Celda>
            {/each}
        {/if}
    </div>
    {ejecutaCreacion()}
</div>